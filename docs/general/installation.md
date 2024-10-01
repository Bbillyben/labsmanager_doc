# Installation


## Docker 

you can find template files in [labsmanager_docker](https://github.com/Bbillyben/labsmanager_docker) repo

default template files should be sufficient to launch a basic labsmanager docker instance.

docker-compose.yml shouldn't be modified, all variables are defined in .env file.
you will need three files to run your docker containers :

<details>
  <summary>docker-compose.yml</summary>
``` YAML
version: '3.8'
services:
    lab-db:
        container_name: lab-db
        image: postgres:13
        ports:
            - ${LAB_DB_PORT:-5435}:5432/tcp
        environment:
            - PGDATA=/var/lib/postgresql/data/pgdb
            - POSTGRES_USER=${LAB_DB_USER:?You must provide the 'LAB_DB_USER' variable in the .env file}
            - POSTGRES_PASSWORD=${LAB_DB_PASSWORD:?You must provide the 'LAB_DB_PASSWORD' variable in the .env file}
            - POSTGRES_DB=${LAB_DB_NAME:?You must provide the 'LAB_DB_NAME' variable in the .env file}
        volumes:
            # Map 'data' volume such that postgres database is stored externally
            - lab_data:/var/lib/postgresql/data/
        restart: unless-stopped

    # lab web server service    
    # Uses gunicorn as the web server
    lab-server:
        build: .
        container_name: lab-server
        # If you wish to specify a particular lab version, do so here
        image: labsmanager/labsmanager:${LAB_TAG:-stable}
        ports :
            - 8000:8000
        depends_on:
            - lab-db
        env_file:
            - .env
        volumes:
            # Data volume must map to /home/lab/data
            - lab_data:/home/labsmanager/data/
        restart: unless-stopped
    # worker to process sceduled tasks
    lab-worker:
        build: .
        container_name: lab-worker
        # If you wish to specify a particular lab version, do so here
        image: labsmanager/labsmanager:${LAB_TAG:-stable}
        command: invoke worker
        depends_on:
            - lab-server
        env_file:
            - .env
        volumes:
            # Data volume must map to /home/lab/data
            - lab_data:/home/labsmanager/data/
        restart: unless-stopped
    lab-proxy:
        container_name: lab-proxy
        image: nginx:stable
        depends_on:
            - lab-server
        env_file:
            - .env
        ports:
            # Default web port is 1337 (can be changed in the .env file)
            - ${LAB_WEB_PORT:-1337}:80
        volumes:
            # Provide nginx configuration file to the container
            # Refer to the provided example file as a starting point
            - ./nginx.prod.conf:/etc/nginx/conf.d/default.conf:ro
            # nginx proxy needs access to static and media files
            - lab_data:/var/www
        restart: unless-stopped

volumes:
    # Persistent data, stored external to the container(s)
    lab_data:
        driver: local
        driver_opts:
            type: none
            o: bind
            # This directory specified where lab data are stored "outside" the docker containers
            device: ${LAB_EXT_VOLUME:?You must specify the 'LAB_EXT_VOLUME' variable in the .env file!}

```
</details>



<details>
  <summary>.env</summary>

``` bash
DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1] ['*'] www.mylabsmanager.com


SQL_ENGINE=django.db.backends.postgresql
LAB_DB_NAME=django_db
LAB_DB_USER=djangoUser
LAB_DB_PASSWORD=djangoUserPass
LAB_DB_HOST=localhost
LAB_DB_PORT=5432

LAB_WEB_PORT=80

LAB_TAG=latest # image tag to used for container

CSRF_TRUSTED_ORIGINS=https://www.mylabsmanager.com

SECRET_KEY='this_is_to_be_updated'
DEBUG='false'
LABS_LOG_LEVEL='WARNING'

# Email Settings
LAB_EMAIL_BACKEND='django.core.mail.backends.smtp.EmailBackend'
LAB_EMAIL_HOST='' # eg smtp server
LAB_EMAIL_PORT='' 
LAB_EMAIL_USERNAME=''
LAB_EMAIL_SENDER=''
LAB_EMAIL_PASSWORD=''
LAB_EMAIL_PREFIX=''
LAB_EMAIL_TLS=false
LAB_EMAIL_SSL=true

LAB_SITE_ID=1 # specify which site id will be used



DJANGO_ADMINS='username1,user1email@somewher.com  username2,user2email@somewhereelse.com' # list of admin couple of username and adresse email coma separated and split by space 

## Admin Site Customisation
ADMIN_HEADER='LabsManager'  # customisation of header in admin panel
ADMIN_SITE_TITLE='LabsManager' # customisation of title in admin panel
ADMIN_INDEX_TITLE='Menu' # customisation of index in admin panel

## volume to mount
LAB_EXT_VOLUME='/home/labsmanager/data' # where persistent data var will be mounted
LABSMANAGER_STATIC_ROOT='/home/labsmanager/data/static/' # set static path
LABSMANAGER_MEDIA_ROOT='/home/labsmanager/data/media/'  # set media path 

## CSP Policies
ADMIN_USE_CSP ='true'
# values separate by a comma "mon.site.com,other.site.gh, 'unsafe-inline','unsafe-eval'"
ADMIN_CSP_DEFAULT="'self'"
ADMIN_CSP_SCRIPT="'unsafe-inline','unsafe-eval'"
ADMIN_CSP_STYLE= "'unsafe-inline'"
ADMIN_CSP_FONT="'unsafe-inline','unsafe-eval',  'data:'"
ADMIN_CSP_DATA="'unsafe-inline','unsafe-eval'"
ADMIN_CSP_IMG="'data:'"
# ADMIN_CSP_MEDIA=""

#security issues 
CSRF_COOKIE_SECURE='true'
CSRF_COOKIE_SAMESITE= 'Strict'
SESSION_COOKIE_SECURE='true'
SECURE_BROWSER_XSS_FILTER='true'
SECURE_CONTENT_TYPE_NOSNIFF='true'
SECURE_SSL_REDIRECT='true'
X_FRAME_OPTIONS = 'DENY'
SECURE_HSTS_SECONDS = 300
SECURE_HSTS_INCLUDE_SUBDOMAINS= 'true'
SECURE_HSTS_PRELOAD= 'true'
```
</details>

<details>
  <summary>nginx.prod.conf</summary>

``` yaml
server {

    # Listen for connection on (internal) port 80
    listen 80;

    real_ip_header proxy_protocol;

    location / {

        proxy_set_header      Host              $http_host;
        proxy_set_header      X-Forwarded-By    $server_addr:$server_port;
        proxy_set_header      X-Forwarded-For   $remote_addr;
        proxy_set_header      X-Forwarded-Proto $scheme;
        proxy_set_header      X-Real-IP         $remote_addr;
        proxy_set_header      CLIENT_IP         $remote_addr;

        proxy_pass_request_headers on;

        proxy_redirect off;

        client_max_body_size 100M;

        proxy_buffering off;
        proxy_request_buffering off;

        proxy_pass http://lab-server:8000;
    }

    # Redirect any requests for static files
    location /static/ {
        alias /var/www/static/;
        # alias /home/labsmanager/data/static/; 
        autoindex on;

        # Caching settings
        expires 30d;
        add_header Pragma public;
        add_header Cache-Control "public";
    }


    # Use the 'user' API endpoint for auth
    location /auth {
        internal;

        proxy_pass http://lab-server:8000/auth/;

        proxy_pass_request_body off;
        proxy_set_header Content-Length "";
        proxy_set_header X-Original-URI $request_uri;
    }

}
```
</details>

#### get files

``` bash
wget https://github.com/Bbillyben/labsmanager_docker/blob/master/docker-compose.yml

wget https://github.com/Bbillyben/labsmanager_docker/blob/master/nginx.prod.conf

wget https://github.com/Bbillyben/labsmanager_docker/blob/master/.template.env -O .env
```

#### Install the application 

run install
``` bash
docker compose run lab-server invoke install
```
or, to directly launche the super user creation process
``` bash
docker compose run lab-server invoke install --super_user
```
this will setup databases and install base group for right management as well as default reports templates

#### Create the admin user 
create super user, and follow the instruction. This will be your first admin user
 
``` bash
docker compose run lab-server invoke superuser
```

#### Run the application and login
run docker compose : 

``` bash
docker-compose up -d
```

log into your brand new Labsmanager application

`localhost:7000`

## Bare Metal


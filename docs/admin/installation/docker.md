# Install with Docker Compose

Use the Compose and Dockerfile in the current application repository. They define four services: **lab-db** (PostgreSQL 13), **lab-server** (Gunicorn/Django), **lab-worker** (Django Q) and **lab-proxy** (Nginx). The image builds React with Node 24.11.1, then runs on Python 3.11.9. There is no React runtime container.

## Prerequisites and configuration

Install Docker Engine and the Docker Compose plugin. Obtain a checkout of the current LabsManager repository, including **Dockerfile**, **docker-compose.yml**, **nginx.prod.conf** and **nginx.proxy.inc**. Run the commands below from that checkout.

Create an absolute host directory for persistent data and ensure the database and application containers can write to it. **LAB_EXT_VOLUME** binds that directory into the shared **lab_data** volume. It holds PostgreSQL files, Django static files and media. Back it up with the database; container recreation does not replace it.

Create **.env** beside **docker-compose.yml**. The tracked **.template.env** can be a reference, but correct its old **LAB_DB_HOST=localhost** value for Compose. At minimum, set the following values to your own paths, domain and secrets:

~~~dotenv
LAB_EXT_VOLUME=/srv/labsmanager/data
LAB_DB_NAME=labsmanager
LAB_DB_USER=labsmanager
LAB_DB_PASSWORD=replace-with-unique-database-password
LAB_DB_HOST=lab-db
LAB_DB_PORT=5432
SECRET_KEY=replace-with-a-long-unique-django-secret
DEBUG=false
DJANGO_ALLOWED_HOSTS=labs.example.org
CSRF_TRUSTED_ORIGINS=https://labs.example.org
LABSMANAGER_STATIC_ROOT=/home/labsmanager/data/static
LABSMANAGER_MEDIA_ROOT=/home/labsmanager/data/media
LAB_WEB_PORT=1337
LAB_TRUST_PROXY_SSL_HEADER=true
~~~

**LAB_DB_HOST=lab-db** is the Compose service name; **LAB_DB_PORT=5432** is the database port inside the Docker network. **LAB_EXT_VOLUME** is a host path, while the static/media paths above are inside the application container. The image does not need Node or npm at runtime. Keep **.env** private and out of version control.

The Compose file publishes PostgreSQL at **LAB_DB_PORT** and the two plain HTTP proxy entrances at **LAB_WEB_PORT** (default 1337) and **LAB_LEGACY_WEB_PORT** (default 1338). It binds Gunicorn to host loopback **127.0.0.1:8000**. Restrict database and plain HTTP ports at the host firewall. For a public HTTPS site, terminate TLS at a trusted front proxy and forward to loopback **127.0.0.1:1339** (the default **LAB_TRUSTED_HTTPS_PORT**); the bundled Nginx listener on internal port 82 then sets **X-Forwarded-Proto=https**. Keep that loopback port private. Use **LAB_TRUST_PROXY_SSL_HEADER=true** only with this controlled proxy path. HTTPS certificates and the outer proxy are deployment-specific.

## Build and initialize a new instance

Build the shared application image, start PostgreSQL alone and wait for its health check:

~~~bash
docker compose build lab-server
docker compose up -d lab-db
docker compose ps lab-db
~~~

The normal container entrypoint checks migrations before starting either Gunicorn or the worker, so a new empty database needs a one-off initialization that bypasses that entrypoint. Run the canonical Invoke task from **/home/labsmanager**, where the image places **tasks.py** and the Django directory:

~~~bash
docker compose run --rm --no-deps --entrypoint /bin/bash lab-server -lc 'cd /home/labsmanager && invoke install'
~~~

This runs migrations and checks, collects static files, then loads **group-fixture** and **initial-report-data**. Do not run the two loaddata commands separately. To create the first superuser immediately, choose this variant of the one-off command **instead of** the preceding install command:

~~~bash
docker compose run --rm --no-deps --entrypoint /bin/bash lab-server -lc 'cd /home/labsmanager && invoke install --super-user'
~~~

If installation was run without that flag, create the first superuser interactively afterward:

~~~bash
docker compose run --rm --no-deps --entrypoint /bin/bash lab-server -lc 'cd /home/labsmanager && invoke superuser'
~~~

Start the remaining services only after installation completes:

~~~bash
docker compose up -d lab-server lab-worker lab-proxy
docker compose ps
~~~

On startup, **lab-server** refreshes the React files in the persistent static volume and runs Django collectstatic. **lab-worker** skips that collection. Nginx serves **/app/** from the collected React build and **/static/** from the same shared volume; it forwards API, admin, protected report and other Django routes to **lab-server**. Uploaded media remains persistent and is not exposed as an unrestricted public Nginx alias.

## Verify and troubleshoot

~~~bash
docker compose exec lab-server python3 /home/labsmanager/labsmanager/manage.py migrate --check --noinput
curl -I http://127.0.0.1:1337/app/
curl -I http://127.0.0.1:1337/static/frontend/index.html
~~~

Check that the first command succeeds, both static URLs respond, and the public HTTPS site opens **/app/**. Sign in with the new account and confirm **/admin/** and an API-backed page work. A bare **/api/v1/me/** request can be unauthenticated; its response should still come from Django.

If **lab-server** or **lab-worker** exits immediately, inspect **docker compose logs lab-server lab-worker** and the migration check. An empty database cannot pass the entrypoint check; run the one-off **invoke install** above. If React is blank, check that **frontend/index.html** and referenced assets exist in the persistent static volume. If API requests redirect repeatedly, check the outer HTTPS proxy, trusted port and **LAB_TRUST_PROXY_SSL_HEADER** configuration.

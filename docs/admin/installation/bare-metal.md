# Install on a host without Docker

The steps below use the application configuration and build process present in the repository. They have not been validated as a complete installation on a reference bare-metal host. Adapt service supervision and the HTTPS reverse proxy to your host.

## Prerequisites and deployment layout

Provide PostgreSQL, Python with venv support, and the native libraries needed by the Python dependencies (including libpq, libffi, Pango, Poppler and image-format support). The container build uses PostgreSQL 13, Python 3.11.9 and Node 24.11.1; use these versions as a known build baseline. Node is needed to build React, not to serve it. Create a dedicated service account with write access to its deployment and data directories.

The repository checkout has `backend/manage.py`, but the checked-in `tasks.py` locates `manage.py` in a sibling directory named `labsmanager`. The Docker image creates that layout. For a host deployment, prepare the same layout in a separate directory; the commands below use `/srv/labsmanager/source` for a fresh checkout and `/srv/labsmanager/runtime` for the runnable copy. These paths are examples, not fixed application paths. Run the commands as the service account unless a system administration command is shown.

Create a PostgreSQL role and database, recording the password for the YAML configuration below. For example, with local PostgreSQL administration rights:

~~~bash
sudo -u postgres createuser --pwprompt labsmanager
sudo -u postgres createdb --owner=labsmanager labsmanager
~~~

Fetch the source, install the Python dependencies and build React:

~~~bash
git clone https://github.com/Bbillyben/labsmanager_docker.git /srv/labsmanager/source
mkdir -p /srv/labsmanager/runtime
python3.11 -m venv /srv/labsmanager/runtime/.venv
. /srv/labsmanager/runtime/.venv/bin/activate
python -m pip install -r /srv/labsmanager/source/requirements.txt
cd /srv/labsmanager/source/frontend
npm ci
npm run build
~~~

Stage the same relative layout used by the container image, including the React build as an input to Django's static collection:

~~~bash
cd /srv/labsmanager/source
cp -a backend /srv/labsmanager/runtime/labsmanager
cp tasks.py gunicorn.conf.py /srv/labsmanager/runtime/
mkdir -p /srv/labsmanager/runtime/labsmanager/data/static/frontend
cp -a frontend/dist/. /srv/labsmanager/runtime/labsmanager/data/static/frontend/
mkdir -p /srv/labsmanager/data/static /srv/labsmanager/data/media
~~~

`npm run build` writes `frontend/dist`; the container copies it to `labsmanager/data/static/frontend`. Django's `STATICFILES_DIRS` includes `labsmanager/data/static`, and `collectstatic` copies those files to the configured `static_root`. Keep the source and collected directories separate. The `media_root` is for uploaded files, not React assets.

## Configure Django

Django reads `config.yaml` from the directory containing `manage.py` by default: `/srv/labsmanager/runtime/labsmanager/config.yaml` in this example. An explicit `LABSMANAGER_CONFIG_FILE` selects another YAML file; otherwise `LABSMANAGER_CONFIG_PROFILE` selects `config.<profile>.yaml` in that directory. If the selected file is absent, the loader copies `config_template.yaml` there. The template contains development values, so edit the configuration **before** running Django. Keep the file readable only by the service account.

Start from the distributed template and set at least these application values for this example:

~~~bash
install -m 600 /srv/labsmanager/runtime/labsmanager/config_template.yaml /srv/labsmanager/runtime/labsmanager/config.yaml
~~~

~~~yaml
secret_key: 'replace-with-a-unique-secret'
debug: false
django_allowed_hosts: 'labs.example.org'
csrf_trusted_origins: 'https://labs.example.org'
sql_engine: 'django.db.backends.postgresql'
lab_db_name: 'labsmanager'
lab_db_user: 'labsmanager'
lab_db_password: 'replace-with-the-postgresql-role-password'
lab_db_host: '127.0.0.1'
lab_db_port: '5432'
static_root: '/srv/labsmanager/data/static'
media_root: '/srv/labsmanager/data/media'
~~~

Replace the domain, both secrets and paths for your host. The database keys are read by `settings.py` even though the template leaves them commented out. `django_allowed_hosts` and `csrf_trusted_origins` must be strings, not YAML lists. Use a unique `secret_key`: production startup rejects the development keys in the template.

For each setting, the loader uses a supported environment variable first, then the YAML key, then the code default. In this example, the environment counterparts are `SECRET_KEY`, `DEBUG`, `DJANGO_ALLOWED_HOSTS`, `CSRF_TRUSTED_ORIGINS`, `SQL_ENGINE`, `LAB_DB_NAME`, `LAB_DB_USER`, `LAB_DB_PASSWORD`, `LAB_DB_HOST`, `LAB_DB_PORT`, `LABSMANAGER_STATIC_ROOT` and `LABSMANAGER_MEDIA_ROOT`. The YAML file is sufficient; no `instance.env` file is loaded by the application. The container's `LAB_STATIC_ROOT` and `LAB_MEDIA_ROOT` variables serve its shell scripts and are not the Django setting names. If the only path to Gunicorn is through a trusted HTTPS proxy, set `trust_proxy_ssl_header: true` in YAML (or `LAB_TRUST_PROXY_SSL_HEADER=true` in its environment) so Django recognizes `X-Forwarded-Proto`.

## Initialize the application

From the staged directory, with the virtual environment active, run:

~~~bash
cd /srv/labsmanager/runtime
. .venv/bin/activate
invoke install
invoke superuser
~~~

Alternatively, use `invoke install --super-user` for the interactive superuser step. `install` runs the `update` task (migrations, Django check and `collectstatic`), then loads `group-fixture` and `initial-report-data`. The migration task also runs `makemigrations`, so its deployed application directory must be writable by the service account. Do not run `invoke install` directly from the unmodified repository checkout: its `tasks.py` would look for `source/labsmanager/manage.py`, which does not exist.

## Run and verify

The application serves through the WSGI module `labsmanager.wsgi`. Gunicorn is in the Python requirements and is used by the container. A host supervisor may run it with the staged configuration, for example:

~~~bash
/srv/labsmanager/runtime/.venv/bin/gunicorn \
  -c /srv/labsmanager/runtime/gunicorn.conf.py \
  --chdir /srv/labsmanager/runtime/labsmanager \
  --bind 127.0.0.1:8000 labsmanager.wsgi:application
~~~

Use a separate supervised process for Django Q if scheduled jobs and notifications are needed:

~~~bash
/srv/labsmanager/runtime/.venv/bin/python \
  /srv/labsmanager/runtime/labsmanager/manage.py qcluster
~~~

A production host also needs HTTPS and routing for `/app/`, `/static/` and Django requests. For example, a reverse proxy can serve the React entry point from `static_root/frontend/index.html`, static assets from `static_root`, and forward API, admin and other Django routes to Gunicorn. Configure TLS, service units, permissions, backups and media access for your host; no systemd or Nginx unit is supplied or validated by this repository. Do not expose uploaded media as an unrestricted static directory.

With the same configuration and virtual environment used by the service, check:

~~~bash
cd /srv/labsmanager/runtime
. .venv/bin/activate
python labsmanager/manage.py migrate --check --noinput
python labsmanager/manage.py check
test -f /srv/labsmanager/data/static/frontend/index.html
~~~

Then confirm that `/app/` loads through HTTPS, its `/static/frontend/` assets load, and `/admin/` is reachable. Check the Django Q process separately if enabled. If React's collected files are missing after a frontend rebuild, copy the new `frontend/dist` into the staged `labsmanager/data/static/frontend` and run `invoke static` from the staged directory.

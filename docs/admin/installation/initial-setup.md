# Initial setup and demo data

Both deployment paths converge on **invoke install** in the environment that contains the Django dependencies and can reach PostgreSQL. Run it once when creating a new instance, before starting the normal web and worker processes. The [Docker steps](docker.md) and [bare-metal steps](bare-metal.md) show the exact working directory and environment for each path.

## What the install task does

The current task sequence is:

1. **update** runs **migrate** and **static**.
2. **migrate** runs Django **makemigrations**, **migrate --noinput** and **check**.
3. **static** runs **collectstatic --no-input**.
4. **install** loads **group-fixture**, then **initial-report-data**.
5. With the optional superuser flag, it opens Django's interactive superuser creation at the end.

These fixtures are part of normal initialization. The first creates LabsManager's expected groups and permissions; the second creates default report template records. Do not run their loaddata commands separately during a normal install. If a pre-existing instance has lost one of these data sets, diagnose that instance before using a repair command.

From the correct Invoke working directory, choose one workflow:

~~~bash
invoke install
invoke superuser
~~~

Or create the superuser during installation:

~~~bash
invoke install --super-user
~~~

Invoke also accepts **-s** for **--super-user**. This spelling was checked with the project's **invoke --help install**. Create the account interactively and keep its credentials private. Use it to sign in at **/admin/**; the main React application is at **/app/**.

The Docker startup script checks that migrations are already applied. It does **not** install or migrate an empty database automatically. Use the one-off bootstrap command in the Docker guide before starting Gunicorn or the worker.

## Instance configuration

At minimum, set a unique **SECRET_KEY**, **DEBUG=false**, **DJANGO_ALLOWED_HOSTS** (space-separated host names), **CSRF_TRUSTED_ORIGINS** (full HTTPS origins), the **LAB_DB_*** connection values, and writable **LABSMANAGER_STATIC_ROOT** and **LABSMANAGER_MEDIA_ROOT** paths. Environment variables take precedence over the YAML configuration file; the application creates a local config file from its template if none exists. Configure SMTP and the public site identity when email, invitations or notifications are needed.

For production, terminate HTTPS at a trusted proxy. **SECURE_SSL_REDIRECT** and secure cookies default to enabled. Only set **LAB_TRUST_PROXY_SSL_HEADER=true** when Django is reachable exclusively through a controlled proxy that sets **X-Forwarded-Proto**. The Docker guide identifies the dedicated trusted-proxy port.

## Demo / synthetic data — optional

The **generate_demo_data** management command is for demonstrations, tests, documentation and interface evaluation on a **dedicated disposable database**. It is separate from the two normal install fixtures. Run it after **invoke install**, on an otherwise empty operational database and **before creating a superuser**: an existing user counts as operational data and blocks a normal generation.

In the bare-metal layout used in this guide:

~~~bash
cd /srv/labsmanager/source/backend
python3 manage.py generate_demo_data --reference-date 2026-10-11 --seed 42
~~~

In Docker, run the same management command inside **lab-server** on a dedicated demo instance:

~~~bash
docker compose run --rm --no-deps --entrypoint /bin/bash lab-server -lc 'cd /home/labsmanager/labsmanager && python3 manage.py generate_demo_data --reference-date 2026-10-11 --seed 42'
~~~ The reference date fixes the scenario's time anchor; the seed makes its generated values reproducible. The data includes users and roles, Employees, Teams, Projects, Funds, Budgets, Expenses, Contracts, Leaves, dashboards and report templates. The [synthetic dataset inventory](https://github.com/Bbillyben/labsmanager_docker/blob/master/docs/demo-data/DATASET.md) describes the fixtures and example accounts in more detail.

Without **--reset**, the command refuses a database that already has operational data. **--reset** deletes operational records, including users, then rebuilds the demo data transactionally while retaining groups and reference catalogs. The command refuses reset unless Django is in DEBUG mode or the database name begins with **test_**. Those guards do not establish that a database is safe to erase: use reset only on a dedicated disposable demo/test database, never on an instance containing real records. For that dedicated database, append **--reset** to the command shown above to rebuild the same scenario. The command prints demo account credentials; keep its logs private.

## Verify the new instance

- Check the migration and service status using the command shown in the selected installation guide.
- Load **/app/** and confirm that React assets resolve from **/static/frontend/**.
- Verify that an unauthenticated API request reaches Django at **/api/**, then sign in with the new account and open **/admin/**.
- Open a report action after suitable data exists; the default templates should be available.
- If background notifications or scheduled jobs are required, confirm the separate worker process is running.

If the SPA is blank, check the built frontend files and collected static root. If the web or worker process refuses to start, check migrations and database connectivity first. If a report template is missing on a new instance, confirm the full **invoke install** task completed without error.

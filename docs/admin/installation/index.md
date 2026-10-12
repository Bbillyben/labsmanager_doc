# Install LabsManager

This guide is for administrators deploying the current Django and React application. Choose [Docker Compose](docker.md) or [bare metal](bare-metal.md), then follow the shared [initial setup](initial-setup.md). Both paths use **invoke install** for a new database.

| Part | Current role |
| --- | --- |
| Django | API, authentication, administrative routes, protected reports and background jobs |
| PostgreSQL | Application database |
| React | Built SPA at **/app/**; build files served from **/static/frontend/** |
| Reverse proxy | Serves the SPA and collected static files; forwards **/api/**, **/admin/** and other Django routes |
| Persistent storage | PostgreSQL data, collected static files and uploaded media |

There is no separate React production server. The Docker image builds React with Node and runs Django with Gunicorn; the worker uses the same image. Bare-metal installations build React once, collect its files with Django and run Gunicorn and the Django Q worker as supervised processes.

## Installation choice

- [Docker Compose](docker.md): use the repository's current Dockerfile, Compose services and Nginx configuration.
- [Bare metal](bare-metal.md): install Python, PostgreSQL and the React build toolchain on the host; provide a process supervisor and reverse proxy.
- [Initial setup and demo data](initial-setup.md): understand the common Invoke command, create the first superuser and optionally populate a disposable demo database.

For a new instance, **invoke install** runs migrations, Django checks, static collection and the two required fixtures: **group-fixture** (groups and permissions) and **initial-report-data** (default report templates). Do not treat these fixtures as optional demo data or load them a second time in the normal installation path.

Production access needs a unique Django secret, correctly scoped hosts and CSRF origins, PostgreSQL credentials, persistent writable paths and HTTPS at the trusted front proxy. Keep secrets outside version control. Run a deployment check and verify the SPA, API and admin routes before opening the instance to users.

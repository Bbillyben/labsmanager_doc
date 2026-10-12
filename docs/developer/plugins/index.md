# Develop a plugin

LabsManager plugins are Python classes discovered by the Django backend. A plugin can contribute settings, scheduled jobs, calendar events and filters, report context, mail subscription content, URL routes, Dashboard sources/widgets and Global Search providers. The React application does not load a plugin's JavaScript bundle. Use the [extension contracts](extensions.md) for features consumed by React.

## Discovery and activation

`plugin.apps.PluginConfig.ready()` reloads the registry when Django can access its database; migration commands skip plugin loading. Discovery scans `plugin.builtin`, `plugin.samples`, configured external directories and, when external plugins are enabled, installed `labsmanager_plugins` Python entry points. The installed sample is `backend/plugin/samples/FrenchHollidayPlugin/FrenchHollidayPlugin.py`; it illustrates Calendar, Dashboard, Settings and Schedule contributions.

For a directory plugin, set `plugin_enable: true` and `plugin_dir: '/absolute/path/to/plugins'` in the backend YAML configuration, or their recognized overrides `LABSMANAGER_PLUGINS_ENABLED` and `LABSMANAGER_PLUGIN_DIR`. The distributed template uses `/home/labsmanager/data/plugins/`, but the actual directory follows the instance configuration. The registry creates a missing plugin directory and its `__init__.py` when possible. It recursively discovers subclasses of `plugin.LabManagerPlugin` with nonempty `NAME`; `SLUG` is optional and otherwise derived from the name. Choose a stable, unique slug.

**Presence is discovery, not activation.** A `PluginConfig` row is created for a discovered plugin with `active=False` by default. Builtins activate automatically; an external or sample plugin must be activated explicitly. A staff operator can use the **Activate plugin(s)** action in Django Admin's Plugin configurations or the staff-only `PATCH /api/plugin/<slug>/activate/` endpoint with `{"active": true}`. **Settings → Administration → Plugins** in React shows registered plugins, settings, errors and a reload action, but does not provide an activation control. Reload the registry after changing plugin code or files. The global plugin switches for URL, Calendar, Schedule and Subscription contributions can also disable those mixins independently. Merely copying a plugin into the directory does not expose routes or UI.

## Small directory plugin

The scanner needs a Python package directory with `__init__.py` and an importable module containing the class. `plugin.py`, `urls.py`, `api.py`, templates and tests are naming choices, not mandatory files. This two-file example exposes one authenticated JSON route; place it under the configured `plugin_dir` as `health_plugin/`:

```text
health_plugin/
├── __init__.py
└── plugin.py
```

```python
# health_plugin/plugin.py
from django.contrib.auth.decorators import login_required
from django.http import JsonResponse
from django.urls import path
from plugin import LabManagerPlugin
from plugin.mixins import UrlsMixin


@login_required
def health(request):
    if not request.user.has_perm("project.view_project"):
        return JsonResponse({"detail": "Forbidden"}, status=403)
    return JsonResponse({"ok": True})


class HealthPlugin(UrlsMixin, LabManagerPlugin):
    NAME = "HealthPlugin"
    SLUG = "health"
    TITLE = "Health example"
    VERSION = "1.0"
    URLS = [path("status/", health, name="status")]
```

The empty `__init__.py` marks the package. With external plugins enabled, this plugin active, and the global **Enable URL integration** setting enabled, its route is `/plugin/health/status/`. The permission is illustrative: use the permission and visibility rules of the records your real endpoint exposes. The example performs no database write and does not claim to be an operational health check. See [routes and permissions](routes-and-api.md) before adding a data endpoint.

Check the active list in **Settings → Administration → Plugins** or `GET /api/plugin/` after logging in. A plugin can be discovered but inactive; verify its `active` value and the relevant global switch before checking the feature itself. The [testing guide](testing-and-debugging.md) covers reproducible checks.

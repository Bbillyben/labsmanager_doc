# Test and debug a plugin

## Focused tests

Use the repository's Django test patterns in `backend/plugin/tests.py`, `backend/dashboard/tests_r37.py` and `backend/global_search/tests.py`. From an environment with the project's Python requirements and Django configuration, run targeted modules, for example:

```bash
cd backend
python manage.py test plugin.tests dashboard.tests_r37 global_search.tests
```

For discovery, configure a temporary plugin directory and assert the registry finds your class and its stable slug; use the project's `labsmanager_PLUGIN_TEST_DIR` testing override where appropriate. Test inactive and active states separately. For URL views, use Django's test client to verify anonymous denial, authenticated access and missing-permission denial. For data endpoints, create both visible and hidden records and assert that only visible objects are returned. Never rely on a menu's visibility as the sole permission test.

For Dashboard, instantiate the plugin, inspect its source/widget definitions, call `available_definitions(context)` with the plugin registry mocked active and inactive, validate config bounds and check the provider payload for each renderer. For Search, test `visible_queryset`, result destinations, field behavior and duplicate-key handling; `SearchRegistry.active(user)` supplies only available providers. For Calendar, test typed events and filters in the relevant context and an empty or unsupported context.

## When a feature is missing

| Symptom | Check |
| --- | --- |
| Plugin absent | `plugin_enable` / `LABSMANAGER_PLUGINS_ENABLED`, `plugin_dir`, package `__init__.py`, importable subclass with nonempty `NAME`, discovery errors and registry reload. |
| Discovered but inactive | `PluginConfig.active` in Django Admin or `GET /api/plugin/`; activate a non-builtin plugin explicitly. |
| Capability missing | Correct mixin and method, global switch for URL/Calendar/Schedule/Subscription, and any provider `available` rule. |
| Route unavailable | `ENABLE_PLUGINS_URL`, active `UrlsMixin`, `URLS` patterns and the `/plugin/<slug>/` prefix. `API_URLS` is not dynamically mounted. |
| Permission denied | Request user, `has_perm`, object visibility and the view's Django/DRF permission class. |
| Initialization error | **Settings → Administration → Plugins** shows errors; check `labsmanager` / `labsmanager.plugin` logs and the registry's discovery/init errors. Migrations intentionally skip loading. |

The staff-only React Plugins page can reload and inspect the active registry. It is a diagnostic aid, not proof that the plugin's URL, Dashboard or Search behavior is correct for every user. No UI screenshot is required for these checks.

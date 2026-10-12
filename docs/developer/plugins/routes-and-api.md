# Routes, API and permissions

## Route boundaries

`UrlsMixin` reads the plugin class's `URLS` list of Django `path()` or `re_path()` patterns. When external plugins are enabled and the global `ENABLE_PLUGINS_URL` setting is true, the registry mounts active plugin patterns under `/plugin/<slug>/`. In the [small example](index.md), `path("status/", ...)` becomes `/plugin/health/status/`. Use normal Django or DRF views in these patterns and enforce authentication and object visibility in each view. Avoid a public response just because the URL is under `/plugin/`.

`/api/plugin/` is a **core-owned** API namespace: it lists plugin configurations, activates or reloads plugins for staff, provides settings endpoints and the historical calendar dispatcher. `UrlsMixin.setup_api_urls()` exists, but this repository's `plugin/urls_api.py` does not mount arbitrary `API_URLS` from plugins. A custom JSON view may live under `/plugin/<slug>/`; obtaining a new `/api/plugin/<slug>/...` route requires a core change. Do not assume an API declaration alone adds it.

## Authorization and data visibility

The URL namespace and plugin activation are not authorization mechanisms. The example uses `login_required` and `has_perm`; an API view can instead use DRF permission classes. When returning core records, use the same visibility querysets and per-object permission checks as the core endpoint for that record type. Check permission again on detail and mutation requests. Never infer permission from a visible menu, a linked record, a Dashboard widget or a Search result.

The plugin registry's staff endpoints and **Settings → Administration → Plugins** are administrative surfaces. They do not grant a plugin permission to read all Employees, Projects or funds. Keep server secrets, filesystem access and privileged actions on the backend; React receives only the data and links that the authenticated user may see.

## Other backend hooks

`SettingsMixin.SETTINGS` registers plugin-specific values; a staff user can edit exposed values in the React plugin detail page. `ScheduleMixin.SCHEDULED_TASKS` registers Django Q jobs when the schedule switch is enabled. `MailSubscriptionMixin` can add subscription-mail context/templates; `ReportMixin` can add report context. Use these hooks only when the corresponding core flow calls them, and test them against an active plugin. See [extension contracts](extensions.md) for Calendar, Dashboard and Search.

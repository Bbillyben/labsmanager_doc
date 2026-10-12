# Dashboard, Search and Calendar extensions

## Dashboard

Inherit `DashboardPluginMixin` before `LabManagerPlugin` and implement `get_dashboard_sources(self, context)` and, when needed, `get_dashboard_widgets(self, context)`. The core collects active contributions when building the Dashboard catalogue. `dashboard.registry.DataSource` declares a stable key, label, category, `supported_scopes`, `compatible_renderers` and a `provider(context, config)` callable. Optional fields include `available(context)`, `default_renderer`, `allow_multiple` and `config_fields`. The context includes the current user and a scope such as `user` or `project`; the provider must apply visibility rules before returning data.

A source with a compatible **core renderer** can create a default `WidgetDefinition` automatically. Return explicit `WidgetDefinition` objects when you need multiple presentations, sizes, availability rules or distinct widget keys. Its `source_key` must refer to an available source, and its `renderer_key` must be compatible with that source. The core validates keys and ignores a plugin's invalid or colliding contribution rather than breaking the whole Dashboard. When a plugin disappears, its definitions disappear from the available catalogue; handle existing configured widgets as unavailable rather than expecting a remote renderer to load.

The existing `FrenchHollidayPlugin.get_dashboard_sources()` is a concrete example: it returns a `DataSource` for `user` and `project`, supports the core `kpi` and `compact-list` renderers, and declares bounded `horizon_days` and `limit` configuration. The provider returns the data shape expected by those renderers. A plugin cannot register a new React renderer by shipping Python or a remote frontend bundle; a new renderer needs a change to the core frontend and its renderer catalogue.

## Global Search

Inherit `SearchPluginMixin` and return `SearchProvider` instances from `get_search_providers(self, user)`. A provider declares a stable `key`, `label`, `icon` and `SearchField` entries. Implement `visible_queryset(user)` and `make_result(obj, *, score, match_reason)`; override field query/value methods only when the standard ORM paths are insufficient. Optional autocomplete and suggestions are provider features. The search engine applies field weights and produces scores; providers must start from a permission-scoped queryset. `SearchResult` requires a nonnegative score, title, object ID, icon, match reason and an `/app/` destination. That destination must already exist in React; adding a provider does not add a page.

The live Search registry asks active plugins for providers per user and rejects duplicate or invalid keys. A provider with a failing `available(user)` check is omitted for that user. The `backend/global_search/contracts.py` contracts and existing core providers show the supported schema and ranking hooks; the plugin pattern is exercised in `backend/global_search/tests.py`.

## Calendar and related hooks

`CalendarEventMixin` supports `get_calendar_events(cls, context)`, `get_calendar_filters(cls, context)` and optional `filter_calendar_queryset(cls, queryset, context)`. The normalized Calendar service collects active plugin events and filters, validates them and scopes them to a `CalendarContext`. `FILTERS` can declare supported select, checkbox, radio, text or color controls. The `FrenchHollidayPlugin` sample returns typed events and a zone filter; project and employee contexts are intentionally handled differently. The historical `/api/plugin/calendar_plugin/` dispatcher remains a core adapter, not a new plugin API mount.

`SettingsMixin`, `ScheduleMixin`, `MailSubscriptionMixin` and `ReportMixin` cover their respective backend flows. Global switches can suppress Calendar, Schedule and Subscription contributions even while a plugin remains active. There is no general plug-and-play React component, sidebar item or remote JavaScript registration contract in this codebase.

# Screenshot scenario requirements

## Purpose and boundary

This is the functional input for Codex Capture. It inventories likely documentation images and defines a small, bounded scenario catalogue so Codex Documentation can compose future requests without knowing browser selectors or routes. The original audit did **not** start P1 Projects, implement Playwright, or change its batch; current implementation status is recorded below. “Proposed” means a capture need is known; it does not certify that a particular React control, demo record or profile has already been verified in a browser.

The source of truth for capture priority and filenames remains `SCREENSHOTS.md`; the source of truth for documented coverage remains `MATRIX.md`. This document maps those needs to scenario behavior. It includes the 22 P1 registry entries that were future at the time of the audit (P1-05–P1-26), the nine completed P0/People entries as a compatibility test, and conditional needs identified in `MATRIX.md`/`BACKLOG.md`.

## Current workflow and contract

Codex Documentation writes `documentation-project/screenshot-request.json` using JSON contract v1 (`version`, `batch`, `captures[]`; each capture has `id`, `enabled`, `profile`, `scenario`, `output`, `parameters`, `captureType`, `notes`). The Windows engine is run separately with `npm run capture:request`; it writes PNGs below `docs/assets/screenshots/` and `documentation-project/screenshot-result.json`. Codex checks the batch, each `status: success`, file presence and visual state before integration. At the time of the original audit, the request/result pair was `P1-people-001`. The current request/result pair is `P1-tools-organization-chart-001`; its single capture passed result and visual review. The earlier `P1-tools-001` batch yielded two integrated images and one rejected attempt. Integrated captures are also listed in the permanent `screenshot-refresh.json`.

Keep **version 1**. Every proposed behavior fits an existing `scenario` plus a JSON `parameters` object; no new top-level field or result format is required. The catalogue and parameter validation are engine behavior, not a wire-format change. Reject unknown scenario names, parameter names and enum values. `notes` may clarify editorial intent but must never be required to disambiguate navigation, filtering or the target state. Existing outputs and IDs remain valid. Profiles are the existing request field. `labmanager` is confirmed and selected for the P1 Finance batch; `employee` and `leader` remain valid for their respective confirmed scenarios.

Defaults below apply only where stated. A record identifier is a controlled synthetic-data anchor, not a route or database key. The initial catalogue should accept the exact anchors listed here (or a stable named fixture alias resolving to them); adding a fixture expands the catalogue without changing JSON v1. A profile must be able to see the target; a visible relationship must not be treated as permission to open a linked record.

## Confirmed catalogue subset for P1 Projects (6 October 2026)

Codex Capture now supports, with profile `employee` and the exact project anchor `ORION — Optical Resilience`: `project-section` with `section=overview|participants`; `project-planning` with `view=tasks|milestones` and `state=default`; and `calendar` with `scope=project`, `view=month`. `project-overview` remains a compatible alias. `calendar(scope=personal,view=month)` is supported and is used for the global General calendar request in P1 Calendars. The `funds`, `overdue`, Gantt and other values below remain **proposals**, not supported request values for `P1-projects-001`. The participant region is a block on Project Overview; tasks and milestones are filtered views of one React section. The corrected `P1-projects-001` run produced distinct Task and Milestone PNGs with the requested kind filters active; both passed visual review and are integrated.

## Existing scenarios and migration

| Existing scenario | Disposition | Generic equivalent or reason |
| --- | --- | --- |
| `home` | Retain | A distinct landing state, already useful for P0 and recent destinations. |
| `navigation` | Retain | A distinct sidebar/top-bar region and state, already useful for P0. |
| `global-search` | Retain and parameterise | Search overlay has unique interaction. Support `state=open\|results`; `query` is required for `results` (known example `ORION`) and absent for `open`. Existing behavior is preserved. |
| `employee-overview` | Compatibility alias | `employee-section(section=overview, employee=Camille ORREN)`. |
| `project-overview` | Compatibility alias | `project-section(section=overview, project=ORION — Optical Resilience)`. |
| `employee-contracts` | Compatibility alias | `employee-section(section=contracts, employee=Camille ORREN)`. |
| `employee-projects` | Compatibility alias | `employee-section(section=projects, view=list, employee=Camille ORREN)`. |
| `employee-leave` | Compatibility alias | `employee-section(section=leave, view=table, employee=Camille ORREN)`. |

Aliases should delegate to one implementation and preserve old defaults, output shape and success semantics. No existing request has to be rewritten. Retire aliases only after consumers have migrated; there is no need to remove them for this work.

## P1 Finance audit and required Capture extension (7 October 2026)

React places **Funds**, **Budgets** and **Contributions** on a project record. Selecting a fund reveals its Overview and scoped Expenses below the fund list; there is no standalone fund route. Tools → **Fund explorer** lists *fund items*, with filters, sorting, pagination, export and a read-only detail sheet. Tools also has **Budget explorer** and **Expenses**, but no separate screenshot of those tools is needed for this initial Finance guide. The Fund explorer sidebar entry does not guarantee data access: the backend intersects visible projects and visible funds. Project Funds is gated by `funding_visible`, derived from `fund.view_fund` globally or on the project. The seed-42 fixture groups grant view permissions to `leader` and `labmanager`; both roles have now been checked by Codex Capture. Use `labmanager` for all five documentary captures and reject an empty result. Do not assume `employee` sees Finance.

The guide documents **reading**. Project Funds, Budgets, Contributions and Expenses expose add/change/delete or sync controls only when capabilities allow them. Fund explorer is read-only. The cost-type overview shows fund items, expense points and totals; project Budgets is a separate allocation table, not a tab of a selected fund. Scoped Expenses has date, reference, description, cost type, status, contract, budget and amount, plus search, cost-type and date-range filters. The Fund explorer shows fund-item rows with project, funder, institution, period, reference, cost type, amount, consumed and available; it can show several rows per fund. Its `stale` UI filter is labelled **Overdue**, not **Ending soon**. End dates can be sorted. The only React expense trend found is a Dashboard widget (“Expense evolution”, monthly history of visible expenses); no standalone fund financial curve was found. Defer that widget to Dashboards; do not implement `financial-curve` for P1 Finance.

### React feature inventory

Here “minimum profile” means the lowest demo group with a declared relevant view permission; actual record visibility still depends on the visible project/fund intersection; the chosen Finance branches were browser checked by Codex Capture. No group alone guarantees a populated screen.

| User need | React entry / main view | Minimum declared demo profile | Read and actions | Filters or ordering | Visible information / decision |
| --- | --- | --- | --- | --- | --- |
| Find funding attached to a project | Project → Funds, fund table | `leader` (`fund.view_fund`); use `labmanager` for initial capture | Read; add/change/delete by capabilities | No list filter in this panel | Funder, institution, dates, reference, budgeted, consumed, available, activity; cover in Finance. |
| Read a fund and remaining balance | Select a row in Project → Funds, Overview | `leader` for a visible project/fund; `labmanager` for capture | Read; fund-item/expense-point actions by capabilities | Grouped cost-type rows, no user filter | Fund items, expense points and total amount/consumed/available; cover without formula claims. |
| Read budgets | Project → Budgets, table and selected budget expenses | `leader` for a visible project/fund; `labmanager` for capture | Read; add/change/delete by capabilities | No table filter in project panel | Fund, cost type, description, amount, consumed, available; cover. |
| Read contributions | Project → Contributions, table and detail sheet | `leader` for a visible project/fund; `labmanager` for capture | Read; add/change/delete by capabilities | No table filter in project panel | Fund, cost type, description, amount, period; detail has staffing/allocation; cover in budgets page without dedicated image. |
| Inspect expenses | Selected fund or budget → Expenses; Tools → Expenses | `leader` for a visible project/fund; `labmanager` for capture | Read; scoped add/change/delete/sync by capabilities; tool list is read-only with export | Scoped search, cost type, date range; tool has status, reference, description, project, funder/institution and date filters | Transaction date, reference, description, type, status, contract, budget, amount; cover read workflow. |
| Compare fund items | Tools → Fund explorer | `leader` has declared view permissions; `labmanager` for initial cross-project capture | Read-only, detail sheet, contracts count, export | Cost type, available, active, project, institution, funder, fund reference, participant, Overdue; sortable headings | One row per fund item; fund dates and balances; cover separately. |
| Find funds ending soon | Fund explorer End date sort, or project Funds End date column | Same as the underlying view | Read | Sort End date in explorer; no dedicated “ending soon” filter | Compare visible dates; no special alert or state claimed. |
| See spending over time | Dashboard Expense evolution widget only | Dashboard profile/visibility to audit in its own lot | Read widget | Not audited for Finance | No standalone fund curve in React Finance; defer. |

The demo dataset names `DM-ORION-BRIDGE` and `DM-HELIX-GRANT`, but their exact displayed numbers have not been recorded in this documentation pass. Their intended consumption contrast is therefore a conditional illustration, not a documented numeric fact.

### Available primitive 1: `project-finance`

Purpose: navigate within a visible project and capture a financial section. Required parameters: `project`, `section`; conditional required parameter: `fund` for selected-fund sections. No optional parameters or implicit section. Initially allow exact `project=ORION — Optical Resilience`; `fund=DM-ORION-BRIDGE` only for that project's selected-fund captures. Allowed `section=funds|fund-overview|fund-expenses|budgets`; reserve `contributions` for a later capture need. Reject `fund` on `funds` or `budgets`, and reject a fund that is absent from the chosen project. Default capture type: `region`, with heading, target row/context and financial columns; a capture must not silently show the whole unrelated project overview. Documentary profile: `labmanager`; `leader` was also checked by Codex Capture.

- `funds`: open Project → Funds; verify funding navigation is visible, the table is settled and the ORION fund reference, period and balance columns are visible. Intended for P1-08.
- `fund-overview`: select the specified fund in Funds; verify that fund is selected, **Overview** is populated with cost-type rows and total amount/consumed/available. Intended for P1-10. Do not assert a particular amount from fixture notes.
- `fund-expenses`: select the specified fund; verify the scoped **Expenses** heading and at least one transaction row with date/reference/amount after loading. Intended for P1-12.
- `budgets`: open Project → Budgets; verify at least one row and amount/consumed/available headings. Intended for P1-11. Do not navigate to a selected fund to reach this section.

Validation must distinguish unknown section, missing project/fund fixture, profile without funding visibility, empty expected business rows and UI drift. The engine owns navigation and waits. The request contains semantic names only, no route, selector or click sequence.

### Available primitive 2: `financial-explorer`

Purpose: capture the cross-project read-only Fund explorer. Required parameters: `view`, `anchor`; no optional parameters. Initially allow `view=fund-items`, `anchor=DM-HELIX-GRANT` only. Default capture type: `full viewport` with sidebar, filters, result count, sortable headings and a matching fund-item row. Documentary profile: `labmanager`; `leader` was also checked by Codex Capture. Open Tools → Fund explorer, confirm a settled, nonempty result, use the fund-reference filter if needed to expose the anchor, and verify a row references the requested fund. A project or funder link may be plain text when permission is absent. Reject unknown view/anchor, hidden data, empty matches and failed filter state explicitly. This covers P1-13. Do not alias it to `list-view(entity=funds)`: that family currently confirms only people/projects, and Fund explorer rows are fund items.

### Fixture and capture gate

The dataset description proposes `DM-ORION-BRIDGE` as nearly consumed and ending at T0+25, and `DM-HELIX-GRANT` as under-consumed and ending at T0+30. The five requested scenario branches have been verified by Codex Capture with `labmanager`; the filtered HELIX explorer state has multiple visible rows. The displayed balances in the five requested images have passed visual review; the usefulness of extra comparison images remains conditional. P1-14/15 remain conditional: request an extra image only if it adds a clear visible comparison beyond P1-10. P1-16 is not needed. `P1-finance-001` captured P1-08 and P1-10–P1-13 using the two available primitives. All five images are integrated after a matching success result and visual review.

The older proposal table and historical coverage matrix below predate this React Finance audit and the subsequent primitive implementation. For P1 Finance, the definitions in this section and `SCREENSHOTS.md` supersede their proposed `fund-section`, `fund-explorer` and `financial-curve` rows; those older names are **not implemented** or valid request values. `project-section(section=funds)` is likewise still unsupported.

## P1 Dashboards audit and Capture coverage (updated 11 October 2026)

React has a personal Dashboard page for any signed-in user. When a user has no personal dashboard, the page asks for a name and one of four starting templates: Employee, Leader, Lab manager or Blank; none is preselected. The seed-42 dataset instead precreates one default personal dashboard for each relevant account: `employee` → **Employee overview** from `employee`, `leader` → **Team overview** from `leader`, and `labmanager` → **Laboratory overview** from the React/backend template key `lab-manager`. A project Dashboard is a separate context. Widgets resolve visible records under the selected account; do not treat a template choice as a permission grant.

| Prepared personal view | Profile | Seed-42 default widget sources and intent | Capture status |
| --- | --- | --- | --- |
| Employee overview | `employee` | Participated projects (count and list), own milestones, own tasks and upcoming leaves | `dashboard(template=employee)` confirmed; P1-17 requested in `P1-dashboards-001`. |
| Team overview | `leader` | Managed projects (count and overdue list), managed-project milestones, subordinate employees and leaves, managed-project funds, contracts ending within 30 days | `dashboard(template=leader)` validated in Chromium with `profile=leader`; P1-18 requested. |
| Laboratory overview | `labmanager` | Visible projects (count and overdue list), upcoming milestones, visible funds (count and those ending within 60 days), contracts ending within 30 days, employee departures within 90 days | `dashboard(template=labmanager)` validated in Chromium with `profile=labmanager`; P1-19 requested. |

The dashboard UI supports selecting another personal dashboard and marking one as default. **Customize** exposes a source catalogue, widget configuration/add/remove, drag and resize on wide screens, and Save layout; personal dashboard management also includes rename, duplicate, order and delete. There is no reset-layout control in the audited React page. No separate screenshot is needed for this basic guidance. `core.expense-trend` is a line-chart source with monthly visible expenses; it is preconfigured in the **project** template, not in the three personal demo templates. It may be added to a compatible dashboard, but a dedicated widget image is not needed in P1 Dashboards. Do not request a Finance curve or assume the personal screenshots show it.

### Available values within the existing `dashboard` scenario

Keep JSON v1, scenario `dashboard`, required `parameters.template`, no optional parameters or new scenario. Three bounded combinations are validated in Chromium. `template=employee` with `profile=employee` is already confirmed; the other two are:

- `template=leader`, `profile=leader`: open the seeded **Team overview** default personal dashboard; verify its name, Leader account context and the managed-project, team, funding and contract widget sources before a `viewport` capture. P1-18.
- `template=labmanager`, `profile=labmanager`: open the seeded **Laboratory overview** default personal dashboard; verify its name, Lab manager account context and the project, fund, contract and employee-movement widget sources before a `viewport` capture. P1-19. The engine maps semantic `labmanager` to the React/backend starting template key `lab-manager`; do not put that internal key in the request.

For all three values, wait for dashboard detail and widget data to settle, reject loading and unavailable/error states for the distinguishing widgets, verify the correct default dashboard and the expected widget set, then capture a useful English viewport including heading and visible first widgets. An individual list may legitimately be empty when no record matches its filter; do not substitute a wrong dashboard to avoid that state. The seven-widget layouts may extend below a 1440 × 900 viewport; validate the complete widget set before capture, but do not require every widget to appear above the fold. Distinguish unsupported enum/profile, missing seeded dashboard, wrong selected template, missing or errored distinguishing widgets, and UI drift. The request is semantic only; no selector, route, click sequence or database ID is needed.

`P1-dashboards-001` now requests all three validated values with matching profiles. The previous `P1-finance-001` result remains untouched until the manual engine run; no Dashboard image is integrated yet.

## Proposed families and bounded parameters

The following are semantic inputs. `captureType` remains in each v1 capture entry; “region” means the useful content and its identifying heading/controls, not an arbitrary crop. The engine owns navigation, selectors, waits and cropping. Unless specified otherwise, every family must wait for final business content, reject loading/empty error states, and verify the requested synthetic anchor is visible.

### A — Existing behavior and aliases

| Scenario | Purpose; parameters | Allowed values and defaults | Capture behavior; usual profile |
| --- | --- | --- | --- |
| `home` | Show signed-in landing and recent destinations. No parameters. | No defaults. | Settled viewport with sidebar; `employee`. |
| `navigation` | Show main navigation. No parameters. | No defaults. | Settled sidebar and top bar region; `employee`. |
| `global-search` | Show the open search or results. Optional `state`; `query` only for results. | `state=open\|results`; default `open` for old requests. Initial known result query `ORION`; future query text may be supplied for a documented synthetic anchor. | Search overlay visible; result state must show matching results and query; `employee`. Free text is necessary for search, unlike finite view enums. |
| `employee-section` | Show a person's record section. Required `employee`, `section`; conditional `view`. | `employee=Camille ORREN` initially; `section=overview\|contracts\|projects\|leave`; `view`: `projects→list` (also `gantt` only after UI verification), `leave→table\|calendar`; defaults `projects→list`, `leave→table`; no `view` for overview/contracts. | Open visible person, select section/view, capture settled region including heading and useful labels. Usually `employee`. Overview may use a broader region. Generic info is already covered by overview; no separate section is justified now. |
| `project-section` | Show a project overview, participants or linked funding. Required `project`, `section`. | `project=ORION — Optical Resilience` initially; `section=overview\|participants\|funds`. No default section. | Open visible project, select section, capture heading and business rows/summary. `employee` is confirmed for overview and participants on ORION; funds remain unconfirmed for this profile. |

### B — Needed for known P1 work

| Scenario | Purpose; parameters | Allowed values and defaults | Capture behavior; usual profile |
| --- | --- | --- | --- |
| `project-planning` | Show project tasks, milestones or an overdue item. Required `project`, `view`; optional `state`. | `project=ORION — Optical Resilience` for normal views; `SELENE — Sustainable Signals` or `LYRA — Learning Research Arrays` only after confirming an overdue fixture. `view=tasks\|milestones\|gantt`; `state=default\|overdue`, default `default`. `overdue` is valid only when a visible overdue item is verified; do not infer it from project end date. | Open project planning, choose requested view, include dates/status and relevant rows. A combined tasks-and-milestones region is acceptable for P1-06 if both are legible; otherwise request two images. `employee` is confirmed for ORION tasks and milestones; other views remain subject to verification. |
| `fund-section` | Historical proposal superseded by `project-finance`. | Do not implement for P1 Finance. | React has no standalone fund section; budgets are a project section. |
| `dashboard` | Show a seeded personal dashboard. Required `template`; no default. | `employee`, `leader` and `labmanager` are confirmed with the matching `employee`, `leader` and `labmanager` profiles. | Capture a settled viewport with the matching profile and template widgets; see P1 Dashboards audit above. |
| `calendar` | Show a calendar in a documented scope. Required `scope`; conditional `project`; optional `view`, `dateAnchor`. | `scope=personal\|project` for confirmed views; `project=ORION — Optical Resilience` required for `project`, forbidden otherwise. Initial `view=month` (default) for personal/project. A Resources mode within `personal` and a global Projects tab need separate bounded parameters before capture. `dateAnchor` is an ISO date within synthetic fixture periods; omit to use the engine's fixed demo date, **not** wall-clock today. | Capture period controls, filters and visible events after navigation. `employee` is confirmed for personal and ORION project month views. The React global General calendar has a Resources mode for visible employees; it is not a separate UserSetting and Capture has no confirmed `mode=resources` parameter. The global Project calendar is a multi-project Gantt; `scope=project` opens a single project record and cannot represent this tab. P1-07 remains the single-project image, while P1-21/22 are deferred images for the global tabs. Do not require 15-day, 2-month or year images merely because controls exist. |
| `list-view` | Show a normal or filtered list where shared list behavior is confirmed. Required `entity`; optional `state`; conditional `anchor`. | Initial `entity=people\|projects`; `state=default\|filtered`; default `default`. `anchor=Camille ORREN` for people or `ORION — Optical Resilience` for projects, required for `filtered`. Expand to `funds\|expenses\|contracts` only after confirming the same filter/result semantics. | Capture list heading, active filter and matching row/count for `filtered`. Filter recipe is a bounded engine preset tied to the entity/anchor; no arbitrary filter fields or selectors. `employee` for common lists. |
| `export-action` | Show a visible export entry point. Required `source`; optional `record`. | Initial `source=project-record\|project-list\|people-list`; `record=ORION — Optical Resilience` only for `project-record`. Support each source only after the action and profile are verified. No format enum until the UI exposes a confirmed choice. | Open the source and export menu/control, capture the action and its context; `leader` likely. Separate from `list-view` because a record export is not a list state. |
| `fund-explorer` | Historical proposal superseded by `financial-explorer`. | Do not implement this name for P1 Finance. | The verified React view lists fund items; see the required primitive above. |
| `financial-curve` | Historical proposal withdrawn for P1 Finance. | Do not implement. | No standalone fund curve in audited React Finance; Dashboard widget is later work. |

`project-planning.view=gantt` is justified by the identified P2 Gantt/dependency guide; reserve this enum value but do not advertise it as implemented until the P2 UI and dependency fixture are verified. The term “15 days”, “2 months” and “year” is known as a possible calendar UI vocabulary, but no current documentation need requires a separate capture of each. Confirm actual supported controls and add finite enum values only when a guide needs them.

### C — Later or conditional, after product verification

Do not implement a general editing framework for create/update forms. If a P1 workflow is confirmed and needs an image, add a narrowly scoped `action-sheet` with bounded `subject=project|task|milestone|leave|expense`, `action=create|edit` and a verified synthetic anchor/profile. Do not expose arbitrary forms, field names or permissions. P1 Reports & Exports uses the React `ReportExportDialog` on Employee/Project records; its needed capture state is specified below, without a legacy chooser. Dashboard editing, advanced search, imports, transversal contract/finance explorers, printing and P3 reference screens likewise require targeted UI verification before a family/enum is committed. P1 Tools has now verified the corresponding React screens; its concrete capture needs are specified in the P1 Tools section below. The inventory below records them as **conditional**, not an instruction to implement now.

## P1 Teams — confirmed Capture capability

Capture supports the React Teams list with `list-view(entity=teams,state=default)` and the Quantum Materials Studio Information section with `team-section(team=Quantum Materials Studio,section=information)`. Both use the existing JSON v1 runner with profile `leader`. The two states were confirmed by Codex Capture and produced two matching `success` results in `P1-teams-001`; both PNGs passed visual review and are integrated.

| Capture | Route and expected settled state | Demo selection | Confirmed request |
| --- | --- | --- | --- |
| P1-27 Teams list | `/app/teams/`; heading, Name/Leader/Members columns, filters and nonempty result including Quantum Materials Studio | `leader`; Quantum Materials Studio, led by Elina Varrel | `list-view` with `{"entity":"teams","state":"default"}`; viewport |
| P1-28 Team Information | `/app/teams/{id}` Information tab; heading, leader and populated members with dates/status; no open sheet or menu | `leader`; Quantum Materials Studio, led by Elina Varrel | `team-section` with `{"team":"Quantum Materials Studio","section":"information"}`; region |

No separate edit-sheet image is needed. P1-27/28 are included in the permanent `screenshot-refresh.json` after visual validation and integration.

## P1 Organizations — confirmed Capture capability

Institutions and Funders share one React list component and one detail component. The two documentary images below are sufficient: one Institutions list illustrates the shared controls, and one Funder Information view illustrates the shared record layout and relationship summary. Separate Funders list and Institution detail images would repeat the interface. The seed-42 fixture contains NVAU (North Vale Academic University) and VRC (Vale Research Council), both referenced by multiple funds. `labmanager` has the relevant organization, fund, project and contract view permissions. The requested NVAU row and VRC summary figures passed result and PNG validation. The fixture does not establish populated contacts or additional-information values; these are explained in text and are not capture gates.

| Requested screen | React route and expected settled state | Demo anchor | Confirmed Capture branch |
| --- | --- | --- | --- |
| P1-29 Institutions list | `/app/organizations/institutions`; heading, short/full name columns, search, sorting, result count and NVAU row; no loading or open sheet | `labmanager`; NVAU — North Vale Academic University | `list-view` with `{"entity":"institutions","state":"default"}`; viewport |
| P1-30 Funder Information | `/app/organizations/funders/{id}`; Information tab selected, VRC title/short name and settled project/contract summary, with additional-information section or empty state | `labmanager`; VRC — Vale Research Council | `organization-section` with `{"entity":"funder","organization":"VRC — Vale Research Council","section":"information"}`; region |

These branches are confirmed in the existing JSON v1 Capture pipeline. `P1-organizations-001` returned two matching successes; both PNGs exist, passed visual review and are integrated in the guide and permanent `screenshot-refresh.json`.

## P1 Reports & Exports — confirmed Capture capability

On Employee and Project records, the heading action menu offers **Export Word** and/or **Export PDF** only when the record's `can_export_word` / `can_export_pdf` capability permits. Choosing a format opens `ReportExportDialog`; React fetches templates for that entity, record and format. The first template is selected when present. With no templates the choice and Export action are disabled; a fetch failure shows an error. Employee reports alone have From/To dates (default previous year through today, individually clearable, validated in order). Project reports have no timeframe controls. On Export, React requests server generation and downloads the returned `.docx` or `.pdf`; failure stays in the dialog. There is no React file preview.

Capture has validated `scenario=entity-report` with required `entity=employee|project`, `target` and `format=word|pdf`. Profile `labmanager` reaches both selected records. The demo deployment now exposes compatible templates, and Capture confirmed a selected template and enabled Export button for both combinations below. The existing JSON v1 contract is unchanged.

| Requested screen | React context and settled state | Confirmed Capture parameters | Output |
| --- | --- | --- | --- |
| P1-24 Employee Word dialog | Camille ORREN → Export Word; selected template, From/To period, enabled Export; no loading or action menu overlay | `{"entity":"employee","target":"Camille ORREN","format":"word"}` | `reports-and-exports/employee-word-dialog.png` |
| P1-25 Project PDF dialog | ORION — Optical Resilience → Export PDF; selected template, enabled Export, no From/To period, loading or action menu overlay | `{"entity":"project","target":"ORION — Optical Resilience","format":"pdf"}` | `reports-and-exports/project-pdf-dialog.png` |

The `P1-reports-001` batch returned two matching successes. Both PNGs passed visual review, are integrated in the guide and are included in `screenshot-refresh.json`. The list-export dialog is a different React workflow on Employees, Projects, Teams, Contracts and financial tools, with XLSX/CSV/TSV/XLS choices and current filters; text is sufficient for this P1 guide. No legacy report-selection route or generated-file screenshot is needed.

## P1 Settings & Preferences — confirmed Capture capability

React exposes five authenticated personal routes under `/app/settings`: `user`, `interface`, `notifications`, `common` (Favorites and subscriptions), and `stale` (dashboard alert horizons). The account menu opens `/app/settings/user`; `/app/settings` redirects there. `lists/:groupKey` manages shared lists, and `admin/*` is restricted to staff. Neither belongs to this personal guide. All five personal routes are available to the normal `employee` profile. The three requested images below cover the account landing page, the compact interface controls, and the distinct notification controls. Common and Stale are accurately described in text without separate images.

Capture has validated `settings-section` with profile `employee`, required `parameters.section` and the values `user|interface|notifications|favorites|stale-alerts`. The semantic `favorites` and `stale-alerts` values map to React routes `/app/settings/common` and `/app/settings/stale`; only `user`, `interface` and `notifications` are requested in this batch. Capture confirmed each requested section active, API-backed settings settled and no stray interface. The JSON v1 contract and existing scenarios are unchanged.

| Requested screen | React route | Expected section and state | Profile | Confirmed Capture parameters |
| --- | --- | --- | --- | --- | --- |
| P1-31 account landing | `/app/settings/user` | User settings selected; account facts, linked Employee if present, email list/actions or honest empty state; no password sheet | `employee` | `{"section":"user"}`; viewport |
| P1-32 interface | `/app/settings/interface` | Interface selected; login destination, current-organization switch, map provider and theme choices with saved values | `employee` | `{"section":"interface"}`; region |
| P1-33 notifications | `/app/settings/notifications` | Notifications selected; email status, frequency, language and useful notification controls; no loading | `employee` | `{"section":"notifications"}`; viewport |

`/app/settings/common` lists favorites and subscriptions with immediate Remove actions; `/app/settings/stale` has four non-negative month inputs used by dashboard summaries. Capture supports these routes through the `favorites` and `stale-alerts` semantic values, but no image of either is necessary for this initial guide. The notification leave Calendar/List choice affects email presentation. The global calendar's Calendar/Resources mode is selected on the calendar page, not by a personal UserSetting. `P1-settings-001` returned three matching successes. P1-31/32/33 passed visual review, are integrated in the guide and are included in `screenshot-refresh.json`.

## Future documentation needs and coverage matrix

“Page” names for unfinished guides are working destinations, not files to create in this pass. `R` = region, `V` = viewport, `I` = interaction state. A row with “conditional” must be verified against the v1 React deployment before Codex Documentation requests it. The scenario column is a proposal; A/B/C indicates implementation scope above. Unless noted, anchors are from the synthetic seed-42 dataset.

| Registry / domain and documentation intent | Likely page | Anchor; likely profile | Expected UI state; type | Scenario and parameters | Priority / note |
| --- | --- | --- | --- | --- | --- |
| P0-01 Home: orient after sign-in | Getting started | Demo home; employee | Sidebar, recents; V | `home` | Done / A |
| P0-02 Navigation: identify main controls | Interface | Demo home; employee | Sidebar and top bar; R | `navigation` | Done / A |
| P0-03 Search: open control | Search | Demo home; employee | Empty open overlay; I | `global-search(state=open)` | Done / A |
| P0-04 Search: find project | Search | ORION; employee | Query and result; I | `global-search(state=results,query=ORION)` | Done / A |
| P0-05 People: orient on a person | View a person | Camille ORREN; employee | Overview, status, hierarchy; R | `employee-section(employee=Camille ORREN,section=overview)` | Done / A |
| P0-06 Projects: orient on a project | View a project | ORION; employee | Overview and primary sections; R | `project-section(project=ORION,section=overview)` | Done / A |
| P1-01 People: read contracts | Projects and contracts | Camille ORREN; employee | Contract row, period, allocation, state; R | `employee-section(employee=Camille ORREN,section=contracts)` | Done / A |
| P1-02 People: read participations | Projects and contracts | Camille ORREN; employee | List with ORION, role and period; R | `employee-section(employee=Camille ORREN,section=projects,view=list)` | Done / A |
| P1-03 People: read absences | Leave | Camille ORREN; employee | Table with two absences; R | `employee-section(employee=Camille ORREN,section=leave,view=table)` | Done / A |
| P1-05 Projects: see participants and allocation | Participants | ORION; employee | Participant rows with role, allocation and period; R | `project-section(project=ORION,section=participants)` | P1 / B; ensure workload visible or use a second planning image |
| P1-06 Projects: see tasks and milestones | Planning | ORION; employee | Task/milestone rows and dates; R | `project-planning(project=ORION,view=tasks)` and `view=milestones` if one image cannot show both | P1 / B |
| P1-07 Projects: read project calendar | Project calendar | ORION; employee | Month, period and filters; R | `calendar(scope=project,project=ORION,view=month)` | P1 / integrated; distinct from the global Projects Gantt |
| P1-08 Finance: find project funding | View a fund | ORION / DM-ORION-BRIDGE; labmanager | Fund table with period and balance; R | `project-finance(project=ORION,section=funds)` | P1 / integrated from `P1-finance-001` |
| P1-09 Projects: explain overdue item | Planning | SELENE or LYRA; leader | Visible overdue item in ended project; R | `project-planning(project=verified fixture,view=tasks,state=overdue)` | P1 conditional / B after fixture check |
| P1-10 Finance: read fund overview | View a fund | ORION / DM-ORION-BRIDGE; labmanager | Selected fund and overview totals; R | `project-finance(project=ORION,section=fund-overview,fund=DM-ORION-BRIDGE)` | P1 / integrated from `P1-finance-001` |
| P1-11 Finance: read budget | Budgets and expenses | ORION; labmanager | Project budget table and balances; R | `project-finance(project=ORION,section=budgets)` | P1 / integrated from `P1-finance-001` |
| P1-12 Finance: read expenses | Budgets and expenses | ORION / DM-ORION-BRIDGE; labmanager | Selected fund expense rows; R | `project-finance(project=ORION,section=fund-expenses,fund=DM-ORION-BRIDGE)` | P1 / integrated from `P1-finance-001` |
| P1-13 Finance: explore fund items | Fund explorer | DM-HELIX-GRANT; labmanager | Filters and matching fund-item row; V | `financial-explorer(view=fund-items,anchor=DM-HELIX-GRANT)` | P1 / integrated from `P1-finance-001` |
| P1-14 Finance: explain low remaining balance | View a fund | DM-ORION-BRIDGE candidate; labmanager | Distinct low balance if visible; R | Reuse `project-finance(section=fund-overview)` only if needed | P1 / conditional |
| P1-15 Finance: explain unused balance | View a fund | DM-HELIX-GRANT candidate; labmanager | Distinct high balance if visible; R | `project-finance(section=fund-overview)` after project and UI check | P1 / conditional |
| P1-16 Finance: explain trend | No Finance page | — | No standalone fund curve; — | No Finance scenario | P1 / not needed; Dashboard widget later |
| P1-17 Dashboards: read personal view | Use your dashboard | Employee overview; employee | Settled project, milestone, task and leave widgets; V | `dashboard(template=employee)` | P1 / requested in `P1-dashboards-001` |
| P1-18 Dashboards: read leader view | Use your dashboard | Team overview; leader | Managed projects, team, funds and contracts; V | `dashboard(template=leader)` | P1 / requested in `P1-dashboards-001` |
| P1-19 Dashboards: read lab view | Use your dashboard | Laboratory overview; labmanager | Projects, funds, contracts and employee movements; V | `dashboard(template=labmanager)` | P1 / requested in `P1-dashboards-001`; alias resolved by Capture |
| P1-20 Calendars: read global General calendar | Calendars | Synthetic leave/events; employee | Month and events; R | `calendar(scope=personal,view=month)` | P1 / integrated from `P1-calendars-001`; target `/app/calendars` |
| P1-21 Calendars: read global Project calendar | Calendars | Visible projects; employee | Cross-project Gantt; R | Needs a bounded global-projects tab value; existing `scope=project` is a single project record | P1 / text prepared, image deferred |
| P1-22 Calendars: global Resources mode | Calendars | Visible employees; employee | Employee rows, visibility selector and leave events; R | Needs bounded `mode=resources` with `scope=personal,view=month`; `scope=resource` does not describe the React screen | P1 / text prepared, image deferred |
| P1-23 Common lists: show applied filter | Search and filters | Camille or ORION; employee | Filter, count, matching row; I | `list-view(entity=people\|projects,state=filtered,anchor=matching fixture)` | P1 / B; choose one actual list |
| P1-24 Employee Word report | Generate reports | Camille ORREN; labmanager | React ReportExportDialog, Word template and dates; I | `entity-report(entity=employee,target=Camille ORREN,format=word)` | P1 / integrated from `P1-reports-001` |
| P1-25 Project PDF report | Generate reports | ORION — Optical Resilience; labmanager | React ReportExportDialog, PDF template, no dates; I | `entity-report(entity=project,target=ORION — Optical Resilience,format=pdf)` | P1 / integrated from `P1-reports-001` |
| P1-26 Favorites: revisit saved item | Favorites/settings | ORION; employee | Favorite item visible; R | No new primitive yet; `home` if recent/favorite is visible, else dedicated state after UI check | P1 conditional / C |
| Matrix: create/edit project | Project guide | ORION; leader | Permitted action and form; I | `action-sheet(subject=project,action=create\|edit)` only after verification | P1 conditional / C |
| Matrix: create/edit task or milestone | Planning | ORION; leader | Permitted detail/form; I | `action-sheet(subject=task\|milestone,action=create\|edit)` after verification | P1 conditional / C |
| Matrix: manage leave | Leave workflow | Camille; authorised profile | Permitted add/edit control; I | `action-sheet(subject=leave,action=create\|edit)` after verification | P1 conditional / C; reading already covered |
| Matrix: contributions and expense entry | Budgets and expenses | ORION; authorised profile | Read-only details or later form; R/I | `project-finance(section=budgets)` for reading; `action-sheet` only after a separate editing scope | P1 reading prepared / editing conditional |
| Matrix: print Gantt/calendar | Exports and printing | ORION; leader | Print entry/preview; I | Dedicated print state after UI verification | P1 conditional / C |
| Matrix P2: advanced search and suggestions | Advanced search | ORION; profile TBD | Query builder/suggestions; I | Dedicated advanced-search after verification | P2 / C |
| Matrix P2: Gantt and dependencies | Gantt guide | ORION; leader | Timeline and visible link; R | `project-planning(project=ORION,view=gantt)` | P2 / C; confirm dependency fixture |
| Matrix P2: personalise dashboard | Dashboard editor | Template TBD; authorised profile | Editor and widget controls; V/I | Dedicated dashboard-editor after verification | P2 / C |
| P1 Tools: cross-record contracts | Tools | Demo contract; labmanager | Searchable cross-record result; V | `list-view(entity=contracts,state=default)` confirmed; see P1 Tools | P1 / integrated |
| P1 Tools: import entry | Tools | Employees profile; admin | Type selected, template and file chooser; V | `tool-view(tool=import,selection=employees)` confirmed; see P1 Tools | P1 / integrated |
| Matrix P3: team/organisation/resource view | Reference guides | Demo team/org/resources; profile TBD | Record or timeline, if in v1 scope; R | Reuse record-section/calendar only after concrete need and fixture | P3 conditional / outside initial implementation |
| Matrix P3: notes, hierarchy, settings, reports/plugins | Reference guides | Camille or fixture TBD; profile TBD | Specific visible state, if documented; R/I | Reuse a confirmed React record/dialog state where fit; otherwise specify after UI audit | P3 conditional / outside initial implementation |

The final two P3 rows group topics that have no approved screenshot request. They are explicitly outside the initial catalogue, not silently omitted. P0 navigation/home/search and People have no additional required image in current P1 work. The current P0 people overview already shows the empty additional-information area; do not fabricate Generic Info data.

## Functional validation and result errors

For every capture, the engine should validate the scenario and bounded parameter combination **before** UI interaction; resolve the requested synthetic anchor; use the requested profile; confirm the target record and section/view are actually accessible; wait for business content to finish loading (including no generic loading state or busy indicator); verify expected headings/controls and a real anchor row/event/amount when relevant; then capture the requested region or viewport. An empty section must not masquerade as a successful example. For a conditional capture, unsupported deployment features should produce a failed/skipped result with a clear reason, never a substitute screen. Preserve the requested `id`, `profile`, `scenario` and output association in the result so Codex Documentation can match it.

Functional error messages should distinguish at least:

- Unknown scenario or parameter; unsupported enum or combination, for example `Unsupported section 'foo' for scenario 'project-section'`.
- Missing fixture, for example `Project 'ORION — Optical Resilience' was not found`.
- Access/profile mismatch, for example `Requested view 'calendar' is unavailable for profile 'employee'`.
- Known section with no expected data, for example `No visible expense rows found for fund 'DM-ORION-BRIDGE'`.
- Timeout while waiting for settled content, for example `Timed out waiting for project participants to finish loading`.
- UI/contract drift, for example `Expected 'Participants' section was not present after opening project`.

Use the existing result's failed-capture status/error field if available; confirm its exact shape with the Capture implementation. Do not report `success` merely because a PNG was written. Keep technical diagnostics in Capture logs; the result should state the functional failure clearly enough for Codex Documentation to repair the request or report a real UI issue.

## Open questions for Codex Capture, in implementation order

1. Finance profile and navigation checks are complete for `labmanager` and `leader`; `labmanager` is the capture profile in `P1-finance-001`. Employee access to ORION overview and participants remains confirmed for P1 Projects.
2. Project Funds, selected-fund Overview/Expenses and project Budgets are implemented as distinct `project-finance` sections. Participants remain a block on Project Overview; tasks and milestones are filtered views of one planning section.
3. Confirm a seed-42 overdue item on SELENE or LYRA, and which of DM-ORION-BRIDGE / DM-HELIX-GRANT actually demonstrates low versus high remaining balance.
4. Confirm calendar scopes and labels. Only month is required initially; resource timeline and 15-day, 2-month and year variants require a concrete page need plus verified UI support.
5. P1-07 is the calendar within one project; P1-21 is the global multi-project Gantt and cannot reuse that image. Participants and tasks/milestones already have integrated images.
6. Confirm list filter semantics and export source/profile. `list-view` must not claim support for fund/expense/contract lists until their behavior is checked. The React Employee/Project report dialog is audited above; confirm favorites scope separately before any dedicated scenario.
7. Confirm the error field and skipped/failed conventions in the existing v1 result implementation; retain the v1 request contract.

## Recommended implementation order

1. **A:** centralise common waits/validation; add `employee-section` and `project-section` with compatibility aliases; parameterise `global-search` while retaining `home` and `navigation`. Prove equivalence using the nine completed captures, without changing their published PNGs.
2. **B for Projects:** `project-planning(view=tasks|milestones)`, `calendar(scope=project,view=month)` and `project-section(section=participants)` are implemented for ORION with `employee` and used in `P1-projects-001`. Project funds are covered by the completed Finance batch; overdue planning remains later work.
3. **Finance complete:** `project-finance` and `financial-explorer(view=fund-items)` were used with `labmanager` in `P1-finance-001`; all five captures are integrated. The Dashboard `employee`, `leader` and `labmanager` values are validated and requested in `P1-dashboards-001`; personal calendar, list/filter and export families remain for their respective lots. No Finance curve scenario is needed.
4. **C:** add later families only for confirmed P2/P3 guides. The bounded Import entry state needed by P1 Tools is now confirmed below; other edit, print and favorite states remain conditional.

`P1-tools-001` completed with two validated successes (Contracts and Import) and one failed Organization chart attempt. The targeted `P1-tools-organization-chart-001` retry with `labmanager` succeeded. All three Tools images are integrated; `screenshot-refresh.json` contains 34 images. P1-21/22 remain text-only.

## P1 Tools — completed captures

Three already selected views now have validated semantic states in the existing JSON v1 pipeline. `financial-explorer(view=fund-items,anchor=DM-HELIX-GRANT)` and integrated P1-13 already cover Fund explorer, so it is not recaptured. Budget explorer, Expenses and Data consistency remain text-only; no Capture extension is required for this lot.

| Capture | React route and settled state | Confirmed request and profile |
| --- | --- | --- |
| P1-34 Organization chart | `/app/tools/organization-chart`; populated and fully rendered hierarchy, Search/Current only/Fit/Print controls, no open search results, loading or overlay | `tool-view`, `{"tool":"organization-chart"}`, `labmanager` (Noé), viewport |
| P1-35 Contract Hub | `/app/tools/contracts`; transversal Contracts list with filters, headings, result count and nonempty rows; no open detail or export dialog | `list-view`, `{"entity":"contracts","state":"default"}`, `labmanager`, viewport |
| P1-36 Import | `/app/tools/import`; Employees selected, template download and file chooser visible; no file loaded or operation started | `tool-view`, `{"tool":"import","selection":"employees"}`, `admin`, viewport |

Capture confirmed all three branches and their profiles. `P1-tools-001` returned success for P1-35 Contracts and P1-36 Import; both images passed visual review and are integrated in the guide and permanent refresh manifest. `labmanager` cannot access Import; P1-36 uses `admin`. The original P1-34 attempt failed before creating a PNG. The corrected Organization chart primitive was validated with 31 visible Employee nodes and relationships using `labmanager` (Noé), with stable framing, no loader and no stray panel. The previous PNG with `employee` showed only Camille ORREN and was rejected visually. The `P1-tools-organization-chart-001` request contained **only P1-34**, using `labmanager` and `tool-view(tool=organization-chart)`. It returned one success; the Noé PNG shows the full multi-node hierarchy and visible edges without loading or stray panel. P1-34 passed visual review and is integrated in the guide and permanent refresh manifest.

## Admin — Instance administration: confirmed Capture capabilities

Capture has validated both states with `profile=admin` and the existing JSON v1 runner:

| Required screen | React route | Confirmed primitive | Expected stable state |
| --- | --- | --- | --- |
| General instance settings | `/app/settings/admin/general` | `admin-settings-section`, `{"section":"general"}` | General active; global setting rows and current values loaded; no edit sheet, loader or stray menu |
| Fund reference-list group | `/app/settings/lists/fund` | `admin-reference-list`, `{"group":"fund"}` | Fund group active; cost-type hierarchy and controls loaded; no form, loader or stray menu |

The two requested states are in `ADMIN-instance-001`; the prior Capture extension requirement is resolved. Data consistency (`/app/tools/data-consistency`) is documented without a new image because no nonempty, stable demo issue has been confirmed. Do not add it to this batch by assumption.

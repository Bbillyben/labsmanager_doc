# Use the tools

Open **Tools** in the sidebar to work across records. The menu contains seven React tools: **Data consistency**, **Import**, **Organization chart**, **Contracts**, **Fund explorer**, **Budget explorer** and **Expenses**. Data consistency and Import appear only when your account has the corresponding permission. Other links may be visible even when a particular record or action is restricted; the lists and record links reflect what you can access.

## Data consistency

**Tools → Data consistency** shows detected issues across the records you can manage. Switch between **Active** and **Accepted** issues; if several rules are available, choose a rule to narrow the list. Each row identifies the issue and its related employee, project and object. Open an available employee or project link to inspect the source record.

Available actions depend on the issue and your rights. They can include adding a missing participant, extending an employee, project or fund date, accepting an exception with a reason, or reopening an accepted issue. Check the proposed change before confirming it. If no issue matches the selected status or rule, the list shows an empty state. This tool has no list export control. For decisions about corrections and accepted exceptions, see [Review data consistency](../../admin/instance-administration/data-consistency.md).

## Import

**Tools → Import** is shown only to accounts allowed to import data. The available types currently include **Expenses**, **Employees** and **Expense timepoints**; the screen lists each type’s accepted file formats and offers a matching template.

1. Choose the import type and download its template if useful.
2. Select a file. If it has multiple sheets, select the sheet to use. Review the recognized, missing and extra columns.
3. Select **Check** to preview the import. The preview reports new, updated, unchanged and erroneous rows, with row details. Download the errors CSV when offered.
4. Select **Confirm** only after reviewing the preview. The button appears only when the preview can be committed; confirmation applies the import and displays its result.

<figure class="lm-screenshot" markdown>
![Import tool with Employees selected, template downloads and no file chosen](../../assets/screenshots/tools/import.png)
</figure>

Selecting a different type or sheet clears the later preview. A failed upload or validation shows an error on the page. Checking a file does not itself confirm the import.

## Organization chart

**Tools → Organization chart** displays the visible employee hierarchy. Search for a person, then choose a matching result to focus their position. Use **Current only** to include or exclude former employees; this choice is saved for your account. Expand or collapse branches, pan or zoom the chart, and use **Fit** to recenter it. **Print** opens the chart print view. A name links to its [Employee record](../people/view-person.md) only when you can view that record. The chart can also show an empty state if no employee is available.

<figure class="lm-screenshot" markdown>
![Organization chart showing visible employees, reporting relationships and chart controls](../../assets/screenshots/tools/organization-chart.png)
</figure>

## Contracts

**Tools → Contracts** lists contracts across the records visible to you. Filter by active, ongoing or stale state, employee, contract type or status, project, funder or institution. Sort a column or move between pages to inspect results. Rows show the employee, contract type and status, dates, project and financial context where available. Select a row to read its details and related expenses; follow Employee or Project links when permitted.

<figure class="lm-screenshot" markdown>
![Contract Hub showing the transversal list, fourteen contracts and its filter and export controls](../../assets/screenshots/tools/contracts.png)
</figure>

Depending on your rights, you may edit the contract or its notes from the selected row. **Export** downloads the currently filtered list through the [list export dialog](../reports-and-exports/generate-reports.md). For contracts belonging to one person, use the [Employee Contracts section](../people/work-and-contracts.md). An empty result means no contract matches the current filters and access rights.

## Fund explorer

**Tools → Fund explorer** lists fund items across visible projects, with funding period, amount, consumed and available values. Filter by project, funder, institution, reference, cost type, participant or availability; use the activity and overdue choices as needed. Sort, open a row’s details or related contracts where offered, and export the filtered list. The [Fund explorer guide](../finance/fund-explorer.md) explains this view and includes its screenshot. To inspect a fund inside one project, use [View a fund](../finance/view-a-fund.md).

## Budget explorer

**Tools → Budget explorer** compares budget lines across visible projects. Filter by activity, cost type, contract or employee type, employee, project, institution, funder, fund reference or available amount. Sort the list, select a line for read-only details, or export the filtered list. To work within one project, use [Budgets and expenses](../finance/budgets-and-expenses.md). The explorer does not expose a budget edit form.

## Expenses

**Tools → Expenses** lists expenses across visible projects. Filter by cost type, date range, description, project, institution, funder, fund reference, status or expense reference. Sort, select a line for read-only details, or export the filtered list. To work within one project or fund, use [Budgets and expenses](../finance/budgets-and-expenses.md). The transversal tool does not expose an expense edit form.

The three financial tools share filtering, sorting, pagination and list export controls. Their rows and related-record links depend on your access rights; a filter can also produce an empty list.

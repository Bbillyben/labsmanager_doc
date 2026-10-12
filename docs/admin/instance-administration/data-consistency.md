# Review data consistency

Open **Tools → Data consistency** (`/app/tools/data-consistency`) to review detected issues in records visible to you. The sidebar entry appears when your account can manage consistency exceptions; the demo `admin` account is suitable. The API permits signed-in users to read issues scoped to visible records, but accepting and reopening exceptions requires staff status or the corresponding exception permission.

The page shows counts, **Active** and **Accepted** views, a rule selector when several rules exist, related Employee and Project links, and pages of results. Current rules cover:

- Contracts whose Employee is absent from Project participants, or whose dates fall outside the Project, Employee or Fund period.
- Funds outside Project dates; Expenses outside Fund dates.
- Tasks or milestones outside Project dates; Projects without a leader.

Choose an issue and inspect its source records before acting. Depending on the rule and your record permissions, React may offer **Add employee to participants**, a date extension with a before/after confirmation, or a link to edit Project participants. Date extension changes the relevant Employee, Project or Fund dates; it is offered only when you can edit that record. Check the effect on other linked records before confirming.

**Accept exception** records an accepted inconsistency and an optional reason; it does not correct the source records. **Accepted** lists accepted issues with the accepting user and date. **Reopen issue** returns an exception to active review when permitted. Acceptance and reopening are restricted to staff or accounts with the corresponding Data consistency exception permission. A stale issue or missing permission can prevent an action even when the row was previously visible.

The [Tools overview](../../user-guide/tools/index.md) explains where to find the tool; this page covers its administrative decisions. No export is offered on the current React page.

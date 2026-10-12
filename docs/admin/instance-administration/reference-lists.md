# Maintain reference lists

Open **Settings → LabsManager lists** and choose a group. React loads the groups from the current backend registry. Any signed-in user can read these lists; **Add** and row **Edit** appear only when the account has the relevant model permission. The current registry exposes nine lists in six groups:

| Group / route under `/app/settings/lists/` | Lists | Used for |
| --- | --- | --- |
| **Fund** · `fund` | Cost types | Classifying funding items, budgets and expenses; the list has a hierarchy and HR/focus flags. |
| **Contract** · `contract` | Contract types | Classifying Employee contracts. |
| **Leaves** · `leaves` | Leave types | Classifying absences; entries include short names and colours. |
| **Project** · `project` | Project information types | Labelling structured additional information on Projects. |
| **Staff** · `staff` | Employee types; Employee information types | Classifying Employees and their structured additional information. |
| **Organization** · `organization` | Organization information types; Contact information types; Contact types | Labelling organization and contact information. |

<figure class="lm-screenshot" markdown>
![Fund reference lists with Cost types, five populated rows and Add control](../../assets/screenshots/admin/instance/reference-fund.png)
</figure>

Choose a group, then use **Add** in the relevant list or the action menu on a row to edit it. The form shows only fields that the backend permits for that operation; save to apply the change. A changed label or type can affect existing records that refer to it, so check its current use before editing. The registry currently disables deletion for all nine lists; do not expect a Delete action. These are instance reference values, not personal settings.

Institutions and funders are separate organization records, not entries in this registry. See [Find and view organizations](../../user-guide/organizations/find-and-view-organizations.md) for their React lists and records.

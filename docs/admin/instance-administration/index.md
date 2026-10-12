# Administer an instance

Use **Settings → Administration** for instance-wide controls. The four sections below appear only for a staff account (`is_staff`); the API also requires staff access. In the demo, use the `admin` profile. Personal preferences under **Settings → User settings** affect only the signed-in account and are covered in the [user settings guide](../../user-guide/settings/manage-your-settings.md).

<figure class="lm-screenshot" markdown>
![Administration General settings with five loaded instance controls and the General section selected](../../assets/screenshots/admin/instance/general-settings.png)
</figure>

| React section | Route under `/app` | What you can do |
| --- | --- | --- |
| **General** | `/settings/admin/general` | Change the mail subject prefix, subordinate and co-leader editing rules, audit-log retention and new-employee name casing. Values are saved per control and apply at instance level. |
| **Users** | `/settings/admin/users` | View accounts and last login; link, change or unlink an Employee record. Send invitations, inspect their state, adjust a pending invitation's Employee assignment, and remove expired invitation confirmations after confirmation. |
| **Notifications** | `/settings/admin/notifications` | Review pending notifications; **Check notifications** queues eligible items and **Send pending** dispatches them. These actions affect notification delivery, so review the queue before sending. |
| **Plugins** | `/settings/admin/plugins` and `/settings/admin/plugins/:pluginKey` | Set global plugin switches, reload the plugin registry, review plugin errors and open a plugin's available settings, schedules and URLs. Plugin details depend on installed plugins and their enabled mixins. |

In **Users**, group choices for invitations are available only to a superuser. The React page does not edit the groups or staff status of an existing account. Use **Django Admin** at `/admin/` for those account and group operations when needed; its user form exposes active, staff, superuser and group fields. The React page handles normal Employee links and invitations. An Employee already linked to another User cannot be assigned again.

The reference lists are a separate Settings area with [their own guide](reference-lists.md). [Data consistency](data-consistency.md) is under **Tools**, with its own record-level permissions. Installation, deployment and initial database setup are covered in the [installation guide](../installation/index.md).

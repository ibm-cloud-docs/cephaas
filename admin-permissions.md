---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: admin permissions, non-admin permissions, role-based access, Fusion as a Service access

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding admin vs non-admin permissions
{: #admin-permissions}

Understand how administrator and non-administrator permissions affect what you can view and manage in Fusion as a Service.
{: shortdesc}

## Administrator access
{: #admin-permissions-list}

Users with administrator permissions can manage deployment and cluster storage settings.

Administrators can do the following tasks:

- View deployment capacity and cluster information.
- Open **Settings** and manage the default cluster quota.
- Enable Fusion services for a cluster.
- Update cluster storage quotas.
- Review warnings, alerts, and cluster status.
- Open the OpenShift console, subject to cluster access permissions.

## Non-administrator access
{: #non-admin-permissions-list}

Users without administrator permissions can review information, but they cannot change deployment or cluster storage settings.

Non-administrators can do the following tasks:

- View deployment capacity and cluster information.
- Review cluster details, storage status, warnings, and alerts.
- Open the OpenShift console, subject to cluster access permissions.

Non-administrators cannot do the following tasks:

- Edit the default cluster quota.
- Enable or disable Fusion services.
- Update cluster storage quotas.
- Change deployment settings.

## How permissions affect the UI
{: #ui-behavior-permissions}

The Fusion as a Service UI changes based on your permission level.

Administrator view
:   Action controls such as **Edit quota**, **Enable Fusion services**, and quota update actions are available when the deployment and cluster state allow them.

Non-administrator view
:   Management controls are unavailable, hidden, or read-only. You can still review deployment and cluster information.

## Related tasks
{: #admin-permissions-next}

- [Actions available to admin users](/docs/sdsaas?topic=sdsaas-admin-user-actions)
- [Actions available to non-admin users](/docs/sdsaas?topic=sdsaas-non-admin-user-actions)
- [Understanding read-only views and restrictions](/docs/sdsaas?topic=sdsaas-readonly-views-restrictions)

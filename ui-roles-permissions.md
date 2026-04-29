---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: UI behavior, user roles, permissions, admin actions, non-admin actions, read-only states, warning states, confirmation actions, Fusion as a Service UI, role-based access

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding UI behavior, roles, and permissions
{: #ui-roles-permissions}

The Fusion as a Service UI adapts based on your role and the current state of deployments and clusters. Understanding how roles affect available actions, when the UI shows warnings or read-only states, and when confirmations are required helps you work efficiently.
{: shortdesc}

## Role-based access and capabilities
{: #role-based-access}

Your role determines which actions you can perform in Fusion as a Service. The UI reflects your permissions by showing, hiding, or disabling certain controls and pages.

### Administrator capabilities
{: #admin-capabilities}

Administrator users can review deployment information and perform management actions for clusters, quotas, and storage settings in Fusion as a Service.

Administrators can do the following tasks:

- Open deployment settings.
- Set or edit the default cluster quota.
- Enable Fusion services for a cluster.
- Update a cluster storage quota.
- Review cluster warnings, alerts, and storage status.
- Open the OpenShift console, subject to cluster access permissions.

Administrators commonly work in the following areas:

Deployment overview
:   Review capacity information for the deployment.

Clusters tab
:   Review clusters, open cluster details, and manage cluster-related storage actions.

Settings
:   Review and manage deployment-level storage settings, such as the default cluster quota.

### Non-administrator capabilities
{: #non-admin-capabilities}

Non-admin users can review deployment and cluster information in Fusion as a Service, but they cannot change storage settings or other administrator-managed values.

Non-admin users can do the following tasks:

- Review deployment capacity.
- Open the **Clusters** tab and review cluster information.
- Open cluster details and review storage status, warnings, and alerts.
- Open the OpenShift console, subject to cluster access permissions.

Non-admin users cannot do the following tasks:

- Set or edit the default cluster quota.
- Enable or disable Fusion services.
- Update cluster storage quotas.
- Change deployment settings.

When you do not have administrator permissions, parts of the UI can appear read-only, unavailable, or hidden for management actions.

## Understanding UI states
{: #ui-states}

The Fusion as a Service UI uses different states to communicate information about deployments, clusters, and available actions.

### Warning states
{: #warning-states}

A warning state indicates that the deployment or cluster needs review.

Warnings can help you identify conditions such as the following items:

- A cluster that needs attention.
- A storage condition that should be reviewed.
- A status that suggests the current state is not ideal for the next action.

When you see a warning state:

1. Review the message or indicator that is shown in the UI.
2. Open cluster details or another related page if you need more context.
3. Decide whether you need administrator help, a quota change, or further investigation.

### Read-only states
{: #readonly-states}

A read-only state means that you can review information, but you cannot change it from the current page.

A page or control can be read-only for reasons such as the following conditions:

- Your role does not allow the action.
- The current state of the deployment or cluster does not allow the action.
- Another operation is already in progress.

Read-only behavior in the UI can appear in the following ways:

- A setting is visible, but you cannot change it.
- A control for an action is unavailable.
- A page shows information only, without management actions.

If a page is read-only, do the following tasks:

1. Review the information that is available on the page.
2. Check whether you need administrator access for the next action.
3. Return to another page if you need to review related cluster or deployment information.

## Confirmation dialogs and irreversible actions
{: #confirmation-actions}

The UI can ask for confirmation before it completes an action that changes deployment or cluster settings.

### Why confirmations are shown
{: #confirmation-purpose}

Confirmation helps you do the following tasks:

- Review the action before it is applied.
- Avoid unintended changes.
- Understand that the action affects deployment or cluster behavior.

### Actions that require confirmation
{: #confirmation-types}

Fusion as a Service can show confirmation for actions such as the following tasks:

- Enabling Fusion services for a cluster.
- Changing a default quota or cluster quota.
- Completing a guided corrective action from the Fix flow.

### Reviewing confirmations
{: #review-confirmations}

When a confirmation dialog appears, review the following items before you continue:

- The action that you are about to take.
- The cluster or deployment that the action affects.
- Any message that explains the result of the action.

If you are not ready to continue, close or cancel the dialog.

## Common UI scenarios
{: #common-scenarios}

The following scenarios illustrate how the UI adapts based on roles and states:

Administrator viewing Settings
:   The Settings page is accessible, and controls for editing the default quota are enabled.

Non-administrator viewing Settings
:   The Settings page might not appear in the navigation, or it appears as read-only if accessible.

Cluster with warning status
:   Warning indicators appear in the cluster list and on the cluster details page, prompting review.

Enabling Fusion services
:   A confirmation dialog appears before the action is completed, allowing you to review the quota and other settings.

Operation in progress
:   Controls related to the operation might be disabled or read-only until the operation completes.

## Best practices for working with the UI
{: #ui-best-practices}

Follow these best practices when working with the Fusion as a Service UI:

- Review warning messages and indicators promptly to identify issues early.
- Check your role and permissions if an expected action is not available.
- Read confirmation dialogs carefully before proceeding with actions.
- Use cluster details pages to get more context when warnings or read-only states appear.
- Contact an administrator if you need to perform an action that requires elevated permissions.

## Next steps
{: #ui-roles-next}

After understanding UI behavior, roles, and permissions, you can:

- [Understand admin vs non-admin permissions](/docs/sdsaas?topic=sdsaas-admin-permissions)
- [View cluster details](/docs/sdsaas?topic=sdsaas-view-cluster-details)
- [Monitor cluster health](/docs/sdsaas?topic=sdsaas-monitor-cluster-health)
- [Enable Fusion services for a cluster](/docs/sdsaas?topic=sdsaas-enable-fusion-services)
- [Manage the default cluster quota](/docs/sdsaas?topic=sdsaas-manage-cluster-quota)

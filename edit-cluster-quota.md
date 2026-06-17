---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-17"

keywords: default cluster quota, deployment settings, storage quota, IBM Fusion as a service admin tasks, edit default cluster quota

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Editing cluster storage quota
{: #manage-cluster-quota}

Edit the default storage quota that IBM Fusion as a service applies when you enable Fusion services for a cluster. The Settings page displays storage capacity information and allows administrators to modify the default cluster quota.
{: shortdesc}

The default cluster quota is initially set during the onboarding process. For information about setting the quota during first-time setup, see [Onboarding to your IBM Fusion as a service deployment](/docs/cephaas?topic=cephaas-onboarding-fusionaas).

To edit the default cluster quota, you must have administrator permissions.

## Opening the Settings page
{: #open-settings}

1. Open your IBM Fusion as a service deployment.
2. In the left navigation, click **Settings**.

The Settings page opens, displaying the Storage tile with deployment storage information.

## Understanding the Settings page
{: #settings-page-overview}

The Settings page displays storage configuration for your deployment. The information shown depends on your user role.

### Storage tile
{: #storage-tile}

The Storage tile displays the following information:

Overall capacity limit
:   The total storage capacity available for the deployment (for example, "100 TB").

Default cluster quota
:   The default amount of storage capacity that is allocated when Fusion services are enabled for a cluster (for example, "10 TB").

### Admin user view
{: #admin-user-view}

If you have administrator permissions, the Storage tile includes an **Edit quota** button in the upper right corner. This button allows you to modify the default cluster quota.

The Storage tile displays:
- Overall capacity limit
- Default cluster quota
- **Edit quota** button (enabled)

### Non-admin user view
{: #non-admin-user-view}

If you do not have administrator permissions, the Storage tile displays the same information but without the **Edit quota** button. You can view the storage settings but cannot modify them.

The Storage tile displays:
- Overall capacity limit
- Default cluster quota
- No Edit quota button

## About the default cluster quota
{: #about-default-quota}

The default cluster storage quota is the amount of storage capacity that is automatically allocated when you enable Fusion services for a cluster. This setting provides a consistent baseline for storage allocation across your deployment.

The default quota is initially configured during the onboarding process when you first access your deployment. After onboarding, you can modify this value at any time from the Settings page.

The default quota is used in the following situations:

- When an administrator enables Fusion services for a cluster and uses the default value.
- When a new cluster needs an initial storage allocation from the deployment.
- When administrators want a consistent starting quota across clusters.

The default quota affects only future enablement of Fusion services. It does not change existing cluster quotas or current storage usage.

## Editing the default cluster quota (admin only)
{: #set-edit-quota-steps}

If you have administrator permissions, you can edit the default cluster quota.

1. Open your IBM Fusion as a service deployment.
2. In the left navigation, click **Settings**.
3. In the **Storage** tile, click **Edit quota**.
4. In the side panel, enter or update the storage quota value in TB.
5. Click **Save**.

The updated default quota is applied to new clusters when Fusion services are enabled. Existing cluster quotas are not changed.

## Understanding the impact of quota changes
{: #quota-change-impact}

When you set or edit the default quota, keep the following considerations in mind:

- The value must fit within the available deployment storage capacity.
- A larger default quota reserves more storage capacity for future cluster use.
- The change affects only future cluster setup that uses the default value.

The change does not affect the following resources:

- Clusters that already have Fusion services enabled.
- Clusters that already use a custom quota.
- Current storage usage on existing clusters.

## Quota validation
{: #quota-validation}

When you set the default quota, the system validates that:

- The quota value is within acceptable limits.
- The deployment has sufficient available storage capacity.
- The value is appropriate for the deployment configuration.

If validation fails, review the error message and adjust the quota value accordingly.

## Next steps
{: #manage-quota-next}

After you set or edit the default quota, you can:

- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services) using the default quota
- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota) to customize individual cluster allocations
- [View deployment capacity](/docs/cephaas?topic=cephaas-view-deployment-capacity) to understand available resources
- [Understand admin vs non-admin permissions](/docs/cephaas?topic=cephaas-admin-permissions)

---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-25"

keywords: default cluster quota, deployment settings, storage quota, IBM Fusion as a service admin tasks, edit default cluster quota

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Editing cluster storage quota
{: #manage-cluster-quota}

Editing the default storage quota that IBM Fusion as a service applies when you enable Fusion services for a cluster. The Settings page displays storage capacity information and allows administrators to modify the default cluster quota.
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

Before a cluster can utilize storage, an administrator must enable Fusion services for that cluster. Until Fusion services are enabled, the cluster displays "Cluster storage not enabled" in the cluster list.
{: important}

### How default and cluster quotas work together
{: #quota-relationship}

The default cluster quota and individual cluster quotas have the following relationship:

Default quota as baseline
:   The default quota serves as the minimum baseline for all cluster quotas. No cluster quota can be set below this value.

Cluster quota constraints
:   Individual cluster quotas must be equal to or greater than the default quota. You can increase a cluster quota above the default, but you cannot decrease it below the default.

Future clusters only
:   Changing the default quota affects only new clusters when Fusion services are enabled. It does not change existing cluster quotas.

Example
:   If the default quota is 10 TB, all cluster quotas must be at least 10 TB. If you later change the default to 15 TB, existing clusters with 10 TB quotas remain unchanged, but new clusters will start with 15 TB.

Storage quota cannot be configured from Red Hat OpenShift on IBM Cloud. All quota management must be done through the IBM Fusion as a service UI.
{: important}

## Editing the default cluster quota (admin only)
{: #set-edit-quota-steps}

If you have administrator permissions, you can edit the default cluster quota.

1. Open your IBM Fusion as a service deployment.
2. In the left navigation, click **Settings**.
3. In the **Storage** tile, click **Edit quota**.
4. In the side panel, enter or update the storage quota value in TB.
5. Click **Save**.

The updated default quota is applied to new clusters when Fusion services are enabled. Existing cluster quotas are not changed.

Remember that setting a default quota does not automatically enable storage for clusters. The administrator for each cluster must enable Fusion services for that cluster before it can begin utilizing storage.
{: note}

## Next steps
{: #manage-quota-next}

After you set or edit the default quota, you can:

- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services) using the default quota
- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota) to customize individual cluster allocations
- [View deployment capacity](/docs/cephaas?topic=cephaas-view-deployment-capacity) to understand available resources
- [Understand admin vs non-admin permissions](/docs/cephaas?topic=cephaas-admin-permissions)

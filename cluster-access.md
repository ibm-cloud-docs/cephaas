---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-17"

keywords: cluster access, cluster permissions, role-based access, admin access, non-admin access

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Cluster access permissions
{: #cluster-access}

Understand how your user role determines what cluster information you can view and what actions you can perform in IBM Fusion as a service.
{: shortdesc}

## Access based on user role
{: #role-based-access}

Both administrators and non-administrators can access and view cluster information. However, the available actions differ based on your role.

### Administrator access
{: #admin-access}

Administrators have full access to view cluster information and perform management actions.

Administrators can:

- View all cluster details including status, compute resources, storage, warnings, and alerts.
- Access both **View details** and **Manage storage** options from the overflow menu (⋮) in the cluster list.
- Enable Fusion services for clusters that don't have storage enabled.
- Update cluster storage quotas.
- Configure storage settings for individual clusters.

### Non-administrator access
{: #non-admin-access}

Non-administrators can view cluster information but cannot perform management actions.

Non-administrators can:

- View all cluster details including status, compute resources, storage, warnings, and alerts.
- Access the **View details** option from the overflow menu (⋮) in the cluster list to open the cluster details panel.
- See any issues or warnings with their clusters, helping them understand the cluster state and identify when administrator action is needed.

Non-administrators cannot:

- Enable or disable Fusion services for clusters.
- Update cluster storage quotas.
- Access the **Manage storage** option in the overflow menu.
- Configure storage settings for clusters.

## How to access cluster information
{: #accessing-cluster-info}

To view cluster information:

1. Open your IBM Fusion as a service deployment.
2. Click the **Clusters** page in the left navigation.
3. In the cluster list, click the cluster name or select **View details** from the overflow menu (⋮).

The cluster details panel opens, displaying information about the selected cluster. The information displayed is the same for all users, but the available actions depend on your role.

## Related information
{: #cluster-access-next}

- [Understanding admin vs non-admin permissions](/docs/cephaas?topic=cephaas-admin-permissions)
- [Viewing clusters](/docs/cephaas?topic=cephaas-view-cluster-list)
- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota) (admin only)
- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services) (admin only)

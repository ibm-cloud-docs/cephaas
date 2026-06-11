---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-11"

keywords: cluster storage status, storage usage, cluster quota, Fusion as a Service storage

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Viewing cluster details
{: #view-cluster-storage-status}

View detailed information about a cluster including its status, compute resources, storage, and any warnings or alerts. The information displayed depends on your user role.
{: shortdesc}

## Before you begin
{: #view-cluster-storage-status-prereqs}

Before you view cluster details, make sure that you can open the deployment in the {{site.data.keyword.cloud_notm}} console.

## Opening cluster details
{: #access-storage-status}

1. Open your Fusion as a Service deployment.
2. Click the **Clusters** page in the left navigation.
3. In the cluster list, click the cluster name or select **View details** from the overflow menu (⋮).

The cluster details panel opens on the right side of the screen, displaying information about the selected cluster.

## Cluster details panel
{: #cluster-details-panel}

The cluster details panel displays comprehensive information about the cluster. The panel includes the following sections:

### Cluster information
{: #cluster-info-section}

At the top of the panel, you can view:

Cluster name
:   The name of the cluster with a link icon to open the cluster in a new window.

Status
:   The current operational status of the cluster (for example, Available, Warning) with a corresponding status icon.

Worker count
:   The number of worker nodes in the cluster.

GPU Worker count
:   The number of GPU worker nodes, if GPU resources are configured for the cluster.

### Compute resources
{: #compute-resources-section}

The Compute resources section displays:

vCPU
:   The number of virtual CPUs allocated to the cluster.

Memory
:   The amount of memory allocated to the cluster, displayed in TB (terabytes).

### Storage
{: #storage-section}

The Storage section shows storage information for the cluster:

Storage consumed
:   Displays the amount of storage currently in use compared to the total allocated storage quota (for example, "20 TB consumed of 100 TB").

If Fusion services are not enabled for the cluster, a warning message appears in this section:

**Cluster storage not enabled**
:   "The admin for this cluster needs to enable Fusion services for this cluster begin utilizing storage."

This message indicates that an administrator must enable Fusion services before the cluster can use storage resources.

## Role-based views
{: #role-based-views}

The cluster details panel displays the same information for both admin and non-admin users. However, the available actions differ based on your role:

Non-admin users
:   Can view all cluster details including warnings and alerts. Non-admin users can see any issues with their clusters through the cluster details panel, helping them understand the cluster state and identify when administrator action is needed.

Admin users
:   Can view all cluster details and have access to additional management actions such as enabling Fusion services or managing storage quotas.

## Why to review cluster storage status
{: #understand-storage-metrics}

Review cluster storage status in the following situations:

- After you enable Fusion services for a cluster.
- After you change a cluster quota.
- When you investigate a warning or alert.
- When you want to compare current usage with the assigned quota.

## Related tasks
{: #view-cluster-storage-status-next}

- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota)
- [Understand storage quota validation and error states](/docs/cephaas?topic=cephaas-storage-quota-validation)
- [Identify clusters that need attention](/docs/cephaas?topic=cephaas-monitor-cluster-health)

---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-25"

keywords: cluster list, IBM Fusion as a service clusters, deployment clusters, cluster navigation

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Viewing clusters
{: #view-cluster-list}

Open the **Clusters** page in your IBM Fusion as a service deployment to view resource summaries and a detailed list of all associated clusters.
{: shortdesc}

Before you view the cluster list, make sure that you can open the deployment in the {{site.data.keyword.cloud_notm}} console.

## Clusters page
{: #access-cluster-list}

1. Open your IBM Fusion as a service deployment.
2. In the left navigation, click **Clusters**.

The **Clusters** page opens, displaying resource summary cards at the top and a table showing all clusters associated with the deployment.

## Resource summary cards
{: #resource-summary-cards}

At the top of the Clusters page, you can view summary cards that show the total resources allocated across all clusters in your deployment.

vCPUs
:   Displays the total number of virtual CPUs allocated across all clusters (for example, "34").

Memory
:   Shows the total memory allocated across all clusters, displaying both used capacity and total available capacity (for example, "6 TB of 12 TB"). A progress bar indicates the percentage of memory in use.

Storage used
:   Shows the total storage used across all clusters, displaying both used capacity and total available capacity (for example, "120 TB of 200 TB"). A progress bar indicates the percentage of storage in use.

GPUs
:   Displays the number of GPUs attached across all clusters (for example, "3 of 8 cards attached"). This card appears only when GPU workloads are present in your deployment (workloads > 0).

These summary cards help you quickly understand the total resource allocation across your deployment.

The GPU resource summary card is visible only when your deployment has GPU workloads configured. If no GPU workloads are present (workloads = 0), the GPU tile is hidden.
{: note}

## Cluster table
{: #cluster-table}

Below the resource summary cards, the Clusters page displays a table with detailed information about each cluster. You can search for specific clusters by name using the search field above the table.

The table includes the following columns:

Name
:   The cluster name. Click the name to open the cluster details page.

Status
:   The current operational status of the cluster. Status values are derived from Red Hat OpenShift on IBM Cloud (ROKS) cluster health. Possible values include Available, Warning, and Error with corresponding icons.

vCPU
:   The number of virtual CPUs allocated to the cluster.

Memory
:   The amount of memory allocated to the cluster, displayed in TB (terabytes).

Quota used
:   The amount of storage quota used by the cluster, displayed in TB (terabytes).

Cluster Quota
:   The total storage quota allocated to the cluster, displayed in TB (terabytes).

Worker count
:   The number of worker nodes in the cluster.

You can click the overflow menu (⋮) at the end of each row to access actions for the cluster. The table includes pagination controls at the bottom to navigate through multiple pages of clusters.

### Available actions
{: #cluster-actions}

The actions available in the overflow menu (⋮) depend on your user role:

Non-admin users
:   Can access **View details** to open the cluster details page.

Admin users
:   Can access both **View details** to open the cluster details page and **Manage storage** to configure storage settings for the cluster.

## Using the Clusters page
{: #using-clusters-page}

Use the Clusters page to do the following tasks:

- Review total resource allocation across all clusters using the summary cards.
- Identify which clusters are associated with the deployment.
- Review the current status of each cluster.
- Find clusters that need attention based on status indicators.
- Search for specific clusters by name.
- Open a cluster to review more detailed information.
- Access cluster management actions through the overflow menu.

Cluster status values reflect the health status from Red Hat OpenShift on IBM Cloud. For detailed cluster diagnostics and troubleshooting, refer to the [Red Hat OpenShift on IBM Cloud documentation](/docs/openshift).
{: note}

## Related tasks
{: #view-cluster-list-next}

- [Understand cluster list status and capacity indicators](/docs/cephaas?topic=cephaas-cluster-health-indicators)
- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)
- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services)

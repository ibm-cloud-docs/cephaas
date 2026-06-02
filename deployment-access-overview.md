---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-02"

keywords: fusion as a service, Fusion as a Service deployment, access deployment, deployment navigation, deployment overview, deployment capacity

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# About your deployment
{: #deployment-access-overview}

Open your Fusion as a Service deployment from the {{site.data.keyword.cloud_notm}} console to review capacity, clusters, storage, and settings. The deployment overview page provides a central location for monitoring resources and navigating to management areas.
{: shortdesc}

Before you begin, make sure that you meet the following requirements:

- You have permission to view the deployment in the {{site.data.keyword.cloud_notm}} console.
- The deployment is available and in a state that you can access.

## Opening your deployment
{: #open-deployment}

1. Log in to [IBM Cloud](https://cloud.ibm.com){: external}.
2. In the navigation menu, click **Resource list** > **Storage** > **Fusion as a Service**.
3. Click **Deployments**.
4. In the deployment list, locate your Fusion as a Service deployment.
5. Click the deployment name to open it.

The deployment opens to the **Clusters** page, displaying resource summary cards and a list of all clusters in your deployment.

## Understanding the Clusters page
{: #clusters-page}

The Clusters page provides a comprehensive view of your deployment's resource utilization and cluster details. It serves as the central location for monitoring and managing all clusters in your deployment.

### Navigation options
{: #deployment-navigation}

Use the left navigation panel to access different areas of your deployment:

Clusters
:   Displays resource summary cards and a table listing all clusters associated with the deployment. You can view cluster status, resource usage, and access cluster management options.

Settings
:   Opens the **Settings** page, where administrators can review or change deployment-level configurations. This option is available only to users with administrator permissions.

### Resource summary cards
{: #resource-summary-cards}

At the top of the Clusters page, summary cards display current resource utilization across your deployment. Each card provides a quick overview of resource consumption and availability.

vCPUs
:   Shows the total number of virtual CPUs allocated across all clusters (for example, "34"). This represents the compute capacity in use.

Memory
:   Displays the amount of memory currently in use compared to the total available memory (for example, "6 TB of 12 TB"). A progress bar shows the percentage of memory utilized.

Storage used
:   Shows the amount of storage currently in use compared to the total available storage (for example, "120 TB of 200 TB"). This represents storage allocated to clusters that use Fusion services. A progress bar indicates storage utilization.

GPUs
:   Displays the number of GPU cards currently attached compared to the total available (for example, "3 of 8 cards attached"). This card appears only when GPU resources are configured for your deployment.

These summary cards help you quickly assess resource availability before you enable Fusion services for a cluster or update a quota.

### Clusters table
{: #clusters-table}

The Clusters table lists all clusters in your deployment with detailed information about each cluster's configuration and resource usage.

The table includes the following columns:

Name
:   The cluster name. Click the cluster name to view detailed cluster information.

Status
:   The current operational status of the cluster. Possible values include Available (green indicator) and Warning (yellow indicator).

vCPU
:   The number of virtual CPUs allocated to the cluster.

Memory
:   The total memory capacity allocated to the cluster (for example, "200 TB").

Quota used
:   The amount of storage quota currently used by the cluster (for example, "12 TB").

Cluster quota
:   The total storage quota allocated to the cluster (for example, "30 TB").

Worker count
:   The number of worker nodes in the cluster.

### Cluster actions
{: #cluster-actions}

For each cluster in the table, you can access a menu of available actions by clicking the overflow menu icon (⋯) in the row.

View details
:   Opens the cluster details page where you can view comprehensive information about the cluster, including resource allocation, storage usage, and configuration settings.

Manage storage
:   Opens the storage management interface where you can enable Fusion services, update storage quotas, and manage storage allocations for the cluster.

### Search and pagination
{: #search-pagination}

Use the search field at the top of the table to filter clusters by name. The table supports pagination, allowing you to navigate through multiple pages of clusters if your deployment contains many clusters.

## Using the Clusters page
{: #clusters-page-usage}

Use the Clusters page for the following tasks:

- Monitor current resource utilization across vCPUs, memory, storage, and GPU resources.
- View the status of all clusters in your deployment at a glance.
- Identify clusters with Warning status that might need attention.
- Check cluster storage quota usage to find clusters approaching their limits.
- Access cluster details to view comprehensive information about a specific cluster.
- Manage storage for individual clusters, including enabling Fusion services and updating quotas.
- Search for specific clusters by name.

## Next steps
{: #deployment-access-next}

After you open the deployment, you can do the following tasks:

- [View cluster details and status](/docs/cephaas?topic=cephaas-view-clusters)
- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services)
- [Update cluster storage quota](/docs/cephaas?topic=cephaas-edit-cluster-quota)
- [Monitor cluster health](/docs/cephaas?topic=cephaas-monitor-cluster-health)

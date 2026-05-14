---

copyright:
  years: 2024, 2026
lastupdated: "2026-05-14"

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

The deployment dashboard opens, displaying resource utilization charts and cluster summaries.

## Understanding the Dashboard
{: #deployment-dashboard}

The Dashboard provides a comprehensive view of your deployment's resource utilization and cluster health. It serves as the starting point for monitoring and managing your deployment.

### Navigation options
{: #deployment-navigation}

Use the left navigation panel to access different areas of your deployment:

Dashboard
:   Displays resource utilization charts, utilization trends over time, and cluster summaries.

Clusters
:   Opens the **Clusters** page, where you can view all clusters associated with the deployment, review their status, check resource usage, and open individual cluster details.

Settings
:   Opens the **Settings** page, where administrators can review or change deployment-level configurations, such as the default cluster storage quota. This option is available only to users with administrator permissions.

### Resource utilization
{: #resource-utilization}

The Dashboard displays circular charts showing current resource utilization across your deployment. Each chart provides a visual representation of how much of each resource is currently in use.

Storage usage
:   Shows the amount of storage currently in use compared to the total available storage (for example, "31 TB of 100 TB"). This represents storage allocated to clusters that use Fusion services.

vCPU capacity
:   Displays the percentage of virtual CPU capacity currently in use (for example, "59%"). This helps you understand compute capacity available for cluster workloads.

Memory usage
:   Shows the amount of memory currently in use compared to the total available memory (for example, "31 TB of 100 TB"). This helps you monitor memory allocation across clusters.

GPU usage
:   Displays the amount of GPU resources currently in use compared to the total available GPU capacity (for example, "30 TB of 100 TB"). This chart appears only when GPU resources are configured for your deployment.

These charts help you quickly assess resource availability before you enable Fusion services for a cluster or update a quota.

### Utilization over time
{: #utilization-over-time}

The Dashboard includes a line chart that shows resource utilization trends over time. This chart helps you understand usage patterns and plan for capacity needs.

The chart displays the following information:

- Storage utilization (blue line)
- vCPU utilization (dark blue line)
- Memory utilization (teal line)
- GPU utilization (purple line)

You can use the controls in the upper right corner of the chart to adjust the view or expand the chart to full screen.

### Cluster summaries
{: #cluster-summaries}

At the bottom of the Dashboard, you can view summary cards that provide quick insights into your clusters.

Clusters
:   Shows the total number of clusters in your deployment, along with counts of clusters in Error and Warning states. Click the arrow to view the full cluster list.

Cluster Storage
:   Displays the total number of clusters and shows how many clusters have storage that is 90%-100% filled or 75%-89% filled. This helps you identify clusters that might need additional storage capacity.

## Using the Dashboard
{: #dashboard-usage}

Use the Dashboard for the following tasks:

- Monitor current resource utilization across storage, vCPU, memory, and GPU resources.
- Review utilization trends over time to identify usage patterns.
- Identify clusters in Error or Warning states that need attention.
- Check cluster storage capacity to find clusters that are approaching storage limits.
- Navigate to the **Clusters** page to view detailed cluster information.
- Navigate to **Settings** to review or manage deployment-level configurations.

## Next steps
{: #deployment-access-next}

After you open the deployment, you can do the following tasks:

- [View deployment capacity and resource usage](/docs/cephaas?topic=cephaas-view-deployment-capacity)
- [View the cluster list](/docs/cephaas?topic=cephaas-view-cluster-list)
- [Set the default cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota)
- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services)

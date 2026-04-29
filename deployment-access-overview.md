---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: fusion as a service, Fusion as a Service deployment, access deployment, deployment navigation, deployment overview, deployment capacity

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Accessing and understanding your deployment
{: #deployment-access-overview}

Open your Fusion as a Service deployment from the {{site.data.keyword.cloud_notm}} console to review capacity, clusters, storage, and settings. The deployment overview page provides a central location for monitoring resources and navigating to management areas.
{: shortdesc}

## Before you begin
{: #deployment-access-prereqs}

Make sure that you meet the following requirements:

- You have permission to view the deployment in the {{site.data.keyword.cloud_notm}} console.
- The deployment is available and in a state that you can access.

## Opening your deployment
{: #open-deployment}

1. Log in to [IBM Cloud](https://cloud.ibm.com){: external}.
2. In the navigation menu, click **Fusion as a Service**.
3. Click **Deployments**.
4. In the deployment list, locate your Fusion as a Service deployment.
5. Click the deployment name to open it.

The deployment overview page opens, showing capacity tiles for vCPU, memory, storage, and GPU resources (if configured).

## Understanding the deployment overview page
{: #deployment-overview}

The deployment overview page provides a summary of your deployment's resources and serves as the starting point for managing clusters and settings.

### Capacity information
{: #capacity-tiles}

The overview page includes capacity tiles that summarize the resources that are available in the deployment. Each tile displays the current usage and total capacity for that resource type.

The page shows the following resource categories:

vCPUs
:   Displays the number of virtual CPUs currently in use. This tile helps you understand compute capacity available for cluster workloads.

Memory
:   Shows memory usage in TB format, displaying both used capacity and total available capacity (for example, "0 TB of 12 TB"). This helps you monitor memory allocation across clusters.

Storage
:   Shows storage capacity in TB format, displaying both allocated storage and total available storage. This capacity represents storage that can be assigned to clusters that use Fusion services.

GPUs
:   Displays the number of GPUs available, if GPU resources are configured for the deployment. This tile appears only when GPU capacity is part of your deployment configuration.

These tiles help you quickly understand the available capacity before you enable Fusion services for a cluster or update a quota.

### Navigation options
{: #deployment-navigation}

From the overview page, you can navigate to the main deployment management areas using the left navigation panel.

Clusters
:   Opens the **Clusters** tab, where you can view all clusters associated with the deployment, review their status, check resource usage, and open individual cluster details.

Settings
:   Opens the **Settings** page, where administrators can review or change deployment-level configurations, such as the default cluster storage quota. This option is available only to users with administrator permissions.

## Using the overview page
{: #overview-usage}

Use the overview page for the following tasks:

- Review deployment capacity before you assign or increase cluster storage quotas.
- Open the **Clusters** tab to see all clusters in the deployment.
- Open **Settings** to review or manage deployment-level storage settings.
- Check whether compute, memory, storage, or GPU capacity might affect your next action.

## Next steps
{: #deployment-access-next}

After you open the deployment, you can do the following tasks:

- [View deployment capacity and resource usage](/docs/sdsaas?topic=sdsaas-view-deployment-capacity)
- [View the cluster list](/docs/sdsaas?topic=sdsaas-view-cluster-list)
- [Set the default cluster storage quota](/docs/sdsaas?topic=sdsaas-manage-cluster-quota)
- [Enable Fusion services for a cluster](/docs/sdsaas?topic=sdsaas-enable-fusion-services)

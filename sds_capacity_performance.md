---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-12"

keywords: cephaas, capacity management, performance management

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Storage capacity and performance
{: #storage-capacity-performance}

IBM Storage Ceph as a Service enables you to view the capacity and performance details of your deployments in real-time. 

To view capacity details of your IBM CephaaS deployments, complete the following steps. 

1. On the **IBM Cloud console**, click the hamburger menu > **Resource list** and expand **Storage**.
2. Click Deployment name link.
3. Click **Deployments link** from the left- hand pane. 
Your deployments are listed on the dashboard. 


{: shortdesc}

## Viewing Capacity of your deployments
{: #view-capacity}

Click on each deployment to display the capacity and performance details. 

The upper section of the deployment dashboard displays the current usage information about the following. 

| Usage Information | Description |
|-------|-------------|
| Overall Capacity | Used block and object capacity, along with the remaining available capacity, including the burst capacity|
| Block capacity | Current usage and a link to update capacity|
| Object capacity | Current usage and a link to update capacity |
{: caption="Table 1. Details about deployment capacity" caption-side="bottom"}

The Overall Capacity is displayed using a bar with visual indicators for both used and available capacity. Till the capacity is not fully utilized, the bar displays blue color. When the Overall Capacity is fully utilized, the bar turns yellow. If the burst capacity is also exhausted, the bar turns red. 

## Viewing Performance of your deployments
{: #view-performance}

The lower section of the deployment dashboard provides graphical insights into various aspects of deployment performance. You can monitor both read and write performance for block and object storage. The dashboard displays performance data from the last 6 to 48 hours.

| Performance Criteria | Description |
|-------|-------------|
| IOPS | Current IOPS (Input/Output Operations Per Second) value for a predefined IOPS tier |
| Latency | Response time delay measured in milliseconds |
| Throughput| The performance a disk can deliver, measured in Gigabytes/second (Gbps)|

{: caption="Table 2. Details about deployment performance" caption-side="bottom"}

## Renaming your deployments
{: #rename-deployment}

1. To rename a deployment, navigate to **Actions** menu on your deployment dashboard. 
2. Enter a new name in the **Rename deployment** screen. 
3. Click **Save**. 

## Adding capacity

Select **Actions** > **Add capacity**. **Purchase additional capacity** screen is displayed which guides you to contact your IBM seller for further process. 

## Next Steps

You can edit the block and object capacity, view the activity tracker, and view docs links from the capacity and performance dashboard. 

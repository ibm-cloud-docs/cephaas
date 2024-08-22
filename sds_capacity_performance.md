---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-22"

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
| Overall Capacity | Available capacity to bust and maximum available capacity  |
| Historical usage | Capacity performance for past month, measured hourly |
| Block capacity | Current usage and a link to update capacity|
| Object capacity | Current usage and a link to update capacity |
{: caption="Table 1. Details about deployment capacity" caption-side="bottom"}

## Viewing Performance of your deployments
{: #view-performance}

The lower section of the deployment dashboard displays the graphical information about the following aspects of the deployment performance. 

| Performance Criteria | Description |
|-------|-------------|
| IOPS | Current IOPS value for a predefined IOPS tier which is based on the default profile |
| Latency | Response time delay measured in milliseconds |
| Throughput| The performance a disk can deliver, measured in Gigabytes/second (Gbps)|

{: caption="Table 2. Details about deployment performance" caption-side="bottom"}

## Renaming your deployments
{: #rename-deployment}

1. To rename a deployment, navigate to **Actions** menu on your deployment dashboard. 
2. Enter a new name in the **Rename deployment** screen. 
3. Click **Save**. 

## Next Steps

You can edit the block and object capacity, view the activity tracker, and view docs links from the capacity and performance dashboard. 


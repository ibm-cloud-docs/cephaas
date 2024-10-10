---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-10"

keywords: cephaas, capacity management, performance management

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# View storage capacity and performance
{: #storage-capacity-performance}

IBM Storage Ceph as a Service enables you to view the capacity and performance details of your deployments in real-time.
{: shortdesc}

To view capacity details of your IBM CephaaS deployments, complete the following steps.

1. On the **IBM Cloud console**, click the hamburger menu > **Resource list** and expand **Storage**.
2. Click Deployment name.
3. Click **Deployments** option from the left - hand panel. Your deployments are listed on the dashboard.
4. Click your deployment.


## Viewing capacity of your deployments
{: #view-capacity}

Click on each deployment to display the capacity and performance details.

The upper section of the deployment dashboard displays the current usage information about the following.

| Usage Information | Description |
|-------|-------------|
| Overall Capacity | Used block and object capacity, along with the remaining available capacity, including the burst capacity|
| Block capacity | Current usage and a link **Go to Block storage** link to update capacity|
| Object capacity | Current usage and a link **Go to Object storage** link to update capacity |
{: caption="Details about deployment capacity" caption-side="bottom"}

The Overall Capacity is displayed using a bar with visual indicators for both used and available capacity. The numerical value in the format of nn used of nn TB reflects used capacity from your Overall capacity.

Till the capacity is not fully utilized, the bar displays blue color. When the Overall capacity is fully utilized, the burst threshold stage is reached and the bar turns yellow. After the burst threshold, the burst capacity begins to utilize. 
If the burst capacity is also exhausted, the bar turns red.

## Viewing Performance of your deployments
{: #view-performance}

The lower section of the deployment dashboard provides graphical insights into various aspects of deployment performance. You can monitor both read and write performance for block and object storage. The dashboard displays performance data from the last 6, 12, 24, 2 days, past week and past 2 weeks.

| Performance Criteria | Description |
|-------|-------------|
| IOPS | Current IOPS (Input/Output Operations Per Second) value for a predefined IOPS tier |
| Latency | Response time delay measured in milliseconds |
| Throughput| The performance a disk can deliver, measured in MB/S|
{: caption="Details about deployment performance" caption-side="bottom"}

## Renaming your deployments
{: #rename-deployment}

1. To rename a deployment, go to **Actions** menu on your deployment dashboard.
2. Enter a new name in the **Rename deployment** screen.
3. Click **Save**.

## Adding capacity
{: #add-capacity}

Select **Actions** > **Add capacity**. **Purchase additional capacity** screen is displayed which guides you to contact your IBM seller for further process.

## Next Steps
{: #view-capacity-nextsteps}

You can edit the block and object capacity, view the activity tracker, and view docs links from the capacity and performance dashboard. 

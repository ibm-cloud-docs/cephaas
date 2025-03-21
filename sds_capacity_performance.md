---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: cephaas, capacity management, performance management, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# View storage capacity and performance
{: #storage-capacity-performance}

{{site.data.keyword.cephaas_full_notm}} enables you to view the capacity and performance details of your deployments in real-time.
{: shortdesc}

To view capacity details of your deployment, in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.

You can view your deployments dashboard which shows the **Overall capacity**, Status of both Block and Object capacity, and **Performance** of each of the storage types.


## Viewing the capacity of your deployments
{: #view-capacity}

The deployment dashboard displays the current usage information about the following.

| Usage Information | Description |
|-------|-------------|
| Overall Capacity | Used block and object capacity, along with the remaining available capacity, including the burst capacity|
| Block capacity | Current usage and a link **Go to Block storage** link to update capacity |
| Object capacity | Current usage and a link **Go to Object storage** link to update capacity |
{: caption="Details about deployment capacity" caption-side="bottom"}

The Overall Capacity is displayed by using a bar with visual indicators for both used and available capacity. The numerical value in the format of **XXX used of YYY** TB reflects used capacity from your Overall capacity.

Till the capacity is not fully used, the bar displays a blue color. When the Overall capacity is fully used, the burst threshold stage is reached and the bar turns yellow. After the burst threshold, the burst capacity begins to use.
If the burst capacity is also exhausted, the bar turns red.

## Viewing Performance of your deployments
{: #view-performance}

The deployment dashboard provides graphical insights into various aspects of deployment performance. You can monitor both read and write performance for block and object storage. The dashboard displays performance data from the last 6 hours, 12 hours, 24 hours, 2 days, past week and past 2 weeks.

| Performance Criteria | Description |
|-------|-------------|
| IOPS | Current IOPS (Input/Output Operations Per Second) value for a predefined IOPS tier |
| Latency | Response time delay measured in milliseconds |
| Throughput| The performance a disk can deliver, measured in MB/S|
{: caption="Details about deployment performance" caption-side="bottom"}


## Renaming your deployments
{: #rename-deployment}

1. To rename a deployment, go to the **Actions** menu on your deployment dashboard.
2. Enter a new name in the **Rename deployment** screen.
3. Click **Save**.

## Adding capacity
{: #add-capacity}

To add additional capacity, select **Actions** > **Add capacity**.

**Purchase additional capacity** screen is displayed which guides you to contact your IBM seller for further process.

## Next Steps
{: #view-capacity-nextsteps}

You can perform various tasks from the links in the right panel such as create block volumes, create storage objects, and go to object storage. Refer to the docs links of Identity and access management, How to connect to the VMware environment, and How to use the CLI for more information.

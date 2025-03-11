---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: ceph as a service, frequently asked questions, faq, faqs, block storage, object storage, low cost object, storage units, usage charges, quota limits, capacity

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# FAQ
{: #faq}

Frequently asked questions (FAQs) provide you with helpful answers and insight into best practices for working with {{site.data.keyword.cephaas_full}}.

* [Block and Object storage](/docs/cephaas?topic=cephaas-faq#block-storage-faq)
* [Low-cost objects](/docs/cephaas?topic=cephaas-faq#faq-low-cost-objects)
* [Monitoring](/docs/cephaas?topic=cephaas-faq#faq-monitoring)

## FAQ about block and object storage
{: #block-storage-faq}

### How am I charged for usage?
{: faq}
{: #faq-usage-cost}

Both block and object storage are charging based on the monthly fee for the plan you choose. If the storage in the burst capacity is used then overage fees are charged on an hourly usage basis.



### Are there quota limits?
{: faq}
{: #faq-quota-limit}

The capacity-based quota limits for your block and object storage are based on the quotas set on the instance. For more information about quotas and limits for your {{site.data.keyword.cephaas_full_notm}} and the resources available within it, see [storage quotas](/docs/cephaas?topic=cephaas-quota-capacity-mgmt&interface=ui).


### After creating a volume with specific capacity, can the capacity later be increased?
{: faq}
{: #faq-increase-capacity}

Yes, you can increase the capacity of a block volume after it is provisioned as long as the total provisioned capacity of all volumes does not exceed the block quota limit. For more information, see [Adding capacity to existing deployment](/docs/cephaas?topic=cephaas-add-capacity-to-deployment).

### What rules apply to volume names and can I rename a volume later on?
{: faq}
{: #faq-rename-rules}

Valid volume names can include a combination of lowercase alphanumeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters.  Volume names must begin with a lowercase letter and be unique across the entire deployment.

You can change the name of an existing volume by using the UI, CLI, API and Terraform. See [this information](/docs/cephaas?topic=cephaas-renaming-block-volume&interface=ui) for details.

### How many volumes can be provisioned per deployment?
{: faq}
{: #faq-count-vol-provision}

You can provision up to 1000 block storage volumes per deployment.




### When can I delete a block storage volume?
{: faq}
{: #faq-how-del-vol}

You can delete a block storage volume only when it is not mapped to a host. [Unmap the volume](/docs/cephaas?topic=cephaas-unmap-hosts) before deleting it.


### What happens to the data when I delete a block storage volume?
{: faq}
{: #faq-data-post-vol-delete}

When you delete a block storage volume, all pointers to the data on that volume are removed and the data becomes inaccessible. If you later reprovision the physical storage to another deployment, a new set of pointers is assigned. The new deployment cannot access any data that was on the physical storage because the pointers were deleted. When new data is written to the volume, any inaccessible data is overwritten.


### Is storage capacity measured in GB or GiB?
{: faq}
{: #faq-storage-units}

One confusing aspect of storage is the units that storage capacity and usage are reported in. Sometime GB represents gigabytes (base-10) and sometimes GB represents gibibytes (base-2) which ought to be abbreviated as GiB.

Humans usually think and calculate numbers in the decimal (base-10) system. In our documentation, we refer to storage capacity by using the unit GB (Gigabytes) to align with the industry standard terminology. In the UI, CLI, API, and Terraform, you see the unit GB used and displayed when you query the capacity. When you want to order a 4-TB volume, you enter 4,000 GB in your provisioning request.

However, computers operate in binary, so it makes more sense to represent some resources like memory address spaces in base-2. Since 1984, computer file systems show sizes in base-2 to go along with the memory. Back then, available storage devices were smaller, and the size difference between the binary and decimal units was negligible. Now that the available Storage Systems are considerably larger this unit difference is causing confusion.

The difference between GB and GiB lies in their numerical representation:
- GB (Gigabyte) is a decimal unit, where 1 GB equals 1,000,000,000 bytes. When you convert GB to TB, you use 1000 as the multiplier.
- GiB (Gibibyte), is a binary unit, where 1 GiB equals 1,073,741,824 bytes. When you convert GiB to TiB, you use 1024 as the multiplier.

The following table shows the same number of bytes expressed in decimal and binary units.

| Decimal SI (base 10) | Binary (base 2)       |
|----------------------|-----------------------|
| 2,000,000,000,000 B  | 2,000,000,000,000 B   |
|     2,000,000,000 KB |     1,953,125,000 KiB |
|         2,000,000 MB |         1,907,348 MiB |
|             2,000 GB |             1,862 GiB |
|                 2 TB |              1.81 TiB |
{: caption="Decimal vs Binary units" caption-side="bottom"}

The storage system uses base-2 units for volume allocation. So if your volume is provisioned as 4,000 GB, that's really 4,000 GiB or 4,294,967,296,000 bytes of storage space. The provisioned volume size is larger than 4 TB. However, your operating system might display the storage size as 3.9 T because it uses base-2 conversion and the T stands for TiB, not TB.



### How many hosts can be provisioned per instance?
{: faq}
{: #faq-host-per-instance}

The total number of hosts that can be provisioned in an instance is 32.

### Can a volume be mapped to multiple hosts?
{: faq}
{: #faq-vol-map-multi-hosts}

Yes, a volume can be mapped to up to 32 hosts.

### How to create a volume for increased performance?
{: faq}
{: #faq-vol-increase-performance}

Volumes are created with fixed IOPS setting of 3 IOPS/GB. The IOPS and bandwidth depend on the capacity of volume. Hence to achieve higher performance, a volume with bigger size must be created.

| Setting name                          |   Values                              |
|---------------------------------------|---------------------------------------|
| IOPS                                  |	3 IOPS/GB                           |
| Min Volume Size                       |	1 GB                                |
| Max Volume Size                       |	32 TB                               |
| Min IOPS  (minimum value of max IOPS that is set on a volume) | 150           |
| Max IOPS                              |	96000 (3 * max vol size)            |
| Blocksize (Throughput Multiplier)     |	16 K                                |
| Min Throughput (Blocksize * Min IOPS) |	1.6 MBps                            |
| Max Throughput (Blocksize * Max IOPS) |   1536 MBps                           |
{: caption="Volume settings" caption-side="bottom"}



### How to create volume for a workload that requires 10,000 IOPS?
{: faq}
{: #faq-create-vol-10k-iops}

To help ensure a throttling of 10000 IOPS, the volume capacity must be at least 10000/3 = 3334 GB. So, you must create a volume with capacity ~3500 GB.

### How to create volume for a workload that requires a throughput of 1000 MBps?
{: faq}
{: #faq-create-vol-thruput-1kmbps}

To help ensure a throttling of 1000 * 1000 KBps, max IOPS must be 1000000/16 = 62500. So, you must create volumes with total capacity 62500/3 = ~21 TB.

### What does the ‘pending’ status mean for block volumes and hosts?
{: #faq-pending-status-block-volumes-hosts}

Block storage POST and DELETE APIs for volumes and host are asynchronous APIs. They accept the request and return after successful validations indicating that the request has been accepted for further processing. In such long-running API cases, the caller can track the status of a resource using the "status" property in the `GET` API.
An ‘available’ status indicates that the process is complete and that the resource is ready for use. The pending statuses indicate that the resource is still being processed.

The Block storage API uses the following pending status:

- ‘pending’: Used when a volume is being created or a volume mapping is in progress. GET APIs on hosts and volumes will return this status after `POST /volumes`, `POST /hosts`, or `PUT /hosts/{id}/volumes/{id}` request if the operation is still in progress.
- ‘pending-deletion’: Used when a volume deletion is in progress. `GET /volumes` API will return this status after `DELETE /volumes/{id}` request if delete operation is still in progress.
- "pending-unmapping": Used when a volume unmapping from a host operation is in progress. `GET /hosts` API will return this status for a volume mapping after unmap single volume from a host `DELETE /hosts/{id}/volumes/{id}` or unmap all volumes from a host `DELETE /hosts/{id}/volumes` request if the unmapping operation is still in progress.

The resource can remain in one of these pending states for as long as the operation does not complete. The backend keeps on trying the operation until it succeeds.

For example, the volume status will continue to show as ‘pending’ after the POST request if the backend cluster is down. It changes to `available` state when the backend cluster is restored. The API does not treat this as permanent failure but a condition that can be fixed. The caller must implement timeouts if needed for such cases.


## FAQ on low-cost objects
{: #faq-low-cost-objects}

### What is the default storage class for low-cost objects?
{: faq}
{: #faq-default-sc}

For Low-cost Object, new S3 accounts have `STANDARD_IA` as the default storage class.



## FAQ on monitoring
{: #faq-monitoring}


### How can i access the IBM Cloud monitoring user interface from the {{site.data.keyword.cephaas_full_notm}} user interface?
{: faq}
{: #faq-access-ic-mon-ui}

The {{site.data.keyword.mon_full_notm}} user interface is not linked from the {{site.data.keyword.cephaas_full_notm}} user interface. Hence it cannot be accessed from the {{site.data.keyword.cephaas_short}} user interface.

---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-03"

keywords: frequently asked questions, faqs

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# FAQs - Block storage
{: #block-storage-faq}

## How am I charged for usage?
{: faq}

Block Storage is calculated hourly. The calculation is based on the total number of hours that the block storage volume exists on the account. It exists on the account until you delete the volume or you reach the end of a billing cycle, whichever comes first.

## Are there quota limits?
{: faq}

There are capacity based quota limits for your block storage volumes based on the block quota set on the instance. For more information about quotas and limits for your {{site.data.keyword.cephaas_full_notm}} and the resources available within it, see [storage quotas](/docs/sdsaas?topic=sdsaas-sdsaas-manage-storage-limit).


## After creating a volume with specific capacity, can the capacity later be increased?
{: faq}

Yes, you can increase the capacity of a block volume after it is provisioned as long as the total provisioned capacity of all volumes does not exceed the block quota limit. For more informaton, see [Managing volume count and capacity limits](/docs/sdsaas?topic=sdsaas-manage-storage-limit).

## What rules apply to volume names and can I rename a volume later on?
{: faq}

Valid volume names can include a combination of lowercase alphanumeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters.  Volume names must begin with a lowercase letter and be unique across the entire deployment.

You can change the name of an existing volume using the UI. See [this information](/docs/sdsaas?topic=sdsaas-updating-block-volume&interface=ui#renaming-block-volume-from-list-view-page-ui) for details.

## How many volumes can be provisioned per deployment?
{: faq}

You can provision up to 1000 block storage volumes per deployment. You can request your quota to be increased by opening a [support case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}.

## When can I delete a block storage volume?
{: faq}

You can delete a block storage volume only when it is not mapped to a host. [Unmap the volume](/docs/sdsaas?topic=sdsaas-deleting-hosts&interface=ui#deleting-volume-mapping-from-host-ui) before deleting it.


## What happens to the data when I delete a block storage volume?
{: faq}

When you delete a block storage volume, all pointers to the data on that volume are removed and the data becomes inaccessible. If you later reprovision the physical storage to another deployment, a new set of pointers is assigned. The new deployment cannot access any data that was on the physical storage because the pointers have been deleted. When new data is written to the volume, any inaccessible data is overwritten.


## Is storage capacity measured in GB or GiB?
{: faq}
{: #faq-storage-units}

One confusing aspect of storage is the units that storage capacity and usage are reported in. Sometime GB is really gigabytes (base-10) and sometimes GB represents gibibytes (base-2) which ought to be abbreviated as GiB.

Humans usually think and calculate numbers in the decimal (base-10) system. In our documentation, we refer to storage capacity by using the unit GB (Gigabytes) to align with the industry standard terminology. In the UI, CLI, API, and Terraform, you see the unit GB used and displayed when you query the capacity. When you want to order a 4-TB volume, you enter 4,000 GB in your provisioning request.

However, computers operate in binary, so it makes more sense to represent some resources like memory address spaces in base-2. Since 1984, computer file systems show sizes in base-2 to go along with the memory. Back then, available storage devices were smaller, and the size difference between the binary and decimal units was negligible. Now that the available storage systems are considerably larger this unit difference is causing confusion.

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
{: caption="Table 1. Decimal vs Binary units" caption-side="bottom"}

The storage system uses base-2 units for volume allocation. So if your volume is provisioned as 4,000 GB, that's really 4,000 GiB or 4,294,967,296,000 bytes of storage space. The provisioned volume size is larger than 4 TB. However, your operating system might display the storage size as 3.9 T because it uses base-2 conversion and the T stands for TiB, not TB.



## How many hosts can be provisioned per instance?
{: faq}
Total number of hosts that can be provisioned in an instance is 32.

## Can a volume be mapped to multiple hosts?
{: faq}

Yes, a volume can be mapped to up to 32 hosts.

## How to create a volume for increased performance?
{: faq}

Volumes are created with fixed IOPS setting of 3 IOPS/GB. The IOPS and hence the bandwidth are dependent on the capacity of volume. Hence to achieve higher performance, a volume with bigger size must be created.


| IOPS                                  |	3 IOPS/GB                           |
| Min Volume Size                       |	1 GB                                |
| Max Volume Size                       |	32 TB                               |
| Min IOPS  (minimum value of max IOPS that is set on a volume) | 150           |
| Max IOPS                              |	96000 (3 * max vol size)            |
| Blocksize / Throughput Multiplier     |	16 K                                |
| Min Throughput (Blocksize * Min IOPS) |	1.6 MBps                            |
| Max Throughput (Blocksize * Max IOPS) |   1536 MBps                           |
{: caption="Table 2. volume settings" caption-side="bottom"}



## How to create volume for a workload that requires 10,000 IOPS?
{: faq}

To ensure a throttling of 10000 IOPS, the volume capacity should be at least 10000/3 = 3334GB. So, you must create a volume with capacity ~3500GB.

## How to create volume for a workload that requires a throughput of 1000MBps?
{: faq}

To ensure a throttling of 1000 * 1000KBps, max IOPS should be 1000000/16 = 62500. So, you must create volumes with total capacity 62500/3 = ~21TB.

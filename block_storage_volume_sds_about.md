---

copyright:
  years: 2024
lastupdated: "2024-05-08"

keywords:

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# About Block Volume storage
{: #sds-block-volume-storage-about}

Block volume storage provides hypervisor-mounted, high-performance data storage for your instances. The infrastructure provides rapid scaling across zones, additional security and performance.
{: shortdesc}

## Overview
{: #block-storage-overview}

SDSaaS volume data is stored redundantly across multiple physical disks in an Availability Zone to prevent data loss due to failure of any single component.

SDSaaS provides primary boot volumes and secondary data volumes. Boot volumes are automatically created and attached during instance provisioning. Data volumes can be created and attached during instance provisioning as well, or as stand-alone volumes that you can later attach to an instance. To protect your data, you can use your own encryption keys or choose IBM-managed encryption.

You pay for only the capacity that you need. SDSaaS capacity ranges from 10 GB up to 16,000 GB for all available [profiles](#block-storage-profiles-intro). For data volumes attached to a virtual server instance, you can [increase volume capacity] in GB increments up to 16,000 GB capacity, depending on your volume profile.



When you create, view, or update a SDSaaS volume, the volume health state is reported in the UI, CLI, or API. For more information, see [SDSaaS volume health states].

## SDSaaS volume types
{: #sds-block-storage-volumes}

SDSaaS offers block-level volumes that are attached to an instance as a boot volume when the instance is created or attached as secondary data volumes. You can configure up to 300 SDSaaS volumes per account in a region. You can request to increase this quota by opening support case and specifying in which zone you need more volumes.

You can attach only one boot volume to a virtual server instance at a time, but you can attach up to 12 SDSaaS data volumes to a single instance. 

### Data volumes
{: #sds-secondary-data-volumes}

SDSaaS data volumes are secondary volumes with total capacity range of 10 GB to 16,000 GB. Maximum IOPS for data volumes varies based on volume size.


You can create data volumes as stand-alone volumes or when you provision an instance. Stand-alone volumes exist in an unattached state until you attach the volume to an instance. When you create a data volume as part of instance provisioning, the volume is automatically attached to the instance.

SDSaaS data volumes can be attached to any available instance in your zone, based on your customer account and permissions, and within certain limits. These volumes are detached by default when the instance is deleted. Detaching by default allows your data to persist beyond the virtual server instance lifecycle. It removes only the volume's association with the instance. You can delete data volumes manually after they are detached. Also, when you create data volumes, you can specify that they be automatically deleted when the instance is deleted.

Detached volumes can be attached to an available, running instance without reprovisioning the volume or the instance.

Data volumes are encrypted by default with IBM-managed encryption. You can also encrypt data volumes by using your own root keys.

### SDSaaS IOPS profiles
{: #sds-block-storage-profiles-intro}

When you create a SDSaaS volume in your availability zone, you can use 3 different tiered profiles with predefined IOPS levels and a custom profile with which you can define your own IOPS level based on the volume capacity. All profiles are backed by solid-state drives (SSDs).

For more information, see [SDSaaS profiles](/docs/sdsaas?topic=sds-block-storage-profiles)

## SDSaaS encryption
{: #sds-storage-encryption}

{{site.data.keyword.cloud_notm}} takes the need for security seriously and understands the importance of being able to encrypt data to keep it safe. When you create a data volume, you can choose to protect your data by using your own root keys, or use the default IBM-managed encryption. Boot volumes that are created during instance provisioning are encrypted with IBM-managed encryption by default. You can edit the boot volume to use your root keys. After you set up encryption for a data volume, you can't change it.



## Cancelling your SDSaaS storage service
{: #sds-cancel-storage}

If you no longer need a volume, you can cancel it at any time. IBM wipes all data before the storage is reused. If you have additional compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. 

## Next steps
{: #sds-block-storage-about-next-steps}

Create your SDSaaS volumes.

* For more information about creating a volume during instance provisioning, see [Create and attach a SDSaaS volume when you create an instance].
* For more information about creating a SDSaaS encrypted by your own encryption keys, see [Creating SDSaaS volumes with customer-managed encryption]

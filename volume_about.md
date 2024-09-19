---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-19"

keywords:

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# About Block storage volume
{: #block-volume-storage-about}

Block storage volume provides hypervisor-mounted, high-performance data storage for your instances. The infrastructure provides rapid scaling across zones, extra security, and performance.
{: shortdesc}

## Overview
{: #block-storage-overview}

{{site.data.keyword.cephaas_full}} volume data is stored redundantly across multiple physical disks in an Availability Zone to prevent data loss due to failure of any single component.

{{site.data.keyword.cephaas_short}} provides primary and secondary data volumes. Data volumes can be created and attached during instance provisioning as well, or as stand-alone volumes that you can later attach to an instance. To protect your data, you can use your own encryption keys or choose IBM-managed encryption.

You pay for only the capacity that you need. {{site.data.keyword.cephaas_short}} capacity ranges from 1 GB up to 16,000 GB for all available instances. For data volumes attached to a virtual server instance, you can [increase volume capacity] in GB increments up to 16,000 GB capacity.



When you create, view, or update a volume, the volume health state is reported in the UI, CLI, or API. For more information, see [{{site.data.keyword.cephaas_short}} volume health states].

## {{site.data.keyword.cephaas_short}} volume
{: #block-storage-volumes}

{{site.data.keyword.cephaas_full_notm}} offers block-level volumes that are attached to a deployment when the deployment is created or attached as secondary data volumes. You can configure up to 300 CephaaS volumes per account in a region. You can request to increase this quota by opening support case and specifying the amount you need for more volumes.

{{site.data.keyword.cephaas_full_notm}} data volumes are secondary volumes with total capacity range of 1 GB to 16,000 GB. Maximum IOPS for data volumes varies based on volume size.


You can create data volumes as stand-alone volumes or when you provision a deployment. Stand-alone volumes exist in an unattached state until you attach the volume to an deployment. When you create a data volume as part of storage provisioning, the volume is automatically attached to the deployment.

{{site.data.keyword.cephaas_short}} data volumes can be attached to any available deployment in your premise and within certain limits. These volumes are detached by default when the deployment is deleted. Detaching by default allows your data to persist beyond the virtual server deployment lifecycle. It removes only the volume's association with the deployment. You can delete data volumes manually after they are detached. Also, when you create data volumes, you can specify that they be automatically deleted when the deployment is deleted.

Detached volumes can be attached to an available, running deployments without reprovisioning the volume or the deployment.

Data volumes are encrypted by default with IBM-managed encryption. You can also encrypt data volumes by using your own root keys.

### {{site.data.keyword.cephaas_short}} IOPS profiles
{: #block-storage-profiles-intro}

When you create a {{site.data.keyword.cephaas_short}} volume in your availability zone, you can use 3 different tiered profiles with predefined IOPS levels and a custom profile with which you can define your own IOPS level based on the volume capacity. All profiles are backed by solid-state drives (SSDs).


## {{site.data.keyword.cephaas_short}} encryption
{: #storage-encryption}

{{site.data.keyword.cloud_notm}} takes the need for security seriously and understands the importance of being able to encrypt data to keep it safe. When you create a volume, you can choose to protect the volume by using your own root keys, or use the default IBM-managed encryption. Volumes that are created during storage provisioning are encrypted with IBM-managed encryption by default. You can edit the volume to using your root keys. After you set up encryption for a volume, you can't change it.



## Cancelling your {{site.data.keyword.cephaas_full}}
{: #cancel-storage}

If you no longer need a volume, you can cancel it at any time. IBM wipes all data before the storage is reused. If you have more compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. 

## Next steps
{: #block-storage-about-nextsteps}

Create your {{site.data.keyword.cephaas_short}} block volumes.

* For more information about creating a volume during instance provisioning, see [Create and attach a block volume when you create an instance].
* For more information about creating a CephaaS encrypted by your own encryption keys, see [Creating block volumes with customer-managed encryption]

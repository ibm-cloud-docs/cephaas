---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-02"

keywords: frequently asked questions, faqs

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# FAQs - Block storage
{: #block-storage-faq}

## How are volumes created and attached to an instance?
{: faq}

When you create a virtual server instance, you can [create a block storage secondary volume](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-creating-block-storage#create-from-vsi-gen1) that is attached to that instance.  ou can also [create a stand-alone volume](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-creating-block-storage#create-standalone-vol-gen1) and later attach it to your instance. You can attach several block storage data volumes to a single instance.

## How many instances can share a provisioned block storage volume?
{: faq}

A block storage volume can be attached to only one instance at a time. Instances cannot share a volume.

## How many block storage secondary data volumes can be attached to an instance?
{: faq}

Instances with fewer than 4 cores can attach up to 4 block storage secondary volumes.

Instances with 4 or more cores can attach up to 12 block storage secondary volumes.

## Are the allocated IOPS enforced by instance or by volume?
{: faq}

IOPS is enforced at the volume level.


## How am I charged for usage?
{: faq}

Block Storage is calculated hourly. The calculation is based on the total number of hours that the block storage volume exists on the account. It exists on the account until you delete the volume or you reach the end of a billing cycle, whichever comes first.

## Are there quota limits?
{: faq}

There are quota limits for your block storage volumes based on the number of vCPUs per instance. For more information about quotas and limits for your {{site.data.keyword.cephaas_full_notm}} and the resources available within it, see [storage quotas](/docs/sdsaas?topic=sdsaas-sdsaas-manage-storage-limit).

## After creating a volume with specific capacity, can the capacity later be increased?
{: faq}

No, you cannot increase the capacity of a volume. Estimate sufficient capacity for projected growth before you provision a block storage volume.

Also, consider how many volumes you need and the capacity of these volumes. For more informaton, see [Managing volume count and capacity limits](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-managingstoragelimit-gen1).

## What rules apply to volume names and can I rename a volume later on?
{: faq}

Valid volume names can include a combination of lowercase alphanumeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters.  Volume names must begin with a lowercase letter and be unique across the entire VPC infrastructure.

You can change the name of an existing volume using the UI. See [this information](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-managing-block-storage-gen1#rename) for details.

## Does the volume need to be pre-warmed to achieve expected throughput?
{: faq}

You do not have to pre-warm a volume. You can see the specified throughput immediately upon provisioning the volume.

## What should I do about data backups for disaster recovery?
{: faq}

Block Storage for VPC secures your data across redundant fault zones in your region. You are are responsible for independently backing up your data. You might also consider using [{{site.data.keyword.blockstoragefull}} - Classic](/docs/BlockStorage?topic=BlockStorage-getting-started), which provides disaster recovery features such as volume cloning, snapshots, and replication. In particular, see the topics under **Replication and Disaster Recovery**.

## How many volumes can be provisioned per account?
{: faq}

You can provision up to 300 block storage volumes per account in a region. You can request your quota to be increased by opening a [support case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}.

## What strategy can I use to manage {{site.data.keyword.block_storage_is_short}} volumes?
{: faq}

Determine the capacity you need based on anticipated growth. Volume size cannot be expanded after provisioning. However, you can create new volumes as needed. Also, if you have well-defined performance requirements, you might consider choosing [custom IOPS](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles-gen1#custom-gen1) that provides a specific range of IOPS per volume size.

## How is the boot disk created for an instance and how does it relate to the virtual machine image?
{: faq}

The boot disk, also called a boot volume, is created when you provision a virtual server instance. The boot disk of an instance is a cloned image of the virtual machine image. The boot volume is deleted when you delete the instance to which it's attached.

## When can I delete a block storage data volume?
{: faq}

You can delete a block storage data volume only when it's not attached to a virtual server instance. [Detach the volume](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-managing-block-storage-gen1#detach-gen1) before deleting it. Boot volumes are detached and deleted when the instance is deleted.

## What happens to the data when I delete a block storage data volume?
{: faq}

When you delete a block storage data volume, all pointers to the data on that volume are removed and the data becomes inaccessible. If you later reprovision the physical storage to another account, a new set of pointers is assigned. The new account can't access any data that was on the physical storage because the pointers have been deleted. When new data is written to the volume, any inaccessible data is overwritten.

## What performance latency can I expect from {{site.data.keyword.block_storage_is_short}}?
{: faq}

Target latency within the storage is less than 1 millisecond. Block storage is connected to compute instances on a shared network, so the exact performance latency depends on the network traffic within a specific timeframe.

## Can I set up shared storage in a multizone cluster?
{: faq}

In the IBM Cloud, storage options are limited to an availability zone. We do not recommend managing shared storage across multiple zones.

Instead, use an IBM Cloud data classic service option such as {{site.data.keyword.cos_full}} or {{site.data.keyword.cloudantfull}} if you must share your data across multiple zones and regions.

## I have volumes on the Classic infrastructure. Can I port them to the VPC?
{: faq}

No. The VPC provides access to new availability zones in multi-zone regions. Compute, network, and storage resources are specifically designed to function in the VPC.

## How secure is data in a {{site.data.keyword.block_storage_is_short}} volume?
{: faq}

All block storage volumes are encrypted at rest with IBM-managed encryption or using your own encryption keys. IBM-managed keys are generated and securely stored in a block storage vault that is backed by Consul and maintained by IBM Cloud operations.

For more security, you can protect your data using your own customer root keys (CRKs). You import your root keys to, or create them in, a supported key management service (KMS). Your root keys are safely managed by the supported KMS, either {{site.data.keyword.keymanagementserviceshort}} (FIPS 140-2 Level 3 compliance) or {{site.data.keyword.hscrypto}}, which offer the highest level of security (FIPS 140-2 Level 4 compliance).  Your key material is protected in transit and at rest. For information, see [Creating block storage volumes with customer-managed encryption](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-encryption).

## What are the advantages of using customer managed encryption over provider managed encryption?
{: faq}

Customer-managed encryption lets you encrypt your block storage volumes using your own root keys. You have complete control over your data security and grant IBM access to use your root keys. In addition:

* Encryption is handled by IBM's host/hypervisor technology for your instances. This feature provides greater level of security over solutions that use storage node encryption technology only.
* Data is encrypted with your root key at all times outside of the host/hypervisor. This means your data is protected while in motion between the host system and IBM's storage systems, and while at rest in IBM's storage system.
* You choose the key management service (KMS) you want to use. You can select {{site.data.keyword.keymanagementserviceshort}}, a public multi-tenant KMS that is FIPS 140-2 L3 compliant, or the more secure {{site.data.keyword.hscrypto}}, which is FIPS 140-2 L4 compliant.
* Customer-managed encryption provides better audit records for key usage. Your key access is logged in the {{site.data.keyword.at_full_notm}} service. The Activity Tracker lets you track interactions with the VPC.

## What encryption technology is used for customer-managed encryption?
{: faq}

A propriety encryption format is used to secure VHD format files using the AES-256 cipher suite.
AES-256 cipher keys used to unlock VHD files are stored separate from the enryption keys. Each VHD file contain the SHA-256 hash for its encryption key, but not for the key itself. The hash is used to verify the key during an unlock &attach operation.

Unique AES-256 cipher keys are generated for each block storage volume independently, and each key is secured by a client root key (CRK) that is stored within a key management system (KMS) of your choice, either {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}}.

Access to root keys stored in KMS instances within IBM Cloud is controlled using IBM Access Management. You grant IBM Block Storage Service access to your root keys before they can be use.  You can also remove access to the keys for any reason, for example, if you suspect that your key was compromised.

## I use customer-managed encryption for my volumes. What happens when I delete my root key?
{: faq}

When you delete your root key or suspend it in your key management system, your workloads remain running in your virtual server instance and volumes remain encrypted.  However, if you power down the VM and then power it back on, any instances with encrypted boot volumes will not start. If your boot volume was encrypted with provider-managed encryption, the instance will start but all secondary volumes encrypted by root key you deleted will be inaccessible.  All volume attachments will fail during the boot process. You can cancel the deletion if your key is in a pending delete state. Look at the list of resources for the status of the key.

## What should I do if my key is compromised?
{: faq}

Independently back up your data. Then, delete the compromised root key and power down the instance with volumes encrypted with that key.

## Am I charged for using customer-managed encryption?
{: faq}

There is no extra charge for creating volumes with customer-managed encryption.  However, there is a charge for setting up a Key Protect or HPCS instance to import, create, and manage your root keys. Contact your IBM customer service representative for details.

## What's the difference between using Key Protect as my KMS compared to HPCS?  When would I use one over the other?
{: faq}

Both key management systems provide you complete control over your data, managed by your root keys. {{site.data.keyword.keymanagementserviceshort}} is a multi-tenant KMS that lets you import or create your root keys and securely manage them. {{site.data.keyword.hscrypto}} is a single-tenant KMS and hardware security module (HSM) that's controlled by you, which offers the highest level of security. For more information and links to documentation about these key managment services, see [Supported key management services for customer-managed encryption](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-creating-instances-byok#kms-for-byok).

## Can I convert my volume from provider-managed encryption to customer-managed encryption?
{: faq}

No, after you provision a volume and specify the encryption type, it can't be changed.

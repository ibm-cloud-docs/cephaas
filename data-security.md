---

copyright:
  years: 2020, 2021
lastupdated: "2024-10-14"

keywords: securing your data, data security, cephaas, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Securing your data
{: #mng-data}

To help ensure that, you can securely manage your data when you use {{site.data.keyword.cephaas_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored data.
{: shortdesc}



## How your data is stored and encrypted?
{: #data-storage}

Each deployment instance is assigned a unique, randomly generated key by IBM when built at the factory.

All the data that is stored by using the data access APIs (S3 and NVMe/TCP), is stored locally within the {{site.data.keyword.cephaas_full_notm}} appliance and all the data within the appliance is encrypted with the unique, IBM managed key.

Currently, {{site.data.keyword.cephaas_full_notm}} does not support BYOK or KYOK.
{: note}


## Deleting your data
{: #data-delete}

If you no longer need a specific resource such as volume, host, S3 object credential or encryption keys, you can delete it any time as long as it is not mapped to any other data. For example, you can delete a block storage volume only when it is not mapped to a host and vice versa.

To delete the data, see the following documentation.

* [Deleting block storage volumes](/docs/cephaas?topic=cephaas-deleting-block-volume)

* [Deleting hosts](/docs/cephaas?topic=cephaas-deleting-hosts)

* [Deleting object storage S3 credential](/docs/cephaas?topic=cephaas-deleting-s3-credential)

When you delete any data, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the resources means your data cannot be restored.


### Deleting {{site.data.keyword.cephaas_full_notm}} instances
{: #service-delete}

If you no longer need a specific deployment, you can delete it at any time. Deleting the deployment from the IBM Cloud resource list removes it from all connected applications and deletes access to all the resources provisioned under the service instance such as volumes/hosts/buckets from spaces that are using it. In addition, all of its data is permanently deleted.

After the storage space is reclaimed, the disk is wiped, and data cannot be restored. When drives are decommissioned, IBM destroys them before they can be disposed of. The drives become unusable. Any data that was written to that drive becomes inaccessible.

Customers with special requirements for compliance such as NIST 800-88 Guidelines for Media Sanitization can perform the data sanitization procedure before they delete their storage.


The {{site.data.keyword.cephaas_full_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.cephaas_short}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

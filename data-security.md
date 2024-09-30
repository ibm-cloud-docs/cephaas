---

copyright:
  years: 2020, 2021
lastupdated: "2024-09-30"

keywords: securing your data, data security, cephaas

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}



# Securing your data in {{site.data.keyword.cephaas_full_notm}}
{: #mng-data}



To ensure that you can securely manage your data when you use {{site.data.keyword.cephaas_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored data. 
{: shortdesc}



## How your data is stored and encrypted in {{site.data.keyword.cephaas_full_notm}}
{: #data-storage}



Each {{site.data.keyword.cephaas_short}} instance is assigned a unique, randomly generated key by IBM when built at the factory.

All the data that is stored using the {{site.data.keyword.cephaas_short}} data access APIs (S3 and NVMe/TCP), is stored locally only within the {{site.data.keyword.cephaas_short}} appliance and all the data within the appliance is encrypted with the unique, IBM managed key.

Currently, {{site.data.keyword.cephaas_short}} does not support BYOK or KYOK.
{: note}





## Deleting your data in {{site.data.keyword.cephaas_short}}
{: #data-delete}

_Document how users can delete their data within the service._

_If applicable, add H3s in this section to tailor the information to particular types of data. For example, you might have a "Deleting keys" section and a "Deleting a database" section._

### Deleting a Volume

TODO

### Deleting a Host

TODO

### Deleting a S3 Bucket

TODO

### Deleting a S3 Object

TODO

### Deleting a S3 Credential

TODO


### Deleting {{site.data.keyword.cephaas_short}} instances
{: #service-delete}

_Include information about whether deleting the service fully erases all data. If deleting the service doesn't remove all personal data, include information about how users can completely delete their data._

_Information about how long services keep data after instances are deleted is covered in the service description. Include the following reference for users to find their data retention period._

The {{site.data.keyword.cephaas_short}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.cephaas_short}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

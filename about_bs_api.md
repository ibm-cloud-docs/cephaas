---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-14"

keywords: rest, s3, compatibility, api, error

subcollection: cephaas


---

{{site.data.keyword.attribute-definition-list}}


# About Block storage management API
{: #about-block-storage-api}

The {{site.data.keyword.cephaas_full}} API is a REST-based API for reading and writing objects.
{: shortdesc}

It uses {{site.data.keyword.iamlong}} for authentication and authorization, and supports a subset of the S3 API for easy migration of applications to {{site.data.keyword.cloud_notm}}.

As {{site.data.keyword.iamshort}} tokens are relatively easy to work with, `curl` is a good choice for basic testing and interaction with your storage. More information can be found in [the `curl` reference](/docs/cephaas?topic=cephaas-curl).

The following tables describe the complete set of operations of the {{site.data.keyword.cephaas_full_notm}} API. For more information, see [the API reference page for block storage](/docs/cephaas?topic=cephaas-block-storage-api) or [object storage](/docs/cephaas?topic=cephaas-object-storage-api).


## Block operations
{: #api-block-ops}

These operations create, delete, get information about, and control the behavior of block storage.

| Bucket operation        | Note                                                                            |
|:------------------------|:--------------------------------------------------------------------------------|
| `GET` /volumes          | Used to retrieve a list of all block volumes.                                   |
| `DELETE` /volume        | Deletes a volume.                                                               |
| `POST` /volumes         | Create a new volume in a deployment.                                            |
| `PATCH` /volumes        | Updates a volume.                                                               |
| `DELETE` /host          | Deletes a host                                                                  |
| `GET` hosts             | Lists hosts in a deployment.                                                    |
{: caption="Block storage operation" caption-side="top"}


More information about {{site.data.keyword.cephaas_full_notm}} features and use-cases can be found at [ibm.com](https://www.ibm.com/products/software-defined-storage).

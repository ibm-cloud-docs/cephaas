---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-14"

keywords: about block storage api, about object storage api, rest, s3, compatibility, api, error

subcollection: cephaas


---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.cephaas_full_notm}} APIs
{: #about-api}


{{site.data.keyword.cephaas_full_notm}} provides you with two APIs to configure and manage your storage resources.

* Block Storage Management API

* Object Storage Adminstration API


These {{site.data.keyword.cephaas_full_notm}} APIs use {{site.data.keyword.iamlong}} for authorize and authenticate requests.

As {{site.data.keyword.iamshort}} tokens are relatively easy to work with, `curl` is a good choice for basic testing and interaction with your storage. More information can be found in [the `curl` reference](/docs/cephaas?topic=cephaas-curl).

The following sections describe the complete set of operations of the {{site.data.keyword.cephaas_full_notm}} API. For more information, see [the API reference page for block storage](/docs/cephaas?topic=cephaas-block-storage-api) or [object storage](/docs/cephaas?topic=cephaas-object-storage-api).


## Block storage management API
{: #block-storage-api}

The Block storage management api allows you to programmatically provision and manage block storage resources within a {{site.data.keyword.cephaas_full_notm}} deployment, including volumes, hosts and volume to host mappings.



## Block operations
{: #api-block-ops}

These operations create, delete, get information about, and control the behavior of block storage.

| Bucket operation        | Note                                                                            |
|:------------------------|:--------------------------------------------------------------------------------|
| `GET` /volumes          | Used to retrieve a list of all block volumes.                                   |
| `DELETE` /volume        | Deletes a volume.                                                               |
| `POST` /volumes         | Create a new volume in a deployment.                                            |
| `PATCH` /volumes        | Updates the name or capacity of a volume.                                       |
| `DELETE` /host          | Deletes a host                                                                  |
| `GET` hosts             | Lists hosts in a deployment.                                                    |
| `POST` /hosts           | Create a new host in a deployment.                                              |
| `PATCH` /hosts          | Updates the name a host.                                                        |
{: caption="Block storage operation" caption-side="top"}


## Object storage management API
{: #object-storage-api}

The {{site.data.keyword.cephaas_full}} Object Storage API is a REST-based API for reading and writing objects.
{: shortdesc}

This {{site.data.keyword.cephaas_full_notm}} API uses {{site.data.keyword.iamlong}} for authentication and authorization, and supports a subset of the S3 API for easy migration of applications to {{site.data.keyword.cloud_notm}}.



## Object operations
{: #api-object-ops}

These operations create, delete, get information about, and control behavior of objects.

| Object operation          | Note                                                                                |
|:--------------------------|:------------------------------------------------------------------------------------|
| `DELETE` Object           | Deletes an object from a bucket.                                                   |
| `DELETE` Batch            | Deletes many objects from a bucket with one operation.                             |
| `GET` Object              | Retrieves an object from a bucket.                                                 |
| `HEAD` Object             | Retrieves an object's headers.                                                     |
| `OPTIONS` Object          | Checks CORS configuration to see whether a specific request can be sent.           |
| `PUT` Object              | Adds an object to a bucket.                                                        |
| `PUT` Object (Copy)       | Creates a copy of an object.                                                       |
| Begin Multipart Upload    | Creates an upload ID for a set of parts to be uploaded.                            |
| Upload Part               | Uploads a part of an object that is associated with an upload ID.                  |
| Upload Part (Copy)        | Uploads a part of an existing object that is associated with an upload ID.         |
| Complete Multipart Upload | Assembles an object from parts that are associated with an upload ID.              |
| Cancel Multipart Upload   | Cancels upload and deletes outstanding parts that are associated with an upload ID. |
| List Parts                | Returns a list of parts that are associated with an upload ID                       |
{: caption="Object operation" caption-side="top"}


## Bucket operations
{: #api-bucket-ops}

These operations create, delete, get information about, and control behavior of buckets.

| Bucket operation        | Note                                                                            |
|:------------------------|:--------------------------------------------------------------------------------|
| `GET` Buckets           | Used to retrieve a list of all buckets that belong to an account.              |
| `DELETE` Bucket         | Deletes an empty bucket.                                                       |
| `DELETE` Bucket CORS    | Deletes any CORS (cross-origin resource sharing) configuration set on a bucket. |
| `GET` Bucket            | Lists objects in a bucket. Limited to listing 1,000 objects at a time.         |
| `GET` Bucket CORS       | Retrieves any CORS configuration set on a bucket.                              |
| `HEAD` Bucket           | Retrieves a bucket's headers.                                                  |
| `GET` Multipart Uploads | Lists multipart uploads that aren't completed or canceled.                     |
| `PUT` Bucket            | Buckets have naming restrictions. Accounts are limited to 100 buckets.         |
| `PUT` Bucket CORS       | Creates a CORS configuration for a bucket.                                     |
{: caption="Bucket operation" caption-side="top"}



More information about {{site.data.keyword.cephaas_full_notm}} features and use-cases can be found at [ibm.com](https://www.ibm.com/products/software-defined-storage).

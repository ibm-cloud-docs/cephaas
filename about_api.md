---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-12"

keywords: about block storage api, about object storage api, rest, s3, compatibility, api, error

subcollection: cephaas


---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.cephaas_full_notm}} APIs
{: #about-api}


{{site.data.keyword.cephaas_full_notm}} provides you with two APIs to configure and manage your storage resources.

* [Block storage management API](/docs/cephaas?topic=cephaas-about-api#block-storage-api)

* [Object storage administration API](/docs/cephaas?topic=cephaas-about-api#object-storage-admin-api)

* [Object storage S3 API](/docs/cephaas?topic=cephaas-about-api#object-storage-s3-api)


These {{site.data.keyword.cephaas_full_notm}} APIs use {{site.data.keyword.iamlong}} for authorize and authenticate requests.

As the {{site.data.keyword.iamshort}} tokens are relatively easy to work with, `curl` is a good choice for basic testing and interaction with your storage. More information can be found in [the `curl` reference](/docs/cephaas?topic=cephaas-curl).

The following sections describe the complete set of operations of the {{site.data.keyword.cephaas_full_notm}} API.


## Block storage management API
{: #block-storage-api}

Use the Block storage management api to programmatically provision and manage block storage resources within the {{site.data.keyword.cephaas_full_notm}} deployment, including volumes, hosts, and volume to host mappings.


### Block operations
{: #api-block-ops}

These operations create, delete, get information about, and control the behavior of block storage.

| Block operation                                           | Action                                            |
|:----------------------------------------------------------|:--------------------------------------------------|
| `GET /volumes`                                            | Used to retrieve a list of all block volumes.     |
| `DELETE /volumes/{id}`                                    | Deletes a volume.                                 |
| `POST /volumes`                                           | Create volume in a deployment.                    |
| `GET /volumes/{id}`                                       | Retrieves a single volume.                        |
| `PATCH /volumes/{id}`                                     | Updates the name or capacity of a volume.         |
|:----------------------------------------------------------|:--------------------------------------------------|
| `GET /hosts`                                              | Retrieves a list of all hosts in the deployment   |
| `POST /hosts`                                             | Creates a new host.                               |
| `DELETE /host/{id}`                                       | Deletes a specific host.                          |
| `GET /hosts/{id}`                                         | Retrieves a specific host.                        |
| `PATCH /hosts/{id}`                                       | Updates the host information.                     |
| `POST /hosts/{id}/volume_mappings`                        | Create a Volume mapping for a host.               |
| `GET /hosts/{id}/volume_mappings/{volume_mapping_id}`     | Retrieves a single volume mapping.                |
| `GET /hosts/{id}/volume_mappings`                         | Retrieves the lists volume mappings for a host.   |
| `DELETE /hosts/{id}/volume_mappings/{volume_mapping_id}`  | Deletes the specific volume mapping.              |
| `DELETE /hosts/{id}/volume_mappings`                      | Deletes all volume mappings for a host.           |
{: caption="Block storage operation" caption-side="top"}



## Object storage administration API
{: #object-storage-admin-api}

### Administration operations
{: #api-object-admin-ops}

These operations create, delete, get information about, and control the behavior of administration objects.

| Administration operation              | Note                                                               |
|:------------------------------------  |:-------------------------------------------------------------------|
| `POST /certificates/{cert_type}`      | Create S3 certificate.                                             |
| `PUT /certificates/{cert_type}`       | Replace or update the S3 certificate                               |
| `GET /certificates/{cert_type}`       | Retrieves the certificate status.                                  |
| `DELETE /certificates/{cert_type}`    | Deletes the S3 certificate.                                        |
| `GET /certificates`                   | Retrieves the list of configured certificates                      |
| `POST /s3_credentials/{access_key}`   | Creates S3 credential for object.                                  |
| `GET /s3_credentials`                 | Retrieves one or more S3 credentials.                              |
| `DELETE /s3_credentials/{access_key}` | Deletes the S3 credential.                                         |
{: caption="Object admin operation" caption-side="top"}


## Object storage S3 API
{: #object-storage-s3-api}

The {{site.data.keyword.cephaas_full}} Object Storage S3 API is a REST-based API for reading and writing objects.
{: shortdesc}

This {{site.data.keyword.cephaas_full_notm}} API uses {{site.data.keyword.iamlong}} for authentication and authorization, and supports a subset of the S3 API for easy migration of applications to {{site.data.keyword.cloud_notm}}.


### Object operations
{: #api-object-ops}

These operations create, delete, get information about, and control the behavior of S3 objects.

| Object operation          | Note                                                                                |
|:--------------------------|:------------------------------------------------------------------------------------|
| `DELETE` Object           | Deletes an object from a bucket.                                                   |
| `DELETE` Batch            | Deletes many objects from a bucket with one operation.                             |
| `GET` Object              | Retrieves an object from a bucket.                                                 |
| `HEAD` Object             | Retrieves an object's headers.                                                     |
| `PUT` Object              | Adds an object to a bucket.                                                        |
| `PUT` Object (Copy)       | Creates a copy of an object.                                                       |
| Begin Multipart Upload    | Creates an upload ID for a set of parts to be uploaded.                            |
| Upload Part               | Uploads a part of an object that is associated with an upload ID.                  |
| Upload Part (Copy)        | Uploads a part of an existing object that is associated with an upload ID.         |
| Complete Multipart Upload | Assembles an object from parts that are associated with an upload ID.              |
| Cancel Multipart Upload   | Cancels upload and deletes outstanding parts that are associated with an upload ID. |
| List Parts                | Returns a list of parts that are associated with an upload ID                       |
{: caption="Object operation" caption-side="top"}


### Bucket operations
{: #api-bucket-ops}

These operations create, delete, get information about, and control the behavior of buckets.

| Bucket operation        | Note                                                                            |
|:------------------------|:--------------------------------------------------------------------------------|
| `GET` Buckets           | Used to retrieve a list of all buckets that belong to an account.              |
| `DELETE` Bucket         | Deletes an empty bucket.                                                       |
| `GET` Bucket            | Lists objects in a bucket. Limited to listing 1,000 objects at a time.         |
| `HEAD` Bucket           | Retrieves a bucket's headers.                                                  |
| `GET` Multipart Uploads | Lists multipart uploads that aren't completed or canceled.                     |
| `PUT` Bucket            | Buckets have naming restrictions. Accounts are limited to 100 buckets.         |
{: caption="Bucket operation" caption-side="top"}



More information about {{site.data.keyword.cephaas_full_notm}} features and use-cases can be found at [ibm.com](https://www.ibm.com/products/software-defined-storage).

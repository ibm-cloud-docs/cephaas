---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-09"

keywords: rest, s3, compatibility, api, error

subcollection: sdsaas


---

{{site.data.keyword.attribute-definition-list}}


# About the {{site.data.keyword.cephaas_full_notm}} S3 API
{: #s3-api}

The {{site.data.keyword.cephaas_full}} API is a REST-based API for reading and writing objects.
{: shortdesc}

It uses {{site.data.keyword.iamlong}} for authentication and authorization, and supports a subset of the S3 API for easy migration of applications to {{site.data.keyword.cloud_notm}}.

This reference documentation is being continuously improved. If you have technical questions about using the API in your application, post them on [StackOverflow](https://stackoverflow.com/). Add both `ibm-cloud-platform` and `cephaas` tags to your post. This will help us to improve this documentation with your feedback. Thanking you in advance for you feedback.

As {{site.data.keyword.iamshort}} tokens are relatively easy to work with, `curl` is a good choice for basic testing and interaction with your storage. More information can be found in [the `curl` reference](/docs/sdsaas?topic=sdsaas-curl).

The following tables describe the complete set of operations of the {{site.data.keyword.cephaas_full_notm}} API. For more information, see [the API reference page for block storage](/docs/sdsaas?topic=sdsaas-block-storage-api) or [object storage](/docs/sdsaas?topic=sdsaas-object-storage-api).


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
{: caption="Table 1. Bucket operation" caption-side="top"}

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
{: caption="Table 1. Object operation" caption-side="top"}

More information about {{site.data.keyword.cephaas_full_notm}} features and use-cases can be found at [ibm.com](https://www.ibm.com/products/software-defined-storage).

---

copyright:
 years: 2025, 2026
lastupdated: "2026-01-28"

keywords: about, basics, cephaas object storage, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.cephaas_full_notm}} Object Storage
{: #about-object-storage}

{{site.data.keyword.cephaas_full}} Object Storage is a highly available, durable, and secure platform for storing unstructured data. Unstructured data that are sometimes called `binary` or "blob" data, refers to data that is not highly structured in the database. Object storage is the most efficient way to store PDFs, media files, database backups, disk images, or even large structured datasets.

The files that are uploaded into {{site.data.keyword.cephaas_full_notm}} Object Storage are called objects. Objects can be anywhere from very small (a few bytes) to very large. They are organized into buckets that serve as containers for objects, and which can be configured independently from one another. Objects themselves have their own metadata in the form of user-defined tags or legal holds. Within a bucket, the hierarchy of objects is effectively "flat", although it is possible to add prefixes to object names to provide some organization and to provide flexibility in listing and other operations. For guidance on creating and managing your buckets and objects, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).

All data stored in {{site.data.keyword.cephaas_full_notm}} Object Storage is encrypted, erasure-coded, and dispersed across storage nodes.

All requests and responses are made over `HTTPS`. All `GET` and `HEAD` requests made to objects return an Etag value with the MD5 hash of the object to ensure integrity on the client side.

Developers use APIs to interact with their object storage. {{site.data.keyword.cephaas_full_notm}} Object Storage supports a subset of the S3 API for reading and writing data, as well as for bucket configuration. Software development kits (SDKs) are available for GO framework.

## Storage classes for object types
{: #storage-class-object-type}

To outline object storage behavior in Amazon S3, different object types are assigned specific storage classes to balance cost and performance. 

In {{site.data.keyword.cephaas_full_notm}}, Capacity objects use the STANDARD_IA (Infrequent Access) storage class. This class is designed for data that is accessed less frequently but still requires rapid retrieval when needed, offering lower storage costs with retrieval charges. 

{{site.data.keyword.cephaas_full_notm}} Performance objects use the STANDARD storage class. This class is optimized for frequently accessed data, providing low latency and high throughput for performance-critical workloads.

This distinction ensures that storage resources are utilized efficiently, delivering cost optimization for capacity workloads and high performance for frequently accessed data.


## Known limitations
{: #known-limitations}

This section includes the known limitations that might impact your experience.

* Only one object user is supported

* S3 features align with IBM Storage Ceph version 7.1

* Virtual hosted buckets not supported

* Static Web Hosting not supported



## HMAC credentials
{: #about-hmac-creds}

HMAC credentials consist of an Access Key and Secret Key pair for use with S3-compatible tools and libraries that require authentication.

The {{site.data.keyword.cephaas_full_notm}} S3 API is a REST-based API for reading and writing objects. It uses HMAC Access Keys for authentication and supports a subset of the S3 API for easy migration of applications to {{site.data.keyword.cloud_notm}}.

You can create a set of HMAC credentials using the console, CLI, and API. For instructions, see [Create HMAC credentials](/docs/cephaas?topic=cephaas-creating-s3-credential-sds).


## Next Steps
{: #about-obj-storage-next-steps}

After creating the credentials and uploading the S3 SSL certificate, you can proceed with creating buckets and objects by using the AWS CLI. For guidance on creating and managing your buckets and objects, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).

Also, see guidance on how to [create S3 HMAC Credentials](/docs/cephaas?topic=cephaas-creating-s3-credential-sds) and [upload the associated S3 SSL Certificate](/docs/cephaas?topic=cephaas-uploading-s3-certificate).

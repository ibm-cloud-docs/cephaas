---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-22"

keywords: about, basics, cephaas object storage

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.cephaas_short}} Object Storage
{: #about-object-storage}

{{site.data.keyword.cephaas_full}} Object Storage is a highly available, durable, and secure platform for storing unstructured data. Unstructured data that are sometimes called `binary` or "blob" data, refers to data that is not highly structured in the database. Object storage is the most efficient way to store PDFs, media files, database backups, disk images, or even large structured datasets.

The files that are uploaded into {{site.data.keyword.cephaas_short}} Object Storage are called objects. Objects can be anywhere from very small (a few bytes) to very large. They are organized into buckets that serve as containers for objects, and which can be configured independently from one another. Objects themselves have their own metadata in the form of user-defined tags or legal holds. Within a bucket, the hierarchy of objects is effectively "flat", although it is possible to add prefixes to object names to provide some organization and to provide flexibility in listing and other operations.

All data stored in {{site.data.keyword.cephaas_short}} Object Storage is encrypted, erasure-coded, and dispersed across storage nodes.

All requests and responses are made over `HTTPS`. All `GET` and `HEAD` requests made to objects return an Etag value with the MD5 hash of the object to ensure integrity on the client side.

Developers use APIs to interact with their object storage. {{site.data.keyword.cephaas_short}} Object Storage supports a subset of the S3 API for reading and writing data, as well as for bucket configuration. Software development kits (SDKs) are available for Go framework. A plug-in is available for the [{{site.data.keyword.cloud_notm}} Command-Line Interface](/docs/cli?topic=cli-getting-started){: external}.


## Known limitations
{: #known-limitations}

This section includes the known limitations that might impact your experience.

* Only one object user is supported

* S3 features align with IBM Storage Ceph version 7.1

* Virtual hosted buckets not supported

* Static Web Hosting not supported


## HMAC credentials
{: #about-hmac-creds}

HMAC credentials consist of an Access Key and Secret Key paired for use with S3-compatible tools and libraries that require authentication.

The {{site.data.keyword.cephaas_short}} S3 API is a REST-based API for reading and writing objects. It uses HMAC Access Keys for authentication and supports a subset of the S3 API for easy migration of applications to IBM Cloud.

You can create a set of HMAC credentials using the console, CLI, and API. For instructions, see [Create HMAC credentials](/docs/cephaas?topic=cephaas-creating-s3-credential).

You must have the IBM Cloud Platform Command Line installed to use the examples.
{: requirement}


## Next Steps
{: #next-steps}

Documentation on the best way to [get started](/docs/cephaas?topic=cephaas-getting-started) since they provide support to [create S3 HMAC Credentials](/docs/cephaas?topic=cephaas-creating-s3-credential) and [upload the associated S3 SSL Certificate](/docs/cephaas?topic=cephaas-uploading-s3-certificate).

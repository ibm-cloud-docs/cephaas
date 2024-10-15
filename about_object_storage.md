---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-15"

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

Developers use APIs to interact with their object storage. {{site.data.keyword.cephaas_short}} Object Storage supports a subset of the S3 API for reading and writing data, as well as for bucket configuration. Software development kits (SDKs) are available for Go framework. A plug-in is available for the IBM Cloud command-line Interface (TODO: Need to update this link).

## Next Steps
{: #next-steps}

Documentation on the best way to get started (TODO: Update link) provides support to create HMAC Credentials and upload the associated S3 SSL Certificate.

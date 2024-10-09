---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-09"

keywords: cephaas, endpoint, location, object storage, bucket, region, rclone, resiliency

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Endpoints
{: #endpoints}

Sending a REST API request or configuring a storage client requires setting a target endpoint or URL. Each storage location has its own set of URLs.
{: shortdesc}

All requests must use SSL when using IAM, and the service will reject any plain-text requests.

All {{site.data.keyword.cephaas_full}} endpoints support TLS 1.2 encryption.
{: note}


## Endpoint Types
{: #advanced-endpoint-types}

{{site.data.keyword.cephaas_full_notm}} is connected to a single network using **direct endpoints**.

**Direct endpoints** are used for requests originating from resources within {{site.data.keyword.cephaas_short}}. Direct endpoints provide better performance over Public endpoints and do not incur charges for any outgoing or incoming bandwidth even if the traffic is cross regions or across data centers.

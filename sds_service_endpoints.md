---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-14"

keywords: cephaas, service endpoints

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Service endpoints
{: #sds-service-endpoints}

Sending a REST API request or configuring a storage client requires setting a target endpoint or URL. Each storage location has its own set of URLs.


## Endpoint Types
{: #sds-endpoint-types}

IBM Cloud® services are connected to a three-tiered network, segmenting public, private, and management traffic.

* **Private endpoints** are available for requests originating from within IBM Cloud. Private endpoints provide better performance and do not incur charges for any outgoing or incoming bandwidth even if the traffic is cross regions or across data centers. Whenever possible, it is best to use a private endpoint.

* **Public endpoints** can accept requests from anywhere and charges are assessed on outgoing bandwidth. Incoming bandwidth is free. Public endpoints should be used for access not originating from an IBM Cloud cloud computing resource.

* **Direct endpoints** are used for requests originating from resources within {{site.data.keyword.cephaas_short}}. Like Private endpoints, Direct endpoints provide better performance over Public endpoints and do not incur charges for any outgoing or incoming bandwidth even if the traffic is cross regions or across data centers.

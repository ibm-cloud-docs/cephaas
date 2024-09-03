---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-03"

keywords: cephaas, endpoint, location, object storage, bucket, region, rclone, resiliency

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Endpoints and storage locations
{: #endpoints}

Sending a REST API request or configuring a storage client requires setting a target endpoint or URL. Each storage location has its own set of URLs.
{: shortdesc}

All requests must use SSL when using IAM, and the service will reject any plain-text requests.

All {{site.data.keyword.cos_full}} endpoints support TLS 1.2 encryption.
{: note}


## Endpoint Types
{: #advanced-endpoint-types}

{{site.data.keyword.cephaas_full_notm}} is connected to a single network using **direct endpoints**.

**Direct endpoints** are used for requests originating from resources within {{site.data.keyword.cephaas_short}}. Like Private endpoints, Direct endpoints provide better performance over Public endpoints and do not incur charges for any outgoing or incoming bandwidth even if the traffic is cross regions or across data centers.


## Regional Endpoints
{: #endpoints-region}

Buckets that are created at a regional endpoint distribute data across three data centers that are spread across a metro area. Any one of these data centers can suffer an outage or even destruction without impacting availability.


| Region     | Type   | Endpoint                                                  |
| ---------- | ------ | --------------------------------------------------------- |
| `us-south` | Direct | `s3.direct.us-south.software-defined-storage.appdomain.cloud` |
| `us-east`  | Direct | `s3.direct.us-east.software-defined-storage.appdomain.cloud`  |
| `eu-gb`    | Direct | `s3.direct.eu-gb.software-defined-storage.appdomain.cloud`    |
| `eu-de`    | Direct | `s3.direct.eu-de.software-defined-storage.appdomain.cloud`    |
| `au-syd`   | Direct | `s3.direct.au-syd.software-defined-storage.appdomain.cloud`   |
| `jp-tok`   | Direct | `s3.direct.jp-tok.software-defined-storage.appdomain.cloud`   |
| `jp-osa`   | Direct | `s3.direct.jp-osa.software-defined-storage.appdomain.cloud`   |
| `ca-tor`   | Direct | `s3.direct.ca-tor.software-defined-storage.appdomain.cloud`   |
| `br-sao`   | Direct | `s3.direct.br-sao.software-defined-storage.appdomain.cloud`   |
| `eu-es`    | Direct | `s3.direct.eu-es.software-defined-storage.appdomain.cloud`    |
{: class="simple-tab-table"}
{: caption="Table 1. Regional Endpoints" caption-side="top"}
{: #regionalendpointtable3}
{: tab-title="Direct"}
{: tab-group="Regional-endpoints"}

## Cross-Region Endpoints
{: #endpoints-geo}

Buckets that are created at a cross-region endpoint distribute data across three regions in a geographical location. Any one of these regions can suffer an outage or even destruction without impacting availability. Requests are routed to the nearest cross-region metropolitan area by using Border Gateway Protocol (BGP) routing. In an outage, requests are automatically rerouted to an active region. Advanced users who want to write their own failover logic can do so by sending requests to a [tethered endpoint](/docs/sdsaas?topic=sdsaas-advanced-endpoints) and bypassing the BGP routing.


| Geo    | Type   | Endpoint                                            |
| ------ | ------ | --------------------------------------------------- |
| `us`   | Direct | `s3.direct.us.software-defined-storage.appdomain.cloud` |
| `eu`   | Direct | `s3.direct.eu.software-defined-storage.appdomain.cloud` |
| `ap`   | Direct | `s3.direct.ap.software-defined-storage.appdomain.cloud` |
{: class="simple-tab-table"}
{: caption="Table 2. Cross Region Endpoints" caption-side="top"}
{: #crossregionalendpointtable3}
{: tab-title="Direct"}
{: tab-group="Cross-regional-endpoints"}

For example:

* Data in `US` cross-region bucket is distributed only across regions (such as Dallas, WDC, and SJC) in the `US` geographical location.
* Data in `EU` cross-region bucket is distributed only across regions (such as, Amsterdam, FRA, and Milan) in the `EU` geographical location.
* Data in `AP` cross-region bucket is distributed only across regions (such as, TOK, SYD, and OSA) in the `AP` geographical location.

## Single Data Center Endpoints
{: #endpoints-zone}

Single data centers are not co-located with IBM Cloud services, such as IAM or Key Protect, and offer no resiliency in a site outage or destruction.

If a networking failure results in a partition where the data center is unable to access IAM, authentication and authorization information is read from a cache that might become stale. This cached data might result in a lack of enforcement of new or altered IAM policies for up to 24 hours.
{: important}



| Region  | Type   | Endpoint                                               |
| ------- | ------ | ------------------------------------------------------ |
| `ams03` | Direct | `s3.direct.ams03.software-defined-storage.appdomain.cloud` |
| `che01` | Direct | `s3.direct.che01.software-defined-storage.appdomain.cloud` |
| `mil01` | Direct | `s3.direct.mil01.software-defined-storage.appdomain.cloud` |
| `mon01` | Direct | `s3.direct.mon01.software-defined-storage.appdomain.cloud` |
| `par01` | Direct | `s3.direct.par01.software-defined-storage.appdomain.cloud` |
| `sjc04` | Direct | `s3.direct.sjc04.software-defined-storage.appdomain.cloud` |
| `sng01` | Direct | `s3.direct.sng01.software-defined-storage.appdomain.cloud` |
{: class="simple-tab-table"}
{: caption="Table 3. Single Data Center Endpoints" caption-side="top"}
{: #sdcendpointtable3}
{: tab-title="Direct"}
{: tab-group="single-datacenter-endpoints"}



## EU-Managed Endpoints
{: #endpoints-eu-managed}

The {{site.data.keyword.at_full_notm}} can archive to a bucket at specific {{site.data.keyword.cos_full_notm}} instances. This table shows the EU-Managed locations of {{site.data.keyword.cos_short}} instances for archiving events.

| {{site.data.keyword.cos_short}} bucket location | Resiliency   | City                        |
| ----------------------------------------------- | ------------ | --------------------------- |
| `ams03`                                         | Single Site  | Amsterdam                   |
| `eu-de`                                         | Regional     | Frankfurt                   |
| `eu-gb`                                         | Regional     | London                      |
| `mil01`                                         | Single Site  | Milan                       |
| `par01`                                         | Single Site  | Paris                       |
| `eu-geo`                                        | Cross Region | Amsterdam, Frankfurt, Milan |
{: caption="Table 4. EU-managed Endpoints" caption-side="top"}

## Resource Configuration Endpoints
{: #endpoints-rc}

Requests made using the Resource Configuration API are sent to a global endpoint, regardless of the bucket's location.

| Type    | Endpoint                                               |
| ------- | ------------------------------------------------------ |
| Public  | `config.software-defined-storage.cloud.ibm.com/v1`         |
| Private | `config.private.software-defined-storage.cloud.ibm.com/v1` |
| Direct  | `config.direct.software-defined-storage.cloud.ibm.com/v1`  |
{: caption="Table 5. Resource Configuration Endpoints" caption-side="top"}

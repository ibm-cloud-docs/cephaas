---

copyright:
 years: 2024, 2025
lastupdated: "2025-04-22"

keywords: planning, site-readiness, ceph as a service, network requirement

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Network requirements
{: #network-requirements}

To facilitate the {{site.data.keyword.cephaas_full_notm}} server infrastructure connectivity, you must evaluate the following network requirements:

* The data center site must provide network cables to connect the {{site.data.keyword.cephaas_full_notm}} on-premises network infrastructure and the data network at the site.

* Network cables within the rack are provided as part of the service.

* The site must provide two uplink cables along with LACP bond over the uplink cables, and compatible switch modules that fit into QSFP+ ports only. For information on supported transceivers, see [Cisco Optics-to-Device Compatibility Matrix](https://tmgmatrix.cisco.com/?si=93600CD-GX).

* IP addresses will need to be provided inside of the customer's IP subnet. More details on the number of IP addresses and internet endpoints will be shared after the order is placed.

    IPv6 is currently not supported in this version.
    {: exception}

* Some of these addresses will need to be able to reach the internet.

{{site.data.keyword.cephaas_short}} does not allow deployment in fully disconnected environments.
{: note}

## Network configuration architecture
{: #network-arch}

The following architecture diagram describes the default components that are part of the required network configuration.

![Network architecture of {{site.data.keyword.cephaas_full_notm}}](images/network-architecture.svg "Network architecture of {{site.data.keyword.cephaas_full_notm}}"){: caption="Network architecture of {{site.data.keyword.cephaas_full_notm}}" caption-side="bottom"}

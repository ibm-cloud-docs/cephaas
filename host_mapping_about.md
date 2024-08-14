---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-14"

keywords: sdsaas cephaas about volume host mappings

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# About volume host mappings
{: #sds-about-volume-host-mappings}

With {{site.data.keyword.cephaas_full}}, block-level access to the Ceph storage cluster can take advantage of the NVMe-oF standard to provide data storage. The NVMe TCP protocol allows clients, which are known as initiators, to send NVMe-oF commands to storage devices, which are known as targets, over an Internet Protocol network. Initiators can be either Linux client or VMWare clients or both. For VMWare clients, the NVMe TCP volumes are shown as VMFS Data store and for Linux clients, the NVMe TCP volumes are shown as block devices.

Initiators are configured to allow the NVMe TCP protocol to send NVMe-oF commands to targets over an Internet Protocol network.

The NVMe-oF gateway initiator can be configured on either of the following platform version:

* Red Hat Enterprise Linux 9.2 or later

* VMware vSphere Hypervisor (ESXi) 7.0U3 or later


For more information, see [link coming soon]





## Limitation
{: #sds-host-mapping-limitations}


* Mapping of the same volume to multiple RHEL hosts is not supported.

* In order for multiple ESXi hosts to be able to access the same volume, they must be part of the same VMWare cluster.

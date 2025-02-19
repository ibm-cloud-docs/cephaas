---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-19"

keywords: cephaas cephaas about volume host mappings

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}


# About NVMe-oF host mappings
{: #about-volume-host-mappings}

With {{site.data.keyword.cephaas_full}}, block-level access to the Ceph storage cluster can take advantage of the NVMe over Fabrics (NVMe-oF) standard to provide data storage. The NVMe TCP protocol allows clients, which are known as initiators, to send NVMe-oF commands to storage devices, which are known as targets, over an Internet Protocol network. Initiators can be either Linux client or VMWare clients or both. For VMWare clients, the NVMe TCP volumes are shown as `VMFS data store` and for Linux clients, the NVMe TCP volumes are shown as `block devices`.

Initiators are configured to allow the NVMe TCP protocol to send NVMe-oF commands to targets over an Internet Protocol network.

The NVMe-oF gateway initiator can be configured on either of the following platform version:

* Red Hat Enterprise Linux 9.2 or later

* VMware vSphere Hypervisor (ESXi) 7.0U3 or later

The NVMe/TCP interface is not encrypted and requires additional network controls.
{: important}

For guidance, see [Connecting from NVME-oF initiators](/docs/cephaas?topic=cephaas-connecting-nvme-initiators).



## Mapping limitation
{: #host-mapping-limitations}


* Mapping of the same volume to multiple RHEL hosts is not supported.

* In order for multiple ESXi hosts to be able to access the same volume, they must be part of the same VMWare cluster.

* A host will not be able to discover any volumes if it is not mapped to any of the volumes. However, the host will be able to discover all volumes even if it is mapped to a single volume.


## Configuring NVMe-oF initiators
{: #config-nvme-initiators}

Before you can use the benefits of the Ceph NVMe-oF gateway, you must install and configure an NVMe-oF gateway by using command-line interface.

* [Configuring the NVMe-oF initiator for Red Hat Enterprise Linux](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvmeof-initiator-rhel)

* [Configuring the NVMe-oF initiator for VMware ESXi](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvmeof-initiator-vmware-esxi)


### Configuring NVMe-oF initiator for RHEL
{: #config-nvmeof-initiator-rhel}

Use this procedure to configure the NMVe fabrics for Red Hat Enterprise Linux (RHEL).

1. Install the nvme-cli.

    ```sh
    yum install nvme-cli
    ```
    {: pre}


1. Install the necessary NVMe packages.

    ```sh
    modprobe nvme-fabrics
    ```
    {: pre}

    Make the boot setting persistent by loading the module on boot with this setting:

    ```sh
    echo nvme_tcp > /etc/modules-load.d/nvme_tcp.conf
    ```
    {: pre}

1. Get the host NVMe Qualified Name (NQN) for each host.

    ```sh
    cat /etc/nvme/hostnqn
    ```
    {: pre}

    For example,

    ```json
    # cat /etc/nvme/hostnqn

    nqn.2014-08.org.nvmexpress:uuid:950ddadf-f995-47b7-9416-b9bb233f66e3
    ```
    {: screen}


### Configuring the NVMe-oF initiator for VMware ESXi
{: #config-nvmeof-initiator-vmware-esxi}

Use this procedure to configure the NMVe fabrics for VMware ESXi.

1. Make sure that the VMware ESXi host is running VMware vSphere Hypervisor (ESXi) 7.0U3 version or later.

2. Configure an NVMe/TCP adapter.

3. Enable NVMe/TCP on a physical network interface controller (NIC).

    ```sh
    esxcli nvme fabrics enable --protocol TCP --device vmnicN
    ```
    {: pre}

    Replace N with the number of NIC.

4. Tag a VMkernel NIC to permit NVMe/TCP traffic.

    ```sh
    esxcli network ip interface tag add --interface-name vmkN --tagname NVMeTCP
    ```
    {: pre}

    Replace N with the ID of the VMkernel.

5. Get the host NVMe Qualified Name (NQN) for each host.

    ```sh
    esxcli nvme info get
    ```
    {: pre}

    For example,

    ```json
    # esxcli nvme info get

    Host NQN: nqn.2014-08.com.ibm.ceph:nvme:host01
    ```
    {: screen}

## Next steps
{: #nvmeof-initiator-nextsteps}

Once the initiator is configured, a corresponding “host” must be created in {{site.data.keyword.cephaas_short}}. See [Creating the host](/docs/cephaas?topic=cephaas-creating-host).

During host creation, NQN from the initiator must be used.
{: note}

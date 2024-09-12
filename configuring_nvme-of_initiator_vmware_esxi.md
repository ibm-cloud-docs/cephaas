---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-12"

keywords: sds, cephaas host, nvme-of initiator rhel

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the NVMe-oF initiator for VMware ESXi
{: #configuring-nvmeof-initiator-vmware-esxi}

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

Once the initiator is configured, a corresponding “host” must be created in {{site.data.keyword.cephaas_short}}. See [Creating the host](/docs/sdsaas?topic=sdsaas-creating-hosts).

During host creation, NQN from the initiator must be used.
{: note}

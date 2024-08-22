---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-22"

keywords: sdsaas cephaas about volume host mappings

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# About volume host mappings
{: #about-volume-host-mappings}

With {{site.data.keyword.cephaas_full}}, block-level access to the Ceph storage cluster can take advantage of the NVMe-oF standard to provide data storage. The NVMe TCP protocol allows clients, which are known as initiators, to send NVMe-oF commands to storage devices, which are known as targets, over an Internet Protocol network. Initiators can be either Linux client or VMWare clients or both. For VMWare clients, the NVMe TCP volumes are shown as VMFS Data store and for Linux clients, the NVMe TCP volumes are shown as block devices.

Initiators are configured to allow the NVMe TCP protocol to send NVMe-oF commands to targets over an Internet Protocol network.

The NVMe-oF gateway initiator can be configured on either of the following platform version:

* Red Hat Enterprise Linux 9.2 or later

* VMware vSphere Hypervisor (ESXi) 7.0U3 or later


For more information, see [Connecting from NVME-oF initiators]



## Limitation
{: #host-mapping-limitations}


* Mapping of the same volume to multiple RHEL hosts is not supported.

* In order for multiple ESXi hosts to be able to access the same volume, they must be part of the same VMWare cluster.


## Connecting from NVME-oF initiators
{: #connecting-from-nvme-of-initiators}


### Before you begin configuring NVMe-oF initiator for RHEL
{: #prereq-config-nvmeof-initiator-rhel}

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


### Connecting from Red Hat Enterprise Linux
{: #connect-from-rhel}

1. Verify that the target is reachable from the initiator.

    ```sh
    nvme discover -t tcp -a GATEWAY_IP -s 4420
    ```
    {: pre}

    See following example.
    ```bash
    [root@host01 ~]# nvme discover -t tcp -a 10.172.19.01 -s 4420
    ```
    {: screen}

1. Connect to the NVMe-oF target.

    Use the storage_identifiers.id that is returned in the host details in GET /hosts API.

    ```sh
    nvme connect -t tcp -a GATEWAY_IP -n storage_identifiers.id
    ```
    {: pre}


    See following example.
    ```sh
    [root@host01 ~]# nvme connect -t tcp -a 10.172.19.01 -n nqn.2016-06.io.spdk:cnode1
    ```
    {: screen}

### Verify that the initiator is set up correctly.
{: #connection-verification}

1. List the NVMe-oF block devices.

    ```sh
    nvme list
    ```
    {: pre}

    See following example.

    ```sh
    [root@host01 ~]# nvme list

    Node                    Generic           SN                   Model                   Namespace Usage                      Format           FW Rev

    ---------------------   ----------------  -------------------  ----------------------- --------- -------------------------- ---------------- --------

    /home/nvme01_node01     /home/ng1n1       SPDK00000000000001   SPDK bdev Controller    1          10,49  MB /  10,49  MB      4 KiB +  0 B   23.01

    ...

    ```
    {: screen}

2. Create a filesystem on the desired target, found in step 1.

    ```sh
    mkfs NVME_NODE_PATH
    ```
    {: pre}

    For example,

    ```sh
    [root@host01 ~]# mkfs /home/nvme01_node01

    mke2fs 1.46.5 (20-Dec-2023)

    Discarding device blocks: done

    Creating filesystem with 2560 4k blocks and 2560 inodes

    Allocating group tables: done

    Writing inode tables: done

    Writing superblocks and filesystem accounting information: done
    ```
    {: screen}

3. Mount the NVMe node on the NVMe-oF directory.

    ```sh
    Mount NVMe-oF.
    mkdir /mnt/nvmeof
    ```
    {: pre}

    For example,

    ```sh
    [root@host01 ~]# mkdir /mnt/nvmeof
    ```
    {: pre}

    Mount the node on within the NVMe-oF directory.

    ```sh
    mount NVME_NODE_PATH /mnt/nvmeof
    ```
    {: pre}

    For example,

    ```sh
    [root@host01 ~]# mount /home/nvme01_node01 /mnt/nvmeof
    ```
    {: pre}

4. Using sudo commands, list mounted NVMe-oF files.

    ```sh
    ls /mnt/nvmeof
    ```
    {: pre}

    For example,
    ```sh
    lost+found
    ```
    {: screen}

5. Create a text file within the mnt/nvmeof directory.

    ```sh
    sudo bash -c "echo Hello NVMe-oF > /mnt/nvmeof/hello.txt"

    ```
    {:pre}

6. Verify that the text file can now be reached.

    ```sh
    cat /mnt/nvmeof/hello.txt
    ```
    {: pre}

    ```sh
    Hello NVMe-oF

    ```
    {:screen}


## Configuring the NVMe-oF initiator for VMware ESXi
{: #configuring-nvmeof-initiator-vmware-esxi}

Use this procedure to configure the NMVe fabrics for VMware ESXi.

1. Make sure that the VMware ESXi host is running VMware vSphere Hypervisor (ESXi) 7.0U3 version or later.

2. Configure NVMe/TCP adapter.

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

Once the initaitor is configured, a corresponding “host” must be created in {{site.data.keyword.cephaas_short}}. See [Creating the host](/docs/sdsaas?topic=sdsaas-creating-hosts).

During host creation, NQN from the initiator must be used.
{: note}

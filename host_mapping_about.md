---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-03"

keywords: sdsaas cephaas about volume host mappings

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# About volume host mappings
{: #about-volume-host-mappings}

With {{site.data.keyword.cephaas_full}}, block-level access to the Ceph storage cluster can take advantage of the NVMe over Fabrics (NVMe-oF) standard to provide data storage. The NVMe TCP protocol allows clients, which are known as initiators, to send NVMe-oF commands to storage devices, which are known as targets, over an Internet Protocol network. Initiators can be either Linux client or VMWare clients or both. For VMWare clients, the NVMe TCP volumes are shown as VMFS Data store and for Linux clients, the NVMe TCP volumes are shown as block devices.

Initiators are configured to allow the NVMe TCP protocol to send NVMe-oF commands to targets over an Internet Protocol network.

The NVMe-oF gateway initiator can be configured on either of the following platform version:

* Red Hat Enterprise Linux 9.2 or later

* VMware vSphere Hypervisor (ESXi) 7.0U3 or later


For more information, see [Connecting from NVME-oF initiators](/docs/sdsaas?topic=sdsaas-about-volume-host-mappings#connecting-nvme-initiators)



## Mapping limitation
{: #host-mapping-limitations}


* Mapping of the same volume to multiple RHEL hosts is not supported.

* In order for multiple ESXi hosts to be able to access the same volume, they must be part of the same VMWare cluster.


## Connecting from NVMe-oF initiators
{: #connecting-nvme-initiators}

Before you can utilize the benefits of the Ceph NVMe-oF gateway, you must install and configure an NVMe-oF gateway by using command line interface.

* [Configuring the NVMe-oF initiator for Red Hat Enterprise Linux](/docs/sdsaas?topic=sdsaas-about-volume-host-mappings#prereq-config-nvmeof-initiator-rhel)

* [Configuring the NVMe-oF initiator for VMware ESXi](/docs/sdsaas?topic=sdsaas-about-volume-host-mappings#configuring-nvmeof-initiator-vmware-esxi)


### Configuring NVMe-oF initiator for RHEL
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

1. Next steps: [Connecting initiators from RHEL](/docs/sdsaas?topic=sdsaas-about-volume-host-mappings#connect-from-rhel)


### Configuring the NVMe-oF initiator for VMware ESXi
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



## Connecting from Red Hat Enterprise Linux
{: #connect-from-rhel}

1. Verify that the target is reachable from the initiator.

    ```sh
    nvme discover -t tcp -a GATEWAY_IP -s 4420
    ```
    {: pre}


1. Connect to the NVMe-oF target.

    Use the storage_identifiers.id that is returned in the host details in GET /hosts API.

    ```sh
    nvme connect -t tcp -a GATEWAY_IP -n storage_identifiers.id
    ```
    {: pre}


### Verify that the initiator is set up correctly.
{: #connection-verification-rhel}

1. List the NVMe-oF block devices.

    ```sh
    nvme list
    ```
    {: pre}

    See following example.

    ```sh
    Node                    Generic           SN                   Model                   Namespace Usage                      Format           FW Rev

    ---------------------   ----------------  -------------------  ----------------------- --------- -------------------------- ---------------- --------

    /home/nvme01_node01     /home/ng1n1       SPDK00000000000001   SPDK bdev Controller    1          10,49  MB /  10,49  MB      4 KiB +  0 B   23.01

    ...
    ```
    {: screen}

1. Create a filesystem on the desired target, found in step 1.

    ```sh
    mkfs NVME_NODE_PATH
    ```
    {: pre}

    See following example.

    ```sh
    $ mkfs /home/nvme01_node01
    mke2fs 1.46.5 (20-Dec-2023)
    Discarding device blocks: done
    Creating filesystem with 2560 4k blocks and 2560 inodes

    Allocating group tables: done
    Writing inode tables: done
    Writing superblocks and filesystem accounting information: done
    ```
    {: screen}

1. Mount the NVMe node on the NVMe-oF directory.

    ```sh
    mkdir /mnt/nvmeof
    ```
    {: pre}

    ```sh
    mount NVME_NODE_PATH /mnt/nvmeof
    ```
    {: pre}

    See following example.

    ```sh
    mount /home/nvme01_node01 /mnt/nvmeof
    ```
    {: screen}

1. Using sudo commands, list mounted NVMe-oF files.

    ```sh
    ls /mnt/nvmeof
    ```
    {: pre}

    For example,
    ```sh
    $ ls /mnt/nvmeof
    lost+found
    ```
    {: screen}


1. Create a text file within the "mnt/nvmeof" directory.

    ```sh
    sudo bash -c "echo Hello NVMe-oF > /mnt/nvmeof/hello.txt"
    ```
    {: pre}

1. Verify that the text file can now be reached.

    ```sh
    $ cat /mnt/nvmeof/hello.txt
    Hello NVMe-oF
    ```
    {: screen}



## Connecting from VMWare ESXi
{: #connecting-from-vmware-esxi}


1. List the NVMe-oF adapter.

    ```sh
    esxcli nvme adapter list
    ```
    {: pre}

    See following example.

    ```sh
    [root@host01:~] esxcli nvme adapter list

    Adapter  Adapter Qualified Name           Transport Type  Driver     Associated Devices
    -------  -------------------------------- --------------  ---------  ------------------
    vmhba64  aqn:nvmetcp:ac-1f-6b-0a-18-74-T  TCP             nvmetcp    vmnic0
    ```
    {: screen}

2. Discover any NVMe-oF-gateway subsystems.

    ```sh
    esxcli nvme fabrics discover -a NVME_TCP_ADAPTER -i GATEWAY_IP -p 4420
    ```
    {: pre}

    See following example.

    ```sh
    [root@host01:~] esxcli nvme fabrics discover -a vmhba64 -i 10.0.211.196 -p 4420

    Transport Type Address Family Subsystem Type Controller ID Admin Queue Max Size Transport Address Transport Service ID Subsystem NQN              Connected

    -------------- -------------- -------------- ------------- -------------------- ----------------- -------------------- -------------------------- ---------

    TCP            IPv4           NVM            65535         128                   10.0.211.196     4420                 nqn.2016-06.io.spdk:cnode1  false
    ```
    {: screen}

3. Connect to NVMe-oF gateway subsystem.

    ```sh
    esxcli nvme fabrics connect -a NVME_TCP_ADAPTER -i GATEWAY_IP -p 4420 -s SUBSYSTEM_NQN
    ```
    {: pre}

    See following example.

    ```sh
    [root@host01:~] esxcli nvme fabrics connect -a vmhba64 -i 10.0.211.196 -p 4420 -s nqn.2016-06.io.spdk:cnode1
    ```
    {: screen}

4. List NVMe/TCP controller list.

    ```sh
    esxcli nvme controller list
    ```
    {: pre}

    See following example.

    ```sh
    [root@host01:~] esxcli nvme controller list

    Name                                                                                        Controller Number  Adapter  Transport Type  Is Online
    ------------------------------------------------------------------------------------------  -----------------  -------  --------------  ---------
    nqn.2016-06.io.spdk:cnode1#vmhba64#10.0.211.196:4420                                                      301  vmhba64  TCP                  true
    ```
    {: screen}

5. List NVMe-oF namespaces in the storage_identifiers.

    ```sh
    esxcli nvme namespace list
    ```
    {: pre}

    See following example.

    ```sh
    [root@host01:~] esxcli nvme namespace list

    Name                                Controller Number  Namespace ID  Block Size  Capacity in MB
    ------------------                  -----------------  ------------  ----------  --------------

    eui.0100000001000000e4d25c00001ae214               256             1         512          953869

    eui.01abc123def456g7e4d25c00001ae214               301             1         512             500

    eui.02abc123def456g7e4d25c00001ae215               301             2         512             500

    eui.03abc123def456g7e4d25c00001ae216               301             3         512             500
    ```
    {: screen}




### Verify that the initiator is set up correctly.
{: #connection-verification-vmware}

1. From the vSphere Client, go to the **ESXi host**.

2. On the Storage page, go to the **Devices** tab.

3. Verify that the `NVMe/TCP` disks are listed in the table.

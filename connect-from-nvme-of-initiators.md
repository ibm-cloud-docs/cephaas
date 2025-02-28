---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-28"

keywords: cephaas cephaas about volume host mappings

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}


# Connecting from NVMe-oF initiators
{: #connecting-nvme-initiators}

Before you can use the benefits of the Ceph NVMe-oF gateway, you must install and configure an NVMe-oF gateway by using command-line interface.

* [Configuring the NVMe-oF initiator for Red Hat Enterprise Linux](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvmeof-initiator-rhel)

* [Configuring the NVMe-oF initiator for VMware ESXi](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvmeof-initiator-vmware-esxi)


## Connecting from Red Hat Enterprise Linux
{: #connect-from-rhel}

1. Verify that the target is reachable from the initiator.

    ```sh
    nvme discover -t tcp -a GATEWAY_IP -s 8009
    ```
    {: pre}

    GATEWAY_IP can be fetched from `GET /hosts` API.
    {: tip}

1. Connect to the NVMe-oF target.

    ```sh
    nvme connect-all -traddr=GATEWAY_IP --transport=tcp -l 1800
    ```
    {: pre}


### Verify that the initiator is set up correctly for RHEL
{: #connection-verification-rhel}

1. List the NVMe-oF block devices.

    ```sh
    nvme list
    ```
    {: pre}

    See the following example.

    ```sh
    Node                    Generic           SN                   Model                   Namespace Usage                      Format           FW Rev

    ---------------------   ----------------  -------------------  ----------------------- --------- -------------------------- ---------------- --------

    /home/nvme01_node01     /home/ng1n1       SPDK00000000000001   SPDK bdev Controller    1          10.74  GB /  10.74  GB      4 KiB +  0 B   23.01

    ...
    ```
    {: screen}

1. Create a filesystem on the desired target, found in step 1.

    ```sh
    mkfs NVME_NODE_PATH
    ```
    {: pre}

    See the following example.

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

    See the following example.

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

    See the following example.

    ```sh
    [root@host01:~] esxcli nvme adapter list

    Adapter  Adapter Qualified Name           Transport Type  Driver     Associated Devices
    -------  -------------------------------- --------------  ---------  ------------------
    vmhba64  aqn:nvmetcp:ac-1f-6b-0a-18-74-T  TCP             nvmetcp    vmnic0
    ```
    {: screen}

2. Discover any NVMe-oF-gateway subsystems.

    ```sh
    esxcli nvme fabrics discover -a NVME_TCP_ADAPTER -i GATEWAY_IP -p 8009
    ```
    {: pre}

    See the following example.

    ```sh
    [root@host01:~] esxcli nvme fabrics discover -a vmhba64 -i 10.0.211.196 -p 8009

    Transport Type Address Family Subsystem Type Controller ID Admin Queue Max Size Transport Address Transport Service ID Subsystem NQN              Connected

    -------------- -------------- -------------- ------------- -------------------- ----------------- -------------------- -------------------------- ---------

    TCP            IPv4           NVM            65535         128                   10.0.211.196     8009                 nqn.2016-06.io.spdk:cnode1  false
    ```
    {: screen}

3. Connect to NVMe-oF gateway subsystem.

    ```sh
    esxcli nvme fabrics connect -a NVME_TCP_ADAPTER -i GATEWAY_IP -p 4420 -s SUBSYSTEM_NQN
    ```
    {: pre}

    See the following example.

    ```sh
    [root@host01:~] esxcli nvme fabrics connect -a vmhba64 -i 10.0.211.196 -p 4420 -s nqn.2016-06.io.spdk:cnode1
    ```
    {: screen}

4. List NVMe/TCP controller list.

    ```sh
    esxcli nvme controller list
    ```
    {: pre}

    See the following example.

    ```sh
    [root@host01:~] esxcli nvme controller list

    Name                                                                                        Controller Number  Adapter  Transport Type  Is Online
    ------------------------------------------------------------------------------------------  -----------------  -------  --------------  ---------
    nqn.2016-06.io.spdk:cnode1#vmhba64#10.0.211.196:8009                                                      301  vmhba64  TCP                  true
    ```
    {: screen}

5. List NVMe-oF namespaces in the storage_identifiers.

    ```sh
    esxcli nvme namespace list
    ```
    {: pre}

    See the following example.

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




### Verify that the initiator is set up correctly for VMware ESXi
{: #connection-verification-vmware}

1. From the vSphere Client, go to the **ESXi host**.

2. On the Storage page, go to the **Devices** tab.

3. Verify that the `NVMe/TCP` disks are listed in the table.

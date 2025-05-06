---

copyright:
 years: 2024, 2025
lastupdated: "2025-05-06"

keywords: cephaas settings, trial version, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Using trial version
{: #using-trial-version}

You can use a trial version of {{site.data.keyword.cephaas_full}} to evaluate if the service meets your use cases. Here are the steps to configure the trial version in your infrastructure.

## Connecting to IBM Cloud VPN
{: #connect-ibmcloud-vpn}

1. Download the latest version of OpenVPN connect client from **Community Downloads** > **Open Source VPN** > **OpenVPN**.
2. Download the openvpn zip file shared by the customer support.
3. Import the trial-x-vpn-client-cert.ovpn file into OpenVPN software.
4. Connect to the VPN.
 
You will not require a password for the VPN connection as the connection is managed via client certificates.
{: note}

## Connecting to VCenter appliance
{: #connect-vcenter-appliance}

After connecting to the VPN, you can directly visit the VMWare systems prepared at the following servers:

- esx1.cephaastrialsx.com - Your esx server 1. Credentials for the same will be provided via the setup zip file.

- esx2.cephaastrialsx.com - Your esx server 2. Credentials for the same will be provided via the setup zip file.

- vcenter.cephaastrialsx.com - Your Vcenter. Credentials for the same will be provided via the setup zip file.

- setup-node.cephaastrialsx.com -  VM provided to run IBMCloud CLI commands.

## Preparing host for connectivity
{: #prepare-host-for-connectivity}

For host connectivity, you will need hostNQN from the ESXi server. This can be retrieved through either VCenter UI or ESXi CLI. 

### Fetching the hostNQN from the ESXi server using the VCenter UI
{: #fetch-host-nqn-esxserver-ui}

1. Select the host you want to add. 
2. Navigate to the **Configure** > **Storage Adapters** tab.
3. Click on the NVME/TCP adapter.
4. Navigate to the **Controllers** tab.
5. Click **Add Controller**.
6. Copy hostNQN from the screen.

### Fetching the hostNQN from the ESXi CLI
{: #fetch-host-nqn-esxserver-cli}

1. Ensure that SSH and ESXi shell services are enabled on the host you want to connect.
2. Login via ssh to the ESXi server you wish to connect.
3. Run the command `esxcli nvme info get`.

## Performing NVME discovery from the VCenter UI
{: #nvme-discovery-vcenter-ui}

1. Select the host you want to add.
2. Navigate to the **Configure** > **Storage Adapters** tab.
3. Click on the NVME/TCP adapter.
4. Navigate to the **Controllers** tab.
5. Click on **Add Controller**.
6. Enter any IP mentioned in the mapping info of the mapped volume(s).
7. Click **Discover Controllers**. A list of available nvme controllers for connect will be displayed.
8. Select all the controllers and click OK.

## Performing NVME discovery from ESXi CLI
{: #nvme-discovery-esxi-cli}

1. Ensure that SSH and ESXi shell services are enabled for the host you want to connect.
2. Login via ssh to the ESX server you wish to connect.
3. Run the command 

    ```sh
    esxcli nvme fabrics discover -a "<adapter> -i <ip-address>"
    ```
    {: pre}
     
    Here is a sample command:

    ```sh
    esxcli nvme fabrics discover -a vmhba65 -i 10.95.76.12
    ```
    {: pre}
     

4. In order to connect, run the same command with -c , to automatically connect to all available controllers. This is the recommended way to connect to all controllers. 

    For example:

    ```sh
    esxcli nvme fabrics discover -a vmhba65 -i 10.95.76.12 -c
    ```
    {: pre}

## Accessing NVME storage
{: #accessing-nvme-storage}

1. After the NVMe discovery and connect is done, you can see the CephaaS volume reflected as a disk on the ESXi server. This can be viewed in the storage devices section of the ESXi server. 
2. Create a VMFS datastore on that host using the newly available disk. 
3. Right click the host and click on Storage/New Datastore. 
4. Select the newly available NVMe disk.
5. You can now use the VMFS datastore for your VM workloads.

---

copyright:
 years: 2024, 2025
lastupdated: "2025-08-26"

keywords: cephaas settings, trial version, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring VMware environment
{: #using-trial-version}

To effectively use the {{site.data.keyword.cephaas_short}} VMware plugin, it is essential to ensure your VMware environment is properly configured. This involves preparing your vCenter setup to support seamless integration and optimal performance. Below are the key steps to configure your VMware environment:


## Connecting to VCenter appliance
{: #trial-connect-to-vcenter}

After connecting to the VPN, the VMWare systems prepared for your trials can be accessed at the following addresses through a web browser. The credentials required to access them can be found in the zip file that was shared by the IBM representative.

- esx1.cephaastrialsx.com - Your esx server 1

- esx2.cephaastrialsx.com - Your esx server 2

- vcenter.cephaastrialsx.com - Your Vcenter


## Preparing Host for NVMe/TCP Connectivity with IBM Cloud Block Storage
{: #trial-prepare-host-for-connectivity}

To connect the ESXi host to IBM Cloud Block Storage over NVMe/TCP, you must first enable NVMe/TCP services on the host and gather specific configuration details, including the hostNQN (Host NVMe Qualified Name). Follow the steps below to complete the setup.

### Enable NVMe/TCP on ESXi VMKernel Adapters
{: #trial-enable-nvme-on-adapters}

1. Open the vCenter UI and select the ESXi host you want to configure.
2. Navigate to **Configure** > **VMKernel adapters**.
3. Select and edit the desired VMKernel adapter.
4. In the edit dialog, enable the NVMe/TCP service.
5. Save the changes.

### Add NVMe/TCP Storage Adapter
{: #trial-add-nvme-adapter}

1. With the same host selected, go to **Configure** > **Storage Adapters** in vCenter UI.
2. Click Add.
3. Select the NVMe/TCP adapter.
4. Select the default physical adapter (NIC) for NVMe/TCP traffic.

### Connecting the VMware environment to CephaaS storage
{: #cephaas-vmware-plugin}

{{site.data.keyword.cephaas_full}} provides a VMware plugin that seamlessly integrates with your vCenter environment, enabling efficient management of virtual infrastructure. With the plugin, you can:

- [Add deployments](/docs/cephaas?topic=cephaas-managing-deployments-vsphere-plug-in&interface=ui#add-deployment): For connecting the VMware environment to CephaaS environment

The FQDN information will be included in the setup.zip file of the trials and the [API key](/docs/account?topic=account-userapikey) will be needed for the access management. 
{: note}

- [Add hosts](/docs/cephaas?topic=cephaas-managing-hosts-vsphere-plug-in&interface=ui#add-host): Register ESXi hosts to enable storage provisioning and management through the plugin
- [Create datastores](/docs/cephaas?topic=cephaas-managing-datastores-vsphere-plug-in&interface=ui#add-datastore): Set up datastores supported by {{site.data.keyword.cephaas_short}} to support your VM workloads

Please note that the trial environment has a total allocated capacity of 1TB. The cumulative capacity allocated to all the datastores that are created cannot exceed this limit.
{: note}



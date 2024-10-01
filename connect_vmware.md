---
copyright:
 years: 2024, 2024
lastupdated: "2024-10-01"

keywords: Connect VMware environment

subcollection: sdsaas
---


{{site.data.keyword.attribute-definition-list}}

# Connect to VMware environment
{: #connecting-to-environment}

These instructions are for a quick installation overview of the IBM Storage Ceph as a Service Plugin for vSphere.

1. Download the Open Virtual Appliance (OVA) installation package.
[IBM® Fix Central](https://www.ibm.com/support/fixcentral){: external}

2. Deploy the appliance.

    From the vSphere Client, deploy the OVF template within a VMware cluster.

    In the Select networks step, select a network that allows communication between vCenter and the management interfaces for IBM Storage Systems.
    {: note}

3. Power on the appliance after the OVA is successfully deployed.

    - By default, the appliance is configured with a firewall and therefore does not respond to ping (ICMP) requests.
    - Initial login has a default password of IBMplugin and requires the user to change the password before continuing.

4. Register the vSphere Plugin into vCenter.

    a. Log in to the vSphere Plugin appliance as root.
    b. Register the vSphere Plugin with the vCenter instance or instances.

        The registration command displays the thumbprint of the vSphere instance for verification.

        ```sh
        ibm-plugin register -u <vCenter Username> -v <IP_or_FQDN_of_vCenter>
        ```
        {: pre}

        To link multiple linked-mode vCenters to a single plug-in appliance, register each vCenter independently.
        {:note}

        Enter the vCenter password when prompted.

    c. To complete the plug-in activation, refresh the vSphere Client browser.

5. Check the plug-in status to see which vCenters are registered to the appliance.

    ```sh
    ibm-plugin status
    ```
    {: pre}

    The ibm-plugin status command can be run at any time.
    
    If the plug-in is not registered to any vCenter, the Plugin Registered output displays as False. 

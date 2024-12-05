---
copyright:
 years: 2024, 2024
lastupdated: "2024-12-05"

keywords: Connect VMware environment

subcollection: cephaas
---


{{site.data.keyword.attribute-definition-list}}

# Installing vSphere plug-in
{: #installing-the-plugin}

These instructions are for a quick installation overview of the {{site.data.keyword.cephaas_full}} plug-in for VMWare vSphere.


## Before you begin
{: #vm-connect-prereq}
{: step}

Download the Open Virtual Appliance (OVA) installation package. [IBM® Fix Central](https://www.ibm.com/support/fixcentral){: external}


## Deploy the appliance
{: #deploy-app}
{: step}

1. From the vSphere Client,  deploy the OVF template within a VMware cluster.

2. In the Select networks step, select a **network** that allows communication between vCenter and the management interfaces for IBM Storage Systems.

3. Power on the appliance after the OVA is successfully deployed.

    - By default, the appliance is configured with a firewall and therefore does not respond to ping (ICMP) requests.

    - Initial login has a default password of IBMplug-in and requires the user to change the password before continuing.


## Register the vSphere plug-in into vCenter.
{: #register-plug-in}
{: step}

1. Log in to the vSphere plug-in appliance as root.

2. Register the vSphere plug-in with the vCenter instance or instances.

    The registration command displays the thumbprint of the vSphere instance for verification.

    ```sh
    ibm-plugin register -u <vCenter Username> -v <IP_or_FQDN_of_vCenter>
    ```
    {: pre}

    To link multiple linked-mode vCenters to a single plug-in appliance, register each vCenter independently.

3. Enter the vCenter password when prompted.

4. To complete the plug-in activation, refresh the vSphere Client browser.


## Verify registration status
{: #verify-connect}
{: step}

Check the plug-in status to see which vCenters are registered to the appliance.

```sh
ibm-plugin status
```
{: pre}

The `ibm-plugin` status command can be run at any time.

If the plug-in is not registered to any vCenter, the plug-in Registered output displays as `False`.

If you wish to unregister the plug-in, run the command `ibm-plugin unregister`.
{: note}

## Next Steps

After the installation, you need to get the following from your admin.

- Service ID with a viewer role for {{site.data.keyword.cephaas_full_notm}}
- API Key

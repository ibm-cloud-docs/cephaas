---

copyright:
 years: 2024, 2026
lastupdated: "2026-02-03"

keywords: cephaas settings, trial version, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to the trial environment 
{: #trial-env}

## Connecting to IBM Cloud VPN
{: #trial-connect-to-ibmcloud}

To securely access IBM Cloud resources during a trial, each new customer must connect through the IBM Cloud VPN. 

1. Download and install the latest version of OpenVPN client from https://openvpn.net/client/.
2. Download the `setup.zip` file provided by your IBM representative and extract its contents to access the `.ovpn` configuration file.
3. Import the `cephaas-trial-(n).ovpn` file into your OpenVPN client.
4. Use the imported configuration to establish a VPN connection to the trial environment.

You will not require a password for the VPN connection as the connection is managed via client certificates. Establishing a VPN connection is a trial-specific requirement. This ensures secure access to the VMware environment that has been provisioned exclusively for trial users. It is important to note that this VPN requirement does not apply to production deployments of IBM Storage for Ceph as a Service.
{: note}

---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-17"


keywords: preorder, checklist, preinstallation checklist, site-readiness, ceph as a service, network validation, account activation

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Prerequisites for installing {{site.data.keyword.cephaas_short}}
{: #pre_installation_checklist}


Proper planning is essential for the successful setup and use of {{site.data.keyword.cephaas_full_notm}} deployment. It ensures that you have everything you need and that you meet all the prerequisites for your deployment.
{: shortdesc}

IBM owns the responsibility to install, upgrade, and update the hardware and software for the on-premises infrastructure. IBM coordinates with you for any dependencies to ensure that your {{site.data.keyword.cephaas_full_notm}} data center meets all the prerequisites before the installation. You will need “pay-as-you-go” {{site.data.keyword.cloud_notm}} account for {{site.data.keyword.cephaas_full_notm}}.

IBM provides a pre-installation checklist after you place an order for {{site.data.keyword.cephaas_full_notm}} and also during the pre-installation stage. You must complete the items in the pre-installation checklist to prepare your {{site.data.keyword.cephaas_full_notm}} environment for the installation. An IBM representative conducts an installation readiness review to ensure that you understand the prerequisites.

## Preorder checklist
{: #pre-order-check}

Before you place the order, you must confirm if the following criteria to install the rack in your data center are met:
*  Identify an {{site.data.keyword.cloud_notm}} region closest to the physical location of your data center where the rack resides. The network latency between your data center and the selected {{site.data.keyword.cloud_notm}} region that will run the control plane must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Network latency](/docs/cephaas?topic=cephaas-network_latency_main).
*  Confirm that the site and environment requirements to place the rack are met. For more information, see [Site-planning and environmental requirements](/docs/cephaas?topic=cephaas-pre_installation_checklist#site-plan-env-req).

## {{site.data.keyword.cephaas_full_notm}} requirements
{: #sds-sys-req}

Before you connect to the {{site.data.keyword.cloud_notm}}, perform other pre-installation activities, you must complete the following tasks or keep the following information in hand:
*  You must have an active {{site.data.keyword.cloud_notm}} account ID. To create an {{site.data.keyword.cloud_notm}} account ID, see [Setting up your IBM Cloud account](/docs/account?topic=account-account-getting-started){: external}.
*  Create a Satellite location associated with an {{site.data.keyword.cloud_notm}} region. Select the {{site.data.keyword.cloud_notm}} region that is closest to the physical location of your data center. The network latency between your data center and the selected {{site.data.keyword.cloud_notm}} region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Create a Satellite location overview](/docs/satellite?topic=satellite-locations){: external}.

## Site-planning and environmental requirements
{: #site-plan-env-req}

Before you place the order, you must prepare your data center site to meet the following site and environmental requirements:
*  The data center can accommodate all the 42U racks.
*  The floor of the data center is able to withstand the weight of the racks and other equipment. For more information about rack dimensions and weight, see [Site access requirements](/docs/cephaas?topic=cephaas-site-access-requirements).
*  Ensure heating, ventilation, and air conditioning (HVAC) setup for front-to-back airflow and humidity control is ready. For more information, see [Environmental requirements](/docs/cephaas?topic=cephaas-environmental-requirements).
*  The data center site meets the power source requirements for rack connector and load requirements. For more information, see [Power requirements](/docs/cephaas?topic=cephaas-power-requirements).
*  The data center is in a secured location with restricted access. For more information, see [Site readiness](/docs/cephaas?topic=cephaas-site-readiness).

The following data center site requirements must be met before the rack is delivered to your data center:
*  Ensure that the IBM TLS SSR team has the security and access approval to operationally manage the rack infrastructure.
*  Ensure that the power cables and network cables are routed to the location where the rack will be installed. The power cables must have connectors that are compatible with rack PDU. For more information, see [Supported PDU power cord](https://www.ibm.com/docs/en/power9/0009-ESS?topic=pr-supported-pdu-power-cords){: external}.
*  Ensure that the data center site also meets the below [networking requirements](/docs/cephaas?topic=cephaas-pre_installation_checklist&interface=ui#network-req).

## Networking requirements
{: #network-req}

The following network requirements must be completed before the rack is delivered to your data center:

*  After the order is placed, IBM provides a pre-installation checklist. Complete the pre-installation checklist to provide network-specific information, such as Autonomous system numbers (ASN), Service key, and others. For more information, see [Network requirements](/docs/cephaas?topic=cephaas-network-requirements).

* A part of these requirements, you must have a list of IP addresses that will be associated with services from {{site.data.keyword.cephaas_short}}. Some of these IP addresses must be able to connect with other services on the internet. Make sure your network is ready to allow for this communication.

{{site.data.keyword.cephaas_short}} does not allow deployment in fully disconnected environments.
{: note}


## Network validation and account activation
{: #validation-activation}

To validate the network functions and activate the {{site.data.keyword.cephaas_full_notm}} account after delivery, the SSR team will work with you to help ensure the visibility of the rack Satellite location in your {{site.data.keyword.cephaas_short}} account.

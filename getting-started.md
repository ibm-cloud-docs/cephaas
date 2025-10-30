---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-30"

keywords: ceph as a service, getting started, cephaas, unified storage, cost estimation, software defined storage, on-premises, consultation request

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

An IBM representative will contact you to understand your requirements. Post discussions and approvals, your IBM representative will place your order. While the order is processing, you can track the status from your {{site.data.keyword.cloud_notm}} account dashboard.
{: important}

# Getting started with {{site.data.keyword.cephaas_full_notm}}
{: #getting-started}

{{site.data.keyword.cephaas_full}} is a powerful software-defined enterprise storage platform that delivers a cloud-like experience on-premises with the convenience and flexibility of a pay-as-you-go model. Designed to provision storage in minutes, it enables self-provisioning of storage resources, allowing enterprises to quickly adapt to rapidly changing demands, breaking down the barriers of managing multiple dedicated Storage Systems.
{: shortdesc}

By eliminating over-provisioning and right-sizing your infrastructure, you can ensure optimal resource utilization and cost-efficiency. Based on the benefits of IBM Storage Ceph, it breaks down the silos of dedicated, proprietary storage infrastructure and software, offering unified support for multiple protocols across a single platform. With a seamless, single point of management, it simplifies operations, giving you control over your entire storage environment from one interface.


## Estimating service cost
{: #estimatecost}
{: step}

{{site.data.keyword.cephaas_full_notm}} is available in {{site.data.keyword.cloud_notm}} catalog as a tile. You can click the **Storage Ceph as a Service** tile to start the service cost estimation tool.

1. To estimate your monthly storage cost, use the **Estimate Cost** option in the product overview page.

2. Select the required **Subscription term**, choose the **Storage Tier** from **Performance** and **Capacity**, and enter the **Total storage** (TB) value to view your estimated costs.

    You can select **Subscription term** for 3, 4, or 5 years with performance or capacity tier, which best matches your needs.  {{site.data.keyword.cephaas_full_notm}} hardware contains optimized racks, servers, storage, networking switches, and integrated software, which connect to the {{site.data.keyword.cloud_notm}}. The Service is an infrastructure as a service (IaaS) offering where the operating system, middleware, and application software is licensed and managed by IBM. The hardware is owned and maintained by IBM and the service infrastructure is installed in your designated datacenter.

     {{site.data.keyword.cephaas_full_notm}} can be provisioned with 100 TB to 3200 TB with two storage options:

    - **Performance Tier** which is tailored to performance intensive application workloads. To serve these workloads, the hardware consists of NVMe storage devices and high-bandwidth network cards as well as the CPU and memory components that are needed to use this equipment. You can provision the capacity starting from 100 TB to 800 TB in this tier.

    - **Capacity Tier** offers cost-effective online storage of less frequently used data. You can provision the capacity from 800 TB - 3200 TB in this tier.



## Requesting for consultation
{: #consultation-request}
{: step}

After saving your cost estimation, click **Start order process** and share your contact details. On submitting the contact form, a Confirmation ID is generated. A notification with the consultation confirmation ID and your service cost estimation is displayed, and an email is sent to IBM.

Soon thereafter, an IBM representative will contact you to understand your requirements. Post discussions and approvals, the IBM representative places your order. The details of your order and order tracking link is email to you. While the order is processing, you can track the status from your {{site.data.keyword.cloud_notm}} account dashboard.


## Preparing your deployment
{: #managingnewstorage}
{: step}



After you receive the email confirmation that your order is placed, the next step is to

1. Select the {{site.data.keyword.satellitelong_notm}} location and naming your deployment.

    You can either select an existing Satellite location or create a new on-premises type of location.
    To create a location, open the [Satellite console](https://cloud.ibm.com/satellite/locations/create/onPrem){: external}.

    This Satellite location is required to be present on {{site.data.keyword.cloud_notm}} without a host for your on-premises deployment, since the location is not dependent on the host and other setup in your infrastructure.
    {: important}

    While creating the {{site.data.keyword.satellitelong_notm}} location, choose Object storage standard plan and make sure to select the **Managed for** region as **Dallas** or **Frankfurt**. The region selected must be closest to where your data center physically reside to ensure low network latency between your Satellite location and {{site.data.keyword.cloud_notm}}.
    {: tip}

2. Create your deployment. To learn how to create your deployments, see [Creating deployments](/docs/cephaas?topic=cephaas-administrators&interface=ui&code=curl#provision-deployment).


## Infrastructure setup and maintenance
{: #setupandmaintenance}
{: step}

After the order is placed and the infrastructure is ready to be installed, IBM will work with you to install your CephaaS deployment in your data center. You are responsible for meeting the physical site requirements; for example, energy, cooling, space, physical network connectivity; where the infrastructure is installed. IBM is responsible for installation, configuration, and operation of the infrastructure.

While IBM owns and operates the infrastructure, you are able to provision your own storage volumes. IBM continues to operate and maintain the respective hardware and software maintenance operations.

To understand and prepare your data center before the rack arrives for installation, read the [prerequisites for installing  {{site.data.keyword.cephaas_full_notm}}](/docs/cephaas?topic=cephaas-pre_installation_checklist).
{: note}

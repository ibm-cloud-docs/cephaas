---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-25"

keywords: unified storage, volume size, Security, Encryption, secondary storage, mount storage, provision storage, cost estimation

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

An IBM representative will contact you to understand your requirements. Post discussions and approvals, your IBM representative will place your order. While the order is processing, you can track the status from your IBM Cloud account dashboard.
{: important}

# Getting started with {{site.data.keyword.cephaas_full_notm}}
{: #getting-started}

{{site.data.keyword.cephaas_full}} is a powerful software-defined enterprise storage platform that delivers a cloud-like experience on-premises with the convenience and flexibility of a pay-as-you-go model. Designed to provision storage in minutes, it enables self-provisioning of storage resources, allowing enterprises to quickly adapt to rapidly changing demands, breaking down the barriers of managing multiple dedicated storage systems.
{: shortdesc}

By eliminating over-provisioning and right-sizing your infrastructure, you can ensure optimal resource utilization and cost-efficiency. Based on the benefits of IBM Storage Ceph, it breaks down the silos of dedicated, proprietary storage infrastructure and software, offering unified support for multiple protocols across a single platform. With a seamless, single point of management, it simplifies operations, giving you control over your entire storage environment from one interface.


## Estimating service cost
{: #estimatecost}
{: step}

{{site.data.keyword.cephaas_full_notm}} is available in IBM Cloud Catalog. You can click on the **Storage Ceph as a Service** tile to start the service cost estimation tool.

1. To estimate your monthly storage cost, use the **Estimate Cost** option in the product overview page.

2. Select the required **Subscription term**, choose the **Storage tier** from `Performance` and `Capacity`, and enter the **Total storage** (TB) value to view your estimated costs.

    You can select **Subscription term** for 3, 4, or 5 years with performance or capacity tier, which best matches your needs. {{site.data.keyword.cephaas_short}} hardware contains optimized racks, servers, storage, networking switches, and integrated software, which connect to the IBM Cloud. The Service is an infrastructure as a service (IaaS) offering where the operating system, middleware, and application software is licensed and managed by IBM. The hardware is owned and maintained by IBM and the service infrastructure is installed in your designated datacenter.

    {{site.data.keyword.cephaas_short}} can be provisioned with 100 TB to 3200 TB with two storage options:

    - **Performance Tier** which is tailored to performance intensive application workloads. To serve these workloads, the hardware consists of NVMe storage devices and high-bandwidth network cards as well as the CPU and memory components needed to utilize this equipment. You can provision the capacity starting from 100 TB to 800 TB in this tier.

    - **Capacity tier** offers cost-effective online storage of less frequently used data. You can provision the capacity from 800 TB - 3200 TB in this tier.



## Requesting for consultation
{: #consultation-request}
{: step}

After saving your cost estimation, click **Start order process** and share your contact details. On submitting the contact form, a Confirmation ID is generated. A notification with the consultation confirmation ID and your service cost estimation is displayed, and an email is sent to IBM.

Soon thereafter, an IBM representative will contact you to understand your requirements. Post discussions and approvals, the IBM representative places your order. The details of your order and order tracking link is email to you. While the order is processing, you can track the status from your IBM Cloud account dashboard.


## Preparing your deployment
{: #managingnewstorage}
{: step}



After IBM places your order, the next step is to select the IBM Cloud Satellite location and naming your deployment.

1. Click **Prepare deployment** link from your `In progress` order.
2. On the **Prepare deployment** screen, select your **IBM Cloud Satellite location** and **Resource group**.

    To understand more about IBM Cloud Satellite locations, refer [IBM Cloud Satellite](/https://test.cloud.ibm.com/satellite/overview).
    {: note}

3. Enter your **Deployment name** and click **Create**.

    Your **Deployment Preparation** status will be reflected as **Completed**.

    After the on-premise hardware setup is done, the deployment will be reflected as **Available** and ready-to-be provisioned.


## Infrastructure setup and maintenance
{: #setupandmaintenance}
{: step}

After the order is placed and the infrastructure is ready to be installed, IBM will work with you to install your CephaaS deployment in your data center. You will be responsible for meeting the physical site requirements (for example, energy, cooling, space, physical network connectivity.) where the infrastructure will be installed. IBM will be responsible for installation, configuration, and operation of the infrastructure.

While IBM will own and operate the infrastructure, you will be able to provision your own storage volumes. IBM will continue to operate and maintain the respective hardware and software maintenance operations.

To understand and prepare your data center before the rack arrives for installation, read the [pre-requisites for installing {{site.data.keyword.cephaas_short}}](/docs/cephaas?topic=cephaas-pre_installation_checklist).
{: note}

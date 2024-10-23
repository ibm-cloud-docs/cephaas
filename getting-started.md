---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-23"

keywords: unified storage, volume size, IOPS, Security, Encryption, LUN, secondary storage, mount storage, provision storage, iSCSI, MPIO, redundant

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

# Getting started with {{site.data.keyword.cephaas_full_notm}}
{: #getting-started}

{{site.data.keyword.cephaas_full}} is a powerful software-defined enterprise storage platform that delivers a cloud-like experience on-premises with the convenience and flexibility of a pay-as-you-go model. Designed to provision storage in minutes, it enables self-provisioning of storage resources, allowing enterprises to quickly adapt to rapidly changing demands, breaking down the barriers of managing multiple dedicated storage systems.
{: shortdesc}

By eliminating over-provisioning and right-sizing your infrastructure, you can ensure optimal resource utilization and cost-efficiency. Based on the benefits of IBM Storage Ceph, it breaks down the silos of dedicated, proprietary storage infrastructure and software, offering unified support for multiple protocols across a single platform. With a seamless, single point of management, it simplifies operations, giving you control over your entire storage environment from one interface.


## Before you begin
{: #prereqs}
{: step}

You can select the term (1, 2, 3, 4, or 5 years), performance tier or capacity tier which best matches your needs. IBM Storage Ceph as a Service hardware contains optimized rack(s), servers, storage, networking switches, and software integrated, which connect to the IBM Cloud.
The Service is an infrastructure as a service (IaaS) offering where the operating system, middleware, and application software is licensed and managed by IBM. The hardware is owned and maintained by IBM and the service infrastructure is installed in your designated datacenter.
IBM Storage Ceph as a Service can be provisioned from 100 TB to 3200 TB with two options:

- The Performance Tier of IBM Storage Ceph as a Service is tailored to performance intensive application workloads. To serve these workloads, the hardware consists of NVMe storage devices and high-bandwidth network cards as well as the CPU and memory components needed to utilize this equipment. You can provision the capacity from 100-800TB in this tier.

- The Capacity tier of IBM Storage Ceph as a Service offers cost-effective online storage of less frequently used data. You can provision the capacity from 800TB-3200TB in this tier.



## Provisioning considerations
{: #provconsiderationsBlockStorage}
{: step}

### Block storage volume size
{: #sdsblockstoragevolumesize}

IBM Storage Ceph as a Service is available in IBM Cloud Catalog under the IBM Storage Ceph as a Service tile. You can use the cost estimator option in the GUI to define the required configuration and get an estimated monthly cost. You can contact IBM or your business partner for more pricing details and to place an order.

After the order is placed and the infrastructure is ready to be installed, IBM works with you to install it in your data center. You are responsible for meeting the physical site requirements (for example, energy, cooling, space, physical network connectivity.) where the infrastructure will be installed. IBM is responsible for installation, configuration, and operation of the infrastructure.

While IBM owns and operates the infrastructure, you can provision your own storage volumes. IBM operates and maintains the respective hardware and software maintenance operations.


## Submitting your order
{: #submitorder}
{: step}

After you estimate the cost of your order, your IBM representative will contact you for placing your order.


## Setting up your deployments
{: #managingnewstorage}
{: step}

To get started, perform the following steps:

1. Set up your satellite

Begin by selecting your IBM Cloud satellite location. This is an important step to ensure your deployment runs smoothly. With IBM Cloud Satellite, you can use your own compute infrastructure that is in your on-premises data center, other cloud providers, or edge networks to create a Satellite location. Then, you can use the capabilities of Satellite to run IBM Cloud services on your infrastructure, and consistently deploy, manage, and control your app workloads.

You can either review your current satellite locations or create a new location.


To learn more about {{site.data.keyword.satellitelong_notm}}, refer [Getting started with IBM Cloud Satellite](/docs/satellite?topic=satellite-getting-started).


2. Prepare Deployment

After setting up the satellite, the next step is to prepare your deployment and assigning  it a name. You will receive the link to set up your deployment in an email after you place the order with your IBM representative.

Make sure to complete both the above steps before your device arrives on-site to ensure a seamless setup.

---

copyright:
 years: 2024, 2026
lastupdated: "2026-06-23"

keywords: fusion as a service, getting started, fusion, openshift, compute, storage, billing options, roks clusters, ceph storage, performance tier, capacity tier

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

An IBM representative will contact you to understand your requirements. Post discussions and approvals, your IBM representative will place your order. While the order is processing, you can track the status from your {{site.data.keyword.cloud_notm}} account dashboard.
{: important}

# Getting started with IBM Fusion as a service
{: #getting-started}

IBM Fusion as a service (Fusion) is IBM's fully managed Red Hat OpenShift on IBM Cloud Satellite platform delivered on-premises with cloud-like consumption and operational models. It allows you to self-service provision Red Hat OpenShift clusters, deploy applications, and consume storage services with cloud-like elasticity and a pay-for-what-you-use model—all while maintaining data sovereignty in your own data center.
{: shortdesc}

This topic guides you through understanding Fusion capabilities, requesting consultation, and getting started with your deployment.

## What is IBM Fusion as a service?
{: #what-is-fusionaas}

Fusion combines the power of Red Hat OpenShift with IBM's enterprise-grade infrastructure management, delivered as a fully managed service in your data center. IBM owns, operates, and maintains the hardware while you focus on deploying and managing your applications.

### Key benefits
{: #key-benefits}

- **Fully managed Red Hat OpenShift on-premises**: IBM Site Reliability Engineering (SRE) teams handle installation, configuration, monitoring, patching, upgrades, and day-to-day operations.
- **Cloud consumption pricing**: Pay only for what you use with metered usage and flexible monthly commitments—no large upfront capital expenditures.
- **IBM SRE-led lifecycle management**: 24x7 monitoring, proactive maintenance, rapid incident response, and coordinated platform updates.
- **Enterprise-grade security, resiliency, and observability**: Multi-layered security controls, redundant components, automated failover, and comprehensive monitoring.
- **GPU-enabled workloads**: Support for AI, machine learning, data analytics, and high-performance computing with GPU acceleration.


## Ordering IBM Fusion as a service
{: #ordering-fusion}
{: step}

Fusion as a service is available in the {{site.data.keyword.cloud_notm}} catalog. To get started, configure your deployment requirements and place your order.

1. Navigate to the {{site.data.keyword.cloud_notm}} catalog and locate the **IBM Fusion** tile.

2. Click the tile to access the configuration page.

3. Configure your deployment requirements:

   **Location**
   
   Select where you want to install Fusion hardware in your data center:
   - **Geography**: Select your geographic region (for example, North America)
   - **Country**: Select your country (for example, United States)
   - **State**: Select your state or region (for example, New York)

   **Infrastructure**
   
   Select the type of infrastructure you want to include:
   - **Compute**: For managing compute resources such as vCPUs, memory, GPUs, and cluster deployments
   - **Storage**: For managing block, file, and object storage capacity across your workloads
   
   You can select one or both options depending on your requirements.

   **Subscription term**
   
   Choose your subscription term to optimize costs:
   - **3 years**: Standard subscription term with flexible monthly commitments

4. For Compute infrastructure, select from the following AI solutions:

   **Integrated AI**
   - 256 vCPUs
   - 2304 GB memory
   - 4 GPUs
   - 22.3 TiB usable storage capacity

   **Data Lakehouse (Small)**
   - 640 vCPUs
   - 4352 GB memory
   - 8 GPUs
   - 74.5 TiB usable storage capacity

   **Application platform**
   
   Choose from availability zone configurations:
   - **1 Availability Zone (XSmall)**: 128 vCPUs, 1280 GB memory, 0 GPUs, 18.6 TB usable storage capacity
   - **1 Availability Zone (Small)**: 256 vCPUs, 1024 GB memory, 0 GPUs, 37.2 usable storage capacity
   - **1 Availability Zone (Medium)**: 512 vCPUs, 2816 GB memory, 0 GPUs, 52.1 TiB usable storage capacity
   - **1 Availability Zone (Large)**: 1024 vCPUs, 4096 GB memory, 0 GPUs, 81.9 TiB usable storage capacity
   - **1 Availability Zone (XLarge)**: 1920 vCPUs, 7424 GB memory, 0 GPUs, 119.1 TiB usable storage capacity

5. Review the total estimated cost in the summary panel.

6. Click **Get consultation** to submit your configuration and request a consultation with IBM experts.

After your consultation and approval, your IBM representative will place your order. You will receive order confirmation and tracking information via email.

The hardware includes optimized racks, servers, storage, networking switches, and integrated software that connects to {{site.data.keyword.cloud_notm}}. IBM owns and maintains the hardware, and the service infrastructure is installed in your designated data center.
{: note}

## Tracking your order
{: #track-order}
{: step}

After your order is placed, you can track its status from the {{site.data.keyword.cloud_notm}} console.

1. Log in to the {{site.data.keyword.cloud_notm}} console.

2. Navigate to **Fusion as a Service** > **Deployments**.

3. The Deployments page displays a welcome message: "Welcome! Your order is on its way."

4. Your IBM representative will soon contact you to assist with the setup. Meanwhile, explore the responsibilities for your deployment by clicking **Review responsibilities**.

5. The page displays your orders with the following information:
   - **Order ID**: Unique identifier for your order
   - **Subscription term**: Duration of your subscription (for example, 3 years)
   - **Tier**: Infrastructure type (Compute or Storage)
   - **Deployment preparation**: Status indicator showing preparation progress

6. Before Preparing your deployment, the deployment preparation status shows as **Not started** until you begin the preparation process.

## Preparing your deployment
{: #prepare-deployment}
{: step}

After your order is confirmed, you need to prepare your deployment by configuring the satellite location and deployment details.

### Configure deployment settings
{: #configure-deployment}

1. From the Deployments page, locate your Compute order.

2. Click **Prepare deployment** next to your order.

3. The **Prepare deployment** side panel opens. Configure the following settings:

   **Satellite location**
   
   To begin configuring your deployment, select an IBM Cloud Satellite location and name your deployment. You can create and manage your satellite locations in IBM Cloud Satellite.
   
   - **Satellite location**: Select an existing Satellite location from the dropdown
     - The Satellite location connects your on-premises infrastructure to {{site.data.keyword.cloud_notm}}
     - To create a new location, you must first create it in [IBM Cloud Satellite](https://cloud.ibm.com/satellite/locations){: external}

   **Deployment details**
   
   - **Name**: Enter a descriptive name for your deployment
   
   - **Resource group**: Select the resource group for organizing your deployment resources. The default Resource group is selected. 
     - You can view all resource groups by clicking **View all resource groups**
     - You can create a new resource group by clicking **Create resource group**

4. Click **Create** to complete the deployment preparation, or click **Cancel** to close the panel without saving.

5. After you create the deployment, your **Deployment preparation** status changes to **Provision in progress**.

6. After you complete the deployment preparation, IBM manages the infrastructure installation and setup. The setup may take a few days. Once the setup is complete, the **Deployment preparation** status changes to **Completed**.




## Next steps
{: #next-steps}

Now that your deployment is set up and ready:

Create clusters
:   Provision Red Hat OpenShift clusters through the IBM Cloud Satellite portal. See [Creating clusters](/docs/cephaas?topic=cephaas-create-clusters).

Manage cluster quotas
:   Update your default cluster quota or set quotas for specific clusters. See [Managing cluster quotas](/docs/cephaas?topic=cephaas-update-cluster-quota).

View deployment capacity
:   Monitor your deployment's resource usage and capacity. See [Viewing deployment capacity](/docs/cephaas?topic=cephaas-view-deployment-capacity).

Access management
:   Configure user access and permissions for your deployment. See [Managing access to Fusion as a Service](/docs/cephaas?topic=cephaas-iam_access-fusionaas).

Learn more
:   Read [What is IBM Fusion as a service?](/docs/cephaas?topic=cephaas-about-fusionaas) for detailed information.

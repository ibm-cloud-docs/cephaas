---

copyright:
 years: 2024, 2026
lastupdated: "2026-06-12"

keywords: fusion as a service, getting started, fusionaas, openshift, compute, storage, billing options, roks clusters, ceph storage, performance tier, capacity tier

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

An IBM representative will contact you to understand your requirements. Post discussions and approvals, your IBM representative will place your order. While the order is processing, you can track the status from your {{site.data.keyword.cloud_notm}} account dashboard.
{: important}

# Getting started with Fusion as a Service
{: #getting-started}

Fusion as a Service (FusionaaS) is IBM's fully managed Red Hat OpenShift on IBM Cloud Satellite platform delivered on-premises with cloud-like consumption and operational models. It allows you to self-service provision Red Hat OpenShift clusters, deploy applications, and consume storage services with cloud-like elasticity and a pay-for-what-you-use model—all while maintaining data sovereignty in your own data center.
{: shortdesc}

This topic guides you through understanding FusionaaS capabilities, estimating costs, and getting started with your deployment.

## What is Fusion as a Service?
{: #what-is-fusionaas}

FusionaaS combines the power of Red Hat OpenShift with IBM's enterprise-grade infrastructure management, delivered as a fully managed service in your data center. IBM owns, operates, and maintains the hardware while you focus on deploying and managing your applications.

### Key benefits
{: #key-benefits}

- **Fully managed Red Hat OpenShift on-premises**: IBM Site Reliability Engineering (SRE) teams handle installation, configuration, monitoring, patching, upgrades, and day-to-day operations.
- **Cloud consumption pricing**: Pay only for what you use with metered usage and flexible monthly commitments—no large upfront capital expenditures.
- **IBM SRE-led lifecycle management**: 24x7 monitoring, proactive maintenance, rapid incident response, and coordinated platform updates.
- **Enterprise-grade security, resiliency, and observability**: Multi-layered security controls, redundant components, automated failover, and comprehensive monitoring.
- **GPU-enabled workloads**: Support for AI, machine learning, data analytics, and high-performance computing with GPU acceleration.

### How it works
{: #how-it-works}

With FusionaaS, IBM delivers, installs, and operates infrastructure in your data center:

- **IBM-owned infrastructure**: IBM provides optimized racks, servers, storage, networking switches, and integrated software that connects to {{site.data.keyword.cloud_notm}}.
- **Fully managed operations**: IBM handles all operational complexity while you retain physical control of your data.
- **Self-service provisioning**: Provision Red Hat OpenShift clusters and storage through familiar {{site.data.keyword.cloud_notm}} interfaces and APIs.
- **Flexible scaling**: Scale resources on-demand without procurement delays.

## Understanding billing options
{: #billing-options}
{: step}

FusionaaS offers flexible billing options based on your workload requirements. You can select either **Compute** or **Storage** services, or both, depending on your needs.

### Compute billing option
{: #compute-billing}

The **Compute** option enables you to provision and manage Red Hat OpenShift on IBM Cloud Satellite clusters in your on-premises environment.

**What you get:**
- Fully managed Red Hat OpenShift clusters with IBM SRE support
- Self-service cluster provisioning through {{site.data.keyword.cloud_notm}} console
- Automated lifecycle management (upgrades, patching, monitoring)
- GPU support for AI and data-intensive workloads
- Pay-per-use pricing based on compute resources consumed

### Storage billing option
{: #storage-billing}

The **Storage** option provides access to IBM Storage Ceph as a Service with two performance tiers to match your workload requirements.

**Storage tiers available:**

- **Performance Tier**: Tailored for performance-intensive application workloads
    - NVMe storage devices for ultra-low latency
    - High-bandwidth network cards
    - Optimized CPU and memory components
    - Capacity range: 100 TB to 800 TB
    - Best for: Databases, transactional workloads, real-time analytics

- **Capacity Tier**: Cost-effective storage for less frequently accessed data
    - Optimized for capacity and cost efficiency
    - Capacity range: 800 TB to 3,200 TB
    - Best for: Backups, archives, secondary storage, large datasets

**What you get:**
- Unified storage platform supporting multiple protocols (block, file, object)
- Self-provisioning of storage volumes
- Single point of management
- Pay-per-use pricing based on storage consumed
- IBM-managed infrastructure and operations

### Combining Compute and Storage
{: #combined-billing}

You can select both Compute and Storage options to create a complete on-premises cloud platform:
- Deploy containerized applications on managed Red Hat OpenShift clusters
- Consume high-performance or capacity storage as needed
- Benefit from integrated management and unified billing
- Scale compute and storage independently based on workload demands

## Estimating service cost
{: #estimatecost}
{: step}

FusionaaS is available in the {{site.data.keyword.cloud_notm}} catalog. Use the cost estimation tool to understand pricing for your specific requirements.

1. Navigate to the {{site.data.keyword.cloud_notm}} catalog and locate the **Fusion as a Service** tile.

2. Click **Estimate Cost** to access the cost estimation tool.

3. For Compute billing:
   - Select the number of Red Hat OpenShift clusters you plan to deploy
   - Choose cluster size (number of worker nodes)
   - Specify GPU requirements if needed
   - Select subscription term

4. For Storage billing:
   - Select the **Storage Tier**: **Performance** or **Capacity**
   - Enter the **Total storage** capacity in TB
   - Choose **Subscription term**: 3, 4, or 5 years

   The cost estimator will display your projected monthly costs based on your selections.

5. Review your estimated costs and save your configuration for reference.

The hardware includes optimized racks, servers, storage, networking switches, and integrated software that connects to {{site.data.keyword.cloud_notm}}. IBM owns and maintains the hardware, and the service infrastructure is installed in your designated data center.
{: note}

## Requesting consultation
{: #consultation-request}
{: step}

After reviewing your cost estimation, the next step is to connect with IBM experts to discuss your specific requirements.

1. Click **Start order process** in the cost estimation tool.

2. Complete the consultation request form with your contact details and requirements:
   - Organization information
   - Desired billing options (Compute, Storage, or both)
   - Estimated capacity needs
   - Timeline for deployment
   - Any specific compliance or regulatory requirements

3. Submit the form to generate a **Confirmation ID**.

4. You will receive:
   - On-screen confirmation with your consultation ID
   - Email confirmation with your cost estimation details
   - Notification sent to IBM sales team

5. An IBM representative will contact you within 1-2 business days. 

After discussions and approvals, the IBM representative will place your order. You will receive order details and a tracking link via email. Track your order status from your {{site.data.keyword.cloud_notm}} account dashboard.

## Preparing your deployment
{: #prepare-deployment}
{: step}

After your order is processed, you will receive an email with a **Prepare deployment** link from your IBM representative. This link directs you to the deployment dashboard where you can configure your deployment settings.

### Access the deployment dashboard
{: #access-deployment-dashboard}

1. Check your email for the **Prepare deployment** link from your IBM representative.
2. Click the link to access the deployment dashboard.
3. The dashboard displays your orders with deployment preparation status.

### Configure deployment settings
{: #configure-deployment}

1. Click **Prepare deployment** from your order.

2. The **Prepare deployment** side panel opens. Configure the following settings:

   **Satellite location**
   
   To begin configuring your deployment, select an IBM Cloud Satellite location and name your deployment. You can create and manage your satellite locations in IBM Cloud Satellite.
   
   - **Satellite location**: Select an existing Satellite location from the dropdown
     - The Satellite location connects your on-premises infrastructure to {{site.data.keyword.cloud_notm}}
     - To create a new location, you must first create it in [IBM Cloud Satellite](https://cloud.ibm.com/satellite/locations){: external}

   **Deployment details**
   
   - **Name**: Enter a descriptive name for your deployment
   
   - **Resource group**: Select the resource group for organizing your deployment resources
     - You can view all resource groups or create a new resource group

3. Click **Create** to complete the deployment preparation, or click **Cancel** to close the panel without saving.

4. After you create the deployment, your **Deployment preparation** status changes to **Completed**.


## Next steps
{: #next-steps}

Now that you understand FusionaaS and have initiated your deployment:

Learn more
:   Read [What is Fusion as a Service?](/docs/cephaas?topic=cephaas-about-fusionaas) for detailed information.

Prepare your environment
:   Review [data center prerequisites](/docs/cephaas?topic=cephaas-pre_installation_checklist).

Complete deployment setup
:   After hardware installation, see [Onboarding to your Fusion as a Service deployment](/docs/cephaas?topic=cephaas-onboarding-fusionaas).

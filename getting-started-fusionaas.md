---

copyright:
 years: 2024, 2026
lastupdated: "2026-04-29"

keywords: fusion as a service, getting started, fusionaas, openshift, compute, storage, billing options, roks clusters, ceph storage, performance tier, capacity tier

subcollection: fusionaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

An IBM representative will contact you to understand your requirements. Post discussions and approvals, your IBM representative will place your order. While the order is processing, you can track the status from your {{site.data.keyword.cloud_notm}} account dashboard.
{: important}

# Getting started with Fusion as a Service
{: #getting-started}

Fusion as a Service (FusionaaS) is IBM's fully managed OpenShift platform delivered on-premises with cloud-like consumption and operational models. It allows you to self-service provision OpenShift clusters, deploy applications, and consume storage services with cloud-like elasticity and a pay-for-what-you-use model—all while maintaining data sovereignty in your own data center.
{: shortdesc}

This tutorial guides you through understanding FusionaaS capabilities, estimating costs, and getting started with your deployment. Estimated completion time: **10 minutes**.

## What is Fusion as a Service?
{: #what-is-fusionaas}

FusionaaS combines the power of Red Hat OpenShift with IBM's enterprise-grade infrastructure management, delivered as a fully managed service in your data center. IBM owns, operates, and maintains the hardware while you focus on deploying and managing your applications.

### Key benefits
{: #key-benefits}

- **Fully managed OpenShift on-premises**: IBM Site Reliability Engineering (SRE) teams handle installation, configuration, monitoring, patching, upgrades, and day-to-day operations.
- **Cloud consumption pricing**: Pay only for what you use with metered usage and flexible monthly commitments—no large upfront capital expenditures.
- **IBM SRE-led lifecycle management**: 24x7 monitoring, proactive maintenance, rapid incident response, and coordinated platform updates.
- **Enterprise-grade security, resiliency, and observability**: Multi-layered security controls, redundant components, automated failover, and comprehensive monitoring.
- **GPU-enabled workloads**: Support for AI, machine learning, data analytics, and high-performance computing with GPU acceleration.

### How it works
{: #how-it-works}

With FusionaaS, IBM delivers, installs, and operates infrastructure in your data center:

1. **IBM-owned infrastructure**: IBM provides optimized racks, servers, storage, networking switches, and integrated software that connects to {{site.data.keyword.cloud_notm}}.
2. **Fully managed operations**: IBM handles all operational complexity while you retain physical control of your data.
3. **Self-service provisioning**: Provision OpenShift clusters and storage through familiar {{site.data.keyword.cloud_notm}} interfaces and APIs.
4. **Flexible scaling**: Scale resources on-demand without procurement delays.

## Understanding billing options
{: #billing-options}
{: step}

FusionaaS offers flexible billing options based on your workload requirements. You can select either **Compute** or **Storage** services, or both, depending on your needs.

### Compute billing option
{: #compute-billing}

The **Compute** option enables you to provision and manage Red Hat OpenShift on IBM Cloud (ROKS) clusters in your on-premises environment.

**What you get:**
- Fully managed OpenShift clusters with IBM SRE support
- Self-service cluster provisioning through {{site.data.keyword.cloud_notm}} console
- Automated lifecycle management (upgrades, patching, monitoring)
- GPU support for AI and data-intensive workloads
- Pay-per-use pricing based on compute resources consumed

**Ideal for:**
- Organizations modernizing applications with containers
- Teams running AI/ML workloads requiring GPU acceleration
- Businesses needing OpenShift expertise without in-house management overhead

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

**Ideal for:**
- Organizations needing flexible, scalable storage
- Businesses eliminating over-provisioning and right-sizing infrastructure
- Teams requiring unified storage across multiple protocols

### Combining Compute and Storage
{: #combined-billing}

You can select both Compute and Storage options to create a complete on-premises cloud platform:
- Deploy containerized applications on managed OpenShift clusters
- Consume high-performance or capacity storage as needed
- Benefit from integrated management and unified billing
- Scale compute and storage independently based on workload demands

## Estimating service cost
{: #estimatecost}
{: step}

FusionaaS is available in the {{site.data.keyword.cloud_notm}} catalog. Use the cost estimation tool to understand pricing for your specific requirements.

1. Navigate to the {{site.data.keyword.cloud_notm}} catalog and locate the **Fusion as a Service** tile.

2. Click **Estimate Cost** to access the cost estimation tool.

3. **For Compute billing**:
   - Select the number of OpenShift clusters you plan to deploy
   - Choose cluster size (number of worker nodes)
   - Specify GPU requirements if needed
   - Select subscription term (monthly commitment options available)

4. **For Storage billing**:
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

5. An IBM representative will contact you within 1-2 business days to:
   - Understand your detailed requirements
   - Discuss technical specifications
   - Review data center prerequisites
   - Answer questions about the service
   - Provide a customized proposal

After discussions and approvals, the IBM representative will place your order. You will receive order details and a tracking link via email. Track your order status from your {{site.data.keyword.cloud_notm}} account dashboard.

## Preparing your deployment
{: #prepare-deployment}
{: step}

Once your order is confirmed, prepare for FusionaaS deployment in your data center.

### Create or select a Satellite location
{: #satellite-location}

FusionaaS requires an {{site.data.keyword.satellitelong_notm}} location to connect your on-premises infrastructure to {{site.data.keyword.cloud_notm}}.

1. **Select an existing location** or **create a new on-premises Satellite location**:
   - Open the [Satellite console](https://cloud.ibm.com/satellite/locations/create/onPrem){: external}
   - Choose an on-premises location type
   - Name your Satellite location

2. **Important configuration requirements**:
   - The Satellite location must be present on {{site.data.keyword.cloud_notm}} without hosts initially
   - The location is not dependent on hosts or other infrastructure setup at this stage
   - Select **Managed from** region as **Dallas** or **Frankfurt** (choose the region closest to your data center for optimal network latency)
   - For Storage billing option, choose Object Storage standard plan

The Satellite location serves as the connection point between your on-premises FusionaaS deployment and {{site.data.keyword.cloud_notm}} management services.
{: tip}

### Review data center prerequisites
{: #datacenter-prereqs}

Before IBM installs the FusionaaS infrastructure, ensure your data center meets the physical requirements:

- **Power requirements**: Adequate electrical capacity and redundancy
- **Cooling**: Sufficient HVAC capacity for rack-mounted equipment
- **Space**: Floor space for rack installation with proper clearances
- **Network connectivity**: Physical network connections to {{site.data.keyword.cloud_notm}}
- **Physical security**: Secure facility access controls

For detailed requirements, see [Prerequisites for installing FusionaaS](/docs/fusionaas?topic=fusionaas-pre_installation_checklist).

### Create your deployment
{: #create-deployment}

After your Satellite location is configured and your data center is ready:

1. Work with your IBM representative to schedule installation
2. IBM will coordinate the delivery and installation of hardware
3. Once installed, you can begin provisioning resources:
   - **For Compute**: Create OpenShift clusters through the {{site.data.keyword.cloud_notm}} console
   - **For Storage**: Provision storage volumes and configure storage classes

For detailed instructions on creating deployments, see [Managing deployments](/docs/fusionaas?topic=fusionaas-administrators).

## Infrastructure setup and maintenance
{: #setup-maintenance}
{: step}

After your order is placed and infrastructure is ready for installation, IBM manages the complete lifecycle:

### IBM responsibilities
{: #ibm-responsibilities}

- **Installation**: IBM installs and configures all hardware and software in your data center
- **Configuration**: Initial setup of OpenShift clusters and storage infrastructure
- **Operations**: 24x7 monitoring, incident response, and performance management
- **Maintenance**: Hardware and software updates, security patches, and upgrades
- **Support**: Enterprise-grade support with defined SLAs

### Your responsibilities
{: #customer-responsibilities}

- **Physical site requirements**: Provide adequate power, cooling, space, and network connectivity
- **Facility access**: Grant IBM personnel access for installation and maintenance
- **Application management**: Deploy, configure, and manage your applications and workloads
- **Data management**: Manage your data, backups, and disaster recovery strategies

IBM owns and operates the infrastructure while you provision and manage your workloads. This shared responsibility model allows you to focus on applications while IBM handles infrastructure complexity.
{: note}

## Next steps
{: #next-steps}

Now that you understand FusionaaS and have initiated your deployment:

- **Learn more**: Read [What is Fusion as a Service?](/docs/fusionaas?topic=fusionaas-about-fusionaas) for detailed information
- **Prepare your environment**: Review [data center prerequisites](/docs/fusionaas?topic=fusionaas-pre_installation_checklist)
- **Plan your deployment**: Understand [deployment management](/docs/fusionaas?topic=fusionaas-administrators)
- **Explore capabilities**: Learn about [IBM Cloud Satellite](/docs/satellite?topic=satellite-getting-started)

For questions or assistance, contact your IBM representative or open a support case through the {{site.data.keyword.cloud_notm}} console.

---

copyright:
 years: 2024, 2026
lastupdated: "2026-06-17"

keywords: fusion as a service, getting started, fusionaas, openshift, compute, storage, billing options, roks clusters, ceph storage, performance tier, capacity tier

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

An IBM representative will contact you to understand your requirements. Post discussions and approvals, your IBM representative will place your order. While the order is processing, you can track the status from your {{site.data.keyword.cloud_notm}} account dashboard.
{: important}

# Getting started with IBM Fusion as a service
{: #getting-started}

IBM Fusion as a service (FusionaaS) is IBM's fully managed Red Hat OpenShift on IBM Cloud Satellite platform delivered on-premises with cloud-like consumption and operational models. It allows you to self-service provision Red Hat OpenShift clusters, deploy applications, and consume storage services with cloud-like elasticity and a pay-for-what-you-use model—all while maintaining data sovereignty in your own data center.
{: shortdesc}

This topic guides you through understanding FusionaaS capabilities, estimating costs, and getting started with your deployment.

## What is IBM Fusion as a service?
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

FusionaaS offers flexible billing options based on your workload requirements. You can select either **Compute** or **Storage** infrastructure, or both, depending on your needs.

### Infrastructure options
{: #infrastructure-options}

Select the type of infrastructure you want to include in your deployment:

Compute
:   For managing compute resources such as vCPUs, memory, GPUs, and cluster deployments. Enables you to provision and manage Red Hat OpenShift on IBM Cloud Satellite clusters in your on-premises environment with fully managed IBM SRE support, self-service cluster provisioning, automated lifecycle management, and GPU support for AI and data-intensive workloads.

Storage
:   For managing block, file, and object storage capacity across your workloads. Provides access to IBM Storage Ceph as a Service with performance tiers optimized for your specific requirements, supporting multiple protocols and self-provisioning capabilities.

You can select both Compute and Storage options to create a complete on-premises cloud platform with integrated management and unified billing.

### Subscription term
{: #subscription-term}

You can save more with a longer subscription term. FusionaaS offers the following subscription term options:

- **3 years**: Standard subscription term
- **4 years**: Extended subscription with cost savings
- **5 years**: Maximum subscription term with optimal cost savings

Longer subscription terms provide better pricing and help you plan your infrastructure costs over an extended period.

## Requesting consultation
{: #consultation-request}
{: step}

FusionaaS is available in the {{site.data.keyword.cloud_notm}} catalog. To get started, you need to request a consultation with IBM experts to discuss your specific requirements and receive customized pricing.

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
   - **3 years**: Standard subscription term
   - **4 years**: Extended subscription with cost savings
   - **5 years**: Maximum subscription term with optimal cost savings

4. For Compute infrastructure:
   - Select from recommended configurations or customize your deployment
   - Choose AI solutions (Integrated AI, Data Lakehouse) or Application platform options
   - Specify vCPUs, memory, GPUs, and usable storage capacity
   - Configure availability zones based on your requirements

5. For Storage infrastructure:
   - Select the storage tier: **Performance** or **Capacity**
   - Enter the total storage capacity in TB
   - Performance tier: 100 TB to 800 TB
   - Capacity tier: 800 TB to 3,200 TB

6. Click **Get consultation** to submit your configuration and request a consultation.

7. Complete the consultation request form with your contact details and requirements:
   - Organization information
   - Desired billing options (Compute, Storage, or both)
   - Estimated capacity needs
   - Timeline for deployment
   - Any specific compliance or regulatory requirements

8. Submit the form to generate a **Confirmation ID**.

9. You will receive:
   - On-screen confirmation with your consultation ID
   - Email confirmation with your configuration details
   - Notification sent to IBM sales team

10. An IBM representative will contact you within 1-2 business days to discuss pricing and next steps.

After discussions and approvals, the IBM representative will provide detailed pricing and place your order. You will receive order details and a tracking link via email. Track your order status from your {{site.data.keyword.cloud_notm}} account dashboard.

The hardware includes optimized racks, servers, storage, networking switches, and integrated software that connects to {{site.data.keyword.cloud_notm}}. IBM owns and maintains the hardware, and the service infrastructure is installed in your designated data center.
{: note}

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
:   Read [What is IBM Fusion as a service?](/docs/cephaas?topic=cephaas-about-fusionaas) for detailed information.

Prepare your environment
:   Review [data center prerequisites](/docs/cephaas?topic=cephaas-pre_installation_checklist).

Complete deployment setup
:   After hardware installation, see [Onboarding to your IBM Fusion as a service deployment](/docs/cephaas?topic=cephaas-onboarding-fusionaas).

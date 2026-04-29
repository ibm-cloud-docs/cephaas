---

copyright:
 years: 2024, 2026
lastupdated: "2026-04-29"

keywords: fusion as a service, fusionaas, fully managed openshift, on-premises, cloud consumption pricing, ibm sre, gpu workloads, ai workloads

subcollection: fusionaas

---
{{site.data.keyword.attribute-definition-list}}


# What is Fusion as a Service?
{: #about-fusionaas}

Fusion as a Service (FusionaaS) is IBM's fully managed OpenShift platform delivered on-premises with cloud-like consumption and operational models. It combines the power of Red Hat OpenShift with IBM's enterprise-grade infrastructure management, allowing you to run containerized workloads in your own data center while benefiting from cloud economics and IBM Site Reliability Engineering (SRE) expertise.
{: shortdesc}

FusionaaS extends the IBM Fusion experience to a fully IBM-managed service that allows you to self-service provision OpenShift clusters, deploy applications, and consume storage and data services with cloud-like elasticity and a pay-for-what-you-use model—all while maintaining data sovereignty and meeting regulatory requirements for on-premises deployment.

## How Fusion as a Service works
{: #how-fusionaas-works}

With FusionaaS, IBM delivers, installs, and operates OpenShift infrastructure in your data center. You retain physical control of your data and infrastructure while IBM handles the operational complexity:

- **IBM-owned infrastructure**: IBM provides and maintains the hardware, including optimized racks, servers, storage, networking switches, and integrated software that connects to {{site.data.keyword.cloud_notm}}.
- **Fully managed operations**: IBM SRE teams handle installation, configuration, monitoring, patching, upgrades, and day-to-day operations of the platform.
- **Self-service provisioning**: You provision OpenShift clusters, deploy workloads, and manage applications through familiar {{site.data.keyword.cloud_notm}} interfaces and APIs.
- **Cloud consumption model**: Pay only for the resources you consume with metered usage and flexible monthly commitments, eliminating large upfront capital expenditures.

## Key capabilities
{: #fusionaas-capabilities}

### Fully managed OpenShift on-premises
{: #managed-openshift}

FusionaaS delivers a complete Red Hat OpenShift Container Platform experience in your data center, fully managed by IBM. This includes:

- **Automated lifecycle management**: IBM SRE teams handle cluster provisioning, upgrades, patching, and maintenance with minimal disruption to your workloads.
- **High availability**: Built-in redundancy and failover capabilities ensure your applications remain available.
- **Integrated monitoring**: Comprehensive observability with built-in monitoring, logging, and alerting managed by IBM.
- **Security hardening**: Enterprise-grade security configurations and compliance controls applied and maintained by IBM security experts.

### Cloud consumption pricing
{: #cloud-pricing}

FusionaaS eliminates traditional infrastructure procurement cycles with flexible, consumption-based pricing:

- **Pay-as-you-grow**: Start with the capacity you need today and scale as your requirements evolve.
- **Metered usage**: Transparent metering tracks your actual resource consumption (compute, storage, network).
- **Monthly commitments**: Flexible commitment terms that align with your business planning cycles.
- **No over-provisioning**: Right-size your infrastructure and avoid the waste of traditional capacity planning.
- **Predictable costs**: Clear pricing models help you forecast and manage infrastructure spending.

### IBM SRE-led lifecycle management
{: #sre-management}

IBM's Site Reliability Engineering teams bring deep expertise in managing mission-critical infrastructure:

- **24x7 monitoring**: Continuous monitoring of infrastructure health, performance, and security.
- **Proactive maintenance**: Scheduled maintenance windows with advance notification and minimal impact.
- **Incident response**: Rapid response to issues with defined service level objectives (SLOs).
- **Capacity planning**: IBM monitors usage trends and works with you to plan capacity expansions.
- **Platform updates**: Coordinated upgrades to OpenShift, Kubernetes, and underlying infrastructure components.

### Enterprise-grade security, resiliency, and observability
{: #enterprise-features}

FusionaaS is built on IBM's decades of experience delivering enterprise infrastructure:

- **Security**: Multi-layered security controls including network isolation, encryption at rest and in transit, identity and access management integration, and compliance with industry standards.
- **Resiliency**: Redundant components, automated failover, backup and disaster recovery capabilities, and business continuity planning.
- **Observability**: Comprehensive monitoring and logging with integration to {{site.data.keyword.cloud_notm}} observability services, custom dashboards, and alerting.

### GPU-enabled workloads for AI and data-intensive use cases
{: #gpu-workloads}

FusionaaS supports GPU-accelerated computing for demanding workloads:

- **AI and machine learning**: Train and deploy machine learning models with GPU acceleration.
- **Data analytics**: Process large datasets with GPU-accelerated analytics frameworks.
- **High-performance computing**: Run compute-intensive simulations and modeling workloads.
- **Flexible GPU options**: Choose from various GPU configurations to match your workload requirements.

## Comparing FusionaaS to traditional on-premises deployments
{: #fusionaas-comparison}

| Aspect | Traditional On-Premises | Fusion as a Service |
|--------|------------------------|---------------------|
| **Capital investment** | Large upfront hardware purchase | No upfront capital expenditure |
| **Operational model** | Self-managed infrastructure | Fully IBM-managed |
| **Scaling** | Requires procurement cycles | Scale on-demand with cloud-like flexibility |
| **Lifecycle management** | Internal IT team responsibility | IBM SRE-led management |
| **Pricing** | Fixed capacity costs | Pay-for-what-you-use metering |
| **Time to value** | Weeks to months for deployment | Rapid provisioning after installation |
| **Expertise required** | Deep OpenShift and infrastructure skills | Focus on applications, not infrastructure |
| **Updates and patches** | Manual planning and execution | Automated by IBM with minimal disruption |

## Is Fusion as a Service right for you?
{: #fusionaas-use-cases}

FusionaaS is ideal for organizations that need:

- **Data sovereignty**: Keep data on-premises to meet regulatory, compliance, or data residency requirements while gaining cloud operational benefits.
- **Hybrid cloud strategy**: Extend your {{site.data.keyword.cloud_notm}} footprint into your data center with consistent management and APIs.
- **Reduced operational burden**: Offload infrastructure management to IBM while maintaining control over applications and data.
- **Predictable performance**: Dedicated infrastructure in your data center with guaranteed resources and low-latency access.
- **AI and GPU workloads**: Run GPU-accelerated workloads on-premises with enterprise support and management.
- **Cost optimization**: Eliminate over-provisioning and align infrastructure costs with actual usage.

Consider FusionaaS if you:
- Need OpenShift on-premises but lack the expertise or resources to manage it
- Want to modernize applications with containers while keeping data on-premises
- Require enterprise-grade SLAs and support for mission-critical workloads
- Seek to reduce capital expenditures and move to an operational expense model
- Need to scale infrastructure dynamically without procurement delays

## Getting started with Fusion as a Service
{: #fusionaas-next-steps}

To begin your FusionaaS journey:

1. **Estimate costs**: Use the cost estimation tool in the {{site.data.keyword.cloud_notm}} catalog to understand pricing for your requirements.
2. **Request consultation**: Submit a consultation request to discuss your specific needs with IBM experts.
3. **Prepare your data center**: Review the [prerequisites for installing FusionaaS](/docs/fusionaas?topic=fusionaas-pre_installation_checklist) to ensure your facility meets requirements.
4. **Deploy**: Work with IBM to install and configure FusionaaS in your data center.

For detailed information on getting started, see [Getting started with Fusion as a Service](/docs/fusionaas?topic=fusionaas-getting-started).

## Related information
{: #fusionaas-related}

- [Getting started with Fusion as a Service](/docs/fusionaas?topic=fusionaas-getting-started)
- [Preparing your data center](/docs/fusionaas?topic=fusionaas-pre_installation_checklist)
- [Managing deployments](/docs/fusionaas?topic=fusionaas-administrators)
- [IBM Cloud Satellite](/docs/satellite?topic=satellite-getting-started)

---

copyright:
 years: 2024, 2026
lastupdated: "2026-06-02"

keywords: gpu, graphics processing unit, gpu availability, nvidia h100, worker node, openshift virtualization, gpu workloads, high availability

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# GPU availability and distribution
{: #gpu-availability}

GPU resources in your Fusion as a Service deployment determine how GPU-enabled workloads are scheduled and managed. Understanding GPU availability patterns and distribution options helps you design workloads that can handle maintenance windows and potential hardware events.
{: shortdesc}

## Available GPU types
{: #gpu-types}

The GPU types and quantities available in your Fusion as a Service deployment depend on your specific deployment configuration. GPU availability must be determined at order time as part of your initial deployment planning. Contact your IBM representative to discuss the GPU options available for your deployment.

## GPU ordering and configuration
{: #gpu-ordering}

GPU resources must be specified at order time when you initially configure your Fusion as a Service deployment. You cannot add GPU resources to an existing deployment after it has been provisioned. When planning your deployment, consider the following:

- The number of GPUs required for your workloads
- Whether you need GPUs distributed across multiple worker nodes for high availability
- Your workload resiliency and availability requirements
- Expected growth in GPU-dependent applications

Contact your IBM representative to discuss your GPU requirements. Your IBM representative can help you:

- Determine the appropriate number and type of GPUs for your workloads
- Plan GPU distribution across worker nodes to meet your availability requirements
- Design a configuration that balances performance, availability, and cost
- Understand the implications of different GPU distribution strategies

## GPU scheduling and availability patterns
{: #gpu-scheduling-availability}

GPU resource distribution affects workload scheduling and availability in the following ways:

GPU-backed OpenShift Virtualization VMs are scheduled only on nodes with available GPU capacity
:   Virtual machines that require GPU resources can only be placed on nodes that have GPUs available. If all GPU capacity is allocated, new GPU requests cannot be fulfilled.

Additional GPU requests remain in a pending state until capacity becomes available
:   When GPU resources are fully allocated, any new workloads that request GPU access will remain unscheduled until existing workloads are terminated or GPU capacity is freed.

GPU workloads are temporarily unavailable during node maintenance or failures
:   During node maintenance, upgrades, or failures, GPU workloads hosted on the affected node become temporarily unavailable until the node returns to service. This can impact workload availability and business continuity.

To minimize the impact of node maintenance or failures, deploy your GPU workloads following high availability best practices. Containerized GPU workloads should be deployed in a highly available manner with multiple replicas distributed across available GPU nodes. This ensures that your applications remain available even when individual nodes are unavailable.
{: note}

## GPU distribution strategies
{: #gpu-distribution-strategies}

To support higher availability and workload resiliency, consider distributing GPUs across multiple worker nodes during your initial deployment planning. This enables better workload placement flexibility and reduces the impact of node-level events.

Distributing GPUs across multiple nodes provides the following benefits:

- Improved workload scheduling flexibility with more placement options
- Reduced impact of node maintenance or failures on GPU workloads
- Better resource utilization across the cluster
- Enhanced high availability for GPU-dependent applications

Work with your IBM representative during the ordering process to plan a GPU distribution strategy that aligns with your availability and resiliency requirements.

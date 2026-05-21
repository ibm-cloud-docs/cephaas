---

copyright:
 years: 2024, 2026
lastupdated: "2026-05-21"

keywords: gpu, graphics processing unit, gpu availability, nvidia h100, worker node, openshift virtualization, gpu workloads, high availability

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# GPU availability and distribution
{: #gpu-availability}

In the current Fusion as a Service deployment, GPU resources may be concentrated on a single worker node. For example, both NVIDIA H100 GPUs in rack F40 are hosted on the same node. This reflects the current hardware distribution and determines how GPU-enabled workloads are scheduled and managed.
{: shortdesc}

## Behavior and impact
{: #gpu-behavior-impact}

The concentration of GPU resources on a single node affects workload scheduling and availability in the following ways:

GPU-backed OpenShift Virtualization VMs are scheduled only on nodes with available GPU capacity
:   Virtual machines that require GPU resources can only be placed on nodes that have GPUs available. If all GPU capacity is allocated, new GPU requests cannot be fulfilled.

Additional GPU requests remain in a pending state until capacity becomes available
:   When GPU resources are fully allocated, any new workloads that request GPU access will remain unscheduled until existing workloads are terminated or GPU capacity is freed.

Live migration of GPU-enabled VMs requires additional GPU-capable nodes
:   Without multiple GPU-capable nodes, live migration of GPU-enabled virtual machines is not possible. Workloads remain on the hosting node and cannot be moved to another node without downtime.

GPU workloads are temporarily unavailable during node maintenance or failures
:   During node maintenance, upgrades, or failures, GPU workloads hosted on the affected node become temporarily unavailable until the node returns to service. This can impact workload availability and business continuity.

## Design consideration
{: #gpu-design-consideration}

To support higher availability and workload resiliency, GPUs should be distributed across multiple worker nodes. This enables better workload placement flexibility and reduces the impact of node-level events.

Distributing GPUs across multiple nodes provides the following benefits:

- Improved workload scheduling flexibility with more placement options
- Support for live migration of GPU-enabled virtual machines
- Reduced impact of node maintenance or failures on GPU workloads
- Better resource utilization across the cluster
- Enhanced high availability for GPU-dependent applications

Contact your IBM representative to discuss GPU distribution options and plan for a configuration that meets your availability and resiliency requirements.

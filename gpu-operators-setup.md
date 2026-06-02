---

copyright:
  years: 2026
lastupdated: "2026-06-02"

keywords: gpu operators, nfd operator, nvidia gpu operator, node feature discovery, gpu setup, satellite roks, openshift gpu configuration

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Setting up GPU operators
{: #gpu-operators-setup}

Configure your Fusion as a Service Satellite ROKS cluster to support GPU workloads by installing the Node Feature Discovery (NFD) Operator and NVIDIA GPU Operator. These operators enable GPU resource discovery, driver management, and workload scheduling on GPU-enabled nodes.
{: shortdesc}

## Before you begin
{: #gpu-operators-prereqs}

Before installing GPU operators, ensure you have:

- A Fusion as a Service Satellite ROKS cluster with GPU-enabled worker nodes
- Cluster administrator access to install operators
- Network connectivity to Red Hat OperatorHub and NVIDIA container registries
- Reviewed [GPU availability and distribution](/docs/cephaas?topic=cephaas-gpu-availability) in your deployment
- Verified OpenShift version compatibility with GPU operators

For detailed prerequisites, see [Deploying GPU workloads on Satellite ROKS clusters](/docs/cephaas?topic=cephaas-gpu-workloads-overview).

## Installation overview
{: #gpu-operators-installation-overview}

The GPU operator installation process follows these steps:

1. Install the Node Feature Discovery (NFD) Operator to detect GPU hardware
2. Install the NVIDIA GPU Operator to manage GPU drivers and runtime components
3. Verify that GPU resources are available to the cluster
4. Deploy GPU-accelerated workloads

The installation process is the same for Fusion as a Service Satellite ROKS clusters as it is for IBM Cloud ROKS clusters. Follow the IBM Cloud ROKS documentation for detailed installation instructions.

## Installing GPU operators
{: #gpu-operators-install}

To install the Node Feature Discovery Operator and NVIDIA GPU Operator on your Satellite ROKS cluster, follow the comprehensive installation guide in the IBM Cloud ROKS documentation:

[Deploying an app on a GPU machine](https://cloud.ibm.com/docs/openshift?topic=openshift-deploy_app&interface=ui#gpu_app){: external}

This guide provides:
- Step-by-step instructions for installing the NFD Operator from OperatorHub
- Detailed steps for installing the NVIDIA GPU Operator
- Configuration guidance for GPU operator settings
- Verification procedures to confirm GPU resources are available
- Sample application deployment examples

The installation process uses the OpenShift web console or CLI to install operators from OperatorHub, which is the standard method for adding operators to OpenShift clusters.
{: note}

## Fusion as a Service considerations
{: #fusionaas-gpu-considerations}

When setting up GPU operators on Fusion as a Service Satellite ROKS clusters, consider the following:

### GPU distribution and availability
{: #gpu-distribution-considerations}

GPU distribution across worker nodes affects workload scheduling and high availability. Review [GPU availability and distribution](/docs/cephaas?topic=cephaas-gpu-availability) to understand:

- How GPU resources are distributed in your deployment
- Impact on workload scheduling and placement
- Considerations for live migration of GPU-enabled virtual machines
- Effects of node maintenance on GPU workload availability

Contact your IBM representative to discuss GPU distribution options that meet your requirements.

### Network connectivity
{: #network-connectivity-considerations}

Your Satellite ROKS cluster must have network connectivity to:

- Red Hat OperatorHub to download operator images
- NVIDIA container registries to download GPU drivers and CUDA runtime
- IBM Cloud services through the Satellite Link connection

Ensure that your network configuration allows outbound connectivity to these services. If you have network restrictions, work with your network team to allow access to required registries.

### Operator updates and maintenance
{: #operator-maintenance-considerations}

GPU operators require periodic updates to support new GPU hardware, OpenShift versions, and security patches. IBM SRE teams manage the underlying infrastructure, but you are responsible for:

- Monitoring operator updates in OperatorHub
- Planning and executing operator upgrades
- Testing operator updates in non-production environments before production deployment
- Reviewing operator release notes for breaking changes or new features

Operator versions and compatibility requirements may change with new OpenShift releases. Always verify compatibility before upgrading operators.
{: important}

## Verifying GPU resources
{: #gpu-verify-resources}

After installing the GPU operators, verify that GPU resources are available to your cluster.

### Using the OpenShift web console
{: #verify-console}

1. Log in to the OpenShift web console for your cluster
2. Navigate to **Compute** > **Nodes**
3. Select a GPU-enabled worker node
4. Review the **Details** tab to confirm GPU resources are listed
5. Check the **Allocatable** section for available GPU capacity

### Using the CLI
{: #verify-cli}

Run the following command to list nodes with GPU resources:

```sh
oc get nodes -o json | jq '.items[] | select(.status.capacity."nvidia.com/gpu" != null) | {name: .metadata.name, gpus: .status.capacity."nvidia.com/gpu"}'
```
{: pre}

This command displays nodes that have NVIDIA GPUs and shows the number of GPUs available on each node.

You can also describe a specific node to see detailed GPU information:

```sh
oc describe node <node-name>
```
{: pre}

Look for `nvidia.com/gpu` in the **Capacity** and **Allocatable** sections of the output.

## Deploying GPU workloads
{: #gpu-deploy-workloads}

After verifying GPU resources, you can deploy GPU-accelerated workloads on your cluster.

### Requesting GPU resources in pods
{: #gpu-request-pods}

To deploy a pod that uses GPU resources, specify the GPU resource request in your pod specification:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: gpu-pod
spec:
  containers:
  - name: gpu-container
    image: nvidia/cuda:11.0-base
    resources:
      limits:
        nvidia.com/gpu: 1
```
{: codeblock}

The `nvidia.com/gpu` resource limit specifies the number of GPUs the pod requires. The OpenShift scheduler places the pod on a node with available GPU capacity.

### Deploying GPU-enabled virtual machines
{: #gpu-vm-deployment}

If you use OpenShift Virtualization, you can create virtual machines with GPU passthrough. GPU-enabled VMs require:

- GPU resources specified in the VM definition
- Appropriate node placement to ensure the VM runs on a GPU-enabled node
- Consideration of GPU distribution for high availability and live migration

For detailed guidance on deploying GPU workloads, including additional examples and best practices, see the [IBM Cloud ROKS GPU documentation](https://cloud.ibm.com/docs/openshift?topic=openshift-deploy_app&interface=ui#gpu_app){: external}.

## Troubleshooting GPU operators
{: #gpu-troubleshooting}

If you encounter issues with GPU operators or GPU workloads, review the following troubleshooting steps.

### GPU resources not appearing
{: #troubleshoot-no-gpu}

If GPU resources do not appear after installing operators:

1. Verify that the NFD Operator is running:
   ```sh
   oc get pods -n openshift-nfd
   ```
   {: pre}

2. Check NFD Operator logs for errors:
   ```sh
   oc logs -n openshift-nfd -l app=nfd-master
   ```
   {: pre}

3. Verify that the NVIDIA GPU Operator is running:
   ```sh
   oc get pods -n nvidia-gpu-operator
   ```
   {: pre}

4. Check GPU Operator logs for errors:
   ```sh
   oc logs -n nvidia-gpu-operator -l app=nvidia-driver-daemonset
   ```
   {: pre}

5. Confirm that GPU hardware is present on worker nodes by checking node labels:
   ```sh
   oc get nodes --show-labels | grep gpu
   ```
   {: pre}

### Pods not scheduling on GPU nodes
{: #troubleshoot-scheduling}

If pods requesting GPU resources remain in pending state:

1. Check if GPU capacity is available:
   ```sh
   oc describe node <gpu-node-name> | grep -A 5 "Allocated resources"
   ```
   {: pre}

2. Verify that the pod's GPU resource request matches available GPU types
3. Review pod events for scheduling errors:
   ```sh
   oc describe pod <pod-name>
   ```
   {: pre}

4. Ensure that GPU-enabled nodes are in Ready state and not cordoned

### Driver installation failures
{: #troubleshoot-drivers}

If NVIDIA GPU drivers fail to install:

1. Check GPU Operator pod status:
   ```sh
   oc get pods -n nvidia-gpu-operator
   ```
   {: pre}

2. Review driver installation logs:
   ```sh
   oc logs -n nvidia-gpu-operator <nvidia-driver-pod-name>
   ```
   {: pre}

3. Verify network connectivity to NVIDIA container registries
4. Check for kernel compatibility issues in the logs
5. Ensure that the GPU Operator version is compatible with your OpenShift version

For additional troubleshooting guidance, see the [NVIDIA GPU Operator troubleshooting documentation](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/troubleshooting.html){: external}.

## Advanced GPU configurations
{: #gpu-advanced-config}

For advanced GPU configurations and features, refer to the following resources:

### Multi-Instance GPU (MIG)
{: #gpu-mig-config}

NVIDIA Multi-Instance GPU (MIG) allows you to partition a single GPU into multiple isolated GPU instances. This feature is useful for maximizing GPU utilization and running multiple workloads on a single GPU.

For MIG configuration guidance, see [Configuring Multi-Instance GPU (MIG)](https://www.ibm.com/docs/en/fusion-hci-systems/2.12.x?topic=cas-configuring-multi-instance-gpu-mig){: external} in the Fusion HCI documentation.

### Customizing Node Feature Discovery
{: #gpu-nfd-custom}

You can customize the Node Feature Discovery Operator to detect specific hardware features or apply custom labels to nodes.

For NFD customization guidance, see [Customizing the Node Feature Discovery (NFD) CR](https://www.ibm.com/docs/en/fusion-hci-systems/2.12.x?topic=racks-customizing-node-feature-discovery-nfd-cr){: external} in the Fusion HCI documentation.

### GPU driver upgrades
{: #gpu-driver-upgrades}

The NVIDIA GPU Operator manages GPU driver versions. To upgrade GPU drivers, you typically update the GPU Operator configuration or upgrade the operator itself.

For driver upgrade guidance, see [Upgrading the NVIDIA GPU driver with the NVIDIA GPU Operator](https://www.ibm.com/docs/en/fusion-hci-systems/2.12.x?topic=racks-upgrading-nvidia-gpu-driver-nvidia-gpu-operator){: external} in the Fusion HCI documentation.

## Next steps
{: #gpu-operators-next-steps}

After setting up GPU operators:

1. Deploy GPU-accelerated applications on your cluster
2. Monitor GPU resource utilization and performance
3. Plan for operator updates and maintenance
4. Review GPU workload best practices in the [NVIDIA GPU Operator documentation](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html){: external}

## Related information
{: #gpu-operators-related}

- [Deploying GPU workloads on Satellite ROKS clusters](/docs/cephaas?topic=cephaas-gpu-workloads-overview)
- [GPU availability and distribution](/docs/cephaas?topic=cephaas-gpu-availability)
- [Deploying an app on a GPU machine (IBM Cloud ROKS)](https://cloud.ibm.com/docs/openshift?topic=openshift-deploy_app&interface=ui#gpu_app){: external}
- [NVIDIA GPU Operator documentation](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html){: external}
- [Node Feature Discovery Operator documentation](https://docs.openshift.com/container-platform/latest/hardware_enablement/psap-node-feature-discovery-operator.html){: external}

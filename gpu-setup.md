---

copyright:
  years: 2026
lastupdated: "2026-06-08"

keywords: gpu operators, nfd operator, nvidia gpu operator, node feature discovery, gpu setup, satellite roks, openshift gpu configuration

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Using GPUs in your clusters
{: #fusionaas-using-gpus}

Fusion as a Service (FusionaaS) supports running GPU-enabled workloads on Red Hat OpenShift on IBM Cloud Satellite (ROKS) clusters that are created in your deployment. GPU-enabled clusters allow you to accelerate compute-intensive workloads such as AI, machine learning, and data processing.
{: shortdesc}

## About GPU workloads in FusionaaS
{: #about-gpu-workloads}

In FusionaaS:

- GPU support is available through **GPU-enabled worker nodes** in your Red Hat OpenShift clusters.
- GPU capacity is limited by the resources available in your deployment.
- Clusters are created in the **IBM Cloud console** and managed through the **Red Hat OpenShift web console**.
- You are responsible for enabling GPU support within the cluster and deploying GPU workloads.

## Before you begin
{: #gpu-prereqs}

Ensure that:

- Your cluster is created with **GPU-enabled worker nodes**.
- You have sufficient available **GPU capacity** in your deployment.
- You have the required permissions to manage cluster resources and deploy workloads.

## Enable GPU support in your cluster
{: #enable-gpu-support}

To run GPU workloads, you must install and configure the required operators in your cluster, such as:

- **Node Feature Discovery (NFD) Operator**
- **NVIDIA GPU Operator** (or equivalent operators for your GPU hardware)

FusionaaS does not manage these operators. You must install them in your cluster by following the Red Hat OpenShift and IBM Cloud documentation.

For instructions, see [Deploying an app on a GPU machine](/docs/openshift?topic=openshift-deploy_app&interface=ui#gpu_app).

In the preceding topic:
- Follow the "Deploying an app on an NVIDIA GPU machine" section
- Use the link to install the Node Feature Discovery (NFD) and NVIDIA GPU operators for your cluster version

Operator installation and configuration depend on the Red Hat OpenShift version of your cluster. Always follow the documentation that matches your cluster version.
{: important}

## Deploy GPU workloads
{: #deploy-gpu-workloads}

After you enable GPU support in your cluster, you can deploy workloads that request GPU resources.

For example, GPU workloads must specify the GPU resource limit in the workload configuration:

```yaml
resources:
  limits:
    nvidia.com/gpu: 1
```
{: codeblock}

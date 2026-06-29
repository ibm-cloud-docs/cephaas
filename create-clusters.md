---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-29"

keywords: cluster creation, IBM Fusion as a service, Red Hat OpenShift on IBM Cloud, IBM Cloud Satellite, GPU workloads

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating clusters
{: #create-clusters}

Create Red Hat OpenShift clusters on IBM Cloud for your IBM Fusion as a service deployment by using IBM Cloud Satellite. Cluster creation, deletion, and compute configuration are performed through Red Hat OpenShift on IBM Cloud, not through the IBM Fusion as a service UI.
{: shortdesc}

Cluster creation is not supported in the IBM Fusion as a service UI. You must use Red Hat OpenShift on IBM Cloud (ROKS) to create, update, and delete clusters.
{: important}

Make sure that you meet the following prerequisites for cluster creation:

- You have access to a IBM Fusion as a service deployment in your IBM Cloud account.
- You have the required IAM permissions to create and manage clusters.
- Your deployment shows available compute, storage, and optional GPU capacity.
- Your Satellite location and IBM Fusion as a service control plane are already set up.

## Understanding Fusion vs Red Hat OpenShift responsibilities
{: #fusion-vs-roks}

IBM Fusion as a service and Red Hat OpenShift on IBM Cloud have distinct responsibilities for cluster management:

### IBM Fusion as a service UI capabilities
{: #fusion-capabilities}

The IBM Fusion as a service UI provides the following capabilities:

- View clusters and monitor resource usage (CPU, GPU, storage)
- Enable Fusion services for clusters (storage, backup, and restore)
- Manage storage quotas (default and per-cluster)
- Monitor cluster health and status

### Red Hat OpenShift capabilities
{: #roks-capabilities}

Red Hat OpenShift on IBM Cloud provides the following capabilities:

- Create, update, and delete clusters
- Configure compute resources (worker nodes, workloads)
- Manage cluster-level operations
- Configure cluster settings and policies

Only users with Administrator or Editor roles in IBM Cloud IAM can create clusters.
{: note}

### Managed components
{: #managed-components}

IBM Fusion as a service and IBM Cloud manage the following components:

Satellite control plane
:   IBM manages the Satellite control plane.

Red Hat OpenShift on IBM Cloud control plane
:   IBM manages the cluster control plane, upgrades, patching, and platform health.

Fusion HCI infrastructure
:   Worker nodes run on the underlying Fusion HCI infrastructure that supports your deployment.

### Your responsibilities
{: #your-responsibilities}

You need to manage the following components:

Applications and workloads
:   You deploy and manage the applications and services that run in the cluster.

Namespaces and access control
:   You manage namespaces, users, and role-based access control (RBAC) within the cluster.

Resource consumption
:   You manage how your applications use compute, storage, and GPU resources within your allocated quotas.

## Create a cluster through Red Hat OpenShift console
{: #create-a-cluster}

Cluster creation must be performed through Red Hat OpenShift on IBM Cloud. The IBM Fusion as a service UI provides visibility into cluster status and resource usage but does not support cluster creation operations.

1. Log in to the {{site.data.keyword.cloud_notm}} console.
2. Navigate to **Containers** > **Clusters** in the IBM Cloud console.
3. Click **Create cluster**.
4. Select **Red Hat OpenShift** as the cluster type.
5. Select **Satellite** as the infrastructure.
6. Follow the detailed steps in [Creating Red Hat OpenShift on IBM Cloud clusters in Satellite](/docs/openshift?topic=openshift-satellite-clusters&interface=ui).

During cluster configuration, ensure you select the Satellite location associated with your IBM Fusion as a service deployment.
{: tip}

## Configure cluster details
{: #configure-cluster-details}

In the Satellite cluster wizard, specify the required configuration for your cluster, such as the following details:

- Cluster name
- Red Hat OpenShift version
- Number of worker nodes
- vCPU and memory per node
- Optional GPU-enabled worker nodes
- Storage quota for the cluster, based on available Fusion Data Foundation capacity

IBM Fusion as a service validates your selections against the available deployment capacity.

### Specify GPU-enabled worker nodes
{: $specify-gpu-enabled-worker-nodes}

Add GPU-enabled worker nodes to your default worker pool by using host labels:

- In the **Default Worker Pool** section specify ibm-gpu and the number of GPU nodes per region in the **Default worker pool host label** field. For example, "ibm-gpu:1"

The specified value for ibm-gpu represents the number of GPU nodes per zone.
{: tip}


## Review and create the cluster
{: #review-and-create-cluster}

1. Review the cluster configuration.
2. Click **Create** to start provisioning.

After the cluster is created, it appears alongside your other Red Hat OpenShift on IBM Cloud clusters in IBM Cloud.

## After the cluster is created
{: #after-cluster-creation}

After the cluster becomes available in ROKS, it appears in your IBM Fusion as a service deployment. You can then complete the following tasks:

In the IBM Fusion as a service UI
:   - View the cluster in your deployment's cluster list
    - Monitor cluster health and resource usage
    - Enable Fusion services for the cluster
    - Manage storage quotas

In Red Hat OpenShift on IBM Cloud
:   - Configure cluster settings and policies
    - Manage worker nodes and compute resources
    - Update or delete the cluster

In the OpenShift console
:   - Deploy applications and services
    - Manage workloads and namespaces
    - Configure application-level settings

## Related tasks
{: #create-clusters-related}

- [Viewing the cluster list](/docs/cephaas?topic=cephaas-view-cluster-list)
- [Viewing cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)
- [Managing the default cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota)
- [Monitoring cluster health](/docs/cephaas?topic=cephaas-monitor-cluster-health)

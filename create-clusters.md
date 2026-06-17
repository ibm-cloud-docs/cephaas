---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-17"

keywords: cluster creation, IBM Fusion as a service, Red Hat OpenShift on IBM Cloud, IBM Cloud Satellite, GPU workloads

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating clusters
{: #create-clusters}

Create Red Hat OpenShift clusters on IBM Cloud for your IBM Fusion as a service deployment by using IBM Cloud Satellite.
{: shortdesc}

Make sure that you meet the following prerequisites for cluster creation:

- You have access to a IBM Fusion as a service deployment in your IBM Cloud account.
- You have the required IAM permissions to create and manage clusters.
- Your deployment shows available compute, storage, and optional GPU capacity.
- Your Satellite location and IBM Fusion as a service control plane are already set up.

## How cluster creation works
{: #how-cluster-creation-works}

When you create a cluster in IBM Fusion as a service, the cluster is created as a Red Hat OpenShift on IBM Cloud cluster on Satellite in your IBM Cloud account.

IBM Fusion as a service and IBM Cloud manage the following components:

Satellite control plane
:   IBM manages the Satellite control plane.

Red Hat OpenShift on IBM Cloud control plane
:   IBM manages the cluster control plane, upgrades, patching, and platform health.

Fusion HCI infrastructure
:   Worker nodes run on the underlying Fusion HCI infrastructure that supports your deployment.

You need to manage the following components in the cluster:

Applications and workloads
:   You deploy and manage the applications and services that run in the cluster.

Namespaces and access control
:   You manage namespaces, users, and role-based access control (RBAC) within the cluster.

Resource consumption
:   You manage how your applications use compute, storage, and GPU resources within your allocated quotas.

## Create a cluster
{: #create-a-cluster}

Use the IBM Cloud console to start cluster creation from your IBM Fusion as a service deployment. The deployment dashboard surfaces capacity, quotas, and status information, while cluster creation is completed in the Red Hat OpenShift on IBM Cloud Satellite workflow.

1. Log in to the {{site.data.keyword.cloud_notm}} console.
2. Open your IBM Fusion as a service deployment from the **Resource list**.
3. From the deployment dashboard, click **Cluster management** > **Clusters**.

The **Clusters** page shows Name, State, Location, Worker count, Created date, Version, and Infrastructure. 

4. Click **Create cluster**.
5. When prompted, choose the option to create the cluster through the Red Hat OpenShift on IBM Cloud Satellite portal.
6. In the Red Hat OpenShift on IBM Cloud Satellite workflow, follow the detailed steps in [Creating Red Hat OpenShift on IBM Cloud clusters in Satellite](/docs/openshift?topic=openshift-satellite-clusters&interface=ui).

The service redirects you to the standard IBM Cloud workflow for creating Satellite clusters.

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

## Review and create the cluster
{: #review-and-create-cluster}

1. Review the cluster configuration.
2. Click **Create** to start provisioning.

After the cluster is created, it appears alongside your other Red Hat OpenShift on IBM Cloud clusters in IBM Cloud.

## After the cluster is created
{: #after-cluster-creation}

After the cluster becomes available, you can complete the following tasks:

- Access the cluster from the OpenShift web console.
- Deploy applications and services as you would for any Red Hat OpenShift on IBM Cloud cluster.
- View health, capacity, and alerts from the IBM Fusion as a service dashboard.
- Enable and use Fusion services, if needed.

## Related tasks
{: #create-clusters-related}

- [Viewing the cluster list](/docs/cephaas?topic=cephaas-view-cluster-list)
- [Viewing cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)
- [Managing the default cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota)
- [Monitoring cluster health](/docs/cephaas?topic=cephaas-monitor-cluster-health)

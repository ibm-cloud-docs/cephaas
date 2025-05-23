---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-19"

keywords: ceph as a service, Managing hosts, vsphere plug-in, cephaas

subcollection: cephaas

---


{{site.data.keyword.attribute-definition-list}}

# Managing hosts in vSphere plug-in
{: #managing-hosts-vsphere-plug-in}

## Viewing host connections
{: #view-host-connection}

For viewing existing host connections, perform the following procedure.

1. Log in to the vSphere client.
2. Navigate to **Inventory** > **Datacenter** > **Cluster** > **Host** > **Configure** tab > **IBM Storage CephaaS** > **Host Connectivity**.
3. Deployments connected to the host are displayed with fields **Deployment Name**, **Deployment Status**, and **Added to deployment**.
3. You can click double-headed arrow icon besides the deployment name to see the host details.


## Adding a new host
{: #add-host}

Use the following procedure to add a host to your deployment.

1. From the vSphere client screen, navigate to **Inventory** > **Datacenter** > **Cluster** > **Host** > **Configure** tab > **IBM Storage CephaaS** > **Host Connectivity**.

2. Select the deployment in which you want to add the host and click **ADD HOST**.

    **Add Host** screen is displayed.

3. Enter values in the fields **Host Name**. Enter the host name to add ESXi host.

    The `host nqn` is fetched automatically. If the network configuration is incorrect and not connected, the auto fetch of `host nqn` will not occur. In that case, you can either enter the `nqn` manually or fix the network configuration settings.
    {: note}

4. Click **Add**.

5. Clicking the arrow besides the deployment name shows the details of the added host.


## Editing host details
{: #edit-host-details}

For editing host details of a deployment, use the following procedure.

1. From the vSphere client screen, navigate to **Inventory** > **Datacenter** > **Cluster** > **Host** > **Configure** tab > **IBM Storage CephaaS** > **Host Connectivity**.

2. Select the deployment that contains the Host you need to edit and click the pencil icon.

    **Edit Host Details** screen is desplayed.

3. Enter a new host name and click **Update**.

## Deleting a host
{: #delete-host}

For deleting a host from a deployment, perform the following procedure.

1. From the vSphere client screen, navigate to **Inventory** > **Datacenter** > **Cluster** > **Host** > **Configure** tab > **IBM Storage CephaaS** > **Host Connectivity**.

2. Select the deployment that contains the Host you need to delete and click the delete icon.

    A confirmation pop-up is displayed about removal of the host.

4. Click **Delete**.

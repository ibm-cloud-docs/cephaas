---
copyright:
 years: 2024, 2024
lastupdated: "2024-10-17"

keywords: Managing hosts, vsphere plug-in, cephaas

subcollection: cephaas
--- 


{{site.data.keyword.attribute-definition-list}}

# Managing hosts in vSphere plug-in
{: #managing-hosts-vsphere-plug-in}

## Viewing host connections
{: #view-host-connection}

For viewing existing host connections, perform the following procedure.

1. Login to the vSphere client.
2. Navigate to **Inventory** > **CephaaS** > **Cluster** > **Configure** tab > **Host Connectivity**.
3. Deployments connected to the host are displayed with fields **Deployment Name**, **Deployment Status**, and **Added to deployment**. 
3. You can click double-headed arrow icon besides the deployment name to see the host details. 


## Adding a new host
{: #add-host}

Use the following procedure to add a host to your deployment.

1. From the vSphere Client screen, navigate to **Inventory** > **CephaaS** > **Cluster** > **Configure** tab > **Host Connectivity**.
2. Click **Add Host**. 
3. **Add Host** screen is displayed. 
4. Enter values in the fields **Host Name** and **Host nqn**. 
5. Click **Add**.
6. Clicking on the arrow besides the deployment name will show details of the added host.


## Editing host details
{: #edit-host-details}

For editing host details of a deployment, use the following procedure.

1. From the vSphere Client screen, navigate to **Inventory** > **CephaaS** > **Cluster** > **Configure** tab > **Host Connectivity**.
2. Select the deployment which contains the Host you need to edit and click the pencil icon.
2. **Edit Host Details** screen is desplayed.
3. Enter a new host name and click **Update**.

## Deleting a host
{: #delete-host}

For deleting a host from a deployment, perform the following procedure.

1. From the vSphere Client screen, navigate to **Inventory** > **CephaaS** > **Cluster** > **Configure** tab > **Host Connectivity**.
2. Select the deployment which contains the Host you need to delete and click the delete icon.
3. A confirmation pop-up is displayed about removal of the host.
4. Click **Remove**.

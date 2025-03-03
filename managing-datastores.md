---
copyright:
 years: 2024, 2025
lastupdated: "2025-03-03"

keywords: managing datastores in vsphere plug-in

subcollection: cephaas
---


{{site.data.keyword.attribute-definition-list}}

# Managing datastores in vSphere plug-in
{: #managing-datastores-vsphere-plug-in}

## Adding a datastore
{: #add-datastore}

Use the following procedure to add an {{site.data.keyword.cephaas_full_notm}} datastore to the vSphere Plug-in.

1. Login to the vSphere client.
2. From the vSphere client dashboard left pane, select the vSphere Cluster that requires new datastores, and navigate to **Actions** > **{{site.data.keyword.cephaas_full_notm}}** > **Create VMFS Datastore**.
3. Select **Deployment** where the datastore needs to be created and click **Next**.
4. Select Hosts to be mapped to your Datastore and click **Next**. You can map a maximum of 32 hosts to the datastore.
5. Select at least one NVMe **Host Adapter** for your datastore and click **Next**.
6. **Define Datastore** screen is displayed where you need to enter **Name** and **Size** of the datastore.
7. Click **Next**. **Review** screen is displayed which lists details entered for the new datastore.
8. Check the datastore details and click **Create**.


## Expanding datastore
{: #expand-datastore}

This task initiates a workflow that increases the available capacity of the selected VMFS datastore.

1. From the vSphere client dashboard left pane, select your vSphere Cluster.
2. Click datastore icon in the top pane.
3. Select the datastore you wish to expand in the left pane and click on **Actions** > **IBM Storage Cephaas from the menu**.
4. From the submenu, select **Expand VMFS Datastore**.
5. Expand VMFS datastore screen is displayed with values **Volume Name**, **Current Total Capacity**, **Expand by**, and **Datastore Capacity Usage** bar.
6. Enter a value to increase the datastore by, select the appropriate unit, for example, TB or GB.
7. Review the Datastore Capacity Usage bar to visualize the updated capacity.
8. Click **Expand**.
9. Your datastore dashboard will reflect the increased capacity.


## Deleting a datastore
{: #delete-datastore}

For deleting a datastore, perform the following procedure.

1. In the datastore dashboard, select the VMFS datastore that needs to be deleted from the left pane. Datastore summary page is displayed in the right pane.
2. Navigate to **Actions** > **{{site.data.keyword.cephaas_full_notm}}** submenu, select **Delete VMFS Datastore**.
3. Review the confirmation pop up and click **Delete**.

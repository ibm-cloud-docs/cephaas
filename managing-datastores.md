---
copyright:
 years: 2024, 2024
lastupdated: "2024-10-04"

keywords: managing datastores in vsphere plug-in

subcollection: sdsaas
---


{{site.data.keyword.attribute-definition-list}}

# Managing Datastores in vSphere plug-in

## Adding a datastore

Use the following procedure to add an IBM Ceph as a Service datastore to the vSphere Plugin.

1. Login to the vSphere client. 
2. From the vSphere Client, select the vSphere Cluster that requires new datastores, and navigate to **Actions** > **IBM Storage Ceph as a Service**.
3. From the plug-in submenu, select **Create VMFS datastore**.
4. Select Deployment where the datastore needs to be created and click **Next**. 
5. Select Hosts to be added to your Datastore and click **Next**. 
   You can add a maximum of 32 hosts to the datastore. 
6. Select at least one NVMe Adapter for your datastore and click **Next**. 
7. Define Datastore screen is displayed where you need to enter name and size of the datastore.
8. Click **Next**. 
9. Review screen is displayed which lists details entered for the new datastore. 
10. Check the datastore details and click **Create**. 


## Expanding datastore

This task initiates a workflow that increases the available capacity of the selected VMFS datastore.

1. From the vSphere Client, select the vSphere Cluster that requires expqnsion of datastore, and click **Actions** > **IBM Storage**. 
2. From the IBM Storage submenu, select **Expand VMFS datastore**.
3. Enter a value to increase the datastore by, select the appropriate unit, for example, TB or GB.
4. Review the capacity consumption bar to visualize the updated projected consumption.
5. Click **Expand**.


## Deleting a datastore

For deleting a Datastore, perform the following procedure. 

1. Select the VMFS datastore that needs to be removed from the datastore dashboard. 
2. From the IBM Storage submenu, select **Delete VMFS datastore**.
3. Review the summary panel and click Delete.

 







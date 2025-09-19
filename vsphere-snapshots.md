---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, managing snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing snapshots in vSphere
{: #managing-snapshots-vsphere}

## Viewing existing snapshots
{: #viewing-snapshots-vsphere}

To monitor and manage your datastore snapshots effectively, you can access snapshot details from the vSphere client UI. The following steps guide you through navigating the dashboard to locate and view snapshot information—such as snapshot count and used capacity—for a selected datastore.

1. From the vSphere client dashboard left pane, select vSphere Cluster.
2. Click the main breadcrumb of the dashboard and select **IBM Storage Ceph as a Service**. 
3. Click Storage icon in the top horizontal pane. The existing datastores are displayed. 
4. Select the datastore of which you wish to view snapshots.
5. The **Summary** tab displays **Datastore Details** which included the Snapshot information. 
6. In the **Datastore Details** tab, you can view  **Snapshot count** and **Snapshot used capacity** fields. 
7. Select **Configure** tab and click **Datastore Snapshots** to view the snapshot details. 


## Taking snapshot of a datastore
{: #taking-snapshots-vsphere}

You can create snapshots of your existing datastore to capture a point-in-time backup of your data. This is useful for preserving the current state of your datastore before making changes or performing maintenance. Follow the steps below to take a snapshot using the vSphere client interface.

1. From the vSphere client dashboard left pane, select vSphere Cluster.
2. Click the main breadcrumb of the dashboard and select **IBM Storage Ceph as a Service**. 
3. Click Storage icon in the top horizontal pane. The existing datastores are displayed. 
4. Select the datastore in which you wish to create snapshots. 
5. Navigate to **Configure** tab and click **TAKE SNAPSHOT**. 
6. Enter Snapshot Name and click **TAKE SNAPSHOT**. A default name is auto-generated, including the timestamp of creation. You have the option to use it or enter a custom name.
7. Once the snapshot is created, its details will appear under the **Configure** tab.

## Editing a snapshot
{: #renaming-snapshots-vsphere}

You can rename an existing snapshot of your datastore to better reflect its purpose or context. Renaming helps maintain clarity in snapshot management, especially when dealing with multiple restore points. Follow the steps below to update the name of a snapshot using the vSphere client interface.

1. From the vSphere client dashboard left pane, select vSphere Cluster.
2. Click the main breadcrumb of the dashboard and select **IBM Storage Ceph as a Service**. 
3. Click Storage icon in the top horizontal pane. The existing datastores are displayed. 
4. Select the datastore in which you wish to create snapshots. 
3. Select the snapshot from the datastore from which you wish to rename.
4. Enter the new Snapshot Name and click **UPDATE**.

## Deleting a snapshot
{: #deleting-snapshots-vsphere}

You can delete an existing snapshot of your datastore when it is no longer needed, helping to free up storage and maintain a clean snapshot inventory. The following steps guide you through locating and removing a snapshot using the vSphere client interface.

1. From the vSphere client dashboard left pane, select vSphere Cluster.
2. Click the main breadcrumb of the dashboard and select **IBM Storage Ceph as a Service**. 
3. Click Storage icon in the top horizontal pane. The existing datastores are displayed. 
4. Select the datastore in which you wish to create snapshots. 
5. Navigate to **Configure** tab and select the snapshot you want to delete. 
5. Click delete icon on the horizontal pane and click **DELETE** in the conformational modal. 
6. The **Configure** tab will no longer list the deleted snapshot. 

## Creating a new datastore from a snapshot
{: #creating-datastore-from-snapshot}

Snapshots enable you to restore datastores from the point in time it was taken. The newly created datastores will be mapped to the same hosts as the original datastore.

1. From the vSphere client dashboard left pane, select vSphere Cluster.
2. Click the main breadcrumb of the dashboard and select **IBM Storage Ceph as a Service**. 
3. Click Storage icon in the top horizontal pane. The existing datastores are displayed. 
4. Select the datastore in which you wish to create snapshots. 
5. Navigate to **Configure** tab and select the snapshot you want to create a snapshot from. 
6. Click copy icon from the horizontal pane. 
7. Select Hosts to be mapped to your Datastore and click **Next**. 
8. Select at least one NVMe **Host Adapter** for your datastore and click **Next**.
9. **Define Datastore** screen is displayed where you need to enter **Name** and **Size** of the datastore.
10. Click **Next**. **Review** screen is displayed which lists details entered for the new datastore.
11. Check the datastore details and click **Create**.
12. Enter name of the new datastore in the **Create New Datastore from Snapshot** screen.
13. Click **CREATE**.

You can view **Recent Tasks** tab in the lower section of the vSphere client interface to see details of recent operations.
{: note}

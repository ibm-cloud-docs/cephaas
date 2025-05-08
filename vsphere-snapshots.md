---

copyright:
 years: 2024, 2025
lastupdated: "2025-05-08"

keywords: cephaas, managing snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing snapshots in vSphere
{: #managing-snapshots-vsphere}

## Taking snapshot of a datastore
{: #taking-snapshots-vsphere}

You can take snapshots of your existing datastore which will be point-in-time backup of your data as follows:

1. From the vSphere client dashboard left pane, select your vSphere Cluster.
2. Click datastore icon in the top pane.
3. Select the datastore from which you wish to create a snapshot.
4. Click **TAKE SNAPSHOT** button.
5. Enter Snapshot Name and click **TAKE SNAPSHOT**.

## Renaming a snapshot
{: #renaming-snapshots-vsphere}

You can rename snapshot of your existing datastore as follows:

1. From the vSphere client dashboard left pane, select your vSphere Cluster.
2. Click datastore icon in the top pane.
3. Select the snapshot from the datastore from which you wish to rename.
4. Enter the new Snapshot Name and click **UPDATE**.

## Deleting a snapshot
{: #deleting-snapshots-vsphere}

You can delete snapshot of your existing datastore as follows:

1. From the vSphere client dashboard left pane, select your vSphere Cluster.
2. Click datastore icon in the top pane.
3. Select the snapshot from the datastore from which you wish to delete.
4. Click **DELETE**. The confirmation modal is displayed.
5. If you wish to proceed with deletion, click **DELETE**.

## Creating a new datastore from a snapshot
{: #creating-datastore-from-snapshot}

Snapshots enable you to restore datastores from the point in time it was taken. The newly created datastores will be mapped to the same hosts as the original datastore.

1. From the vSphere client dashboard left pane, select your vSphere Cluster.
2. Click datastore icon in the top pane.
3. Select the snapshot from the datastore from which you wish to clone.
4. Enter name of the new datastore in the **Create New Datastore from Snapshot** screen.
5. Click **CREATE**.

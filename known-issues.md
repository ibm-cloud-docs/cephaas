---

copyright:
 years: 2024, 2025
lastupdated: "2025-11-27"

keywords: ceph as a service, known issues

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Known issues
{: #knownissues}

## Snapshot size display limitation for large sets
{: #snapshotlimitation}

When the number of snapshots exceeds 100, the total snapshot size shown in the **Volume Details** view may be inaccurate. 


## PVC expansion failure scenario - CSI Driver
{: #pvclimitation}

When a Persistent Volume Claim (PVC) expansion request exceeds the available storage capacity, such as going beyond 32TB or exceeding the assigned block storage quota, OpenShift does not allow the PVC to be resized to a smaller, valid size. To recover and use the available space, you need to create a snapshot of the existing PVC. After that, restore the snapshot into a new PVC and specify a size that fits within the current storage limits.

## PVC deletion with existing snapshots - CSI Driver
{: #pvcdeletionlimitation}

If a PVC is deleted while snapshots still exist, the associated PV and storage volume are retained to avoid data loss. This makes the volume unusable but still consumes space.
To fix this, either delete all related VolumeSnapshots to trigger automatic cleanup, or reuse the PV by removing its claimRef and creating a new PVC that binds to it.

## Snapshot deletion timeout in CLI
{: #snapshotdeletiontimeoutissue}

Snapshot deletion via CLI may fail with a 504 Gateway Time-out error, even though the operation completes successfully. This is caused by a short client timeout in the SDK. 


## Placeholder values for datastore and snapshot sizes
{: #placeholder-values-ds}

There are known inconsistencies in how size values are displayed and validated in the vSphere plug-in UI when working with datastores and snapshots.

### Datastore size placeholder
{: #ds-size-placeholder}

On the **Create New Datastore From Snapshot** page, the **Size** field in the **Define Datastore** step displays a placeholder value representing the minimum required size for the new datastore. However, if the size exceeds 1024 GB, the value is converted to terabytes (TB) using a binary conversion (divided by 1024 and rounded to two decimal places). 

**Workaround**: If the entered size is below the actual minimum required size, the UI may allow the input to pass validation. However, the datastore restore operation will fail. To avoid this, ensure that the entered size is equal to or greater than the minimum required size.

### Snapshot size display
{: #snapshot-size}

On the **Snapshots List Dashboard**, the **Size** column reflects the snapshot size. Similar to the datastore size, values greater than 1024 GB are converted to TB using binary conversion (divided by 1024), which may result in a slightly lower displayed value compared to the actual snapshot size. There is no workaround for this discrepancy. 

---

copyright:
 years: 2024, 2026
lastupdated: "2026-08-18"

keywords: ceph as a service, known issues

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Known issues
{: #knownissues}

## Snapshot display limitation for sets larger than 100
{: #snapshotlimitation}

When the number of snapshots exceeds 100, the total snapshot capacity shown in the **Volume Details** view may be inaccurate.


## PVC expansion failure scenario - CSI Driver
{: #pvclimitation}

When a Persistent Volume Claim (PVC) expansion request exceeds the available storage capacity, such as going beyond 32TB or exceeding the assigned block storage quota, OpenShift does not allow the PVC to be resized to a valid, smaller capacity. To recover and use the available space, you need to create a snapshot of the existing PVC. After that, restore the snapshot into a new PVC and specify a capacity that fits within the current storage limits.

## PVC deletion with existing snapshots - CSI Driver
{: #pvcdeletionlimitation}

If a PVC is deleted while snapshots still exist, the associated PV and storage volume are retained to avoid data loss. This makes the volume unusable but still consumes space.
To fix this, either delete all related VolumeSnapshots to trigger automatic cleanup, or reuse the PV by removing its claimRef and creating a new PVC that binds to it.

## Snapshot deletion timeout in CLI
{: #snapshotdeletiontimeoutissue}

Snapshot deletion via CLI may fail with a 504 Gateway Time-out error, even though the operation completes successfully. This is caused by a short client timeout in the SDK. 


## Placeholder values for datastore and snapshot sizes
{: #placeholder-values-ds}

There are known inconsistencies in how capacity values are displayed and validated in the vSphere plug-in UI when working with datastores and snapshots.

### Datastore capacity placeholder
{: #ds-size-placeholder}

On the **Create New Datastore From Snapshot** page, the **Size** field in the **Define Datastore** step displays a placeholder value representing the minimum required capacity for the new datastore. However, if the capacity exceeds 1024 GB, the value is converted to terabytes (TB) using a binary conversion (divided by 1024 and rounded to two decimal places).

**Workaround**: If the entered capacity is below the actual minimum required capacity, the UI may allow the input to pass validation. However, the datastore restore operation will fail. To avoid this, ensure that the entered capacity is equal to or greater than the minimum required capacity.

### Snapshot capacity display
{: #snapshot-size}

On the **Snapshots List Dashboard**, the **Size** column reflects the snapshot capacity. Similar to the datastore capacity, values greater than 1024 GB are converted to TB using binary conversion (divided by 1024), which may result in a slightly lower displayed value compared to the actual snapshot capacity. There is no workaround for this discrepancy.

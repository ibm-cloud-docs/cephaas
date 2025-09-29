---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-29"

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

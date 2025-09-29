---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-29"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Static provisioning
{: #static-provision}

Static provisioning allows you to manually create and manage PersistentVolumes (PVs), PersistentVolumeClaims (PVCs), and snapshots. This method is useful when you want to bind existing storage resources to Kubernetes workloads. 

## Static provisioning for volumes
{: #static-provision-volumes}

In static volume provisioning, both the PV and PVC must be created manually. Ensure that the storage size specified in both resources matches the actual size of the underlying volume.

* Create a PersistentVolume (PV) by creating a file named pv.yaml with the following content.

```sh
    apiVersion: v1
    kind: PersistentVolume
    metadata:
    name: pv-static
    spec:
    capacity:
        storage: 2G
    accessModes:
        - ReadWriteOnce
    volumeMode: Filesystem
    persistentVolumeReclaimPolicy: Delete
    storageClassName: cephaascsi-sc
    csi:
    controllerExpandSecretRef:
    name: cephaascsi-secret
    namespace: default
    controllerPublishSecretRef:
    name: cephaascsi-secret
    namespace: default
    driver: csi.cephaas.io
    fsType: ext4
    volumeHandle: r134-e20564d0-2aea-4992-ae07-b4a06e23e139
```
{: pre}

* Create a PersistentVolumeClaim (PVC) by creating a file named pvc.yaml with the following content.

```sh
 apiVersion: v1
 kind: PersistentVolumeClaim
 metadata:
 name: pvc-static
 spec:
 accessModes:
 - ReadWriteOnce
 resources:
 requests:
 storage: 2G
 storageClassName: cephaascsi-sc
 volumeName: pv-static
```
{: pre}


A storage class is required for delete and expand operations to work correctly.
{: note}

Once the PV and PVC are created, you can use them in pod configurations just like dynamically provisioned volumes.


## Static provisioning for snapshots
{: #static-provision-snapshots}

Static snapshot provisioning allows you to manually bind existing snapshot resources to Kubernetes workloads. In this method, both the VolumeSnapshot (VS) and VolumeSnapshotContent (VSC) must be created manually and must reference each other.

**Key considerations**: 

* Both VS and VSC must be created manually.
* The VolumeSnapshotContent must reference the underlying snapshot handle.
* The VolumeSnapshot must reference the corresponding VolumeSnapshotContent.
* After setup, snapshot-based restore operations work the same as in dynamic provisioning.

    1. Create a file named volumesnapshot.yaml with the following content.

```sh
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshot
metadata:
  name: volumesnapshot-static
  namespace: default
spec:
  source:
    volumeSnapshotContentName: volume-snapshot-content-static
```
{: pre}

This resource defines the snapshot and links it to the corresponding VolumeSnapshotContent.

2. Create a file named volumesnapshotcontent.yaml with the following content. 

```sh
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshotContent
metadata:
  name: volume-snapshot-content-static
  annotations:
   	snapshot.storage.kubernetes.io/deletion-secret-name: cephaascsi-secret
  	snapshot.storage.kubernetes.io/deletion-secret-namespace: default
spec:
  deletionPolicy: Delete
  driver: csi.cephaas.io
  source:
    snapshotHandle: r134-bbcfe9bc-b863-4495-8b11-86382c27f2eb
  volumeSnapshotRef:
    name: volumesnapshot-static
    namespace: default
```
{: pre}

Once both resources are created and linked, you can restore the snapshot into a PVC using the standard restore procedure. Pod creation and volume mounting work the same as with dynamically provisioned snapshots.

## Known limitation
{: #csi-knownlimitation}

**Volume size in statically provisioned Persistent Volumes (PVs) may differ from the actual volume size on the storage or deployment**

In static provisioning, the administrator manually provisions storage and creates a PV manifest that references this storage. OpenShift uses the `spec.capacity.storage` field in the PV manifest as metadata to represent the volume size.
Since static provisioning bypasses the CSI driver’s CreateVolume gRPC call—which is used in dynamic provisioning to create the volume and ensure the `spec.capacity.storage` matches the actual size on RSOS—there is no built-in validation to confirm that the declared capacity aligns with the real backend volume size.
If the PV size specified in the manifest differs from the actual volume size on the deployment, pods will only be able to use and see the actual volume size, not the declared size in the manifest.

**Suggestion**

To avoid discrepancies between OpenShift’s metadata and the actual storage behavior, we recommend setting the PV’s `spec.capacity.storage` to match the actual size of the underlying storage. This ensures consistency, accurate scheduling, and prevents OpenShift from under-reporting or over-reporting capacity relative to what pods can actually consume.

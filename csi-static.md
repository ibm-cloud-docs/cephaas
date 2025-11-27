---

copyright:
 years: 2024, 2025
lastupdated: "2025-11-27"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Static provisioning
{: #static-provision}


Static provisioning is a method where PersistentVolumes (PVs) and VolumeSnapshotContents (VSCs) are manually created to reference existing volumes or snapshots on the storage system managed by the CSI driver. When a user creates a PersistentVolumeClaim (PVC) or VolumeSnapshot (VS) that matches the specifications of a pre-created PV or VSC, Kubernetes binds the claim to that resource.
This approach is useful when you need to connect existing storage resources to Kubernetes workloads.

## Static provisioning for volumes
{: #static-provision-volumes}

In static volume provisioning, both the PV and PVC must be created manually. Ensure that the storage size specified in both resources matches the actual size of the underlying volume.

* Create a PersistentVolume (PV) by creating a file named **pv.yaml** with the following content.

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
        volumeHandle: <Volume_ID>
 ```
{: codeblock}

Replace the VolumeHandle value with the actual Volume ID of the pre-provisioned volume.

* Create a PersistentVolumeClaim (PVC) by creating a file named **pvc.yaml** with the following content.

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
{: codeblock}

In the pvc.yaml file, you can use the volumeName field to explicitly bind the PVC to a specific PersistentVolume (PV).
Replace the placeholder with the actual PV name if you want to implement this binding. This step is optional. 

A storage class is required for delete and expand operations to work correctly.
{: note}

The names of PersistentVolumes (PV) and PersistentVolumeClaims (PVC) are editable and can be customized.
{: note}

Once the PV and PVC are created, you can use them in pod configurations just like dynamically provisioned volumes.


## Static provisioning for snapshots
{: #static-provision-snapshots}

Static snapshot provisioning allows you to manually bind existing snapshot resources to Kubernetes workloads. In this method, both the VolumeSnapshot (VS) and VolumeSnapshotContent (VSC) must be created manually and must refer each other.

**Key considerations**: 

* Both VS and VSC must be created manually.
* The VolumeSnapshotContent must refer the underlying snapshot handle.
* The VolumeSnapshot must refer the corresponding VolumeSnapshotContent.
* After setup, snapshot-based restore operations work the same as in dynamic provisioning.

Create a file named **volumesnapshot.yaml** with the following content.


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
{: codeblock}


This resource defines the snapshot and links it to the corresponding VolumeSnapshotContent.


Create a file named **volumesnapshotcontent.yaml** with the following content. 

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
{: codeblock}


In the volumesnapshotcontent.yaml file, the value of the snapshotHandle field should be set to the snapshot ID of an existing snapshot.
{: note}


Once both resources are created and linked, you can restore the snapshot into a PVC using the standard restore procedure. Pod creation and volume mounting work the same as with dynamically provisioned snapshots.

## Known limitation
{: #csi-knownlimitation}

- Volume size in statically provisioned Persistent Volumes (PVs) may differ from the actual volume size on the storage or deployment

In static provisioning, the administrator manually provisions storage and creates a PV manifest that references this storage volume. OpenShift uses the `spec.capacity.storage` field in the PV manifest as metadata to represent the volume size.
Since static provisioning bypasses the CSI driver’s CreateVolume gRPC call, which is used in dynamic provisioning to create the volume and ensure the `spec.capacity.storage` matches the actual size on RSOS—there is no built-in validation to confirm that the declared capacity aligns with the real backend volume size.
If the PV size specified in the manifest differs from the actual volume size on the deployment, pods will only be able to use and see the actual volume size, not the declared size in the manifest.

- Suggestion: To avoid discrepancies between OpenShift’s metadata and the actual storage behavior, we recommend setting the PV’s `spec.capacity.storage` to match the actual size of the underlying storage. This ensures consistency, accurate scheduling, and prevents OpenShift from under-reporting or over-reporting capacity relative to what pods can actually consume.

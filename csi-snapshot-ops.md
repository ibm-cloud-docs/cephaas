---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-23"

keywords: cephaas snapshots

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# CSI snapshot operations
{: #csi-snapshot-ops}

This section describes how to create, delete, and restore volume snapshots using the {{site.data.keyword.cephaas_short}} CSI driver. 


## Create a snapshot
{: #create-pvc-snapshot}

* Create a YAML file named snapshot.yaml with the following content. 

```sh
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshot
metadata:
  name: cephaas-snapshot
spec:
  volumeSnapshotClassName: csi-cephaas-snapclass
  source:
    persistentVolumeClaimName: cephaascsi-pvc
```
{: pre}

Replace cephaas-snapshot with your desired snapshot name, and cephaascsi-pvc with the name of the PVC you want to snapshot.

* Apply the configuration with the command `oc apply -f snapshot.yaml`.

* View the snapshot details with the command `oc get VolumeSnapshot`.


## Delete a snapshot
{: #delete-pvc-snapshot}

To delete an existing volume snapshot, run the command `oc delete VolumeSnapshot <snapshot-name>`.

Replace <snapshot-name> with the name of the snapshot you want to delete.


## Restore a snapshot to a PVC
{: #restore-pvc-snapshot}

* To restore a volume snapshot into a new PVC, create a YAML file named restore.yaml with the following content:

```sh
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cephaascsi-restore-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: cephaascsi-sc
  resources:
    requests:
      storage: 2G
  dataSource:
    name: <snapshot-name >                
    kind: VolumeSnapshot
    apiGroup: snapshot.storage.k8s.io
```
{: pre}

The requested storage size must be equal to or greater than the size of the original PVC.

* Apply the configuration with the command `oc apply -f restore.yaml`.

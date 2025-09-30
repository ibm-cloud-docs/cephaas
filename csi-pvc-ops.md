---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-30"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# PersistentVolumeClaim (PVC) operations
{: #pvc-ops}

This section provides step-by-step instructions for managing PersistentVolumeClaims (PVCs) using the CephaaS CSI driver. It covers essential operations such as creating, viewing, expanding, and deleting PVCs, as well as verifying PVC functionality by referencing them in pods.

## Create PVC
{: #create-pvc}

* Create a YAML file named pvc.yaml with the following content. 

```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: <your-pvc-name>
spec:
  accessModes:
  - ReadWriteOnce
  resources:
  requests:
  storage: <required-size>G
  storageClassName: cephaascsi-sc
 ```
{: codeblock}

The G in storage section specifies the volume size in gigabytes (GB). 

* Apply the PVC configuration. 

```
oc apply -f pvc.yaml
 ```
{: codeblock}

## View PVC
{: #view-pvc}

To check the status and details of the PVC:

```
oc get pvc <your-pvc-name>
oc describe pvc <your-pvc-name>
 ```
{: codeblock}

## Expand PVC
{: #expand-pvc}

To increase the size of the PVC:

* Edit the PVC. 

```
oc edit pvc <your-pvc-name>
 ```
{: codeblock}

* Edit `spec.resources.requests.storage` field and update the value to the new size.

Kubernetes does not support shrinking a volume. During a PVC expansion operation, the new requested size must be greater than the current size. Before attempting to expand a PVC, verify that sufficient block storage quota is available. If the current PVC size exceeds the available quota, the expansion will fail.
{: note}

### Known limitation
{: #knownlimitation-expand-pvc}

**Expand PVC operation timeout**

This issue occurs when a small PVC (e.g., 1 GB) is expanded to a very large size (e.g., 32 TB). The operation may fail with a timeout error in the pod event logs, as shown below: 

`Expander.NodeExpand failed to expand the volume: rpc error: code = DeadlineExceeded desc = context deadline exceeded`

The cause is that the resize2fs utility takes longer to expand volumes that are mounted or in use. This process, known as online expansion, is supported by the CSI driver but can take more than 3 minutes for large volumes. Note that on RSOS, the actual volume expansion is instant—it's the resize2fs step that takes extra time.

**Suggestion**

The CSI driver automatically retries the expansion operation after a timeout. The PVC will eventually expand to the requested size without requiring user action. Users can monitor progress in the pod description and node plugin logs.

## Create a pod
{: #create-pod}

* Create a YAML file named pod.yaml with the following content:

```
kind: Pod
apiVersion: v1
metadata:
  name: <name-of-your-pod>
spec:
  containers:
  - name: alpine
    image: alpine:3
    imagePullPolicy: "IfNotPresent"
    command:["sleep", "365d"]
    volumeMounts:
    - mountPath: "/cephaasvol"
      name: cephaas-volume
  volumes:
  - name: cephaas-volume
    persistentVolumeClaim:
    claimName: cephaascsi-pvc
 ```
{: codeblock}

You need to replace this container block with your own application containers. 

* Apply the configuration. 

```
oc apply -f pod.yaml
 ```
{: codeblock}

If needed, you can delete the pod running this command `oc delete pod <pod_name>`.
{: note}

## Delete PVC
{: #delete-pvc}

To delete a PersistentVolumeClaim (PVC), run the following command:

```
oc delete pvc <your-pvc-name>
 ```
{: codeblock}

Before deleting a PersistentVolumeClaim (PVC), make sure there are no existing VolumeSnapshots associated with it.If snapshots exist, the PVC deletion will fail, preventing the volume and its snapshots from being removed.
{: note}


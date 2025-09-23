---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-23"

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

```sh
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
{: pre}

The G in <required-size>G specifies the volume size unit in gigabytes (GB).

* Apply the PVC configuration. 

```sh
oc apply -f pvc.yaml
```
{: pre}

## View PVC
{: #view-pvc}

To check the status and details of the PVC:

```sh
oc get pvc <your-pvc-name>
oc describe pvc <your-pvc-name>
```
{: pre}

## Expand PVC
{: #expand-pvc}

To increase the size of the PVC:

* Edit the PVC. 

```sh
oc edit pvc <your-pvc-name>
```
{: pre}

* Edit `spec.resources.requests.storage` field and update the value to the new size.

Kubernetes does not support shrinking a volume. During a PVC expansion operation, the new requested size must be greater than the current size. Before attempting to expand a PVC, verify that sufficient block storage quota is available. If the current PVC size exceeds the available quota, the expansion will fail.
{: note}

## Create pod referencing the PVC
{: #create-pod}

* Create a YAML file named pod.yaml with the following content:

```sh
kind: Pod
apiVersion: v1
metadata:
  name: <name-of-your-pod>
spec:
  containers:
  - name: alpine
    image: alpine:3
    imagePullPolicy: "IfNotPresent"
    command: ["sleep", "365d"]
    volumeMounts:
    - mountPath: "/cephaasvol"
      name: cephaas-volume
  volumes:
  - name: cephaas-volume
    persistentVolumeClaim:
      claimName: cephaascsi-pvc
```
{: pre}

* Apply the configuration. 

```sh
oc apply -f pod.yaml
```
{: pre}

If needed, you can delete the pod running this command `oc delete pod <pod_name>`.
{: note}

## Delete PVC
{: #delete-pvc}

To delete a PersistentVolumeClaim (PVC), run the following command:

```sh
oc delete pvc <your-pvc-name>
```
{: pre}

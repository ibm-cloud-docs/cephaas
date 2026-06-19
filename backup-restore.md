---

copyright:
  years: 2026

lastupdated: "2026-06-19"

keywords: backup, restore, disaster recovery, data protection, snapshots, replication, block storage, backup, ROKS, velero

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data on your clusters
{: #backup-restore}

You can configure and use Backup and Restore (BNR) on a Red Hat OpenShift on IBM Cloud cluster by using a CLI-based workflow. This guide focuses on backing up an application namespace, including secrets and persistent volume claims (PVCs), not the entire cluster.
{: shortdesc}

With Backup and Restore, you can:

- Enable backup and restore on a cluster
- Verify that the BNR components are installed
- Configure IBM Cloud Object Storage (COS)
- Define backup policies and schedules
- Run backups manually or on a schedule
- Restore application data, such as PVCs and secrets

## Prerequisites
{: #backup-restore-prereqs}

Before you configure backup and restore, ensure that you have the following prerequisites:

- Access to a Red Hat OpenShift on IBM Cloud cluster with the [`oc`](backup-restore.md:36) CLI configured
- Fusion services enabled on the cluster. For more information, see [Enabling Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services).
- Permission to label the [`managedcluster`](backup-restore.md:47) custom resource or call the internal enablement API
- An IBM Cloud account with an IBM Cloud Object Storage instance
- A COS bucket for storing backups
- COS credentials that you can base64 encode for use in a Kubernetes secret
- The namespace that contains the application that you want to protect

## Enabling backup and restore
{: #enable-bnr}

Before you use the CR-based backup and restore workflow, enable Fusion services on the cluster. After Fusion services are enabled, you can enable and use Backup and Restore (BNR) by labeling the [`managedcluster`](backup-restore.md:47) custom resource or by calling the internal API.

1. Enable BNR on your cluster by running the following command:

   ```sh
   oc label managedcluster <cluster-name> isf.ibm.com/fusion-backup=true
   ```
   {: pre}

2. Verify that the installation completed by checking the pods in the [`ibm-backup-restore`](backup-restore.md:52) namespace:

   ```sh
   oc get pods -n ibm-backup-restore
   ```
   {: pre}

3. Confirm that the BNR pods are in `Running` or `Completed` status. The following table shows the expected pod types after installation:

   | Pod name | Ready | Status | Restarts | Age |
   | -------- | ----- | ------ | -------- | --- |
   | 5531d81ef75328ec4c863d6b38c60668479a0be44d8b007ede366c53f1hz854 | 0/1 | Completed | 0 | 6m28s |
   | 913043d495569b683138873c165fa34c5e3adedfc74a5dec7cce76fb3fqzwq4 | 0/1 | Completed | 0 | 6m30s |
   | b04fc6523bd46f414e8463cd10dce8ce62ad97dd4224a269ffc9553eeejp86h | 0/1 | Completed | 0 | 6m29s |
   | dbr-controller-649bb968b6-wmqpv | 1/1 | Running | 2 (4m48s ago) | 5m8s |
   | guardian-dm-controller-manager-85fb656bd5-6rptg | 2/2 | Running | 0 | 5m56s |
   | guardian-dp-operator-controller-manager-7595665775-5hkjf | 2/2 | Running | 0 | 6m1s |
   | guardian-minio-0 | 1/1 | Running | 0 | 5m12s |
   | ibm-dataprotectionagent-controller-manager-7759f7cd8-mxbrj | 2/2 | Running | 0 | 6m3s |
   | ibm-fusion-backup-restore-catalog-cskvb | 1/1 | Running | 0 | 7m15s |
   | node-agent-4s6vh | 1/1 | Running | 0 | 4m37s |
   | node-agent-k4lrg | 1/1 | Running | 0 | 4m41s |
   | node-agent-xrt7z | 1/1 | Running | 0 | 4m46s |
   | openshift-adp-controller-manager-645ff5b555-cj5fk | 1/1 | Running | 0 | 5m58s |
   | transaction-manager-75f6f85cd7-xppb4 | 1/1 | Running | 2 (4m57s ago) | 5m15s |
   | velero-7c49df784b-nv5fw | 1/1 | Running | 0 | 4m47s |
   {: caption="Expected BNR pods after installation" caption-side="bottom"}

## Configuring backup storage
{: #configure-storage}

Configure IBM Cloud Object Storage as the backup destination for your cluster.

1. If you do not already have an IBM Cloud Object Storage instance, create one.

2. Create a bucket to store your backups.

3. Create a secret that contains your COS credentials.

   Create a file named `cos-secret.yaml` with the following content:

   ```yaml
   kind: Secret
   apiVersion: v1
   metadata:
     name: ibm-cos-creds
     namespace: <namespace>
     labels:
       dp.isf.ibm.com/provider-name: isf-backup-restore
   data:
     access-key-id: <base64-encoded-access-key-id>
     secret-access-key: <base64-encoded-secret-access-key>
   type: Opaque
   ```
   {: codeblock}

   Replace [`<base64-encoded-access-key-id>`](backup-restore.md:91) and [`<base64-encoded-secret-access-key>`](backup-restore.md:92) with your encoded COS credentials, and replace [`<namespace>`](backup-restore.md:88) with the namespace that contains the application that you want to back up.

4. Apply the secret to your cluster:

   ```sh
   oc apply -f cos-secret.yaml
   ```
   {: pre}

5. Create a backup storage location that points to your COS bucket.

   Create a file named `backup-storage-location.yaml` with the following content:

   ```yaml
   apiVersion: data-protection.isf.ibm.com/v1alpha1
   kind: BackupStorageLocation
   metadata:
     name: ibm-cos-public-2
     namespace: <namespace>
   spec:
     credentialName: ibm-cos-creds
     params:
       bucket: <bucket-name>
       endpoint: https://s3.us.cloud-object-storage.appdomain.cloud
     provider: isf-backup-restore
     type: ibm
   ```
   {: codeblock}

6. Apply the backup storage location to your cluster:

   ```sh
   oc apply -f backup-storage-location.yaml
   ```
   {: pre}

## Creating a backup policy
{: #create-backup-policy}

A backup policy defines the backup schedule and retention rules for your application data.

1. Create a file named `backup-policy.yaml` with the following content:

   ```yaml
   apiVersion: data-protection.isf.ibm.com/v1alpha1
   kind: BackupPolicy
   metadata:
     name: daily-policy
     namespace: <namespace>
   spec:
     backupStorageLocation: ibm-cos-public-2
     provider: isf-backup-restore
     retention:
       number: 1
       unit: days
     schedule:
       cron: '*/15 * * * * '
       timezone: America/Chicago
   ```
   {: codeblock}

   This example creates a backup policy that runs every 15 minutes and retains backups for 1 day.

2. Apply the backup policy to your cluster:

   ```sh
   oc apply -f backup-policy.yaml
   ```
   {: pre}

## Assigning a backup policy
{: #assign-backup-policy}

Assign the backup policy to your application namespace to enable scheduled backups.

1. Create a file named `policy-assignment.yaml` with the following content:

   ```yaml
   apiVersion: data-protection.isf.ibm.com/v1alpha1
   kind: PolicyAssignment
   metadata:
     name: policy-assignment
     namespace: <namespace>
   spec:
     application: <namespace>
     appCluster: <cluster-url>
     backupPolicy: daily-policy
     runNow: false
   ```
   {: codeblock}

   The [`application`](backup-restore.md:176) value is the name of the namespace that you want to back up.

2. Apply the policy assignment to your cluster:

   ```sh
   oc apply -f policy-assignment.yaml
   ```
   {: pre}

## Running a manual backup
{: #run-manual-backup}

You can trigger a manual backup at any time, in addition to the scheduled backups.

1. Create a file named `manual-backup.yaml` with the following content:

   ```yaml
   apiVersion: data-protection.isf.ibm.com/v1alpha1
   kind: Backup
   metadata:
     annotations:
       dp.isf.ibm.com/provider-name: isf-backup-restore
     name: namespace-backup
     namespace: <namespace>
   spec:
     appCluster: <cluster-url>
     application: <namespace>
     backupPolicy: daily-policy
   ```
   {: codeblock}

2. Apply the backup resource to your cluster:

   ```sh
   oc apply -f manual-backup.yaml
   ```
   {: pre}

3. Check the backup status by running the following command:

   ```sh
   oc get fbackup -n <namespace>
   ```
   {: pre}

   The backup progresses through the following statuses:

   - `SnapshotInprogress`
   - `DataTransferInprogress`
   - `Complete`

## Restoring data from a backup
{: #restore-data}

You can restore specific resources from a backup, such as persistent volume claims (PVCs) and secrets.

1. Create a file named `restore.yaml` with the following content:

   ```yaml
   apiVersion: data-protection.isf.ibm.com/v1alpha1
   kind: Restore
   metadata:
     name: restore-example
     namespace: <namespace>
   spec:
     backup: <backup-name>
     overwrite: true
     objectsToRestore:
       PersistentVolumeClaim.v1:
         - "<namespace>/<pvc-name>"
       Secret.v1:
         - "<namespace>/<secret-name>"
   ```
   {: codeblock}

2. Apply the restore resource to your cluster:

   ```sh
   oc apply -f restore.yaml
   ```
   {: pre}

3. Check the restore status by running the following command:

   ```sh
   oc get frestore -n <namespace>
   ```
   {: pre}

## Enabling backup and restore by using the API
{: #enable-bnr-api}

As an alternative to labeling the [`managedcluster`](backup-restore.md:43) custom resource, you can enable backup and restore by calling the internal API.

```sh
curl -X POST \
  $CERT_FLAG \
  --header "Authorization: Bearer $TOKEN" \
  --header "Content-Type: application/json" \
  "${URL}" \
  -d '{"enabled": "true"}' \
  -v
```
{: pre}

After you enable the feature, verify the deployment by checking the pod status:

```sh
oc get pods -n ibm-backup-restore
```
{: pre}

Ensure that all pods are in `Running` or `Completed` status.

## Important considerations
{: #backup-restore-considerations}

These instructions show how to back up and restore an application namespace. They do not cover backing up the entire cluster.

Use namespace-specific values for your environment, such as the namespace name, cluster URL, backup name, PVC name, secret name, and COS bucket name.

Avoid restoring an entire namespace on top of itself unless you fully understand the impact. Doing so can remove the backup and restore configuration from that namespace.

## Self-service backup and restore for application owners
{: #backup-restore-self-service}

If you are an application owner (a user who manages applications within a specific namespace), you can create IBM Fusion Backup & Restore Custom Resource (CRs) within your application's namespace to self-manage your application's backup and restore needs. This self-service capability allows you to protect your namespace application without requiring cluster-level permissions or IBM Fusion Backup & Restore administrator rights.

This approach is ideal for development teams or application users who need to manage their own backups independently, without involving cluster administrators.

For more information about self-service backup and restore, see see [IBM Fusion Backup & Restore documentation](https://www.ibm.com/docs/en/storage-fusion/2.8?topic=fusion-backup-restore){: external}.

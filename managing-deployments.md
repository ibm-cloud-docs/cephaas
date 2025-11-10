---
copyright:
 years: 2024, 2025
lastupdated: "2025-10-30"

keywords: ceph as a service, managing deployments in vsphere plug-in

subcollection: cephaas
---


{{site.data.keyword.attribute-definition-list}}

# Managing deployments in vSphere plug-in
{: #managing-deployments-vsphere-plug-in}

## Adding a deployment
{: #adding-dep-trials}

Use the following procedure to add an {{site.data.keyword.cephaas_full_notm}} deployment to the vSphere plug-in.

1.	Login to the vSphere Web client Navigate to **Main menu** -> **IBM Storage CephaaS** for the plug-in dashboard.
2. Click **ADD DEPLOYMENT**.
3. **Add Deployment** screen is displayed which shows the first step of **Connect to IBM Storage CephaaS**.
4. Enter the information in the fields **Block Endpoint FQDN** and **API Key**.
5. Click **Next**. **Deployment Details** screen is displayed where you need to enter the name of the deployment.
6. Click **Next**. **Review** screen is displayed which shows the new deployment details entered by you in the previous steps.
7. Click **Add**. The newly added deployment details will be reflected on the deployment dashboard.

## Editing deployment details
{: #edit-deployment-details}

If you detect any inconsistencies between the deployment and vSphere datastore volumes or hosts, click the ‘Reconcile’ button to fetch the latest data.
{: note}

For editing deployment details such as the name and API key, use the following prodedure.

1. From the deployment dashboard of the vSphere Client, select the deployment you need to edit and click the pencil icon.
2. **Edit Deployment Details** screen is displayed.
3. Enter the valid API key to either replace the key or rename the deployment
4. Click **Edit**.

## Deleting a deployment
{: #delete-deployment}

For deleting a deployment, perform the following procedure.

1. From the deployment dashboard of the vSphere Client, select the deployment you need to delete.
2. Click the delete icon.
3. A pop-up is displayed which asks about confirming the delete process.
4. Click **Delete**.

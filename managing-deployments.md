---
copyright:
 years: 2024, 2024
lastupdated: "2024-11-12"

keywords: managing deployments in vsphere plug-in

subcollection: cephaas
---


{{site.data.keyword.attribute-definition-list}}

# Managing deployments in vSphere plug-in
{: #managing-deployments-vsphere-plug-in}

## Adding a deployment
{: #add-deployment}

Use the following procedure to add an IBM Ceph as a Service deployment to the vSphere plug-in.

1. From the vSphere Client, go to the plug-in dashboard from the vSphere Client main menu and click IBM Ceph as a Service.
2. Click **Add Deployment**. 
3. **Add Deployment** screen is displayed which shows the first step of **Connect to IBM Storage CephaaS**.
4. Enter the information in the fields **Block Endpoint FQDN** and **API Key**.
5. Click **Next**. **Deployment Details** screen is displayed where you need to enter the name of the deployment.
6. Click **Next**. **Review** screen is displayed which shows the new deployment details entered by you in the previous steps.
7. Click **Add**. The newly added deployment details will be reflected on the deployment dashboard.

## Editing deployment details
{: #edit-deployment-details}

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

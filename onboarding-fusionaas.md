---
copyright:
  years: 2026
lastupdated: "2026-06-23"

keywords: fusion as a service, onboarding, welcome modal, first time user, cluster quota, set cluster quota, getting started

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Onboarding to your IBM Fusion as a service deployment
{: #onboarding-fusionaas}

After you finish setting up your deployment and the hardware setup is done in your data center, you can onboard to your IBM Fusion as a service deployment.

When you log in to your IBM Fusion as a service deployment after the activation for the first time, a welcome banner guides you through the initial setup process. This onboarding flow helps you configure your deployment and understand the next steps for provisioning clusters.
{: shortdesc}

## Understanding the onboarding flow
{: #onboarding-flow-overview}

The onboarding experience varies based on your user role:

- **Administrator users**: Can set the default cluster storage quota during onboarding
- **Non-administrator users**: Can view deployment information 

## Onboarding for administrator users
{: #admin-onboarding}

If you have administrator permissions, the onboarding flow includes the option to set the default cluster storage quota.

### Setting the default cluster quota
{: #set-cluster-quota-onboarding}

As an administrator, you can set the default cluster storage quota directly from the welcome modal.

1. In the welcome banner, click **Set cluster quota**.

   The **Set default cluster quota** side panel opens.

2. In the **Storage quota (TB)** field, enter the default storage quota value in terabytes.

   The default value that you set for the cluster quota is applied to all new clusters. You can increase the cluster quota from the default value, but you cannot decrease it. The default cluster quota can be changed later from the Settings page. For more information, see [Editing cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota).
   {: note}

3. Click **Save** to set the default cluster quota, or click **Cancel** to close the side panel without making changes.

After you save the default cluster quota, you can begin using your deployment.

## Onboarding for non-administrator users
{: #non-admin-onboarding}

If you do not have administrator permissions, the onboarding flow provides an overview of your deployment without the option to set the cluster quota.

### Viewing your clusters
{: #view-clusters-onboarding}

As a non-administrator user, you can proceed directly to view your clusters.

1. In the welcome banner, click **View your clusters**.

   The Clusters page opens, where you can view all clusters associated with your deployment.

The **Set cluster quota** button is not available for non-administrator users. Only administrators can set or modify the default cluster storage quota.
{: note}

## After onboarding
{: #after-onboarding}

After you complete the onboarding flow, you can access your deployment directly from the {{site.data.keyword.cloud_notm}} console.

### Next steps for administrators
{: #admin-next-steps}

After onboarding, administrators can:

- [Create clusters](/docs/cephaas?topic=cephaas-create-clusters)
- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services)
- [Update the default cluster quota](/docs/cephaas?topic=cephaas-manage-cluster-quota) from the Settings page
- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)

### Next steps for non-administrator users
{: #non-admin-next-steps}

After onboarding, non-administrator users can:

- [View clusters](/docs/cephaas?topic=cephaas-view-cluster-list)
- [Understand cluster access permissions](/docs/cephaas?topic=cephaas-cluster-access)

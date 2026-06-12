---
copyright:
  years: 2026
lastupdated: "2026-06-12"

keywords: fusion as a service, onboarding, welcome modal, first time user, cluster quota, set cluster quota, getting started

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Onboarding to your Fusion as a Service deployment
{: #onboarding-fusionaas}

When you log in to your Fusion as a Service deployment for the first time, a welcome banner guides you through the initial setup process. This onboarding flow helps you configure your deployment and understand the next steps for provisioning clusters.
{: shortdesc}

## Understanding the onboarding flow
{: #onboarding-flow-overview}

The onboarding experience varies based on your user role:

- **Administrator users**: Can set the default cluster storage quota during onboarding
- **Non-administrator users**: Can view deployment information and proceed to cluster provisioning

The welcome banner appears automatically when you access your deployment for the first time. It displays the message "Your order is on its way." and provides an overview of your deployment status, guiding you to the appropriate next steps.

## Onboarding for administrator users
{: #admin-onboarding}

If you have administrator permissions, the onboarding flow includes the option to set the default cluster storage quota.

### Setting the default cluster quota
{: #set-cluster-quota-onboarding}

As an administrator, you can set the default cluster storage quota directly from the welcome modal.

1. In the welcome banner, click **Set cluster quota**.

   The **Set default cluster quota** side panel opens.

2. Review the information in the side panel:

   **This cluster quota will be the default amount of storage capacity allocated each time a cluster is created. This setting can be changed at a later time.**

3. In the **Storage quota (TB)** field, enter the default storage quota value in terabytes.

   The default value is 10 TB. You can increase or decrease this value based on your deployment capacity and requirements.

4. Review the note: **This quota will be applied to all new clusters created.**

5. Click **Save** to set the default cluster quota, or click **Cancel** to close the side panel without making changes.

After you save the default cluster quota, the welcome banner closes and you can begin using your deployment.

The default cluster quota can be changed later from the Settings page. For more information, see [Editing cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota).
{: tip}

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
- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)

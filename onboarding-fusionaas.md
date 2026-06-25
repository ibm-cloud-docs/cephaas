---
copyright:
  years: 2026
lastupdated: "2026-06-25"

keywords: fusion as a service, onboarding, welcome modal, first time user, cluster quota, set cluster quota, getting started

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Onboarding to your IBM Fusion as a service deployment
{: #onboarding-fusionaas}

After your deployment is provisioned and becomes available, you can onboard to your IBM Fusion as a service deployment. The onboarding flow appears only the first time you access your deployment.
{: shortdesc}

## Before you begin
{: #onboarding-prereqs}

Before you can onboard to your deployment, the following conditions must be met:

- Your order has been confirmed by IBM Sales (handled offline, no system email sent).
- IBM Sales has shared the deployment link with you after your IBM Cloud account is set up (typically within 1 day).
- You have completed the **Prepare deployment** step by providing your Satellite location and resource group (mandatory fields).
- The deployment status has progressed from **Provision in progress** to **Available** (infrastructure setup completed by SRE, may take a few days).

## Understanding the deployment flow
{: #deployment-flow}

Your IBM Fusion as a service deployment progresses through the following states:

Not started
:   Initial state after order confirmation. You must take action to prepare the deployment.

Prepare deployment
:   You provide the required Satellite location and resource group. After submission, the deployment instance is created in your resource list with status **Completed**.

Provision in progress
:   The SRE backend team completes infrastructure setup, including rack configuration. This process may take a few days.

Available
:   The deployment is ready for use. You can now onboard and begin managing clusters.

The onboarding welcome modal appears only when you first access an **Available** deployment.

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

3. Click **Save** to set the default cluster quota, or click **Cancel** to close the side panel without making changes.

After you save the default cluster quota, you can begin using your deployment.

## Understanding default and cluster quotas
{: #quota-logic}

The default cluster quota and individual cluster quotas work together to manage storage allocation:

Default cluster quota
:   The baseline storage quota that is automatically applied when you enable Fusion services for a new cluster. This value is set during onboarding and can be changed later from the Settings page.

Cluster quota
:   The storage quota assigned to an individual cluster. Each cluster quota must be equal to or greater than the default cluster quota. You cannot set a cluster quota below the default quota value.

The default quota applies only to new clusters when Fusion services are enabled. It does not affect existing clusters or change their current quotas.
{: note}

### Quota constraints
{: #quota-constraints}

When working with quotas, keep the following constraints in mind:

- The default cluster quota serves as the minimum baseline for all cluster quotas.
- Individual cluster quotas can be increased above the default but cannot be decreased below it.
- Changing the default quota affects only future clusters, not existing ones.
- Storage quota cannot be configured from Red Hat OpenShift on IBM Cloud (ROKS). All quota management is done through the IBM Fusion as a service UI.

For more information about managing quotas, see [Editing cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota) and [Updating a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota).

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

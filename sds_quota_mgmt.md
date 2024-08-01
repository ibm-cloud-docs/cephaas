---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-01"

keywords:

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# Block quota and capacity management
{: #sds-quota-capacity-mgmt}

CephaaS supports service instance level quotas for both the unified (block & object )and low cost object storage plans. The block and object level quota allocation depends on the committed capacity along with the user opted max burst capacity usage limit. Object storage quota can be set by allocating the quota value to the default STANDARD for the unified storage plan and the default storage class STANDARD-IA for the low cost object storage plan.

Since the provisioned capacity and quota is at service instance level setting, the quota can be set for block storage pool as well as object storage pool.

## Managing quota from the UI
{: #managing-sds-block-quota-ui}

1. On the {{site.data.keyword.cloud_notm}} console, click the **hamburger menu > Resource list** and expand **Storage**.

2. Click **Deployment name** link and go to **Settings**.

3. Click **Edit preferences**.

    If you want to manage quota for a different Deployment, then click **Deployments** drop down to choose the one whose quota you want to manage and click **Edit preferences**.
    {: note}

4. Review the capacity limit. Select **Include burst capacity** if you want to expand your total available capacity.

    Including burst capacity may incur overage fees for the amount of burst capacity userd.
    {: note}

4. Click **Next** and review the storage capacity allocations.

5. Use the plus & minus controls to modify the allocated capacity.

    The allocated capacity cannot be reduced or set below the current amount of used or provisionied capacity.
    {: note}

6. Click **Save** to set the new storage capacity allocations.


## Managing block quota using the CLI
{: #managing-sds-block-quota-cli}

Use the following command to modify the block and object storage quota.

```sh
ibmcloud resource service-instance-update ( NAME | ID ) [-n, --name NEW_NAME] [--service-plan-id SERVICE_PLAN_ID] [-p, --parameters @JSON_FILE | JSON_STRING ] [-g RESOURCE_GROUP] [--service-endpoints SERVICE_ENDPOINTS_TYPE] [--allow-cleanup true|false] [-f, --force] [-q, --quiet]
```
In the `--parameters` specify the capacity amounts as `JSON_STRING`. See the following example.

```bash
ibmcloud resource service-instance-update cephaas-unified-2 --parameters `{"quota": {"block": "60", "object": "40"}, "allocate_burst_capacity":"true"}`

Updating service instance cephaas-unified-2 with ID crn:vi:staging:public:software-defined-storage:us-south:a/7a30fdf....:: is updated successfully
```
{: screen}




---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-26"

keywords: cephaas, quota, capacity, manage

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}


# Managing quota
{: #quota-capacity-mgmt}

{{site.data.keyword.cephaas_full_notm}} supports deployment level quotas for both the Performance and Capacity plans. The block and object level quota allocation depends on the committed capacity along with the user opted max burst capacity usage limit.

Since the provisioned capacity and quota is at deployment level setting, the quota can be set for block storage as well as object storage. The quota is set initially by default when the deployment instance is created that also includes the maximum burst capacity usage limit.

## Managing quota from the UI
{: #managing-quota-ui}
{: ui}

1. On the {{site.data.keyword.cloud_notm}} console, click the **hamburger menu > Resource list** and expand **Storage**.

2. Click **Deployment name** link and go to **Settings**.

3. Click **Edit preferences**.

    If you want to manage quota for a different Deployment, then click **Deployments** drop down to choose the one whose quota you want to manage and click **Edit preferences**.
    {: note}

4. Review the capacity limit. Select **Include burst capacity** if you want to include the burst capacity to expand your total available capacity.

    Including burst capacity may incur overage fees for the amount of burst capacity used.
    {: note}

4. Click **Next** and review the storage capacity allocations.

5. Use the plus & minus controls to modify the allocated capacity.

    The allocated capacity cannot be reduced or set below the current amount of used or provisioned capacity.
    {: note}

6. Click **Save** to set the new storage capacity allocations.


## Managing quota using the CLI
{: #managing-quota-cli}
{: cli}

Use the following command to modify the block and object storage capacity quota.

```sh
ibmcloud resource service-instance-update <Service_Instance_ID>  --parameters '{"quota": {"block": <n>, "object": <n>}, "allocate_burst_capacity": <bool>}'
```
{: pre}

In the `--parameters` specify the capacity amounts. See the following example where the Service_Instance_ID is `cephaas-unified-2` and the quota to be updated are specified as parameters.

```bash
ibmcloud resource service-instance-update cephaas-unified-2 --parameters `{"quota": {"block": 60, "object": 40}, "allocate_burst_capacity":"true"}`

Updating service instance cephaas-unified-2 with ID crn:vi:staging:public:software-defined-storage:us-south:a/7a30fdf....:: is updated successfully
```
{: screen}

To verify that the capacity quota was updated, run the following command

```sh
ibmcloud resource service-instance <instancename> --output json
```
{: pre}





## Managing quota with the API
{: #managing-quota-api}
{: api}

Make a `PATCH` request to modify the block and object quota.

```sh
curl -X PATCH $rc_endpoint/v2/resource_instances/$guid -H "Authorization: Bearer $token" -H 'Content-Type: application/json' -d '{
"parameters": {
       "quota":{"block":60,"object":40},
       "allocate_burst_capacity":true
   }
}'
```
{: pre}

In the example, `$rc_endpoint` is the resource controller endpoint. Make sure that `crn` is included in the url in encoded format.

When `allocate burst capacity` is set to `true` then 30% extra quota is set which is the total of block and object quota where the bust capacity is also included in this total quota leading to increase in the overages and pricing fees.

When the `allocate burst capacity` value is set to `false`, the bust capacity is disabled and the quota does not exceed the total of the current set value.

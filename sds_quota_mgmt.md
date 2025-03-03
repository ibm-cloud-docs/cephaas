---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-03"

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

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link > **Settings**.

1. Click **Edit preferences**.

    If you want to manage quota for a different Deployment, then click **Deployments** drop down to choose the one whose quota you want to manage and click **Edit preferences**.
    {: note}

1. Review the capacity limit. Select **Include burst capacity** if you want to include the burst capacity to expand your total available capacity.

    Including burst capacity may incur overage fees for the amount of burst capacity used.
    {: note}

1. Click **Next** and review the storage capacity allocations.

1. Use the plus & minus controls to modify the allocated capacity.

    The allocated capacity cannot be reduced or set below the current amount of used or provisioned capacity.
    {: note}

1. Click **Save** to set the new storage capacity allocations.


## Managing quota using the CLI
{: #managing-quota-cli}
{: cli}

Use the following command to modify the block and object storage capacity quota.

```sh
ibmcloud resource service-instance-update <Service_Instance_name>  --parameters '{"quota": {"block": <n>, "object": <n>}, "allocate_burst_capacity": <bool>}'
```
{: pre}

In the `--parameters` specify the capacity amounts. See the following example where the Service_Instance_ID is `cephaas-unified-2` and the quota to be updated are specified as parameters.

```bash
ibmcloud resource service-instance-update cephaas-unified-2 --parameters `{"quota": {"block": 60, "object": 40}, "allocate_burst_capacity":"true"}`
...

Updating service instance cephaas-unified-2 with ID crn:vi:staging:public:software-defined-storage:us-south:a/7a30fdf....:: is updated successfully
```
{: screen}

To verify that the capacity quota was updated, run the following command

```sh
ibmcloud resource service-instance <Service_Instance_name> --output json
```
{: pre}





## Managing quota with the API
{: #managing-quota-api}
{: api}

Make a `PATCH` request to modify the block and object quota.

```sh
curl -X PATCH $rc_endpoint/v2/resource_instances/$guid -H "Authorization: Bearer $IAM_TOKEN" -H 'Content-Type: application/json' -d '{
"parameters": {
       "quota":{"block":60,"object":40},
       "allocate_burst_capacity":true
   }
}'
```
{: pre}

In the example, `$rc_endpoint` is the resource controller endpoint. Make sure that `crn` is included in the url in encoded format.

You can configure and set the default endpoint for resource controller `$rc_endpoint` to `https://resource-controller.cloud.ibm.com/v2/resource_instances`. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

When `allocate burst capacity` is set to `true` then 30% extra quota is set which is the total of block and object quota where the burst capacity is also included in this total quota leading to increase in the overages and pricing fees.

When the `allocate burst capacity` value is set to `false`, the burst capacity is disabled and the quota does not exceed the total of the current set value.

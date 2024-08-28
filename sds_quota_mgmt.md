---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-28"

keywords:

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# Block quota and capacity management
{: #sds-quota-capacity-mgmt}

{{site.data.keyword.cephaas_full_notm}} supports service instance level quotas for both the unified (block & object) and value object storage plans. The block and object level quota allocation depends on the committed capacity along with the user opted max burst capacity USAGE limit.

Since the provisioned capacity and quota is at service instance level setting, the quota can be set for block storage as well as object storage. The quota is set initially by default when the deployment instance is created.

## Managing quota from the UI
{: #managing-sds-block-quota-ui}
{: ui}

1. On the {{site.data.keyword.cloud_notm}} console, click the **hamburger menu > Resource list** and expand **Storage**.

2. Click **Deployment name** link and go to **Settings**.

3. Click **Edit preferences**.

    If you want to manage quota for a different Deployment, then click **Deployments** drop down to choose the one whose quota you want to manage and click **Edit preferences**.
    {: note}

4. Review the capacity limit. Select **Include burst capacity** if you want to expand your total available capacity.

    Including burst capacity may incur overage fees for the amount of burst capacity used.
    {: note}

4. Click **Next** and review the storage capacity allocations.

5. Use the plus & minus controls to modify the allocated capacity.

    The allocated capacity cannot be reduced or set below the current amount of used or provisionied capacity.
    {: note}

6. Click **Save** to set the new storage capacity allocations.


## Managing block quota using the CLI
{: #managing-sds-block-quota-cli}
{: cli}

Use the following command to modify the block and object storage capacity quota.

```sh
ibmcloud resource service-instance-update <Service_Instance_ID>  --parameters '{"quota": {"block": <n>, "object": <n>}, "allocate_burst_capacity": <bool>}'
```
{:pre}

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





## Managing block quota with the API
{: #managing-sds-block-quota-api}
{: api}

Make a PATCH request to modify the quota for provisioned and object capacity.

```sh
curl --location --request PATCH '$rc_endpoint' -H "Authorization: $token" -d '{"parameters":{"allocate_burst_capacity":"true", quota":{"block":"70","object":"50"}}}

```
{: pre}

`$rc_endpoint` is the resource controller endpoint. Make sure that `crn` is included in the url in encoded format.
{: note}

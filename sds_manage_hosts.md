---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-18"

keywords: sds, sdsaas Block Storage Volume, update volume for sdsaas, manage volume

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing hosts
{: #managing-sds-hosts}

You can manage hosts in the UI, from the CLI, or with the API.
{: shortdesc}

## Managing hosts in the UI
{: #managing-sds-host-name-ui}
{: ui}

Use the console to manage the hosts. In the console, you can complete the following actions.

* Rename a host
* Map volumes to a host
* Unmap volumes for a host
* Delete a host


### Renaming a host in the UI
{: #renaming-sds-hosts-ui}
{: ui}

To rename a host, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), navigate to **SDS as a Service > Block storage > Hosts**.
2. Locate the Host **Name** and click the `options` icon at the end of the Host row to open a list of options.
3. From the options menu, click **Rename**.
4. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. For example, if you create two hosts with the same name in the same service instance, a duplicate host name error is displayed.
5. Click **Rename**.


### Renaming a host from details page in the UI
{: #renaming-sds-hosts-from-details-page-ui}
{: ui}

1. In the **Host** details page, click the `Actions` button.
3. From the Actions menu, you can click **Rename** OR you can click the `pen` icon next to the host name to modify the host name.
4. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. For example, if you create two hosts with the same name in the same service instance, a duplicate host name error is displayed.
5. Click **Rename**.


### Mapping volumes to a host in the UI
{: #mapping-volume-sds-hosts-ui}
{: ui}


To map a volume to a host from Hosts page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), navigate to **SDS as a Service > Block storage > Hosts**.
2. Locate the host **Name** and click the `options` icon at the end of the row to open a list of options.
3. From the options menu, click **Map volumes**.
4. Select one or more volumes that you would like to map to the host.
5. Click **Map**.




## Managing hosts from the CLI
{: #managing-sds-hosts-cli}
{: cli}

Using CLI, you can complete the following actions.

* Rename a host.
* Map a volume to a host.


### Rename a host
{: #ic-sds-rename-host}

Use the `host-update` command to rename a specific host.

Run the following command to update the details of a specific host in a service instance.

```sh
ibmcloud software-defined-storage host-update --host-id HOST-ID --instanceid INSTANCEID [--host-patch HOST-PATCH]
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage host-update \
    --host-id exampleString \
    --instanceid exampleString \
    --name my-host
```

### Mapping volume to a host from CLI
{: #mapping-sds-hosts-cli}
{: cli}

Use the `host-vol-update` command and specify the `HOST-ID`, `VOLUME-ID` and `INSTANCEID` to create a volume mapping to the given host ID.

Run the following command to map the volume to the given host.

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-vol-update \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString

```
{: screen}



## Managing host with the API
{: #managing-sds-hosts-api}
{: api}

To manage your hosts with the API, you can make use of the `PATCH /hosts/{id}` request to modify the host details. Specify the values for the parameter that you want to modify in the request to update the details.


PATCH operation to change more than one parameter value in the same command is not supported.
{: note}



### Renaming a host with the API
{: #renaming-sds-host-api}
{: api}

Make a `PATCH /hosts/{id}` request to update or rename a host.

```sh
{{curl -X PATCH '$sds_api_endpoint/v1/hosts/{host-name-1}' }}
{{--header 'Authorization: Bearer $IAM_TOKEN' }}
{{--header 'Content-Type: application/json' }}
--data '{
    "name": "sds-host-name-updated"
}'
```
{: pre}

A successful response looks like this:

```json
COMING SOON

```
{: screen}

### Mapping volume to a host with the API
{: #mapping-sds-hosts-api}
{: api}

Make a `PUT /hosts/{id}/volumes/{vol_id}` request to map the volume to a given host.

```sh
curl -X PUT '$sds_api_endpoint/v1/hosts/{host-id}/volumes/{volume-id}'
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

A successful response looks like this:

```json
{
  "created_at": "string",
  "id": "string",
  "name": "string",
  "nqn": "string",
  "service_instance_id": "string",
  "storage_workspace_id": "string",
  "volume_mappings": [
    {
      "status": "string",
      "volume_id": "string",
      "volume_name": "string"
    }
  ]
}

```
{: screen}



## Next steps
{: #next-step-updating-volume-sds}

You can continue with renaming or mapping hosts.

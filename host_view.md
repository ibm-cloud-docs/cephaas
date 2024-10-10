---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-10"

keywords: sds, host, view host details, host summary list

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# View host details
{: #view-host-details}

View details of a host or summary information about all hosts for the chosen deployment.
{: shortdesc}

## Viewing host details in the UI
{: #view-host-details-ui}
{: ui}

You can view a summary of all host and view details for a single volume for the chosen deployment on the user interface.

### Viewing all host in the UI
{: #view-all-hosts-ui}
{: ui}

To view all hosts and all mapped volumes, in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to  **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

By default, all Hosts are displayed for the chosen Deployment. In the list of all **Hosts**, you can see the following information.

| Field | Description |
|-------|-------------|
| Name | Click the name of the host to see individual host details. |
| Volumes mapped | Shows the count of number of volumes mapped to the host. |
| Host NQN | The NVMe Qualified Name (NQN) of the configured host. |
{: caption="Details about all hosts" caption-side="bottom"}

By default, 10 hosts are shown from the list of all hosts. Change this default by clicking the Page Control down arrow and increase the list to 25, 50 or 100 hosts. Use the Page Control arrows after the list to go to the following page or return to the current page.

Row actions menu on the Hosts list page provides you with options to manage the single host information.

Table 2 describes the Row actions menu options.

| Action | Description |
|--------|-------------|
| View host details | Click to open the detailed view of the host. |
| Rename | Click to change the host name. |
| Map to volumes | Click to map the host to a volume. |
| Delete | Remove the mapping between the volume and host. |
{: caption="Row actions menu options for Hosts." caption-side="bottom"}



### Viewing single host details in the UI
{: #view-single-host-details-ui}
{: ui}

To view details of a single host, go to the list of all hosts and click on the hostname link.

The Host details page shows the details of the chosen hostname and all its mapped volumes. Table 3 describes this information.


| Field | Description |
|-------|-------------|
| **Host details** | |
| Name  | Name of the host you specified when you created the host. Click the pencil icon to edit the host name. The name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. The name must be unique for the deployments. |
| Total volumes mapped | Shows the total number of volumes mapped to the host. |
| Added date | System-generated date when the host was added.|
| Host NQN | The NVMe Qualified Name (NQN) of the configured host |
| Deployment | Name of the instance |
{: caption="Host details" caption-side="bottom"}

The Actions menu on the Host details page shows the actions that you can take.

Table 4 describes the Actions menu options.

| Action | Description |
|--------|-------------|
| Rename | Rename the host name |
| Delete | Remove the mapping between the volume and host |
{: caption="Actions menu options for Hosts." caption-side="bottom"}


## Viewing Hosts from the CLI
{: #viewing-hosts-cli}
{: cli}

View details of a single host or summary information about all hosts from the CLI.


### Viewing details of a single host from the CLI
{: #view-single-host-detail-cli}

Run the following command to show host details for a specific host `ID` within the specific service `INSTANCEID`.

```sh
ibmcloud software-defined-storage host --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}


The following example uses the volume ID to show volume details.

```sh
$ ibmcloud software-defined-storage host \
    --host-id exampleString \
    --instanceid exampleString
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}

You can also use the aliase `sds` an alternative to `software-defined-storage` for the CLI actions.
{: tip}



### Viewing a list of all hosts from the CLI
{: #view-all-host-cli}

Run this command to view the list summary information about all hosts:

```sh
ibmcloud software-defined-storage hosts --instanceid INSTANCEID [--start START] [--limit LIMIT] [--name NAME] --url string
```
{: pre}

Specifying the service instance ID is required since it is used to filter the list of volumes that belong to the specified service instance.

The following example shows all volumes for the service instance specified in your availability zone.

```sh
ibmcloud software-defined-storage hosts \
    --instanceid exampleString \
    --start exampleString \
    --limit 10 \
    --name exampleString
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}

You can also use the aliase `sds` an alternative to `software-defined-storage` for the CLI actions.
{: tip}

For more information about available command options, run `ibmcloud sds hosts --help`.


## View all hosts with the API
{: #viewing-hosts-api}
{: api}

You can list all hosts and view details for a specific host within all deployments that you have access to.

Before you begin, make sure that you [set up your API environment](/docs/sdsaas?topic=sdsaas-set-up-environment&interface=api).

### Viewing list of all hosts with the API
{: #view-all-host-api}

Make a `GET /hosts` call to list summary information about all hosts. See the following example.

```sh
curl -X 'GET' '$sds_api_endpoint/v1/hosts -H 'accept: application/json'
```
{: pre}

A successful response looks like the following example.

```json
{
  "first": {
    "href": "string"
  },
  "hosts": [
    {
      "created_at": "string",
      "id": "r134-69d40d27-bb86-4f52-83f9-6d3acb8d74eb",
      "name": "sds-host-name-updated",
      "nqn": "nqn.2014-08.com.vmware:nvme:vm2-esx-host",
      "service_instance_id": "9f158770-66a4-4746-a2aa-245a8e06f451",
      "storage_workspace_id": "default",
      "volume_mappings": [
        {
          "status": "string",
          "storage_identifiers": {
            "id": "string",
            "namespace_id": 0,
            "network_info": [
              {
                "gateway_ip": "string",
                "port": 0
              }
            ]
          },
          "volume_name": "vol1",
          "volume_id": "r134-f02df74f-dcba-4a85-93cb-088d0ffc1ae5",
        }
      ]
    }
  ],
  "limit": 0,
  "next": {
    "href": "string"
  },
  "total_count": 0
}
```

### Viewing single host details with the API
{: #view-single-host-details-api}

Make a `GET /hosts/{id}` call to see details of a host. See the following example.

```sh
curl -X 'GET' '$sds_api_endpoint/v1/hosts/r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921' -H 'accept: application/json'
```
{: pre}

A successful response provides details of the host, such as the host id, host name, nqn, service instance id and also includes mapped volume details if it mapped to a volume.

```json
{
    "id" : "host_id",
    "name": "my-host",
    "nqn": "nqn-xxxxx-xxxxx",
    "created_at": "date-time",
    "service_instance_id": "xxxx",
    "storage_workspace_id": "yyyy",
      volume_mappings" : [
        {
           "volume_name": "<volume_name>",
           "volume_id": "<volume_id1>",
            "status": "mapped"
           "storage_identifiers": {
                   "id": "<subsystem_nqn>",
                  "network_info": [
                        {
                       "gateway_ip": <gateway_ip>,
                      "port": "<port_id>",
                       },
                  ],
                  "namespace_id" : "<volume_namespace_id>"",
             }
        },
   ]

}

```
{: codeblock}

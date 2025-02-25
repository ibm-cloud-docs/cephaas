---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-25"

keywords: list all volumes, view volume details

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# View block volumes
{: #view-volume}

View details about a block storage volume or summary information about all volumes for the deployment.
{: shortdesc}


## View list of all volumes in the UI
{: #viewvols-ui}
{: ui}

To view the list of all the volumes, in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Volumes**.

By default, all {{site.data.keyword.cephaas_short}} volumes for the chosen service instance are displayed. In the list of all **Volumes**, you see the following information.

| Field | Description |
|-------|-------------|
| Name | Click the name of the volume to see individual volume details. |
| Status | Status of the volume |
| Provisioned size | Size of the volume you specified, in GBs.|
| Mapped hosts | Shows the count of number of hosts mapped to the volume. |
{: caption="Details about all volumes" caption-side="bottom"}

By default, 10 volumes are shown in the list of all volumes. Change this default by clicking the Page Control down arrow and increase the list to 25, 50 or 100 volumes. Use the Page Control arrows after the list to go to the following page or return to the current page.

Row actions menu on the Volume list page provides you with options to manage the volume information.

Table 2 describes the Actions menu options.

| Action | Description |
|--------|-------------|
| View volume details | Click to open the detailed view of the Volume. |
| Rename volume | Click to change the volume name. |
| Map to host | Click to map the volume to one or more hosts. |
| Expand volume | Allows you to increase the capacity of the volume. |
| Delete | Delete the volume. |
{: caption="Row actions menu options for volumes." caption-side="bottom"}


## View details of a single volume
{: #view-vol-details-ui}
{: ui}

To view details of a single volume, go to the list of all volumes and click on the volume name.

The volumes details page shows the details of the chosen volume and all its mapped hosts. Table 3 describes this information.

| Field | Description |
|-------|-------------|
| **Volume details** | |
| Name  | Name of the volume you specified when you created the volume. Click the pencil icon to edit the volume name. The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. Volume names must be unique for the service instance. |
| volume ID | System-generated volume ID. |
| Provisioned size | Size of the volume you specified, in GBs. |
| Created date | System-generated date when the volume was created.|
| Service instance | Name of the instance in the region.|
| IOPS | Current IOPS value for a predefined IOPS tier which is based on the default profile. |
| Throughput | The performance a disk can deliver, measured in Gigabytes/second (Gbps). Based on your volume profile, throughput is calculated as the amount of `IOPS * 16` K block size.|
| Mapped hosts | Displays a list of all hosts present in the system. You can also create a new host to map using the `Map host +` option. See [Creating a host](/docs/cephaas?topic=cephaas-creating-host&interface=ui).|
{: caption="Volume details" caption-side="bottom"}

The Actions menu on the volume details page shows the actions that you can take.
Table 4 shows Actions menu options from the volume details page.

| Action | Description |
|--------|-------------|
| Expand volume | Allows you to increase the capacity of the volume. |
| Delete | Delete the volume. |
{: caption="Actions menu options from the volume details page." caption-side="bottom"}






## View single volume details from the CLI
{: #viewvol-cli}
{: cli}

Run the following command to show volume details for a specific volume `ID` along with the endpoint url.

```sh
ibmcloud software-defined-storage volume --volume-id VOLUME-ID --url string
```
{: pre}


See the following example.

```sh
$ ibmcloud sds volume --url $sds_endpoint --volume-id r134-af4273d1-b1a2-4ba8-82aa-2285133e2682
...

Volume_ID     r134-af4273d1-b1a2-4ba8-82aa-2285133e2682
Volume_Name   example1
Status        pending
Bandwidth     19
Capacity_GB   10
Created       2025-02-11T19:08:21.000Z
IOPS          150
Hosts         -

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `vol` as an alternative to `volume` for the CLI actions.
{: tip}



## View list of all volumes from the CLI
{: #viewall-vol-cli}
{: cli}

Run this command to list summary information about all volumes:

```sh
ibmcloud software-defined-storage volumes [--limit LIMIT] [--name NAME] --url string
```
{: pre}

Specifying the service instance ID is required since it is used to filter the list of volumes that belong to the specified service instance.

The following example shows all volumes for the service instance specified in your availability zone.

```sh
ibmcloud software-defined-storage volumes --url $sds_endpoint

ID                                          Name       Status      Capacity_GB   Mapped_Host
r134-2613272e-ff23-461e-94a3-3d3f77c13aa1   example2   available   10            -
r134-d75e1aeb-4bcf-4d41-8926-517198d55448   example1   available   10            -

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `vols` as an alternative to `volumes` for the CLI actions.
{: tip}

For more information about available command options, run `ibmcloud sds volumes --help`.




## View list of all volumes with the API
{: #viewall-vol-api}
{: api}

Make a `GET /volumes` request to retrieve and view a list of all volumes within your deployment.

See the following example.

```sh
curl -X GET "$sds_api_endpoint/v1/volumes"  \
  -H 'accept: application/json'   \
  -H "Authorization: Bearer $IAM_TOKEN"   \
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response looks like the following example. This example shows the first volume mapped to a host.

```json
{
  "first": {
    "href": "https://localhost:8000/hosts?limit=50"
  },
  "limit": 50,
  "total_count": 1,
  "volumes": [
    {
      "id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4800",
      "name": "vol1",
      "bandwidth": 19,
      "capacity": 10,
      "iops": 150,
      "created_at": "2024-06-21T07:22:15Z",
      "host_mappings": [
        {
          "host_id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921",
          "host_name": "host1",
          "host_nqn": "nqn.2014-08.cloud.appdomain.cephaas:nvme:esx-dev-1-23"
        }
      ],
      "profile": {
        "name": "sds-general-purpose"
      },
      "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
      "storage_workspace_id": "default"
      "status": "available",
    }
  ]
}
```

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


## Viewing volume details with the API
{: #viewvol-details-api}
{: api}

Make a `GET /volumes/{volume_id}` request to see details of a volume. See the following example.

```sh
curl -X GET "$sds_api_endpoint/v1/volumes/r134-04f0e415-3c70-43a8-a98d-a0160e50cc88" \
  -H 'accept: application/json'   \
  -H "Authorization: Bearer $IAM_TOKEN"   \
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response provides details of the volume, including capacity and IOPS, the volume status, and the host to which the volume is mapped.

```json
    {
      "id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4800",
      "name": "vol1",
      "bandwidth": 19,
      "capacity": 10,
      "iops": 150,
      "created_at": "2024-06-21T07:22:15Z",
      "host_mappings": [
        {
          "host_id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921",
          "host_name": "host1",
          "host_nqn": "nqn.2014-08.cloud.appdomain.cephaas:nvme:esx-dev-1-23"
        }
      ],
      "profile": {
        "name": "sds-general-purpose"
      },
      "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
      "storage_workspace_id": "default"
      "status": "available",
    }
```
{: codeblock}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).




## Next steps
{: #next-step-viewing-block-storage-volumes}

Create more volumes, map volume to hosts or manage your existing volumes.

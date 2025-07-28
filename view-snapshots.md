---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, view snapshots with UI, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# View existing snapshots
{: #view-snapshots}

View existing snapshots using the UI, CLI, or API.

## Viewing block volume snapshots in the UI
{: #viewing-snapshots-ui}
{: ui}

To view snapshots for a deployment, use the {{site.data.keyword.cephaas_full_notm}} console.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/software-defined-storage/overview), access your deployment and then go to **Block storage** > **Volumes**.
2. The Block storage volumes page displays **Snapshots** column which shows the number of snapshots created for each volume.
3. Select an individual volume to see the **Volume details** page.
4. **Overview** tab of the selected volume displays number of Snapshots of the volume and the corresponding Snapshot size.
5. **Snapshots** tab displays a link to the support documentation.

## Viewing existing snapshots with the API
{: #listing-snapshots-api}
{: api}

You can view the existing snapshots by calling the Snapshots API.

Make a `GET /snapshots` request to view the existing snapshot.

```sh
$ curl -X GET $sds_endpoint/snapshots
 -H 'accept: application/json'
 -H "Authorization: Bearer $IAM_TOKEN"
 -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

A successful response looks like this.

```json
{
  "snapshots": [
    {
      "id": "r134-da70a486-b8d3-44ce-b6ea-d6d3201400d7",
      "href": "http://example.com/aeiou1",
      "name": "my-snap1",
      "source_volume": {
        "id": "r134-79ef7df6-9c86-42a7-baad-6561b1e5b96f",
        "name": "my-vol1",
        "resource_type": "volume"
      },
      "created_at": "2025-06-13T13:37:37Z",
      "captured_at": "2025-06-13T13:37:37Z",
      "lifecycle_state": "stable",
      "minimum_capacity": 10,
      "size": 1,
      "deletable": true,
      "resource_type": "snapshot"
    },
    {
      "id": "r134-641f14f6-515e-464e-91a3-0558f81dacb0",
      "href": "http://example.com/aeiou2",
      "name": "my-snap2",
      "source_volume": {
        "id": "r134-79ef7df6-9c86-42a7-baad-6561b1e5b96f",
        "name": "my-vol2",
        "resource_type": "volume"
      },
      "created_at": "2025-06-13T13:37:33Z",
      "captured_at": "2025-06-13T13:37:34Z",
      "lifecycle_state": "stable",
      "minimum_capacity": 10,
      "size": 1,
      "deletable": true,
      "resource_type": "snapshot"
    },
    {
      "id": "r134-e3851236-1b9d-44fb-b7eb-07328a58a21e",
      "href": "http://example.com/aeiou3",
      "name": "my-snap3",
      "source_volume": {
        "id": "r134-99c368a1-9595-4c78-9577-ce7980aefe0c",
        "name": "my-vol3",
        "resource_type": "volume"
      },
      "created_at": "2025-06-13T07:00:09Z",
      "captured_at": "2025-06-13T07:00:10Z",
      "lifecycle_state": "stable",
      "minimum_capacity": 2000,
      "size": 1,
      "deletable": true,
      "resource_type": "snapshot"
    }
  ],
  "first": {
    "href": "https://sds-cephaas.scp-4cb930cc8cf9-8ce82ab061950a7b6121a1b00b849d81-0000.eu-de.containers.appdomain.cloud/snapshots?limit=50"
  },
  "limit": 50,
  "total_count": 3
}
```
{: screen}

## View existing snapshots from the CLI
{: #view-snapshots-from-from-cli}
{: cli}

To view existing snapshots using the command-line interface (CLI) from a snapshot, run the following command.

```sh
ibmcloud sds volume-snapshots --start <token>, --limit <int>, --name <snap-name>, --source-volume-id <string> , --all-pages
```
{: pre}

All parameters are optional.

See the following example.

```bash
ic sds volume-snapshots
...

Snapshot_Name         Snapshot_ID                                 Created_At                 Snapshot_Size_GiB   Deletable    Source_Volume_Name   More info
shweta-snap-22may-3   r134-ff7620ed-f0cc-420c-9783-652ced6892f2   2025-05-22T05:11:12.000Z   1                   true         shweta-22may-3       ...
```
{: screen}

---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, view specific snapshot with API, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# View a specific snapshot
{: #view-specific-snapshot}

View a specific snapshot of a volume using API or CLI.

## Viewing a specific snapshot from the API
{: #retrieve-snapshots-api}
{: api}

Make a `GET /snapshots/{id}` request to retrieve a single snapshot specified by the identifier in the URL.

```sh
curl -X GET $sds_endpoint/snapshots/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response looks like this:

```json
{
  "id": "r134-e3851236-1b9d-44fb-b7eb-07328a58a21e",
  "href": "http://example.com/aeiou1",
  "name": "my-snap1",
  "source_volume": {
    "id": "r134-99c368a1-9595-4c78-9577-ce7980aefe0c",
    "name": "my-vol1",
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
```
{: screen}

## Viewing a specific snapshot from the CLI
{: #view-specific-snapshot-cli}
{: cli}

To view a specific snapshot through CLI, run the following command.

```sh
ibmcloud sds volume-snapshot --snap-id <snap-id>
```
{: pre}

`--snap-id <string>` is required.

See the following example.

```bash
ic sds volume-snapshot --snap-id r134-ff7620ed-f0cc-420c-9783-652ced6892f2
...

Snapshot_Name        shweta-snap-22may-3
Snapshot_ID          r134-ff7620ed-f0cc-420c-9783-652ced6892f2
Created_At           2025-05-22T05:11:12.000Z
Snapshot_Size_GiB    1
Deletable            true
Source_Volume_Name   shweta-22may-3
Source_Volume_ID     r134-8e024f61-cf87-4031-90ac-ef581028f04c
Lifecycle_State      stable
Minimum_Capacity     1
```
{: screen}

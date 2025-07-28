---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, updating snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Update snapshots
{: #update-a-snapshot}


You can update a new snapshot using the API or CLI.

Only the name of a snapshot can be updated.
{: note}

## Updating a snapshot in the API
{: #update-snapshot-api}
{: api}

Make a `PATCH /snapshots/{id}` request to update a snapshot. This request updates a snapshot with the information in a provided snapshot patch.



```sh
curl -X PATCH $sds_endpoint/snapshots/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
   --data'{
   "name": "snapshot-2025-05-13"
}'
```
{: pre}

A successful response looks like this:

```json
{   "id": "r134-f5505e26-3f1e-4c30-832f-dfbd2b36f450",   
"href": "http://example.com/aeiou",   
"name": "snapshot-2025-05-13",   "source_volume": \
{"id": "r134-99c368a1-9595-4c78-9577-ce7980aefe0c",    
 "name": "my-vol1",     
 "resource_type": "volume"},
  "created_at": "2025-06-13T14:39:09Z",
  "captured_at": "2025-06-13T14:39:11Z",
  "lifecycle_state": "stable",
  "minimum_capacity": 2000,
  "size": 1,
  "deletable": true,
  "resource_type": "snapshot"
}
```
{: screen}

## Updating a snapshot in the CLI
{: #update-snapshot-cli}
{: cli}

To update a new snapshot through CLI, run the following command.

```sh
ibmcloud sds volume-snapshot-update --snap-id <snap-id> --name <snap-name>, --snapshot-patch <snapshot-patch>
```
{: pre}

`--snap-id <snap-id>` is required. `-name <snap-name>`, `--snapshot-patch <snapshot-patch>` are optional.

See the following example.

```bash
ic sds volume-snapshot-update --snap-id r134-535b6bdf-d93f-4233-a239-5a2e78ae88af --name snap-2-updated
...

Snapshot_Name        snap-2-updated
Snapshot_ID          r134-535b6bdf-d93f-4233-a239-5a2e78ae88af
Created_At           2025-05-22T19:55:51.000Z
Snapshot_Size_GiB    1
Deletable            true
Source_Volume_Name   alisha-vol-test
Source_Volume_ID     r134-87a59338-a801-4090-a657-72867fc9ba44
Lifecycle_State      stable
Minimum_Capacity     1
```
{: screen}

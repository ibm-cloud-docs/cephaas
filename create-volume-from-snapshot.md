---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, managing snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Create volumes from snapshots
{: #volume-from-snapshots}

You can restore block volumes from the snapshots with the API and CLI.

## Creating block volumes from snapshots with the API
{: #create-volume-from-snapshot-api}
{: api}

You can create block volumes by making a `POST /volumes` request to retrieve a volume from a snapshot. Specify the source snapshot id. Note that the capacity should be the size of volume from which the snapshot is created & not the snapshot size.

```sh
curl -X POST $sds_endpoint/volumes    
-H "accept: application/json"    
-H "Authorization: Bearer $IAM_TOKEN"    
-H "IBM-API-Version: 2025-02-01"    
--data '{
     "capacity": 10,
     "name": "sandbox-stability-pasta-stroller"
}' 
```
{: pre}


A successful response looks like this:

```json
{
  "id": "r134-8cdec173-1bcb-4b85-ada9-a6374a4f5906",
  "name": "sandbox-stability-pasta-stroller",
  "capacity": 10,
  "iops": 150,
  "status": "pending",
  "created_at": "2025-02-27T10:18:01Z",
  "status_reasons": [],
  "bandwidth": 19,
  "resource_type": "volume",
  "href": "$sds_endpoint/volumes/r134-8cdec173-1bcb-4b85-ada9-a6374a4f5906"
} 
```
{: screen}

## Creating block volumes from snapshots from the CLI
{: #creating-volumes-from-snapshots-cli}
{: cli}

To create block volumes by using the command-line interface (CLI) from a snapshot, run the following command.

```sh
ibmcloud sds volume-create ---capacity <int> --name <string>, --source-snapshot-id <string>, --source-snapshot <JSON-string>
```
{: pre}

`--capacity <int>` is required and `--name <string>`, `--source-snapshot-id <string>`, `--source-snapshot <JSON-string>` are optional.

See the following example.

```bash
ic sds volume-create --name test-volume-restored --source-snapshot-id  r134-eda57df4-41f2-48d8-812d-3d81955b6a1a --capacity 3
...

Volume_ID        r134-dcc720a8-10ae-4b84-8ffe-463402e0a845
Volume_Name      test-volume-restored
Status           pending
Capacity_GB      3
Created          2025-05-28T20:35:03.000Z
Bandwidth        19
IOPS             150
Snapshot_Count   0
Hosts            -
```
{: screen}

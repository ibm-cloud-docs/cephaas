---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, managing snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Create new snapshots
{: #create-new-snapshots}

You can create a new snapshot using the API or CLI.

## Creating a new snapshot in the API
{: #creating-snapshots-api}
{: api}

You can create snapshots by directly calling the Snapshots API.

Make a `POST /snapshots` request to create a new snapshot. Specify block volume id and optional snapshot name.

```sh
curl -X POST $sds_endpoint/snapshots\
   -H "accept: application/json"\
   -H "Authorization: Bearer $IAM_TOKEN"\
   -H "IBM-API-Version: 2025-02-01"\
   --data '{
  "name": "my-snapshot",
  "source_volume": {
    "id": "r006-1a6b7274-678d-4dfb-8981-c71dd9d4daa5"
    }
  }'
```
{: pre}

The snapshot names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Snapshot names must begin with a lowercase letter. It must not begin with a hypen or a number nor end with a hyphen. If you create two snapshots with the same name in the same deployment and region, a `snapshot name duplicate` error is displayed.
{: tip}

A successful response looks like this:

```json

{   "id": "r134-f5505e26-3f1e-4c30-832f-dfbd2b36f450",  
    "href": "http://example.com/aeiou",   
    "name": "my-snap1",   
    "source_volume": \
    {     "id": "r134-99c368a1-9595-4c78-9577-ce7980aefe0c",    
     "name": "my-vol1",     
     "resource_type": "volume"   }
,
  "created_at": "2025-06-13T14:39:09Z",
  "lifecycle_state": "pending",
  "minimum_capacity": 2000,
  "size": 1,
  "deletable": true,
  "resource_type": "snapshot"
}
```
{: screen}

## Creating a new snapshot from the CLI
{: #create-new-snapshot-cli}
{: cli}

To create a new snapshot, run the following command.

```sh
ibmcloud sds volume-snapshot-create -source-volume-id <volume-id> OR --source-volume (SOURCE-VOLUME | @SOURCE-VOLUME-FILE) --name  <snap-name>
```
{: pre}

`--source-volume-id <string>` OR `--source-volume <string>` are required.

See the following example.

```bash
ic sds volume-snapshot-create --source-volume-id r134-87a59338-a801-4090-a657-72867fc9ba44
...

id                 r134-9ede0937-511c-422e-b8e5-b65bb49ed1fd
href               https://sds-cephaas.dev3-8ce82ab061950a7b6121a1b00b849d81-0000.us-south.containers.appdomain.cloud/v1/snapshots/r134-9ede0937-511c-422e-b8e5-b65bb49ed1
                  fd
name               glamour-capillary-unknowing-tavern
created_at         2025-05-22T19:44:07.000Z
resource_type      snapshot
lifecycle_state    pending
size               1
minimum_capacity   1
deletable          true
source_volume
                  id              r134-87a59338-a801-4090-a657-72867fc9ba44
                  href            https://sds-cephaas.dev3-8ce82ab061950a7b6121a1b00b849d81-0000.us-south.containers.appdomain.cloud/volumes/r134-87a59338-a801-4090-a657
                                  -72867fc9ba44
                  name            alisha-vol-test
                  resource_type   volume
```
{: screen}

---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-24"


keywords: cli, command line reference, unified storage, sds, software-defined-storage

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}

# IBM Software Defined Storage as a Service CLI
{: #ic-sds-cli-reference}

The Software defined storage as a service (SDSaaS) plug-in extends the {{site.data.keyword.cloud_notm}} command line interface (CLI) with an API wrapper for working with unified storage resources.
{: shortdesc}

## Installation and configuration
{: #ic-sds-installation}

The plug-in is compatible with linux64, ppc64le, Windows&reg;, and macOS&reg; platforms that run on 64-bit processors.

Install the plug-in by using the `plugin install` command.

```sh
ibmcloud plugin install software-defined-storage
```


## Update the SDS plugin
{: #ic-update}

Update the plug-in by using the `plugin update` command.

```sh
ibmcloud plugin update software-defined-storage
```

## Command index
{: #ic-sds-command-index}

Each operation has an explanation of what it does, how to use it, and any optional or required parameters. Unless specified as optional, any listed parameters are mandatory.

The CLI plug-in doesn't yet support the full suite of features available in Software Defined Storage.
{: note}

### Retrieve a volume profile
{: #ic-sds-retrieve-volume-profile}

* **Action:** Retrieves a single volume profile specified by ID.
* **Usage:** `ibmcloud software-defined-storage volume --instanceid INSTANCEID --id ID`

* **Example**
	  ibmcloud software-defined-storage volume \
	    --instanceid exampleString \
	    --id exampleString

* **Parameters to provide:**
	* **--id**: Specify the volume profile id. Required.
	* **--instanceid**: Specify the service instance id. Required.

### Create a volume
{: #ic-sds-create-volume}

* **Action:** Create a new volume.
* **Usage:** `ibmcloud software-defined-storage volume-create [--capacity CAPACITY] [--name NAME] [--sdsaas-instance-id SDSAAS-INSTANCE-ID] [--hostnqnstring HOSTNQNSTRING]`

* **Example**
	  ibmcloud software-defined-storage volume-create \
	    --capacity 40 \
	    --name my-volume \
	    --sdsaas-instance-id exampleString \
	    --hostnqnstring exampleString

* **Parameters to provide:**
	* **--capacity**: Specify the capacity of the volume (in gigabytes).
	* **--hostnqnstring**: The host nqn.
	* **--instanceid**: Specify the service instance id.
	* **--name**: Name of the volume.
	* **--sdsaas-instance-id**: The service instance ID where the volume will be created in.


### Update a volume
{: #ic-sds-update-volume}

* **Action:** Update a volume with the information in provided volume patch.
* **Usage:** `ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID [--volume-patch VOLUME-PATCH] [--if-match IF-MATCH]`

* **Example**
	ibmcloud software-defined-storage volume-update \
	  --instanceid exampleString \
	  --id exampleString \
	  --if-match exampleString \
	  --capacity 38 \
	  --name exampleString

* **Parameters to provide:**
	* **--capacity**: The capacity of the volume (in gigabytes).
	* **--id**: The volume profile id. Required.
	* **--if-match**: If present, the request will fail if the specified ETag value does not match the resource's current ETag value.
	* **--instanceid**: The service instance id.
	* **--name**: The name of the volume.
	* **--volume-patch**: JSON object containing volume information.


### Delete a volume
{: #ic-sds-delete-volume}

* **Action:** Deletes a single volume profile based on the name.
* **Usage:** `ibmcloud software-defined-storage volume-delete --instanceid INSTANCEID --id ID [--if-match IF-MATCH]`

* **Parameters to provide:**
	* **--id**: The volume profile id. _**Required**_.
	* **--if-match**: If present, the request will fail if the specified ETag value does not match the resource's current ETag value.
	* **--instanceid**: The service instance id.


### List all volumes
{: #ic-sds-list-volumes}

Volumes are network-connected block storage devices that may be attached to one or more service instances in the same region..

* **Action:** Run this command to list summary information about all volumes  .
* **Usage:** `ibmcloud software-defined-storage volumes [--instanceid INSTANCEID]`

* **Parameters to provide:**
	* **--instanceid**: The service instance id. Required.

* **Global options:**
	* **-h, --help** Show help
	* **-j, --jmes-query** Provide a JMESPath query as a string to customize output.
	* **--output** Choose an output format - can be 'json', 'yaml', 'tui', or 'table'. (default "table")
	* **-q, --quiet** Suppresses verbose messages.
	* **--url** API Endpoint

## Next Steps
{: #cli-ref-next-steps}

Run `ibmcloud sds --help` for more information about which commands you could run.

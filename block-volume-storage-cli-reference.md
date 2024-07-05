---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-05"


keywords: cli, command line reference, unified storage, sds, software-defined-storage

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}

# IBM Software Defined Storage as a Service CLI
{: #ic-sds-cli-reference}

The Software defined storage as a service (SDSaaS) plug-in extends the {{site.data.keyword.cloud_notm}} command line interface (CLI) with an API wrapper for working with unified storage resources.
{: shortdesc}


## Before you begin
{: #before-creating-block-volume-cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the SDS CLI plug-in.

Log in to the IBM Cloud.

```sh
ibmcloud login --sso -a cloud.ibm.com
```
{: pre}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.
{: pre}


### Installation and configuration
{: #ic-sds-installation}

The plug-in is compatible with linux64, ppc64le, Windows&reg;, and macOS&reg; platforms that run on 64-bit processors.

Install the plug-in by using the `plugin install` command.

```sh
ibmcloud plugin install software-defined-storage
```


### Update the SDS plugin
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

## Block volume commands

### Create a volume
{: #ic-sds-create-volume}

Create a new volume.

**Usage:**

```sh
ibmcloud software-defined-storage volume-create [--capacity CAPACITY] [--name NAME] [--sdsaas-instance-id SDSAAS-INSTANCE-ID] [--hostnqnstring HOSTNQNSTRING]
```

**Example**

```sh
ibmcloud software-defined-storage volume-create \
	--capacity 40 \
	--name my-volume \
	--sdsaas-instance-id exampleString \
	--hostnqnstring exampleString
```
**Parameters to provide:**
* **--capacity**: Specify the capacity of the volume (in gigabytes).
* **--hostnqnstring**: The host nqn.
* **--instanceid**: Specify the service instance id.
* **--name**: Name of the volume.
* **--sdsaas-instance-id**: The service instance ID where the volume will be created in.


### Retrieve a volume profile
{: #ic-sds-retrieve-volume-profile}

Retrieves a single volume profile specified by ID.

**Usage:**

```sh
ibmcloud software-defined-storage volume --instanceid INSTANCEID --id ID
```
**Example**

```sh
ibmcloud software-defined-storage volume \
	--instanceid exampleString \
	--id exampleString
```

**Parameters to provide:**
* **--id**: Specify the volume profile id. Required.
* **--instanceid**: Specify the service instance id. Required.


### Update a volume
{: #ic-sds-update-volume}

Update a volume with the information in provided volume patch.

**Usage:**

```sh
ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID [--volume-patch VOLUME-PATCH] [--if-match IF-MATCH]
```

**Example**

```sh
ibmcloud software-defined-storage volume-update \
	--instanceid exampleString \
	--id exampleString \
	--if-match exampleString \
	--capacity 38 \
	--name exampleString
```


**Parameters to provide:**
* **--capacity**: The capacity of the volume (in gigabytes).
* **--id**: The volume profile id. Required.
* **--if-match**: If present, the request will fail if the specified ETag value does not match the resource's current ETag value.
* **--instanceid**: The service instance id.
* **--name**: The name of the volume.
* **--volume-patch**: JSON object containing volume information.


### Delete a volume
{: #ic-sds-delete-volume}

Deletes a single volume profile based on the name.

**Usage:**

```sh
ibmcloud software-defined-storage volume-delete --instanceid INSTANCEID --id ID [--if-match IF-MATCH]
```

**Parameters to provide:**
* **--id**: The volume profile id. _**Required**_.
* **--if-match**: If present, the request will fail if the specified ETag value does not match the resource's current ETag value.
* **--instanceid**: The service instance id.


### List all volumes
{: #ic-sds-list-volumes}

Lists the summary information about all volumes.

**Usage:**
```sh
ibmcloud software-defined-storage volumes [--instanceid INSTANCEID]
```

**Parameters to provide:**
* **--instanceid**: The service instance id. Required.




## Account management commands
{: #sds-account-mgmt-cmd}

### Create service credential
{: #ic-sds-create-service-cred}

Updates credentials for a storage account or creates them if they do not exist.

**Usage:**

```sh
ibmcloud software-defined-storage cred-create --instanceid INSTANCEID --access-key ACCESS-KEY
```
**Example**
```sh
ibmcloud software-defined-storage cred-create \
	--instanceid exampleString \
	--access-key exampleString
```

**Aliases:** cred-create, crc

**Parameters to provide:**
* **--instanceid**: The service instance id. Required.
* **--access-key**: Access key to update or set. Required.




### Retrieve certificate details
{: #ic-sds-retrieve-cert-details}

Retrieves the S3 SSL certificate expiration date and status.

**Usage:**

```sh
ibmcloud software-defined-storage certificate --instanceid INSTANCEID
```

**Aliases:** certificate, crts

**Parameters to provide:**
* **--instanceid**: The service instance id. Required.



## Next Steps
{: #cli-ref-next-steps}

Run `ibmcloud sds --help` for more information about which commands you could run.

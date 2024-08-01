---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-01"


keywords: cli, command line reference, unified storage, sds, software-defined-storage

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}

# IBM SDSaaS CLI reference
{: #ic-sds-cli-reference}

The IBM Storage Ceph as a Service plug-in extends the {{site.data.keyword.cloud_notm}} command line interface (CLI) with an API wrapper for working with unified storage resources.
{: shortdesc}


## Before you begin
{: #before-creating-block-volume-cli}

Before you can use the SDS CLI plug-in, you must first install the IBM Cloud CLI, login to the CLI and then install the SDS CLI plug-in. For instruction on how to install IBM Cloud CLI, see [Getting started with the IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started)

Log in to the IBM Cloud.

```sh
ibmcloud login --sso -a cloud.ibm.com
```
{: pre}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.



### Installation and configuration
{: #ic-sds-installation}

The plug-in is compatible with linux64, Windows&reg;, and macOS&reg; platforms that run on 64-bit processors.

Install the plug-in by using the `plugin install` command.

```sh
ibmcloud plugin install software-defined-storage
```
{: pre}

### Update the SDS plugin
{: #ic-sds-update}

Update the plug-in by using the `plugin update` command.

```sh
ibmcloud plugin update software-defined-storage
```
{: pre}


## Command index
{: #ic-sds-command-index}

Each operation has an explanation of what it does, how to use it, and any optional or required parameters. Unless specified as optional, any listed parameters are mandatory.

The CLI plug-in doesn't yet support the full suite of features available in Software Defined Storage.
{: note}

## software-defined-storage
{: #ic-sds-plugin}

`software-defined-storage` -  an OpenAPI definition for the SDSaaS CLI.

**USAGE**:
```sh
ibmcloud software-defined-storage [command] [options]
```

**ALIASES**: software-defined-storage, sds


## Block volume
{: #sds-volume-cmds}

### Create a new volume
{: #ic-sds-create-volume}

**Usage:**

```sh
ibmcloud software-defined-storage volume-create --instanceid INSTANCEID [--capacity CAPACITY] [--name NAME] [--sdsaas-instance-id SDSAAS-INSTANCE-ID] [--hostnqnstring HOSTNQNSTRING]
```
**Aliases**: volume-create, volc

**Example**

```sh
ibmcloud software-defined-storage volume-create \
	--capacity 40 \
	--name my-volume \
	--sdsaas-instance-id exampleString \
	--hostnqnstring exampleString
```
**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* [Optional] Specify the capacity of the volume (in gigabytes).
	* Flag: `--capacity CAPACITY`

* [Optional] Name of the volume.
	* Flag: `--name NAME`

	If you do not specify a name for the new volume, the system generates a name which is a hyphenated list of randomly-selected words.
	{: note}

* [Optional] Sets the service instance ID where the volume will be created in.
	* Flag: `--sdsaas-instance-id SDSAAS-INSTANCE-ID`

* [Optional] The host NVMe Qualified Name
	* Flag: `--hostnqnstring HOSTNQNSTRING`


### Retrieve a single volume profile
{: #ic-sds-retrieve-volume-profile}

**Usage:**

```sh
ibmcloud software-defined-storage volume --instanceid INSTANCEID --id ID
```
**Aliases**: volume, vol

**Example**

```sh
ibmcloud software-defined-storage volume \
	--instanceid exampleString \
	--id exampleString
```

**Parameters to provide:**
* Specify the volume profile id.
	* Flag: `--id ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`


### Update a volume
{: #ic-sds-update-volume}

Update a volume with the information in provided volume patch.

**Usage:**

```sh
ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID [--volume-patch VOLUME-PATCH] [--if-match IF-MATCH]
```

**Aliases**: volume-update, volu

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

* The volume profile ID.
	* Flag:`--id ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* [Optional] Specify the capacity of the volume (in gigabytes).
	* Flag: `--capacity CAPACITY`

* [Optional] Name of the volume.
	* Flag: `--name NAME`

* [Optional] JSON object containing volume information.
	* Flag: `--volume-patch VOLUME-PATCH`

* [Optional] A string value if provided then the query will fail when the specified ETag value does not match the resource's current ETag value.
	* Flag: `--if-match IF-MATCH`


### Delete a single volume
{: #ic-sds-delete-volume}

**Usage:**

```sh
ibmcloud software-defined-storage volume-delete --instanceid INSTANCEID --id ID [--if-match IF-MATCH]
```
**Aliases**: volume-delete, vold

**Example**

```sh
ibmcloud software-defined-storage volume-delete \
	--instanceid exampleString \
    --id exampleString \
    --if-match exampleString
```

**Parameters to provide:**

* The volume profile ID.
	* Flag:`--id ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* [Optional] A string value if provided then the query will fail when the specified ETag value does not match the resource's current ETag value.
	* Flag: `--if-match IF-MATCH`


### List all volumes
{: #ic-sds-list-volumes}

**Usage:**
```sh
ibmcloud software-defined-storage volumes [--instanceid INSTANCEID]
```

**Aliases**: volumes, vols

**Example**

```sh
ibmcloud software-defined-storage volumes \
    --instanceid exampleString
```

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`


## Hosts
{: #ic-sds-hosts}

### Create new host
{: #ic-sds-create-host-from-template}

**Usage:**

```sh
ibmcloud software-defined-storage host-create --instanceid INSTANCEID --nqn NQN [--name NAME] [--volume-mappings VOLUME-MAPPINGS]
```

**Aliases**: host-create, hstc

**Example**

```sh
ibmcloud software-defined-storage host-create \
    --instanceid exampleString \
    --nqn nqn.abc.1234 \
    --name my-host \
    --volume-mappings '[{"volume_id": "exampleString"}]'
```

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Provide the NVME Qualifier Name (NQN) of the host configured in customer's environment. The maximum length is 64 characters.
	* Flag: `--nqn NQN`

* [Optional] Specify the name for the new host. Ensure that the new name is unique.
	* Flag: `--name NAME`

	If you do not specify a name for the new volume, the system generates a name which is a hyphenated list of randomly-selected words.
	{: note}

* Specify the unique identifier of the volume to be mapped to this host.  Must be in the form `['volume_id':'1a6b7274-678d-4dfb-8981-c71dd9d4daa5']`.
	* Flag: `--volume-mappings VOLUME-MAPPINGS`


### Retrieve a single host
{: #ic-sds-retrieve-host-profile}

**Usage:**

```sh
ibmcloud software-defined-storage host --host-id HOST-ID --instanceid INSTANCEID
```


**Example**

```sh
ibmcloud software-defined-storage host \
    --host-id exampleString \
    --instanceid exampleString
```

**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`



### List all hosts
{: #ic-sds-list-all-hosts}

**Usage:**

```sh
ibmcloud software-defined-storage hosts --instanceid INSTANCEID [--start START] [--limit LIMIT] [--name NAME]
```

**Aliases**: hosts, hsts

**Example**

```sh
ibmcloud software-defined-storage hosts \
    --instanceid exampleString \
    --start exampleString \
    --limit 10 \
    --name exampleString
```

**Parameters to provide:**

* Specify the service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Specify the server-provided token for determining what resource to start the page on.
	* Flag: `--start START`

* Specify the number of resources to return on a page.
	* Flag: `--limit LIMIT`

* Including this option will filter the collection of resources by name.
	* Flag: `--name NAME`

* Including this option will display all pages of the collection for hosts.
	* Flag: `--all-pages`



### Update a host
{: #ic-sds-update-host}

**Usage:**

```sh
ibmcloud software-defined-storage host-update --host-id HOST-ID --instanceid INSTANCEID [--host-patch HOST-PATCH]
```

**Aliases**: host-update, hstu

**Example**

```sh
ibmcloud software-defined-storage host-update \
    --host-id exampleString \
    --instanceid exampleString \
    --name my-host
```

**Parameters to provide:**

* Specify the host id whose details you want to update
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* [Optional] Specify the JSON Merge-Patch content for `host_update`.
	* Flag: `--host-patch HOST-PATCH`

* [Optional] Specify the name for the new host. Ensure that the new name is unique.
	* Flag: `--name NAME`

	If you do not specify a name for the new volume, the system generates a name which is a hyphenated list of randomly-selected words.
	{: note}


### Map volume to a host
{: #ic-sds-map-volume-to-host}

**Usage:**

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID
```

**Aliases**: host-vol-update, hstvidu

**Example**

```sh
ibmcloud software-defined-storage host-vol-update \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString
```

**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Specify the unique volume identifier.
	* Flag: `--volume-id VOLUME-ID`


### Delete a host
{: #ic-sds-delete-host}

**Usage:**

```sh
ibmcloud software-defined-storage host-delete --host-id HOST-ID --instanceid INSTANCEID
```

**Aliases**: host-delete, hstd

**Example**

```sh
ibmcloud software-defined-storage host-delete \
	--host-id exampleString \
    --instanceid exampleString
```

**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`


### Delete a single volume from a host
{: #ic-sds-delete-single-volume-from-host}

**Usage:**

```sh
ibmcloud software-defined-storage host-volid-delete --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID
```

**Aliases**: host-volid-delete, hstvidd

**Example**

```sh
ibmcloud software-defined-storage host-volid-delete \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString
```

**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* Specify the service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Specify the unique volume identifier.
	* Flag: `--volume-id VOLUME-ID`


### Delete all volume mappings associated with a host
{: #ic-sds-delete-all-volume-mapped-to-host}

**Usage:**

```sh
ibmcloud software-defined-storage host-vol-deleteall --host-id HOST-ID --instanceid INSTANCEID
```

**Aliases**: host-vol-deleteall, hstvd

**Example**

```sh
ibmcloud software-defined-storage host-vol-deleteall \
    --host-id exampleString \
    --instanceid exampleString
```

**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`







## Account management
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
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Sets the access key for the service instance.
	* Flag: `--access-key ACCESS-KEY`

### Delete a service credential
{: #ic-sds-delete-service-cred}

**Usage:**

```sh
ibmcloud software-defined-storage cred-delete --instanceid INSTANCEID --access-key ACCESS-KEY
```
**Aliases**: cred-delete, crd

**Example**

```sh
ibmcloud software-defined-storage cred-create \
	--instanceid exampleString \
	--access-key exampleString
```

**Aliases:** cred-delete, crd

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Sets the access key for the service instance.
	* Flag: `--access-key ACCESS-KEY`

### List service credential
{: #ic-sds-list-service-cred}

Retrieves credentials for a specific storage account.

**Usage:**

```sh
ibmcloud software-defined-storage credentials --instanceid INSTANCEID
```
**Example**

```sh
ibmcloud software-defined-storage credentials \
    --instanceid exampleString
```

**Aliases:** credentials, crl

**Parameters to provide:**
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`


### Create or modify certificate
{: #ic-sds-upload-cert}

Updates the S3 SSL Certificates or creates them if they do not exist.

**Usage:**

```sh
ibmcloud software-defined-storage cert-upload --instanceid INSTANCEID --body BODY
```
**Example**

```sh
ibmcloud software-defined-storage cert-upload \
	--instanceid exampleString \
    --body exampleString
```
**Aliases:** cert-upload, crtu

**Parameters to provide:**
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* The request body containing the S3 TLS certificate. The body must be in string format with single quotes at the beginning and end of all cert data.
	* Flag: `--body BODY`


### Retrieve certificate details
{: #ic-sds-retrieve-cert-details}

Retrieves the S3 SSL certificate expiration date and status.

**Usage:**

```sh
ibmcloud software-defined-storage certificate --instanceid INSTANCEID
```

**Aliases:** certificate, crts

**Parameters to provide:**
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`



## Next steps
{: #cli-ref-next-steps}

Run `ibmcloud sds --help` for more information about which commands you could run.

---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-14"


keywords: cli, command-line reference, unified storage, sds, software-defined-storage

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cephaas_short}} CLI
{: #ic-sds-cli-reference}

The {{site.data.keyword.cephaas_full_notm}} plugin extends the {{site.data.keyword.cloud_notm}} command-line interface (CLI) to give you the ability to run commands that perform various operations for the service that includ but not limited to managing volumes, hosts, mappings, object credentials, and certificates.
{: shortdesc}


## Before you begin
{: #before-you-begin-using-cli}

Before you can use the {{site.data.keyword.cephaas_short}} CLI plug-in, you must first install the {{site.data.keyword.cloud_notm}} CLI, login to the CLI and then install the `software-defined-storage` CLI plug-in. For instruction on how to install the {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the IBM Cloud CLI](/docs/cli?topic=cli-getting-started)



## Installation and configuration
{: #ic-sds-installation}

The plug-in is compatible with linux64, Windows&reg;, and macOS&reg; platforms that run on 64-bit processors.

Install the plug-in by using the `plugin install` command.

```sh
ibmcloud plugin install software-defined-storage
```
{: pre}

Once the plug-in is installed, you can verify the installation by running the `help` command.

```sh
ibmcloud software-defined-storage help
```
{: pre}

The output lists the USAGE instructions and the supported commands.


## Updating the plug-in
{: #ic-sds-update}

Update the plug-in by using the `plugin update` command.

```sh
ibmcloud plugin update software-defined-storage
```
{: pre}

The latest plug-in version is downloaded and replaces your current plug-in service commands. If there are no updates available, the message `No updates are available` is displayed.

You're notified on the command-line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}



## Command index
{: #ic-command-index}

Each operation has an explanation of what it does, how to use it, and any optional or required parameters. Unless specified as optional, any listed parameters are mandatory.

The CLI plug-in doesn't yet support the full suite of features available in Software Defined Storage.
{: note}

### software-defined-storage
{: #ic-sds-plug-in}

`software-defined-storage` -  an OpenAPI definition for the cephaas CLI on IBM Cloud platform.

```sh
ibmcloud software-defined-storage [command] [options]
```
{: pre}

Aliases of `software-defined-storage`: sds


## Block storage
{: #block-storage-cmds}

### Create volume
{: #ic-create-volume}

```sh
ibmcloud sds volume-create --capacity CAPACITY [--name NAME] --url string
```
{: pre}

Aliases of `volume-create`: volc

Example

```sh
ibmcloud sds volume-create \
	--capacity 10 \
	--name my-volume \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).



**Parameters to provide:**

* Capacity of the volume (in gigabytes).
	* Flag: `--capacity CAPACITY`

* Name of the volume.
	* Flag: `--name NAME`

	If you do not specify a name for the new volume, the system generates a name which is a hyphenated list of randomly selected words.
	{: note}

* API Endpoint in the URL form.
	* Flag: `--url string`



### Retrieve a single volume details
{: #ic-retrieve-volume-details}

```sh
ibmcloud sds volume --volume-id VOLUME-ID --url string
```
{: pre}

Aliases of `volume`: vol

Example command:

```sh
ibmcloud sds volume \
	--volume-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

**Parameters to provide:**
* The volume identifier.
	* Flag: `--volume-id VOLUME-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Update a volume
{: #ic-update-volume}

Use `volume-update` command along with the new information provided in volume patch parameter to update the volume capacity or the volume name.

You can change only one parameter value at a time in the command. More than one change in the same command is not supported.
{: note}

```sh
ibmcloud sds volume-update --volume-id VOLUME-ID [--volume-patch VOLUME-PATCH | @VOLUME-PATCH-FILE] --url string
```
{: pre}

Aliases of `volume-update`: volu

Example command:

```sh
ibmcloud sds volume-update \
	--volume-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
	--capacity 38 \
	--name my-volume-updated \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

**Parameters to provide:**

* The volume identifier.
	* Flag:`--volume-id VOLUME-ID`

* Capacity of the volume (in gigabytes).
	* Flag: `--capacity CAPACITY`

* Name of the volume.
	* Flag: `--name NAME`

* [Optional] JSON object that contains the volume information such as a path to a JSON file.
	* Flag: `--volume-patch VOLUME-PATCH`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Delete a single volume
{: #ic-delete-volume}

```sh
ibmcloud sds volume-delete --volume-id VOLUME-ID --url string
```
{: pre}

Aliases of `volume-delete`: vold

Example command:

```sh
ibmcloud sds volume-delete \
	--volume-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

**Parameters to provide:**

* The volume identifier.
	* Flag:`--volume-id VOLUME-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### List all volumes
{: #ic-list-volumes}


```sh
ibmcloud sds volumes [--limit LIMIT] [--name NAME]
```
{: pre}

Aliases of `volumes`: vols

Example command:

```sh
ibmcloud sds volumes \
    --limit 10 \
    --name my-volume \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* The number of resources to return on a page. The default value is 1. Maximum limit value is 1000.
	* Flag: `--limit int`

* Filter by name from the resource collection. You can specify 0 to 200 characters in string length.
	* Flag: `--name string`




## Hosts
{: #ic-sds-hosts}

### Create new host
{: #ic-create-host-from-template}

```sh
ibmcloud sds host-create --name NAME --nqn NQN [--volume-mappings VOLUME-MAPPINGS | @VOLUME-MAPPINGS-FILE] --url string
```
{: pre}

Aliases of `host-create`: hstc

Example command:

```sh
ibmcloud sds host-create \
    --name my-host \
    --nqn nqn.2014-06.org:9345 \
    --volume-mappings '[{"volume": {"id": "1a6b7274-678d-4dfb-8981-c71dd9d4daa5"}}]' \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* NVMe Qualified Name (NQN) of the host configured in the customer's environment. The maximum supported length is 223 bytes.
	* Flag: `--nqn NQN`

* Name for the new host. Ensure that the new name is unique.
	* Flag: `--name NAME`

	If you do not specify a name for the new host, the system generates a name that is a hyphenated list of randomly selected words.
	{: note}

* The unique identifier of the volume to be mapped to this host. Must be in the form `[{"volume": {"id": "1a6b7274-678d-4dfb-8981-c71dd9d4daa5"}}]`.
	* Flag: `--volume-mappings VOLUME-MAPPINGS`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Retrieve a single host
{: #ic-retrieve-host-profile}

```sh
ibmcloud sds host --host-id HOST-ID --url string
```
{: pre}


Example command:

```sh
ibmcloud sds host \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to view
	* Flag: `--host-id HOST-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### List all hosts
{: #ic-sds-list-all-hosts}

```sh
ibmcloud sds hosts [--limit LIMIT] [--name NAME] --url string
```
{: pre}

Aliases of `hosts`: hsts

Example command:

```sh
ibmcloud sds hosts \
    --limit 10 \
    --name my-host \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Number of resources to return on a page.
	* Flag: `--limit LIMIT`

* Including this option filters the collection of resources by name.
	* Flag: `--name NAME`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Update a host
{: #ic-sds-update-host}

```sh
ibmcloud sds host-update --host-id HOST-ID [--host-patch HOST-PATCH | @HOST-PATCH-FILE] --url string
```
{: pre}

Aliases of `host-update`: hstu

Example command:

```sh
ibmcloud sds host-update \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
    --name my-host
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to update
	* Flag: `--host-id HOST-ID`

* [Optional] Specify the JSON Merge-Patch content for `host_update`.
	* Flag: `--host-patch HOST-PATCH`

* Name for the new host. Ensure that the new name is unique.
	* Flag: `--name NAME`

	If you do not specify a name for the new host, the system generates a name that is a hyphenated list of randomly-selected words.
	{: note}

* API Endpoint in the URL form.
	* Flag: `--url string`

### Map volume to a host
{: #ic-map-volume-to-host}


```sh
ibmcloud sds host-mapping-create --host-id HOST-ID [--volume (VOLUME | @VOLUME-FILE) | --volume-id VOLUME-ID]
```
{: pre}

Aliases of `host-mapping-create`: hstmc

Example command:

```sh
ibmcloud sds host-mapping-create \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
    --volume '{"id": "r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39"}' \
    --url $sds_endpoint
```
{: screen}

Or

```sh
ibmcloud sds host-mapping-create \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
    --volume-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* Specify the unique volume identifier.
	* Flag: `--volume-id VOLUME-ID`

* The unique identifier of the volume to be mapped to this host. Must be in the form `[{"volume": {"id": "1a6b7274-678d-4dfb-8981-c71dd9d4daa5"}}]`.
	* Flag: `--volume VOLUME-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### View all host-mappings for a host
{: #ic-view-all-host-mappings}

```sh
ibmcloud sds host-mappings --host-id HOST-ID
```
{: pre}

Aliases of `host-mappings`: hstms

Example command:

```sh
ibmcloud sds host-mappings \
	--host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to view
	* Flag: `--host-id HOST-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### View a single host mapping for a host
{: #ic-view-host-mapping}

```sh
ibmcloud sds host-mapping --host-id HOST-ID --volume-mapping-id VOLUME-MAPPING-ID
```
{: pre}

Aliases of `host-mapping`: hstm

Example command:

```sh
ibmcloud sds host-mapping \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
    --volume-mapping-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to view
	* Flag: `--host-id HOST-ID`

* Unique volume-mapping identifier. This can be found by viewing either the associated volume or host you'd like to complete this operation against
	* Flag: `--volume-mapping-id VOLUME-MAPPING_ID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Delete a host
{: #ic-delete-host}

```sh
ibmcloud sds host-delete --host-id HOST-ID --url string
```
{: pre}

Aliases of `host-delete`: hstd

Example command:

```sh
ibmcloud sds host-delete \
	--host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to view
	* Flag: `--host-id HOST-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Delete a single volume mapping from a host
{: #ic-delete-single-volume-from-host}

```sh
ibmcloud sds host-mapping-delete --host-id HOST-ID --volume-mapping-id VOLUME-MAPPING-ID
```
{: pre}

Aliases of `host-mapping-delete`: hstmd

Example command:

```sh
ibmcloud sds host-mapping-delete \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
    --volume-mapping-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to view
	* Flag: `--host-id HOST-ID`

* Unique volume-mapping identifier. This can be found by viewing either the associated volume or host you'd like to complete this operation against
	* Flag: `--volume-mapping-id VOLUME-MAPPING_ID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Delete all volume mappings associated with a host
{: #ic-delete-all-volume-mapped-to-host}

```sh
ibmcloud sds host-mapping-delete-all --host-id HOST-ID
```
{: pre}

Aliases of `host-vol-delete-all`: hstmda

Example command:

```sh
ibmcloud sds host-mapping-delete-all \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* Host ID whose details you want to view
	* Flag: `--host-id HOST-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`




## Object storage
{: #object-storage-cmds}

### Create service credential
{: #ic-create-service-cred}

Updates credentials for a storage account or creates them if they do not exist.

```sh
ibmcloud sds cred-create --access-key ACCESS-KEY --url string
```
{: pre}

Example command:

```sh
ibmcloud sds cred-create \
	--access-key mytestkey
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


Aliases of `cred-create`: crc

**Parameters to provide:**

* Sets the access key for the service instance.
	* Flag: `--access-key ACCESS-KEY`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Delete a service credential
{: #ic-delete-service-cred}

```sh
ibmcloud sds cred-delete --access-key ACCESS-KEY --url string
```
{: pre}

Example command:

```sh
ibmcloud sds cred-delete \
	--access-key mytestkey
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


Aliases of `cred-delete`: crd

**Parameters to provide:**

* Sets the access key for the service instance.
	* Flag: `--access-key ACCESS-KEY`

* API Endpoint in the URL form.
	* Flag: `--url string`

### List service credential
{: #ic-list-service-cred}

Retrieves credentials for a specific storage account.

```sh
ibmcloud sds creds --url string
```
{: pre}

Example command:

```sh
ibmcloud sds creds \
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


Aliases of `creds`: crl

**Parameters to provide:**

* API Endpoint in the URL form.
	* Flag: `--url string`

### View certificate types
{: #ic-cert-types}

Retrieves the list of configured SSL Certificates.

```sh
ibmcloud sds cert-types --url string
```
{: pre}

Example command:

```sh
ibmcloud sds cert-types \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


Aliases of `cert-types`: crtt

**Parameters to provide:**

* API Endpoint in the URL form.
	* Flag: `--url string`


### Create a certificate
{: #ic-create-cert}

Creates a new SSL Certificates if one does not exist.

```sh
ibmcloud sds cert-create --cert CERT --body BODY --url string
```
{: pre}

Example command:

```sh
ibmcloud sds cert-create \
    --cert s3 \
    --body tempdir/test-file.txt \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


Aliases of `cert-create`: crtc

**Parameters to provide:**

* The request body that contains the TLS certificate. The CLI accepts certificate file in `.pem` format.
	* Flag: `--body BODY`

* The certificate type that is to be used in the request. Acceptable values include - s3.
	* Flag: `--cert CERT`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Update a certificate
{: #ic-update-cert}

Updates the existing SSL Certificate.

```sh
ibmcloud sds cert-update --cert CERT --body BODY --url string
```
{: pre}

Example command:

```sh
ibmcloud sds cert-update \
  --cert s3 \
  --body tempdir/test-file.pem \
  --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


Aliases of `cert-update`: crtu

**Parameters to provide:**

* The request body that contains the TLS certificate. The CLI accepts certificate file in `.pem` format.
	* Flag: `--body BODY

* The certificate type that is to be used in the request. Acceptable values include - s3.
	* Flag: `--cert CERT`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Retrieve certificate details
{: #ic-retrieve-cert-details}

Retrieves the SSL certificate expiration date and status.

```sh
ibmcloud sds cert --cert CERT --url string
```
{: pre}


Example command:

```sh
ibmcloud sds cert \
	--cert s3
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* The certificate type that is to be used in the request. Acceptable values include - s3.
	* Flag: `--cert CERT`

* API Endpoint in the URL form.
	* Flag: `--url string`



### Delete certificate
{: #ic-delete-cert}

Deletes the SSL certificate.

```sh
ibmcloud sds cert-delete --cert CERT --url string
```
{: pre}

Aliases of `cert-delete`: crtd

Example command:

```sh
ibmcloud sds cert-delete \
	--cert s3
	--url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


**Parameters to provide:**

* The certificate type that is to be used in the request. Acceptable values include - s3.
	* Flag: `--cert CERT`

* API Endpoint in the URL form.
	* Flag: `--url string`






## Config commands
{: #ic-config-commands}

`Config` Command can be used for controlling or viewing persistent configuration of global options.

To control or view persistant configurations, run `ibmcloud sds config` command along with the global options to list, set, and unset the config values.

You can set the `url` variable such that you do not need to use the `--url` flag when using with the `sds` command.

```sh
ibmcloud sds config
```
{: pre}


Example for setting the url option.

```sh
pc@mac ~ % ibmcloud sds config set url http://sds-endpoint.satellite.cloud.ibm.com:33189/v1
OK
```
{: screen}


Example that shows how to use the command without the config set.

```sh
ibmcloud sds volumes --url $endpoint
```
{: pre}


Example shows how to use the command with the `url` configured.

```sh
ibmcloud sds volumes
```
{: pre}

**COMMAND OPTIONS**
{: #ic-config-command-options}

* `get` - Retrieves the currently set configured value of an option.

* `list` - Retrieves all the currently set configured values.

* `set` - Set a config value for an option.

* `unset` - Unset the config value of an option.



### Retrieve configuration values
{: #ic-get-config-values}

Use `get` option with `config` command to retrieve the currently set value for a specific option.

When `Get` option is used together with `url` option, the currently set value for the 'url' option is retrieved.

```sh
ibmcloud sds config get url
```
{: pre}

See example output.

```sh
pc@mac ~ % ibmcloud sds config get url
http://sds-endpoint.satellite.cloud.ibm.com:33189/v1
```
{: screen}

### List all configuration values
{: #ic-list-config-values}

Use `List` option with `config` command to retrieve and view all of the currently set configured values.

```sh
ibmcloud sds config list
```
{: pre}

See example output.

```sh
pc@mac ~ % ibmcloud sds config list
url
http://sds-endpoint.satellite.cloud.ibm.com:33189/v1
```
{: screen}


### Set new config values
{: #ic-set-config-values}

Use `set` option with `config` command to configure new values for a specific option.

```sh
ibmcloud sds config set [option]
```
{: pre}

When `set` option is used together with `url` option, the value for the 'url' option is set.

See example with `url` option.

```sh
pc@mac ~ % ibmcloud sds config set url http://sds-endpoint.satellite.cloud.ibm.com:33189/v1
OK
```
{: screen}


### Unset config values
{: #ic-unset-config-values}

Use `unset` option with `config` command to reset the current configured values for a specific option.

```sh
ibmcloud sds config unset [option]
```
{: pre}

When `unset` option is used together with `url` option, the currently configured value for the 'url' option is reset.

See example with `url` option.

```sh
ibmcloud sds config unset url
```
{: pre}

```sh
pc@mac ~ % ibmcloud sds config unset url
OK
```
{: screen}


## Next steps
{: #cli-ref-next-steps}

Run `ibmcloud sds --help` for more information about which commands you could run.

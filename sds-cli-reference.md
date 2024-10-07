---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-07"


keywords: cli, command line reference, unified storage, sds, software-defined-storage

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cephaas_short}} CLI
{: #ic-sds-cli-reference}

The {{site.data.keyword.cephaas_full_notm}} plug-in extends the {{site.data.keyword.cloud_notm}} command line interface (CLI) with an API wrapper for working with unified storage resources.
{: shortdesc}


## Before you begin
{: #before-you-begin-using-cli}

Before you can use the {{site.data.keyword.cephaas_short}} CLI plug-in, you must first install the {{site.data.keyword.cloud_notm}} CLI, login to the CLI and then install the SDS CLI plug-in. For instruction on how to install {{site.data.keyword.cloud_notm}} CLI, see [Getting started with the IBM Cloud CLI](/docs/cli?topic=cli-getting-started)

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

Once the plug-in is installed, you can verify the installation by running the `help` command.

```sh
ibmcloud software-defined-storage help
```
{: pre}

The output lists the USAGE instructions and the supported commands.




### Updating the plugin
{: #ic-sds-update}

Update the plug-in by using the `plugin update` command.

```sh
ibmcloud plugin update software-defined-storage
```
{: pre}

The latest plug-in version is downloaded and replaces your current plugin service commands. If there are no updates available, the message `No updates are available` is displayed.

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}



## Command index
{: #ic-command-index}

Each operation has an explanation of what it does, how to use it, and any optional or required parameters. Unless specified as optional, any listed parameters are mandatory.

The CLI plug-in doesn't yet support the full suite of features available in Software Defined Storage.
{: note}

## software-defined-storage
{: #ic-sds-plugin}

`software-defined-storage` -  an OpenAPI definition for the SDSaaS CLI.

**USAGE:**
```sh
ibmcloud software-defined-storage [command] [options]
```
{: pre}

**ALIASES**: software-defined-storage, sds


## Block storage
{: #block-storage-cmds}

### Create volume
{: #ic-create-volume}

**USAGE:**

```sh
ibmcloud software-defined-storage volume-create --instanceid INSTANCEID --capacity CAPACITY --name NAME --url string
```
{: pre}

**ALIASES**: volume-create, volc

**Example**

```sh
ibmcloud software-defined-storage volume-create \
	--instanceid sds-instance-1
	--capacity 40 \
	--name my-volume \
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Capacity of the volume (in gigabytes).
	* Flag: `--capacity CAPACITY`

* Name of the volume.
	* Flag: `--name NAME`

	If you do not specify a name for the new volume, the system generates a name which is a hyphenated list of randomly-selected words.
	{: note}


* API Endpoint in the URL form.
	* Flag: `--url string`

### Retrieve a single volume details
{: #ic-retrieve-volume-details}

**USAGE:**

```sh
ibmcloud software-defined-storage volume --instanceid INSTANCEID --id ID --url string
```
{: pre}

**ALIASES**: volume, vol

**Example**

```sh
ibmcloud software-defined-storage volume \
	--instanceid exampleString \
	--id exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**
* The volume identifier.
	* Flag: `--id ID`

* Service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Update a volume
{: #ic-update-volume}

Update a volume with the information in provided volume patch.

**USAGE:**

```sh
ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID  --capacity CAPACITY [--if-match IF-MATCH] --url string
```
{: pre}

**ALIASES**: volume-update, volu

**Example**

```sh
ibmcloud software-defined-storage volume-update \
	--instanceid exampleString \
	--id exampleString \
	--if-match exampleString \
	--capacity 38 \
	--name exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* The volume identifier.
	* Flag:`--id ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Capacity of the volume (in gigabytes).
	* Flag: `--capacity CAPACITY`

* Name of the volume.
	* Flag: `--name NAME`

* [Optional] JSON object that contains the volume information.
	* Flag: `--volume-patch VOLUME-PATCH`

* [Optional] A string value if provided then the query fails when the specified ETag value does not match the resource's current ETag value.
	* Flag: `--if-match IF-MATCH`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Delete a single volume
{: #ic-delete-volume}

**USAGE:**

```sh
ibmcloud software-defined-storage volume-delete --instanceid INSTANCEID --id ID --url string
```
{: pre}

**ALIASES**: volume-delete, vold

**Example**

```sh
ibmcloud software-defined-storage volume-delete \
	--instanceid exampleString \
	--id exampleString \
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* The volume identifier.
	* Flag:`--id ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* [Optional] A string value if provided then the query fails when the specified ETag value does not match the resource's current ETag value.
	* Flag: `--if-match IF-MATCH`

* API Endpoint in the URL form.
	* Flag: `--url string`


### List all volumes
{: #ic-list-volumes}

**USAGE:**
```sh
ibmcloud software-defined-storage volumes [--limit LIMIT] [--name NAME]
```
{: pre}

**ALIASES**: volumes, vols

**Example**

```sh
ibmcloud software-defined-storage volumes \
    --limit 10 \
    --name myhost1 \
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* The number of resources to return on a page. The default value is 1. Maximum limit value is 1000.
	* Flag: `--limit int`

* Filter by name from the resource collection. You can specify 0 to 200 characters in string length.
	* Flag: `--name string`




## Hosts
{: #ic-sds-hosts}

### Create new host
{: #ic-create-host-from-template}

**USAGE:**

```sh
ibmcloud software-defined-storage host-create --instanceid INSTANCEID --nqn NQN [--name NAME] [--volume-mappings VOLUME-MAPPINGS] --url string
```
{: pre}

**ALIASES**: host-create, hstc

**Example**

```sh
ibmcloud software-defined-storage host-create \
    --instanceid exampleString \
    --nqn nqn.2014-08.org.nvmexpress:uuid:abcd1234-1234-1234-1234-abcd1234abcd \
    --name my-host \
    --volume-mappings '[{"volume_id": "exampleString"}]'
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* NVMe Qualified Name (NQN) of the host configured in customer's environment. The maximum supported length is 223 bytes.
	* Flag: `--nqn NQN`

* Name for the new host. Ensure that the new name is unique.
	* Flag: `--name NAME`

	If you do not specify a name for the new host, the system generates a name that is a hyphenated list of randomly-selected words.
	{: note}

* The unique identifier of the volume to be mapped to this host.  Must be in the form `['volume_id':'1a6b7274-678d-4dfb-8981-c71dd9d4daa5']`.
	* Flag: `--volume-mappings VOLUME-MAPPINGS`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Retrieve a single host
{: #ic-retrieve-host-profile}

**USAGE:**

```sh
ibmcloud software-defined-storage host --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}


**Example**

```sh
ibmcloud software-defined-storage host \
    --host-id exampleString \
    --instanceid exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* Host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### List all hosts
{: #ic-sds-list-all-hosts}

**USAGE:**

```sh
ibmcloud software-defined-storage hosts --instanceid INSTANCEID [--start START] [--limit LIMIT] [--name NAME] --url string
```
{: pre}

**ALIASES**: hosts, hsts

**Example**

```sh
ibmcloud software-defined-storage hosts \
    --instanceid exampleString \
    --start exampleString \
    --limit 10 \
    --name exampleString
	--url $endpoint
```
{: screen}

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* The server-provided token for determining what resource to start the page on.
	* Flag: `--start START`

* Number of resources to return on a page.
	* Flag: `--limit LIMIT`

* Including this option filters the collection of resources by name.
	* Flag: `--name NAME`

* Including this option displays all pages of the collection for hosts.
	* Flag: `--all-pages`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Update a host
{: #ic-sds-update-host}

**USAGE:**

```sh
ibmcloud software-defined-storage host-update --host-id HOST-ID --instanceid INSTANCEID [--host-patch HOST-PATCH] --url string
```
{: pre}

**ALIASES**: host-update, hstu

**Example**

```sh
ibmcloud software-defined-storage host-update \
    --host-id exampleString \
    --instanceid exampleString \
    --name my-host
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* Host id whose details you want to update
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

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

**USAGE:**

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID --url string
```
{: pre}

**ALIASES**: host-vol-update, hstvidu

**Example**

```sh
ibmcloud software-defined-storage host-vol-update \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* Specify the host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Specify the unique volume identifier.
	* Flag: `--volume-id VOLUME-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Delete a host
{: #ic-delete-host}

**USAGE:**

```sh
ibmcloud software-defined-storage host-delete --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}

**ALIASES**: host-delete, hstd

**Example**

```sh
ibmcloud software-defined-storage host-delete \
	--host-id exampleString \
    --instanceid exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* Host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Delete a single volume from a host
{: #ic-delete-single-volume-from-host}

**USAGE:**

```sh
ibmcloud software-defined-storage host-volid-delete --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID --url string
```
{: pre}

**ALIASES**: host-volid-delete, hstvidd

**Example**

```sh
ibmcloud software-defined-storage host-volid-delete \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* Host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Unique volume identifier.
	* Flag: `--volume-id VOLUME-ID`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Delete all volume mappings associated with a host
{: #ic-delete-all-volume-mapped-to-host}

**USAGE:**

```sh
ibmcloud software-defined-storage host-vol-deleteall --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}

**ALIASES**: host-vol-deleteall, hstvd

**Example**

```sh
ibmcloud software-defined-storage host-vol-deleteall \
    --host-id exampleString \
    --instanceid exampleString
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**

* Host id whose details you want to view
	* Flag: `--host-id HOST-ID`

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* API Endpoint in the URL form.
	* Flag: `--url string`




## Object storage
{: #object-storage-cmds}

### Create service credential
{: #ic-create-service-cred}

Updates credentials for a storage account or creates them if they do not exist.

**USAGE:**

```sh
ibmcloud software-defined-storage cred-create --access-key ACCESS-KEY --url string
```
{: pre}

**Example**

```sh
ibmcloud software-defined-storage cred-create \
	--access-key mytestkey
	--url $sds_endpoint
```
{: screen}

**ALIASES:** cred-create, crc

**Parameters to provide:**
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Sets the access key for the service instance.
	* Flag: `--access-key ACCESS-KEY`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Delete a service credential
{: #ic-delete-service-cred}

**USAGE:**

```sh
ibmcloud software-defined-storage cred-delete --access-key ACCESS-KEY --url string
```
{: pre}

**Example**

```sh
ibmcloud software-defined-storage cred-delete \
	--access-key mytestkey
	--url $sds_endpoint
```
{: screen}

**ALIASES:** cred-delete, crd

**Parameters to provide:**

* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* Sets the access key for the service instance.
	* Flag: `--access-key ACCESS-KEY`

* API Endpoint in the URL form.
	* Flag: `--url string`

### List service credential
{: #ic-list-service-cred}

Retrieves credentials for a specific storage account.

**USAGE:**

```sh
ibmcloud software-defined-storage creds --instanceid INSTANCEID --url string
```
{: pre}

**Example**

```sh
ibmcloud software-defined-storage credentials \
	--instanceid examplestring \
	--url $sds_endpoint
```
{: screen}

**ALIASES:** creds, crl

**Parameters to provide:**
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* API Endpoint in the URL form.
	* Flag: `--url string`


### Create or modify certificate
{: #ic-upload-cert}

Updates the S3 SSL Certificates or creates them if they do not exist.

**USAGE:**

```sh
ibmcloud software-defined-storage cert-upload --body BODY --url string
```
{: pre}

**Example**

```sh
  ibmcloud software-defined-storage cert-upload \
    --body tempdir/certificate-file.pem \
	--url $sds_endpoint
```
{: screen}

**ALIASES:** cert-upload, crtu

**Parameters to provide:**

* The request body that contains the S3 TLS certificate. The CLI accepts certificate file in `.pem` format.
	* Flag: `--body BODY`

* API Endpoint in the URL form.
	* Flag: `--url string`

### Retrieve certificate details
{: #ic-retrieve-cert-details}

Retrieves the S3 SSL certificate expiration date and status.

**USAGE:**

```sh
ibmcloud software-defined-storage cert --instanceid INSTANCEID --url string
```
{: pre}

**Example**

```sh
ibmcloud software-defined-storage cert \
	--instanceid examplestring \
	--url $sds_endpoint
```
{: screen}

**Parameters to provide:**
* The service instance identifier.
	* Flag: `--instanceid INSTANCEID`

* API Endpoint in the URL form.
	* Flag: `--url string`




## Config commands
{: #ic-config-commands}

`Config` Command can be used for controlling or viewing persistent configuration of global options.

To control or view persistant configurations, you can run `ibmcloud sds config` command along with the global options to list, set and unset the config values.

You can set the `url` variable such that you do not need to use the `--url` flag when using with the `sds` command.


**USAGE:**

```sh
ibmcloud software-defined-storage config
```
{: pre}


This is an example for setting the url option.

```sh
pc@mac ~ % ibmcloud sds config set url http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
OK
```
{: screen}


This example shows how to use the command without the config set.

```sh
ibmcloud sds volumes --url $endpoint
```
{: pre}


This example shows how to use the command with the `url` configured.

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

Using `get` with `config` command allows you to retrieve the currently set value for a specific option.

When `Get` command is used together with `url` option, the currently set value for the 'url' option is retrieved.

**USAGE**

```sh
ibmcloud software-defined-storage config get url
```
{: pre}

See example.

```sh
pc@mac ~ % ibmcloud sds config get url
http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
```
{: screen}

### List all configuration values
{: #ic-list-config-values}

Using `List` with `config` command allows you to retrieve and view all of the currently set configured values.

**USAGE**

```sh
ibmcloud software-defined-storage config list
```
{: pre}

See example.

```sh
pc@mac ~ % ibmcloud sds config list url
url
http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
```
{: screen}


### Set new config values
{: #ic-set-config-values}

Using `set` with `config` command allows you to configure new values for a specific option.

**USAGE**

```sh
ibmcloud software-defined-storage config set [option]
```
{: pre}

When `set` command is used together with `url` option, the value for the 'url' option is set.

See example on with `url` option.

```sh
pc@mac ~ % ibmcloud sds config set url http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
OK
```
{: screen}


### Reset config values
{: #ic-unset-config-values}

Using `unset` with `config` command allows you to reset the current configured values for a specific option.

**USAGE**

```sh
ibmcloud software-defined-storage config set [option]
```
{: pre}

When `unset` command is used together with `url` option, the currently configured value for the 'url' option is reset.

See example on with `url` option.

```sh
ibmcloud software-defined-storage config unset url
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

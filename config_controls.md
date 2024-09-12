---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-12"

keywords: cephaas, configure, persistant, viewing, controls

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring persistant controls
{: #configure-controls}


The `Config` Command can be used for controlling or viewing persistent configuration of global options.

To control or view persistant configurations, you can run `ibmcloud sds config` command along with the global options to list, set and unset the config values.

You can set the `url` variable such that they do not need to use the `--url` flag when using with the `sds` command.


**USAGE:**

```sh
ibmcloud software-defined-storage config
```
{: pre}


This is an example for setting the url option.

```sh
ibmcloud sds config set url http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
OK
```
{: screen}


**COMMAND OPTIONS**
{: #ic-config-command-options}

* `get` - Retrieves the currently set config value of an option.

* `list` - Retrieves the currently set config values.

* `set` - Set a config value for an option.

* `unset` - Unset the config value of an option.



## Retrieving configuration values
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

## Listing all config values
{: #ic-list-config-values}

Using `List` with config command allows you to retrieve and view all of the currently set config values.

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


## Setting config values
{: #ic-set-config-values}

Using `set` with `config` command allows you to set new config values for a specific option.

**USAGE**

```sh
ibmcloud software-defined-storage config set [option]
```
{: pre}

When `set` command is used together with `url` option, the config value for the 'url' option is set.

See example on with `url` option.

```sh
pc@mac ~ % ibmcloud sds config set url http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
OK
```
{: pre}


## Resetting config values
{: #ic-unset-config-values}

Using `unset` with `config` command allows you to reset the current config values for a specific option.

**USAGE**

```sh
ibmcloud software-defined-storage config set [option]
```
{: pre}

When `unset` command is used together with `url` option, the currently config value for the 'url' option is reset.

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

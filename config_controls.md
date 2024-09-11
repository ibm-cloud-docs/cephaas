---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-11"

keywords: cephaas, configure, persistant, viewing, controls

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring persistant controls
{: #configure-controls}


To control or view persistant configurations, you can use `ibmcloud sds config` command .

You can set the url variable so that they do not need to use the `--url` flag.

For example, the configuration can be viewed using the list command. The url can then be set by the set command. Specific values can be retrieved using the get command

```sh
ibmcloud sds config list

```
{: pre}

```sh
ibmcloud sds config set url http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
OK
```
{: screen}


```sh
ibmcloud sds config list url http://c-01.private.eu-de.link.satellite.cloud.ibm.com:33189/v1
```
{: pre}

can be shortened to

```sh
ibmcloud sds volumes
```

## Reset variables
{: #unset-variables}

```sh
ibmcloud sds config unset url
OK
```
{: pre}

```sh
ibmcloud sds config list
url
```
{: pre}

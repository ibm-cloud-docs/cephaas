---

copyright:
 years: 2024, 2024
lastupdated: "2024-12-13"

keywords: object storage, go, sdk, {{site.data.keyword.cephaas_full_notm}}

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Using Go
{: #using-go}

The {{site.data.keyword.cephaas_full}} SDK for Go provides features to make the most of {{site.data.keyword.cephaas_full_notm}}.
{: shortdesc}

The {{site.data.keyword.cephaas_full_notm}} SDK for Go is comprehensive, with many features and capabilities that exceed the scope and space of the guide. For detailed class and method documentation, [see the Go API documentation](https://ibm.github.io/sds-go-sdk){: external}. Source code can be found in the [GitHub repository](https://github.com/IBM/sds-go-sdk){: external}.

## Getting the SDK
{: #go-get-sdk}

Use `go get` to retrieve the SDK to add it to your GOPATH workspace, or project's Go module dependencies. The SDK requires a minimum version of Go 1.10 and maximum version of Go 1.12. Future versions of Go will be supported once our quality control process has been completed.

```sh
go get github.com/IBM/sds-go-sdk/sdsaasv1
```
{: pre}

To update the SDK use `go get -u` to retrieve the latest version of the SDK.

```sh
go get -u github.com/IBM/sds-go-sdk/sdsaasv1
```
{: pre}

### Import packages
{: #go-import-packages}

After installing the SDK, import the packages that is required for the Go applications to use the SDK, as shown in the following example:

```sh
import (
	"github.com/IBM/sds-go-sdk/sdsaasv1"
)
```
{: codeblock}



## Code Examples
{: #go-code-examples}

### Creating a new volume
{: #go-new-volume}


```Go


```
{: codeblock}

### List available volumes
{: #go-list-volumes}

```Go


```
{: codeblock}


### Get volume details
{: #go-get-object}

```Go


```
{: codeblock}

### Delete a volume
{: #go-delete-volume}

```Go

```
{: codeblock}

### Delete multiple volumes
{: #go-multidelete}

```Go

```
{: codeblock}

### List hosts
{: #go-list-hosts}

```Go

```
{: codeblock}

### Before You Begin
{: #go-examples-prereqs}

The following items are necessary to create a volume or a host:

* A Key Protect service [provisioned](/docs/key-protect?topic=key-protect-provision)
* A Root key available (either [generated](/docs/key-protect?topic=key-protect-create-root-keys) or [imported](/docs/key-protect?topic=key-protect-import-root-keys))




## Next Steps
{: #go-next-steps}

If you haven't already, please see the detailed class and method documentation available at the [Go API documentation](https://ibm.github.io/ibm-sds-go-sdk/){: external}.

---

copyright:
 years: 2024, 2025
lastupdated: "2025-01-09"

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

### Before You Begin
{: #go-examples-prereqs}

The following items are necessary to create a volume or a host:

* A Ceph as a service instance [provisioned - TODO: Update link](/docs/key-protect?topic=key-protect-provision)
* TODO: Are there any other items that are required?

### Setup
{: #go-setup}

```Go
var (
	sdsaasService *sdsaasv1.SdsaasV1
)

func main() {

	authenticator := &core.IamAuthenticator{
		ApiKey: <apiKey>,
	}

	sdsaasServiceOptions := &sdsaasv1.SdsaasV1Options{
		URL:           <serviceEndpoint>,
		Authenticator: authenticator,
	}

	sdsaasService, err = sdsaasv1.NewSdsaasV1(sdsaasServiceOptions)
	if err != nil {
		panic(err)
	}
}

```
{: codeblock}

### Creating a new volume
{: #go-new-volume}


```Go
	volumeCreateOptions := sdsaasService.NewVolumeCreateOptions(
		int64(5),
	)
	volumeCreateOptions.SetName("my-volume")

	volume, _, err := sdsaasService.VolumeCreate(volumeCreateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### List available volumes
{: #go-list-volumes}

```Go
	volumesOptions := sdsaasService.NewVolumesOptions()
	volumesOptions.SetLimit(int64(10))

	volumeCollection, _, err := sdsaasService.Volumes(volumesOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Printing out a collection of volumes")
	for _, volume := range volumeCollection.Volumes {
		fmt.Println("Volume: ", *volume.Name, "    Volume ID: ", *volume.ID)
	}
```
{: codeblock}

### Updating a volume
{: #go-update-volume}


```Go
	volumeUpdateOptions := sdsaasService.NewVolumeUpdateOptions(
		*volume.ID,
	)

	volumePatch := map[string]interface{}{
		"name": "my-volume-updated",
	}

	volumeUpdateOptions.SetVolumePatch(volumePatch)

	volume, _, err = sdsaasService.VolumeUpdate(volumeUpdateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Get volume details
{: #go-get-object}

```Go
	volumeOptions := sdsaasService.NewVolumeOptions(
		*volume.ID,
	)

	volume, _, err = sdsaasService.Volume(volumeOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Printing out volume ", *volume.Name)
	fmt.Println("Volume: ", *volume.Name, "    Volume ID: ", *volume.ID)

```
{: codeblock}

### Delete a volume
{: #go-delete-volume}

```Go
	volumeDeleteOptions := sdsaasService.NewVolumeDeleteOptions(
		*volume.ID,
	)
	_, err = sdsaasService.VolumeDelete(volumeDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Create a host
{: #go-create-host}

```Go
	hostCreateOptions := sdsaasService.NewHostCreateOptions(
		<hostNQN>,
	)

	hostCreateOptions.SetName("my-host")

	host, _, err := sdsaasService.HostCreate(hostCreateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### List hosts
{: #go-list-hosts}

```Go
	hostsOptions := sdsaasService.NewHostsOptions()
	hostsOptions.SetLimit(int64(10))

	hostCollection, _, err := sdsaasService.Hosts(hostsOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Printing out a collection of hosts")
	for _, host := range hostCollection.Hosts {
		fmt.Println("Host: ", *host.Name, "    Host ID: ", *host.ID)
	}
```
{: codeblock}

### Updating a host
{: #go-update-host}

```Go
	hostUpdateOptions := sdsaasService.NewHostUpdateOptions(
		*host.ID,
	)

	hostPatch := map[string]interface{}{
		"name": "my-host-updated",
	}

	hostUpdateOptions.SetHostPatch(hostPatch)

	host, _, err = sdsaasService.HostUpdate(hostUpdateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Get host details
{: #go-host-details}

```Go
	hostOptions := sdsaasService.NewHostOptions(
		*host.ID,
	)

	host, _, err = sdsaasService.Host(hostOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Printing out host ", *host.Name)
	fmt.Println("Host: ", *volume.Name, "    Host ID: ", *host.ID)
```
{: codeblock}

### Map a host to a volume
{: #go-host-map}


```Go
	hostVolUpdateOptions := sdsaasService.NewHostVolUpdateOptions(
		*host.ID,
		*volume.ID,
	)

	host, _, err = sdsaasService.HostVolUpdate(hostVolUpdateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Unmap a host from a volume
{: #go-host-unmap}


```Go
	hostVolDeleteOptions := sdsaasService.NewHostVolDeleteOptions(
		*host.ID,
		*volume.ID,
	)

	_, err = sdsaasService.HostVolDelete(hostVolDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Delete a host
{: #go-host-delete}


```Go
	hostDeleteOptions := sdsaasService.NewHostDeleteOptions(
		*host.ID,
	)

	_, err = sdsaasService.HostDelete(hostDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Credential create
{: #go-cred-create}


```Go
	credCreateOptions := sdsaasService.NewCredCreateOptions(
		"test-key",
	)

	credentialsUpdated, _, err := sdsaasService.CredCreate(credCreateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Credentials list
{: #go-cred-list}


```Go
	credsOptions := sdsaasService.NewCredsOptions()

	credentialsFound, _, err := sdsaasService.Creds(credsOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate list
{: #go-cert-list}


```Go
	certOptions := sdsaasService.NewCertOptions()

	certificateFound, response, err := sdsaasService.Cert(certOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

## Next Steps
{: #go-next-steps}

If you haven't already, please see the detailed class and method documentation available at the [Go API documentation](https://ibm.github.io/ibm-sds-go-sdk/){: external}.

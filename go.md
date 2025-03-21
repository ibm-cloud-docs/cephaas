---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-21"

keywords: object storage, go, sdk, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Using Go
{: #using-go}

The {{site.data.keyword.cephaas_full}} SDK for GO provides features to make the most of {{site.data.keyword.cephaas_full_notm}}.
{: shortdesc}

The {{site.data.keyword.cephaas_full_notm}} SDK for GO is comprehensive, with many features and capabilities that exceed the scope and space of the guide. For detailed class and method documentation, see the GO API documentation for [Block Storage](/apidocs/block-storage?code=go){: external} and [Object Storage](/apidocs/object-storage?code=go){: external}. Source code can be found in the [GitHub repository](https://github.com/IBM/sds-go-sdk){: external}.



## Getting the SDK
{: #go-get-sdk}

Use `go get` to retrieve the SDK and add it to your GOPATH workspace, or project's GO module dependencies. The SDK requires a minimum version of GO 1.21 or above. Future versions of GO will be supported once our quality control process has been completed. For more information, see the GO API documentation for [Block Storage](/apidocs/block-storage?code=go){: external} and [Object Storage](/apidocs/object-storage?code=go){: external}.

```sh
go get github.com/IBM/sds-go-sdk/sdsaasv1
```
{: pre}

To update the SDK use `go get -u` to retrieve the latest version of the SDK.

```sh
go get -u github.com/IBM/sds-go-sdk/sdsaasv1
```
{: pre}

The SDK Go github links mentioned in the examples will work only post General Availability (GA).
{: important}


### Import packages
{: #go-import-packages}

After installing the SDK, import the packages that are required for the GO applications to use the SDK, as shown in the following example.

```sh
import (
	"github.com/IBM/sds-go-sdk/sdsaasv1"
)
```
{: codeblock}



## Before you begin using code examples
{: #go-examples-prereqs}

The following items are necessary to create or modify volume or host details:

* An {{site.data.keyword.cephaas_full_notm}} deployment instance
* A service endpoint associated with the deployment
* API Key



## Code Examples
{: #go-code-examples}


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

	sdsaasService, err := sdsaasv1.NewSdsaasV1(sdsaasServiceOptions)
	if err != nil {
		panic(err)
	}
}

```
{: codeblock}

### Creating new volume
{: #go-new-volume}


```Go
	volumeCreateOptions := sdsaasService.NewVolumeCreateOptions(
		int64(5),
	)
	volumeCreateOptions.SetName("my-volume")

	volume, response, err := sdsaasService.VolumeCreate(volumeCreateOptions)
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

	volumeCollection, response, err := sdsaasService.Volumes(volumesOptions)
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

	volume, response, err := sdsaasService.VolumeUpdate(volumeUpdateOptions)
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

	volume, response, err := sdsaasService.Volume(volumeOptions)
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
	response, err = sdsaasService.VolumeDelete(volumeDeleteOptions)
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

	host, response, err := sdsaasService.HostCreate(hostCreateOptions)
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

	hostCollection, response, err := sdsaasService.Hosts(hostsOptions)
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

	host, response, err := sdsaasService.HostUpdate(hostUpdateOptions)
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

	host, response, err := sdsaasService.Host(hostOptions)
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

	volumeIdentityModel := &sdsaasv1.VolumeIdentity{
		ID: volume.ID,
	}

	hostMappingCreateOptions := sdsaasService.NewHostMappingCreateOptions(
		*host.ID,
		volumeIdentityModel,
	)

	volumeMapping, response, err := sdsaasService.HostMappingCreate(hostMappingCreateOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Host mapping created")
	fmt.Println("Volume ID: ", *volumeMapping.Volume.ID)
	fmt.Println("Host ID: ", *volumeMapping.Host.ID)
	fmt.Println("Volume mapping ID: ", *volumeMapping.ID)
```
{: codeblock}

### View all host mappings
{: #go-host-mappings}

```Go
	hostMappingsOptions := sdsaasService.NewHostMappingsOptions(
		*host.ID,
	)

	volumeMappingCollection, response, err := sdsaasService.HostMappings(hostMappingsOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Printing out a collection of host mappings")
	for _, mapping := range volumeMappingCollection.VolumeMappings {
		fmt.Println("Host ID: ", *mapping.Host.ID)
		fmt.Println("Volume ID: ", *mapping.Volume.ID)
		fmt.Println("Volume mapping ID: ", *mapping.ID)
		fmt.Println()
	}
```
{: codeblock}

### View a specific host mapping
{: #go-host-mapping}

```Go
	hostMappingOptions := sdsaasService.NewHostMappingOptions(
		*host.ID,
		<VOLUME-MAPPING-ID>,
	)

	volumeMapping, response, err := sdsaasService.HostMapping(hostMappingOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Host mapping")
	fmt.Println("Volume ID: ", *volumeMapping.Volume.ID)
	fmt.Println("Host ID: ", *volumeMapping.Host.ID)
	fmt.Println("Volume mapping ID: ", *volumeMapping.ID)

```
{: codeblock}

### Unmap a host from a volume
{: #go-host-unmap}


```Go
	hostMappingDeleteOptions := sdsaasService.NewHostMappingDeleteOptions(
		*host.ID,
		<VOLUME-MAPPING-ID>,
	)

	response, err := sdsaasService.HostMappingDelete(hostMappingDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Unmap all mappings from a host
{: #go-host-unmap-all}

```Go
	hostMappingDeleteAllOptions := sdsaasService.NewHostMappingDeleteAllOptions(
		*host.ID,
	)

	_, err = sdsaasService.HostMappingDeleteAll(hostMappingDeleteAllOptions)
	if err != nil {
		panic(err)
	}
```

### Delete a host
{: #go-host-delete}


```Go
	hostMappingDeleteAllOptions := sdsaasService.NewHostMappingDeleteAllOptions(
		*host.ID,
	)

	response, err := sdsaasService.HostMappingDeleteAll(hostMappingDeleteAllOptions)
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

### Credential delete
{: #go-cred-delete}


```Go
	credDeleteOptions := sdsaasService.NewCredDeleteOptions(
		"test-key",
	)

	response, err := sdsaasService.CredDelete(credDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate types list
{: #go-cert-list}


```Go

	certTypesOptions := sdsaasService.NewCertTypesOptions()

	certificateList, response, err := sdsaasService.CertTypes(certTypesOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate create
{: #go-cert-create}


```Go
	certCreateOptions := sdsaasService.NewCertCreateOptions(
		"s3",
		CreateMockReader("This is a mock file."),
	)

	certificateUpdated, response, err := sdsaasService.CertCreate(certCreateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate list
{: #go-list-certs}


```Go
	certOptions := sdsaasService.NewCertOptions()

	certificateFound, response, err := sdsaasService.Cert(certOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate update
{: #go-cert-update}


```Go
	certUpdateOptions := sdsaasService.NewCertUpdateOptions(
		"s3",
		CreateMockReader("This is a mock file."),
	)

	certificateUpdated, response, err := sdsaasService.CertUpdate(certUpdateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate delete
{: #go-cert-delete}


```Go
	certDeleteOptions := sdsaasService.NewCertDeleteOptions(
		"s3",
	)

	response, err := sdsaasService.CertDelete(certDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}




## Next Steps
{: #go-next-steps}

If you haven't already, see the detailed class and method documentation available at the GO API documentation for [Block Storage](/apidocs/block-storage?code=go){: external} and [Object Storage](/apidocs/object-storage?code=go){: external}.

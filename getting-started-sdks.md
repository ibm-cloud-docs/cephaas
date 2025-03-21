---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-19"

keywords: ceph as a storage, sdk, guide

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Getting Started with the SDKs
{: #getting-started-sdk}

{{site.data.keyword.cephaas_full}} provides an SDK for GO, which can help you to make the most of {{site.data.keyword.cephaas_short}}.
{: shortdesc}

This Quick Start guide provides a code example that demonstrates the following operations:

* Create a new volume or host
* List the available volumes or hosts
* Retrieve all volumes or hosts
* Modify volume or host details
* Map or unmap volume to host
* Delete a volume or hosts

## Before you begin
{: #sdk-gs-prereqs}

You need:

* An [{{site.data.keyword.cloud}} Platform account](https://cloud.ibm.com/login)
* An [{{site.data.keyword.cephaas_full_notm}} deployment](/docs/cephaas?topic=cephaas-administrators&interface=ui#provision-deployment)
* An [IAM API key](/docs/cephaas?topic=cephaas-iam-overview) to allow the SDK to access your account

## Getting the SDK
{: #sdk-gs-install}

Specific instructions for downloading and installing the SDK are available in [Using Go](/docs/cephaas?topic=cephaas-using-go){: external}{: go}.


## Code Example
{: #sdk-gs-example}

The code example provides introductory examples of running the basic operations with {{site.data.keyword.cos_short}}. For simplicity, the code example can be run multiple times as it uses Universally Unique Identifiers (UUIDs) for bucket or item names to prevent potential conflicts.

In your code, you must remove the angled brackets or any other excess characters that are provided here as an illustration.
{: note}

To complete the code example, you need to replace the following values:

|Value|Description|Example|
|---|---|---|
|`<service-endpoint>`|Regional endpoint for your {{site.data.keyword.cephaas_short}} instance|`s3.us-south.software-defined-storage.appdomain.cloud`|
|`<apikey>`|IAM API Key with at least `Writer` permissions|`xxxd12V2QHXbjaM99G9tWyYDgF_0gYdlQ8aWALIQxXx4`|
|`<resource-instance-id>`|Unique ID for the Service Instance|`crn:v1:bluemix:public:software-defined-storage:global:a/xx999cd94a0dda86fd8eff3191349999:9999b05b-x999-4917-xxxx-9d5b326a1111::`|
{: caption="Code value variable descriptions" caption-side="bottom"}

For more information about endpoints, see [Endpoints and storage locations](/docs/cephaas?topic=cephaas-endpoints).


``` Go
package main

import (
	"fmt"
	"os"
	"time"

	"github.com/IBM/go-sdk-core/core"
	"github.com/IBM/sds-go-sdk/sdsaasv1"
)

var (
	sdsaasService *sdsaasv1.SdsaasV1
)

const (
	apiKey          = "<apikey>"
	serviceEndpoint = "<service-endpoint>"
)

func main() {

	var err error

	newVolume := "volume1"
	newHost := "host1"
	hostNQN := "nqn.2014-06.org:9345"

	// Create sds service

	authenticator := &core.IamAuthenticator{
		ApiKey: apiKey,
	}

	sdsaasServiceOptions := &sdsaasv1.SdsaasV1Options{
		URL:           serviceEndpoint,
		Authenticator: authenticator,
	}

	sdsaasService, err = sdsaasv1.NewSdsaasV1(sdsaasServiceOptions)
	if err != nil {
		exitErrorf("Unable to create sds service %v", err)
	}

	// Volume create

	volumeCreateOptions := sdsaasService.NewVolumeCreateOptions(
		int64(5),
	)
	volumeCreateOptions.SetName(newVolume)

	fmt.Printf("Creating new volume %q...\n", newVolume)

	volume, _, err := sdsaasService.VolumeCreate(volumeCreateOptions)
	if err != nil {
		exitErrorf("Unable to create sds volume %q, %v", newVolume, err)
	}

	time.Sleep(5 * time.Second)

	// Host create

	hostCreateOptions := sdsaasService.NewHostCreateOptions(
		hostNQN,
	)

	hostCreateOptions.SetName("my-host")

	fmt.Printf("Creating new host %q...\n", newHost)

	host, _, err := sdsaasService.HostCreate(hostCreateOptions)
	if err != nil {
		exitErrorf("Unable to create sds host %q, %v", newHost, err)
	}

	time.Sleep(5 * time.Second)

	// Assign volume to host

	volumeIdentityModel := &sdsaasv1.VolumeIdentity{
		ID: volume.ID,
	}

	hostMappingCreateOptions := sdsaasService.NewHostMappingCreateOptions(
		*host.ID,
		volumeIdentityModel,
	)

	fmt.Printf("Assigning volume %q to host %q...\n", newVolume, newHost)

	_, _, err = sdsaasService.HostMappingCreate(hostMappingCreateOptions)
	if err != nil {
		exitErrorf("Unable to assign sds host %q to sds volume %q, %v", newHost, newVolume, err)
	}

	time.Sleep(5 * time.Second)

	// Display host and volume

	volumeOptions := sdsaasService.NewVolumeOptions(
		*volume.ID,
	)
	volume, _, err = sdsaasService.Volume(volumeOptions)
	if err != nil {
		panic(err)
	}

	fmt.Printf("\nGetting volume %q\n", newVolume)
	fmt.Printf("Volume ID: %q\n", *volume.ID)
	fmt.Printf("Volume Name: %q\n", *volume.Name)
	fmt.Printf("Volume capacity: %d\n", *volume.Capacity)
	fmt.Printf("Volume mapping ID: %q\n", *volume.VolumeMappings[0].ID)
	fmt.Printf("Volume mapping Host ID: %q\n", *volume.VolumeMappings[0].Host.ID)
	fmt.Printf("Volume mapping Name: %q\n", *volume.VolumeMappings[0].Host.Name)

	hostOptions := sdsaasService.NewHostOptions(
		*host.ID,
	)
	host, _, err = sdsaasService.Host(hostOptions)
	if err != nil {
		exitErrorf("Unable to get sds host %q, %v", newHost, err)
	}

	fmt.Printf("\nGetting host %q\n", newHost)
	fmt.Printf("Host ID: %q\n", *host.ID)
	fmt.Printf("Host Name: %q\n", *host.Name)
	fmt.Printf("Host VolumeMapping ID: %q\n\n", *host.VolumeMappings[0].ID)

	// Remove host and volume assignment

	fmt.Printf("Removing assignment from volume %q...\n", newVolume)

	hostMappingDeleteOptions := sdsaasService.NewHostMappingDeleteOptions(
		*host.ID,
		*host.VolumeMappings[0].ID,
	)

	_, err = sdsaasService.HostMappingDelete(hostMappingDeleteOptions)
	if err != nil {
		exitErrorf("Unable to delete host %q assigment between volume %q, %v", newHost, newVolume, err)
	}

	time.Sleep(5 * time.Second)

	// Volume Delete
	fmt.Printf("Deleting volume %q...\n", newVolume)

	volumeDeleteOptions := sdsaasService.NewVolumeDeleteOptions(
		*volume.ID,
	)

	_, err = sdsaasService.VolumeDelete(volumeDeleteOptions)
	if err != nil {
		exitErrorf("Unable to create sds volume %q, %v", newVolume, err)
	}

	// Host Delete
	fmt.Printf("Deleting host %q...\n", newHost)

	hostDeleteOptions := sdsaasService.NewHostDeleteOptions(
		*host.ID,
	)

	_, err = sdsaasService.HostDelete(hostDeleteOptions)
	if err != nil {
		exitErrorf("Unable to delete host %q, %v", newHost, err)
	}
}

func exitErrorf(msg string, args ...interface{}) {
	fmt.Fprintf(os.Stderr, msg+"\n", args...)
	os.Exit(1)
}
```
{: pre}
{: go}

## Running the Code Example
{: #sdk-gs-run}

To run the code sample, copy the preceding code blocks and run the following command.

``` sh
go run go_example.go
```
{: pre}
{: go}

## Output from the code example
{: #sdk-gs-output}

The output from the code example resembles:

```go
Creating new volume "volume1"...
Creating new host "host1"...
Assigning volume "volume1" to host "host1"...

Getting volume "volume1"
Volume ID: "r134-221e4eb4-ed0c-4165-957b-8a54e65829f4"
Volume Name: "volume1"
Volume capacity: 5
Volume mapping ID: "r134-106ff4ca-4564-4f07-abcd-4dc8c819af00"
Volume mapping Host ID: "r134-d7369321-da97-4998-948c-ddecefa7d39f"
Volume mapping Name: "my-host"

Getting host "host1"
Host ID: "r134-d7369321-da97-4998-948c-ddecefa7d39f"
Host Name: "my-host"
Host volume mapping ID "r134-106ff4ca-4564-4f07-abcd-4dc8c819af00" for volume %!q(*string=0x1400018f6b0)

Removing assignment from volume "volume1"...
Deleting volume "volume1"...
Deleting host "host1"...
```
{: pre}
{: go}

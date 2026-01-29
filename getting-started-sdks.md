---

copyright:
 years: 2024, 2026
lastupdated: "2026-01-29"

keywords: ceph as a storage, sdk, guide

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Getting Started with the SDKs
{: #getting-started-sdk}

{{site.data.keyword.cephaas_full}} provides an SDK for GO, which can help you to make the most of  {{site.data.keyword.cephaas_full_notm}}.
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
|`<service-endpoint>`|Regional endpoint for your  {{site.data.keyword.cephaas_full_notm}} instance|`s3.us-south.software-defined-storage.appdomain.cloud`|
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
	"github.com/IBM/sds-go-sdk/v2/sdsaasv2"
)

var (
	sdsaasService *sdsaasv2.SdsaasV2
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

	sdsaasServiceOptions := &sdsaasv2.SdsaasV2Options{
		URL:           serviceEndpoint,
		Authenticator: authenticator,
	}

	sdsaasService, err = sdsaasv2.NewSdsaasV2(sdsaasServiceOptions)
	if err != nil {
		exitErrorf("Unable to create sds service %v", err)
	}

	// Volume create

	createVolumeOptions := sdsaasService.NewCreateVolumeOptions(
		int64(5),
	)
	createVolumeOptions.SetName(newVolume)

	fmt.Printf("Creating new volume %q...\n", newVolume)

	volumeSummary, _, err := sdsaasService.CreateVolume(createVolumeOptions)
	if err != nil {
		exitErrorf("Unable to create sds volume %q, %v", newVolume, err)
	}

	time.Sleep(5 * time.Second)

	// Host create

	createHostOptions := sdsaasService.NewCreateHostOptions(
		hostNQN,
	)

	createHostOptions.SetName("my-host")

	fmt.Printf("Creating new host %q...\n", newHost)

	hostSummary, _, err := sdsaasService.CreateHost(createHostOptions)
	if err != nil {
		exitErrorf("Unable to create sds host %q, %v", newHost, err)
	}

	time.Sleep(5 * time.Second)

	// Assign volume to host

	volumeIdentityModel := &sdsaasv2.VolumeIdentity{
		ID: volumeSummary.ID,
	}

	hostMappingCreateOptions := sdsaasService.NewCreateVolumeMappingOptions(
		*hostSummary.ID,
		volumeIdentityModel,
	)

	fmt.Printf("Assigning volume %q to host %q...\n", newVolume, newHost)

	_, _, err = sdsaasService.CreateVolumeMapping(hostMappingCreateOptions)
	if err != nil {
		exitErrorf("Unable to assign sds host %q to sds volume %q, %v", newHost, newVolume, err)
	}

	time.Sleep(5 * time.Second)

	// Display host and volume

	volumeOptions := sdsaasService.NewGetVolumeOptions(*volumeSummary.ID)

	volume, _, err := sdsaasService.GetVolume(volumeOptions)
	if err != nil {
		exitErrorf("Unable to get sds volume %q, %v", newVolume, err)
	}

	fmt.Printf("\nGetting volume %q\n", newVolume)
	fmt.Printf("Volume ID: %q\n", *volume.ID)
	fmt.Printf("Volume Name: %q\n", *volume.Name)
	fmt.Printf("Volume capacity: %d\n", *volume.Capacity)
	fmt.Printf("Volume mapping ID: %q\n", *volume.VolumeMappings[0].ID)
	fmt.Printf("Volume mapping Host ID: %q\n", *volume.VolumeMappings[0].Host.ID)
	fmt.Printf("Volume mapping Name: %q\n", *volume.VolumeMappings[0].Host.Name)

	hostOptions := sdsaasService.NewGetHostOptions(
		*hostSummary.ID,
	)
	host, _, err := sdsaasService.GetHost(hostOptions)
	if err != nil {
		exitErrorf("Unable to get sds host %q, %v", newHost, err)
	}

	fmt.Printf("\nGetting host %q\n", newHost)
	fmt.Printf("Host ID: %q\n", *host.ID)
	fmt.Printf("Host Name: %q\n", *host.Name)
	fmt.Printf("Host VolumeMapping ID: %q\n\n", *host.VolumeMappings[0].ID)

	// Remove host and volume assignment

	fmt.Printf("Removing assignment from volume %q...\n", newVolume)

	hostMappingDeleteOptions := sdsaasService.NewDeleteHostMappingOptions(
		*host.ID,
		*host.VolumeMappings[0].ID,
	)

	_, err = sdsaasService.DeleteHostMapping(hostMappingDeleteOptions)
	if err != nil {
		exitErrorf("Unable to delete host %q assigment between volume %q, %v", newHost, newVolume, err)
	}

	time.Sleep(5 * time.Second)

	// Volume Delete
	fmt.Printf("Deleting volume %q...\n", newVolume)

	deleteVolumeOptions := sdsaasService.NewDeleteVolumeOptions(
		*volume.ID,
	)

	_, err = sdsaasService.DeleteVolume(deleteVolumeOptions)
	if err != nil {
		exitErrorf("Unable to create sds volume %q, %v", newVolume, err)
	}

	// Host Delete
	fmt.Printf("Deleting host %q...\n", newHost)

	deleteHostOptions := sdsaasService.NewDeleteHostOptions(
		*host.ID,
	)

	_, err = sdsaasService.DeleteHost(deleteHostOptions)
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
go run main.go
Creating new volume "volume1"...
Creating new host "host1"...
Assigning volume "volume1" to host "host1"...

Getting volume "volume1"
Volume ID: "r134-deb1ed70-8811-4957-aa4f-53a910e97652"
Volume Name: "volume1"
Volume capacity: 5
Volume mapping ID: "r134-037a348b-7f35-4d46-bd18-27613bc8a50e"
Volume mapping Host ID: "r134-30edff08-01da-41fe-9f06-47156457aa30"
Volume mapping Name: "my-host"

Getting host "host1"
Host ID: "r134-30edff08-01da-41fe-9f06-47156457aa30"
Host Name: "my-host"
Host VolumeMapping ID: "r134-037a348b-7f35-4d46-bd18-27613bc8a50e"

Removing assignment from volume "volume1"...
Deleting volume "volume1"...
Deleting host "host1"...
```
{: pre}
{: go}

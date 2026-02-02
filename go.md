---

copyright:
 years: 2024, 2026
lastupdated: "2026-01-30"

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
go get github.com/IBM/sds-go-sdk/v2/sdsaasv2
```
{: pre}

To update the SDK use `go get -u` to retrieve the latest version of the SDK.

```sh
go get -u github.com/IBM/sds-go-sdk/v2/sdsaasv2
```
{: pre}

The SDK Go github links mentioned in the examples will work only post General Availability (GA).
{: important}


### Import packages
{: #go-import-packages}

After installing the SDK, import the packages that are required for the GO applications to use the SDK, as shown in the following example.

```sh
import (
	"github.com/IBM/sds-go-sdk/v2/sdsaasv2"
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
	sdsaasService *sdsaasv2.SdsaasV2
)

func main() {

	authenticator := &core.IamAuthenticator{
		ApiKey: <apiKey>,
	}

	sdsaasServiceOptions := &sdsaasv2.SdsaasV2Options{
		URL:           <serviceEndpoint>,
		Authenticator: authenticator,
	}

	sdsaasService, err := sdsaasv2.NewSdsaasV2(sdsaasServiceOptions)
	if err != nil {
		panic(err)
	}
}

```
{: codeblock}

### Creating new volume
{: #go-new-volume}


```Go
	createVolumeOptions := sdsaasService.NewCreateVolumeOptions(
		int64(5),
	)
	createVolumeOptions.SetName("my-volume")

	volumeSummary, response, err := sdsaasService.CreateVolume(createVolumeOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### List available volumes
{: #go-list-volumes}

```Go
	listVolumesOptions := sdsaasService.NewListVolumesOptions()
	listVolumesOptions.SetLimit(int64(10))

	volumeCollection, response, err := sdsaasService.ListVolumes(listVolumesOptions)
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
	volumePatch := map[string]interface{}{
		"name": "my-volume-updated",
	}

	updateVolumeOptions := sdsaasService.NewUpdateVolumeOptions(
		*volume.ID,
	)

	volume, response, err := sdsaasService.UpdateVolume(updateVolumeOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Get volume details
{: #go-get-object}

```Go
	volumeOptions := sdsaasService.NewGetVolumeOptions(
		*volumeSummary.ID,
	)

	volume, response, err := sdsaasService.GetVolume(volumeOptions)
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
	volumeDeleteOptions := sdsaasService.NewDeleteVolumeOptions(
		*volume.ID,
	)
	response, err = sdsaasService.DeleteVolume(volumeDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Create a volume snapshot
{: #go-create-volume-snapshot}

```Go
	sourceVolumeModel := &sdsaasv2.SourceVolume{
		ID: core.StringPtr(*volume.ID),
	}

	volumeSnapshotCreateOptions := sdsaasService.NewCreateSnapshotOptions(
		sourceVolumeModel,
	)

	snapshot, response, err := sdsaasService.CreateSnapshot(volumeSnapshotCreateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### List all volume snapshots
{: #go-list-volume-snapshot}

```Go
	listSnapshotsOptions := sdsaasService.NewListSnapshotsOptions()

	pager, err := sdsaasService.NewSnapshotsPager(listSnapshotsOptions)
	if err != nil {
		panic(err)
	}

	var allResults []sdsaasv2.Snapshot
	for pager.HasNext() {
		nextPage, err := pager.GetNext()
		if err != nil {
			panic(err)
		}
		allResults = append(allResults, nextPage...)
	}
	b, _ := json.MarshalIndent(allResults, "", "  ")
	fmt.Println(string(b))
```
{: codeblock}

### Update a volume snapshot
{: #go-update-volume-snapshot}

```Go
	snapshotPatchModel := &sdsaasv2.SnapshotPatch{
		Name: core.StringPtr("my-snapshot-updated"),
	}
	snapshotPatchModelAsPatch, asPatchErr := snapshotPatchModel.AsPatch()
	if asPatchErr != nil {
		panic(asPatchErr)
	}

	updateSnapshotOptions := sdsaasService.NewUpdateSnapshotOptions(
		*snapshot.ID,
		snapshotPatchModelAsPatch,
	)

	snapshot, response, err := sdsaasService.UpdateSnapshot(updateSnapshotOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### List a volume snapshot
{: #go-list-volume-snapshot}

```Go
	getSnapshotOptions := sdsaasService.NewGetSnapshotOptions(
		*snapshot.ID,
	)

	snapshot, _, err = sdsaasService.GetSnapshot(getSnapshotOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Restore a volume from a snapshot
{: #go-restore-volume-from-snapshot}

```Go
	volumeCreateOptions := sdsaasService.NewCreateVolumeOptions(
		int64(10),
	)
	volumeCreateOptions.SetName("volume-restored-from-snapshot")

	sourceSnapshot, err := sdsaasService.NewSourceSnapshot(*snapshot.ID)
	if err != nil {
		panic(err)
	}
	volumeCreateOptions.SetSourceSnapshot(sourceSnapshot)

	volumeSummary, response, err := sdsaasService.CreateVolume(volumeCreateOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Delete a volume snapshot
{: #go-delete-volume-snapshot}

```Go
	deleteSnapshotOptions := sdsaasService.NewDeleteSnapshotOptions(
		*snapshot.ID,
	)

	response, err := sdsaasService.DeleteSnapshot(deleteSnapshotOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Delete all snapshots related to a volume
{: #go-delete-snapshots-related-to-volume}

```Go
	volumeSnapshotsDeleteOptions := sdsaasService.NewDeleteSnapshotsOptions(
		<snap-id-1>,
		<snap-id-2>,
	)

	response, err := sdsaasService.DeleteSnapshots(volumeSnapshotsDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Create host
{: #go-create-host}

```Go
	createHostOptions := sdsaasService.NewCreateHostOptions(
		<hostNQN>,
	)

	createHostOptions.SetName("my-host")

	hostSummary, response, err := sdsaasService.CreateHost(createHostOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### List hosts
{: #go-list-hosts}

```Go
	hostsOptions := sdsaasService.NewListHostsOptions()
	hostsOptions.SetLimit(int64(10))

	hostCollection, response, err := sdsaasService.ListHosts(hostsOptions)
	if err != nil {
		panic(err)
	}

	fmt.Println("Printing out a collection of hosts")
	for _, host := range hostCollection.Hosts {
		fmt.Println("Host: ", *host.Name, "    Host ID: ", *host.ID)
	}
```
{: codeblock}

### Update host
{: #go-update-host}

```Go
	hostPatch := map[string]interface{}{
		"name": "my-host-updated",
	}

	updateHostOptions := sdsaasService.NewUpdateHostOptions(
		*hostSummary.ID,
		hostPatch,
	)

	host, response, err := sdsaasService.UpdateHost(updateHostOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Get host
{: #go-host-details}

```Go
	hostOptions := sdsaasService.NewGetHostOptions(
		*host.ID,
	)

	host, response, err := sdsaasService.GetHost(hostOptions)
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
	volumeIdentityModel := &sdsaasv2.VolumeIdentity{
		ID: volume.ID,
	}

	createVolumeMappingOptions := sdsaasService.NewCreateVolumeMappingOptions(
		*host.ID,
		volumeIdentityModel,
	)

	volumeMappingReference, response, err := sdsaasService.CreateVolumeMapping(createVolumeMappingOptions)
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
	volumeMappingOptions := sdsaasService.NewListVolumeMappingsOptions(
		*host.ID,
	)
	volumeMappingCollection, response, err := sdsaasService.ListVolumeMappings(volumeMappingOptions)
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
	getVolumeMappingOptions := sdsaasService.NewGetVolumeMappingOptions(
		*host.ID,
		<VOLUME-MAPPING-ID>,
	)

	volumeMapping, response, err := sdsaasService.HostMapping(getVolumeMappingOptions)
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
	hostDeleteOptions := sdsaasService.NewDeleteHostOptions(
		*host.ID,
	)
	_, err = sdsaasService.DeleteHost(hostDeleteOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Share create
{: #go-share-create}

```Go
	createShareOptions := sdsaasService.NewCreateShareOptions(
		int64(10),
	)

	share, response, err := sdsaasService.CreateShare(createShareOptions)
	if err != nil {
		panic(err)
	}
```

{: codeblock}

### Shares list
{: #go-shares-list}

```Go
	listSharesOptions := &sdsaasv2.ListSharesOptions{
		Limit: core.Int64Ptr(int64(20)),
	}

	pager, err := sdsaasService.NewSharesPager(listSharesOptions)
	if err != nil {
		panic(err)
	}
```

{: codeblock}

### Share list
{: #go-share-list}

```Go
	getShareOptions := sdsaasService.NewGetShareOptions(
		*share.ID,
	)

	share, response, err := sdsaasService.GetShare(getShareOptions)
	if err != nil {
		panic(err)
	}
```

{: codeblock}

### Share update
{: #go-share-update}

```Go
	sharePatchModel := &sdsaasv2.SharePatch{
		Name: core.StringPtr("my-share")
	}
	sharePatchModelAsPatch, asPatchErr := sharePatchModel.AsPatch()

	updateShareOptions := sdsaasService.NewUpdateShareOptions(
		*share.ID,
		sharePatchModelAsPatch,
	)

	share, response, err := sdsaasService.UpdateShare(updateShareOptions)
	if err != nil {
		panic(err)
	}
```

{: codeblock}

### Share delete
{: #go-share-delete}

```Go
	deleteShareOptions := &sdsaasv2.DeleteShareOptions{
		ShareID:     *share.ID,
		ForceDelete: core.BoolPtr(false),
	}

	response, err := sdsaasService.DeleteShare(deleteShareOptions)
```

{: codeblock}

### Mount-target create
{: #go-mt-create}

```Go
	cidrClientTypeModel := &sdsaasv2.CIDRClientType{
		CIDR: []string{"192.168.3.0/24"},
	}

	createMountTargetOptions := sdsaasService.NewCreateMountTargetOptions(
		*share.ID,
		"mountTargetName",
		cidrClientTypeModel,
	)

	mountTarget, response, err := sdsaasService.CreateMountTarget(createMountTargetOptions)
	if err != nil {
		panic(err)
	}
```

{: codeblock}

### Mount-targets list
{: #go-mts-list}

```Go
	listMountTargetsOptions := &sdsaasv2.ListMountTargetsOptions{
		ShareID: *share.ID,
	}

	listMountTargetsOptions.Start = nil
	listMountTargetsOptions.Limit = core.Int64Ptr(1)

	var allResults []sdsaasv2.MountTarget
	for {
		mountTargetCollection, response, err := sdsaasService.ListMountTargets(listMountTargetsOptions)
		Expect(err).To(BeNil())
		Expect(response.StatusCode).To(Equal(200))
		Expect(mountTargetCollection).ToNot(BeNil())
		allResults = append(allResults, mountTargetCollection.MountTargets...)

		listMountTargetsOptions.Start, err = mountTargetCollection.GetNextStart()
		Expect(err).To(BeNil())

		if listMountTargetsOptions.Start == nil {
			break
		}
	}

	fmt.Println("All mount-targest: ", allResults)
```

{: codeblock}

### Mount-target list
{: #go-mt-list}

```Go
	getMountTargetOptions := &sdsaasv2.GetMountTargetOptions{
		ShareID: *share.ID,
		MountID: *mount.ID,
	}

	mountTarget, response, err := sdsaasService.GetMountTarget(getMountTargetOptions)
```

{: codeblock}

### Mount-target update
{: #go-mt-update}

```Go
	cidrClientTypeModel := &sdsaasv2.CIDRClientType{
		CIDR: []string{"192.168.3.0/24"},
	}

	mountTargetPatchModel := &sdsaasv2.MountTargetPatch{
		Name:    core.StringPtr("mountTargetNameUpdated"),
		Clients: cidrClientTypeModel,
	}

	mountTargetPatchModelAsPatch, asPatchErr := mountTargetPatchModel.AsPatch()

	updateMountTargetOptions := &sdsaasv2.UpdateMountTargetOptions{
		ShareID: *share.ID,
		MountID: *mountTarget.ID,
		MountTargetPatch: mountTargetPatchModelAsPatch,
	}

	mountTarget, response, err := sdsaasService.UpdateMountTarget(updateMountTargetOptions)
```

{: codeblock}

### Mount-target delete
{: #go-mt-delete}

```Go
	deleteMountTargetOptions := &sdsaasv2.DeleteMountTargetOptions{
		ShareID: *share.ID,
		MountID: *mountTarget.ID,
	}

	response, err := sdsaasService.DeleteMountTarget(deleteMountTargetOptions)
```

{: codeblock}

### Volume-group create
{: #go-vg-create}

```Go
	volume1Model := &sdsaasv2.Volume1{
		ID: *volume.ID,
	}

	createVolumeGroupOptions := &sdsaasv2.CreateVolumeGroupOptions{
		Name:    core.StringPtr("my-volume-group"),
		Volumes: []sdsaasv2.Volume1{*volume1Model},
	}

	volumeGroup, response, err := sdsaasService.CreateVolumeGroup(createVolumeGroupOptions)
```

{: codeblock}

### Volume-groups list
{: #go-vgs-list}

```Go
	listVolumeGroupsOptions := &sdsaasv2.ListVolumeGroupsOptions{
		Start: *volumeGroup.ID,
	}

	listVolumeGroupsOptions.Start = nil
	listVolumeGroupsOptions.Limit = core.Int64Ptr(1)

	var allResults []sdsaasv2.VolumeGroup
	for {
		volumeGroupCollection, response, err := sdsaasService.ListVolumeGroups(listVolumeGroupsOptions)

		allResults = append(allResults, volumeGroupCollection.VolumeGroups...)

		listVolumeGroupsOptions.Start, err = volumeGroupCollection.GetNextStart()

		if listVolumeGroupsOptions.Start == nil {
			break
		}
	}

	fmt.Println("All volumeGroups: ", allResults)
```

{: codeblock}

### Volume-group list
{: #go-vg-list}

```Go
	getVolumeGroupOptions := &sdsaasv2.GetVolumeGroupOptions{
		VolumeGroupID: *volumeGroup.ID,
	}

	volumeGroup, response, err := sdsaasService.GetVolumeGroup(getVolumeGroupOptions)

```

{: codeblock}

### Volume-group update
{: #go-vg-update}

```Go
	volumeGroupPatchModel := &sdsaasv2.VolumeGroupPatch{
		Name: core.StringPtr("my-volume-group"),
	}
	volumeGroupPatchModelAsPatch, asPatchErr := volumeGroupPatchModel.AsPatch()

	updateVolumeGroupOptions := &sdsaasv2.UpdateVolumeGroupOptions{
		VolumeGroupID:    *volumeGroup.ID,
		VolumeGroupPatch: volumeGroupPatchModelAsPatch,
	}

	volumeGroup, response, err := sdsaasService.UpdateVolumeGroup(updateVolumeGroupOptions)
```

{: codeblock}

### Volume-group add volume
{: #go-vg-add-volume}

```Go
	createVolumeInVolumeGroupOptions := &sdsaasv2.CreateVolumeInVolumeGroupOptions{
		VolumeGroupID: *volumeGroup.ID,
		VolumeID:      *volume.ID,
	}

	volumeGroup, response, err := sdsaasService.CreateVolumeInVolumeGroup(createVolumeInVolumeGroupOptions)
```

{: codeblock}

### Volume-group delete volume
{: #go-vg-delete-volume}

```Go
	deleteVolumeFromVolumeGroupOptions := &sdsaasv2.DeleteVolumeFromVolumeGroupOptions{
		VolumeGroupID: *volumeGroup.ID,
		VolumeID:      *volume.ID,
	}

	response, err := sdsaasService.DeleteVolumeFromVolumeGroup(deleteVolumeFromVolumeGroupOptions)
```

{: codeblock}

### Volume-group delete
{: #go-vg-delete}

```Go
	deleteVolumeGroupOptions := &sdsaasv2.DeleteVolumeGroupOptions{
		VolumeGroupID: volumeGroup.ID,
	}

	response, err := sdsaasService.DeleteVolumeGroup(deleteVolumeGroupOptions)
```

{: codeblock}

### Credential create
{: #go-cred-create}

```Go
	createHmacCredentialsOptions := sdsaasService.NewCreateHmacCredentialsOptions(
		"test-key",
	)

	accessKeyResponse, response, err := sdsaasService.CreateHmacCredentials(createHmacCredentialsOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Credentials list
{: #go-cred-list}

```Go
	listHmacCredentialsOptions := sdsaasService.NewListHmacCredentialsOptions()

	storageCredResponse, response, err := sdsaasService.ListHmacCredentials(listHmacCredentialsOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Credential delete
{: #go-cred-delete}

```Go
	deleteHmacCredentialsOptions := sdsaasService.NewDeleteHmacCredentialsOptions(
		"test-key",
	)

	response, err := sdsaasService.DeleteHmacCredentials(deleteHmacCredentialsOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificates list
{: #go-cert-list}

```Go
	listCertificatesOptions := sdsaasService.NewListCertificatesOptions()

	certListResponse, response, err := sdsaasService.ListCertificates(listCertificatesOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate create
{: #go-cert-create}

```Go
	createSslCertOptions := sdsaasService.NewCreateSslCertOptions(
		"s3",
	)

	certResponse, response, err := sdsaasService.CreateSslCert(createSslCertOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate list
{: #go-list-certs}


```Go
	getS3SslCertStatusOptions := sdsaasService.NewGetS3SslCertStatusOptions(
		"s3",
	)

	statusResponse, response, err := sdsaasService.GetS3SslCertStatus(getS3SslCertStatusOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate update/replace
{: #go-cert-update}

```Go
	replaceSslCertOptions := sdsaasService.NewReplaceSslCertOptions(
		"s3",
	)

	certResponse, response, err := sdsaasService.ReplaceSslCert(replaceSslCertOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}

### Certificate delete
{: #go-cert-delete}

```Go
	deleteSslCertOptions := sdsaasService.NewDeleteSslCertOptions(
		"s3",
	)

	response, err := sdsaasService.DeleteSslCert(deleteSslCertOptions)
	if err != nil {
		panic(err)
	}
```
{: codeblock}


## Next Steps
{: #go-next-steps}

If you haven't already, see the detailed class and method documentation available at the GO API documentation for [Block Storage](/apidocs/block-storage?code=go){: external} and [Object Storage](/apidocs/object-storage?code=go){: external}.

---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-25"

keywords: ceph as a storage, sdk, guide

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Getting Started with the SDKs
{: #getting-started-sdk}

{{site.data.keyword.cephaas_full}} provides SDK for Go which can help you to make the most of {{site.data.keyword.cephaas_short}}.
{: shortdesc}

This Quick Start guide provides a code example that demonstrates the following operations:

* Create a new bucket
* List the available buckets
* Create a new text file
* List the available files
* Retrieve the text file contents
* Upload a large binary file
* Delete a file
* Delete a bucket

## Before you begin
{: #sdk-gs-prereqs}

You need:

* An [{{site.data.keyword.cloud}} Platform account](https://cloud.ibm.com/login)
* An [instance of {{site.data.keyword.cos_full_notm}}](/docs/cephaas?topic=cephaas-provision)
* An [IAM API key](/docs/cephaas?topic=cephaas-iam-overview) with Writer access to your {{site.data.keyword.cos_short}}

## Getting the SDK
{: #sdk-gs-install}

Specific instructions for downloading and installing the SDK is available in [Using Go](/docs/cephaas?topic=cephaas-using-go){: external}{: go}.

## Code Example
{: #sdk-gs-example}

The code examples below provide introductory examples of running the basic operations with {{site.data.keyword.cos_short}}. For simplicity, the code example can be run multiple times as it uses Universally Unique Identifiers (UUIDs) for bucket/item names to prevent potential conflicts.

In your code, you must remove the angled brackets or any other excess characters that are provided here as illustration.
{: note}

To complete the code example, you need to replace the following values:

|Value|Description|Example|
|---|---|---|
|`<endpoint>`|Regional endpoint for your COS instance|`s3.us-south.cloud-object-storage.appdomain.cloud`|
|`<api-key>`|IAM API Key with at least `Writer` permissions|`xxxd12V2QHXbjaM99G9tWyYDgF_0gYdlQ8aWALIQxXx4`|
|`<resource-instance-id>`|Unique ID for the Service Instance|`crn:v1:bluemix:public:cloud-object-storage:global:a/xx999cd94a0dda86fd8eff3191349999:9999b05b-x999-4917-xxxx-9d5b326a1111::`|
|`<storage-class>`|Storage class for a new bucket|`us-south-standard`|

For more information about endpoints, see [Endpoints and storage locations](/docs/cephaas?topic=cephaas-endpoints).


``` Go
package main
import (
    "bytes"
    "fmt"
    "github.com/IBM/ibm-cos-sdk-go/aws"
    "github.com/IBM/ibm-cos-sdk-go/aws/credentials/ibmiam"
    "github.com/IBM/ibm-cos-sdk-go/aws/session"
    "github.com/IBM/ibm-cos-sdk-go/service/s3"
    "io"
    "math/rand"
    "os"
    "time"
)

// Constants for IBM COS values
const (
    apiKey            = "<api-key>" // example: xxxd12V2QHXbjaM99G9tWyYDgF_0gYdlQ8aWALIQxXx4
    serviceInstanceID = "<resource-instance-id>" // example: crn:v1:bluemix:public:software-defined-storage:global:a/xx999cd94a0dda86fd8eff3191349999:9999b05b-x999-4917-xxxx-9d5b326a1111::
    authEndpoint      = "https://iam.cloud.ibm.com/identity/token"
    serviceEndpoint   = "<endpoint>" // example: https://s3.us-south.software-defined-storage.appdomain.cloud
)

// UUID
func random(min int, max int) int {
    return rand.Intn(max-min) + min
}

func main() {

    // UUID
    rand.Seed(time.Now().UnixNano())
    UUID := random(10, 2000)

    // Variables
    newBucket := fmt.Sprintf("%s%d", "go.bucket", UUID) // New bucket name
    objectKey := fmt.Sprintf("%s%d%s", "go_file_", UUID, ".txt") // Object Key
    content := bytes.NewReader([]byte("This is a test file from Go code sample!!!"))
    downloadObjectKey := fmt.Sprintf("%s%d%s", "downloaded_go_file_", UUID, ".txt") // Downloaded Object Key

    //Setting up a new configuration
    conf := aws.NewConfig().
        WithRegion("<storage-class>"). // Enter your storage class (LocationConstraint) - example: us-standard
        WithEndpoint(serviceEndpoint).
        WithCredentials(ibmiam.NewStaticCredentials(aws.NewConfig(), authEndpoint, apiKey, serviceInstanceID)).
        WithS3ForcePathStyle(true)

    // Create client connection
    sess := session.Must(session.NewSession()) // Creating a new session
    client := s3.New(sess, conf)               // Creating a new client

    // Create new bucket
    _, err := client.CreateBucket(&s3.CreateBucketInput{
        Bucket: aws.String(newBucket), // New Bucket Name
    })
    if err != nil {
        exitErrorf("Unable to create bucket %q, %v", newBucket, err)
    }

    // Wait until bucket is created before finishing
    fmt.Printf("Waiting for bucket %q to be created...\n", newBucket)

    err = client.WaitUntilBucketExists(&s3.HeadBucketInput{
        Bucket: aws.String(newBucket),
    })
    if err != nil {
        exitErrorf("Error occurred while waiting for bucket to be created, %v", newBucket)
    }

    fmt.Printf("Bucket %q successfully created\n", newBucket)

    // Retrieve the list of available buckets
    bklist, err := client.ListBuckets(nil)
    if err != nil {
        exitErrorf("Unable to list buckets, %v", err)
    }

    fmt.Println("Buckets:")

    for _, b := range bklist.Buckets {
        fmt.Printf("* %s created on %s\n",
            aws.StringValue(b.Name), aws.TimeValue(b.CreationDate))
    }

	// Uploading an object
	input3 := s3.CreateMultipartUploadInput{
		Bucket: aws.String(newBucket), // Bucket Name
		Key:    aws.String(objectKey), // Object Key
	}

	upload, _ := client.CreateMultipartUpload(&input3)

	uploadPartInput := s3.UploadPartInput{
		Bucket:     aws.String(newBucket), // Bucket Name
		Key:        aws.String(objectKey), // Object Key
		PartNumber: aws.Int64(int64(1)),
		UploadId:   upload.UploadId,
		Body:       content,
	}

	var completedParts []*s3.CompletedPart
	completedPart, _ := client.UploadPart(&uploadPartInput)

	completedParts = append(completedParts, &s3.CompletedPart{
		ETag:       completedPart.ETag,
		PartNumber: aws.Int64(int64(1)),
	})

	completeMPUInput := s3.CompleteMultipartUploadInput{
		Bucket: aws.String(newBucket), // Bucket Name
		Key:    aws.String(objectKey), // Object Key
		MultipartUpload: &s3.CompletedMultipartUpload{
			Parts: completedParts,
		},
		UploadId: upload.UploadId,
	}

	d, _ := client.CompleteMultipartUpload(&completeMPUInput)
	fmt.Println(d)

	// List objects within a bucket
	resp, err := client.ListObjects(&s3.ListObjectsInput{Bucket: aws.String(newBucket)})
	if err != nil {
		exitErrorf("Unable to list items in bucket %q, %v", newBucket, err)
	}
	for _, item := range resp.Contents {
		fmt.Println("Name:         ", *item.Key)          // Print the object's name
		fmt.Println("Last modified:", *item.LastModified) // Print the last modified date of the object
		fmt.Println("Size:         ", *item.Size)         // Print the size of the object
		fmt.Println("")
	}

	fmt.Println("Found", len(resp.Contents), "items in bucket", newBucket)


	// Download an object
	input4 := s3.GetObjectInput{
		Bucket: aws.String(newBucket), // The bucket where the object is located
		Key:    aws.String(objectKey), // Object you want to download
	}

	res, err := client.GetObject(&input4)
	if err != nil {
		exitErrorf("Unable to download object %q from bucket %q, %v", objectKey, newBucket, err)
	}

	f, _ := os.Create(downloadObjectKey)
	defer f.Close()
	io.Copy(f, res.Body)

	fmt.Println("Downloaded", f.Name())


	// Delete object within the new bucket
	_, err = client.DeleteObject(&s3.DeleteObjectInput{Bucket: aws.String(newBucket), Key: aws.String(objectKey)})
	if err != nil {
		exitErrorf("Unable to delete object %q from bucket %q, %v", objectKey, newBucket, err)
	}

	err = client.WaitUntilObjectNotExists(&s3.HeadObjectInput{
		Bucket: aws.String(newBucket),
		Key:    aws.String(objectKey),
	})
	if err != nil {
		exitErrorf("Error occurred while waiting for object %q to be deleted, %v", objectKey)
	}

	fmt.Printf("Object %q successfully deleted\n", objectKey)

	// Delete the new bucket
	// It must be empty or else the call fails
	_, err = client.DeleteBucket(&s3.DeleteBucketInput{
		Bucket: aws.String(newBucket),
	})
	if err != nil {
		exitErrorf("Unable to delete bucket %q, %v", newBucket, err)
	}

	// Wait until bucket is deleted before finishing
	fmt.Printf("Waiting for bucket %q to be deleted...\n", newBucket)

	err = client.WaitUntilBucketNotExists(&s3.HeadBucketInput{
		Bucket: aws.String(newBucket),
	})
	if err != nil {
		exitErrorf("Error occurred while waiting for bucket to be deleted, %v", newBucket)
	}

	fmt.Printf("Bucket %q successfully deleted\n", newBucket)
}


func exitErrorf(msg string, args ...interface{}) {
	fmt.Fprintf(os.Stderr, msg+"\n", args...)
	os.Exit(1)
```
{: codeblock}
{: go}

## Running the Code Example
{: #sdk-gs-run}

To run the code sample, copy the code blocks above and run the following:

``` sh
go run go_example.go
```
{: codeblock}
{: go}

## Output from the Code Example
{: #sdk-gs-output}

The output from the Code Example should resemble the following:

```go
Waiting for bucket "go.bucket645" to be created...
Bucket "go.bucket645" successfully created

Listing buckets:
* go.bucket645 created on 2019-03-10 13:25:12.072 +0000 UTC

{
  Bucket: "go.bucket645",
  ETag: "\"686d1d07d6de02e920532342fcbd6d2a-1\"",
  Key: "go_file_645.txt",
  Location: "http://s3.us.software-defined-storage.appdomain.cloud/go.bucket645/go_file_645.txt"
}

Name:          go_file_645.txt
Last modified: 2019-03-10 13:25:14 +0000 UTC
Size:          42

Found 1 items in bucket go.bucket645

Downloaded downloaded_go_file_645.txt

Object "go_file_645.txt" successfully deleted

Waiting for bucket "go.bucket645" to be deleted...
Bucket "go.bucket645" successfully deleted
```
{: codeblock}
{: go}

<br/>

---

copyright:
 years: 2024, 2026
lastupdated: "2026-01-22"

keywords: ceph as a service, known issues

subcollection: cephaas

---

# Object asynchronous disaster recovery
{: #object-async-dr}

The **Object async DR** feature in {{site.data.keyword.cephaas_full_notm}} enables asynchronous object storage replication between a primary instance and a secondary instance. This capability is designed to provide robust disaster recovery in the event of a catastrophic failure or site loss, ensuring data durability and business continuity.

## Secure communication between sites
{: #secure-com-bet-sites}

To facilitate secure communication between the primary and secondary sites, the following features are implemented:

- **TLS Encryption**: TLS certificates secure the replication connections between the sites. These certificates are issued for the domain `software-defined-storage.appdomain.cloud` and are rotated periodically to maintain security.

- **High availability and site management**: To ensure continuous availability between sites, load balancing is used. It allows traffic to seamlessly route across sites, even during upgrades or node outages, minimizing service disruption.

Site fail overs are fully managed by IBM, ensuring operational consistency.

## Supported operations
{: #supported-ops}

Credential operations and quota modifications are restricted to the primary site which users can perform via the UI, CLI, or API. 

## Monitoring multisite DR with UI
{: #monitoring-multisite}

The {{site.data.keyword.cephaas_full_notm}} UI includes monitoring capabilities based on replication performance. **Multi-site** tab of the object storage dashboard displays the following graphs:

- Replication throughput: Measures the data transfer rate during replication.



## Potential capacity mismatch in multisite DR
{: #capacity-mismatch}

You may notice a mismatch between the used capacity reported on the primary and secondary sites in the asynchronous disaster recovery setup.

This issue occurs due to failed multipart uploads. Multipart uploads allow large objects to be uploaded in parts, but if the upload fails, each uploaded part still contributes to the object count and used capacity on the primary site. These failed uploads are not replicated to the secondary site because replication only occurs after a successful upload. As a result, the primary site may report higher used capacity compared to the secondary site.

### Identifying failed multipart uploads
{: #identifying-failed-multipart}

Use the AWS CLI to list incomplete multipart uploads:

```sh
aws s3api --endpoint-url <endpoint> list-multipart-uploads --bucket <bucket-name>
```
{: codeblock}

Example output: 

```sh
  {
    "Uploads": [
        {
            "UploadId": "2~h3wQpOikK6d-gfzJ2G8Zx8OYODz227e",
            "Key": "2025-02-12-test/19_aaa_test_4gb_file.png",
            "Initiated": "2025-11-27T23:57:31.902000+00:00"
        }
    ]
}
```
{: codeblock}

To check the size and number of parts:

```sh
aws s3api list-parts --endpoint-url <endpoint> --bucket <bucket-name> --key <object-key> --upload-id <upload-id>
```
{: codeblock}

Multiply the size of each part by the number of parts to estimate the capacity consumed by failed uploads.

### Preventing capacity mismatches
{: #preventing-mismatches}

#### Abort failed multipart uploads
{: #abort-failed-multipart}

Run the following command: 

```sh
aws s3api abort-multipart-upload --endpoint-url <endpoint> --bucket <bucket-name> --key <object-key> --upload-id <upload-id>
```
{: codeblock}

Regularly monitor for incomplete uploads using `list-multipart-uploads`.

#### Automating Cleanup
{: #automating-cleanup}

You can configure S3 lifecycle policies to automatically remove incomplete multipart uploads after a specified number of days. Here is an example snippet:

```sh
{
    "Rules": 
        {
            "ID": "AbortIncompleteMultipartUpload",
            "Status": "Enabled",
            "AbortIncompleteMultipartUpload": {
                "DaysAfterInitiation": 7
        }
}
```
{: codeblock}

After aborting incomplete multipart uploads using the abort-multipart-upload command, the used capacity on both the primary and secondary sites becomes consistent. The DR works as expected after the failed uploads are removed.

## Risks of load balancing between primary and secondary sites
{: #load-balancing}

When an application distributes requests across both sites (primary and secondary), the following issues may occur:

- Race condition: The same object may be updated by both systems simultaneously. Due to network latency differences, requests can arrive in an unexpected order.

- Impact on object state: Even if the application sends updates in the correct sequence, the two sites may process them out of order. This can result in the object ending up in an unwanted or inconsistent state.

Recommendation: Avoid configuring applications to load balance between the two sites.


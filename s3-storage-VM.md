---

copyright:
 years: 2024, 2026
lastupdated: "2026-02-03"

keywords: cephaas settings, trial version, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Using {{site.data.keyword.cephaas_full_notm}} object Storage for unstructured data
{: #using-cephaas-object-storage}

Object storage is ideal for managing large volumes of unstructured data such as images, videos, backups, and logs. {{site.data.keyword.cephaas_full_notm}} provides S3-compatible object storage, allowing you to use tools like the AWS CLI to interact with your storage resources.

In this section, you will learn how to:
- Connect to your virtual machine using SSH
- Generate object storage credentials
- Configure the AWS CLI
- Perform basic S3 operations such as listing buckets, creating a bucket, and uploading files

These steps will help you quickly integrate {{site.data.keyword.cephaas_full_notm}} object storage into your trial environment.

The `<vm-ip>` and `<s3-ip>` details are available in a text file inside your `setup.zip` folder.
{: note}

Follow these steps to configure and access S3-compatible object storage from your deployed VM.

1. Use SSH to login `ssh root@<vm-ip>` to your VM using the credentials provided during setup.
2. Generate object storage credentials using the [Ceph as a Service UI](/docs/cephaas?topic=cephaas-creating-s3-credential-sds&interface=ui).
3. Copy the credential name and hmac access key.
4. Open AWS CLI and the preinstalled AWS CLI can be configured using the command `aws configure`. 
5. Enter the S3 credentials.
6. Run the following AWS S3 command using the AWS CLI provided to list the S3 buckets. 

`aws s3api --endpoint-url https://<s3-ip> list-buckets --no-verify-ssl`




![AWS CLI](images/aws-cli.png "VMWare Web console"){: caption="AWS CLI for S3 storage" caption-side="bottom"}




You can now perform additional [S3 operations](https://docs.aws.amazon.com/cli/v1/userguide/cli-services-s3-commands.html).

Here are a few examples of the S3 operation. 

- Create S3 bucket

`aws s3api --endpoint-url https://<s3-api> --no-verify-ssl create-bucket --bucket test-bucket`

- Upload a file to the bucket

`aws s3 --endpoint-url https://<s3-api> --no-verify-ssl cp awscliv2.zip s3://test-bucket/awscli`

In the steps above, we successfully connected to the {{site.data.keyword.cephaas_full_notm}} object storage, created a bucket, and uploaded a sample file. This trial use case gives you a glimpse of how IBM Storage Ceph as a Service can help you harness the power of object storage.

When you deploy {{site.data.keyword.cephaas_full_notm}} in your data center, you can integrate your own applications and software with S3-compatible object storage. This allows you to focus on consuming and utilizing storage resources, while we take care of providing and managing the underlying object storage infrastructure. 

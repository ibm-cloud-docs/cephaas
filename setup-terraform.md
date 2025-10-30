---

copyright:
  years: 2021, 2023
lastupdated: "2025-10-30"

keyword: ceph as a service, setting up terraform, installing terraform, configuring resources

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Setting up Terraform
{: #terraform-setup}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent creation of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitier cloud environments according to **Infrastructure as Code (IaC)** principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API, and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.cephaas_full}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}


## Installing Terraform and configuring resources
{: #install-terraform}


Before you can create an authorization by using Terraform, make sure that you have completed the following:

* Make sure that you have the [required access](/docs/cephaas?topic=cephaas-managing-iam) to create and work with {{site.data.keyword.cephaas_full_notm}} resources.

* Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.

* Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

## Creating a sample volume and host instance
{: #sample-vol-host-instance}

1. Create a volume and host instance by using the `ibm_sds_volume` and `ibm_sds_host` resource argument in your `main.tf` file. The volume and host instance in the following example are named `sds_volume_instance` and `sds_host_instance` respectively.

   ```terraform
   // Provision sds_volume resource instance
   resource "ibm_sds_volume" "sds_volume_instance" {
     capacity = 10
     name = "demo-volume"
   }

   // Provision sds_host resource instance
   resource "ibm_sds_host" "sds_host_instance" {
     name = "demo-host"
     nqn = "<hostNQN>"
   }
   ```
   {: codeblock}

2. Set your SDS endpoint as an environment variable

   ```bash
   export IBMCLOUD_SDS_ENDPOINT="<sds_endpoint>"
   ```
   {: pre}

   Setting the endpoint can also be accomplished by including the below tag in your terraform resources.

   ```terraform
   // Provision sds_volume resource instance
   resource "ibm_sds_volume" "sds_volume_instance" {
      sds_endpoint="<sds_endpoint>"
      capacity = 10
      name = "demo-volume"
   }
   ```
   {: pre}

3. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

4. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   2. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

5. From the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, expand **Storage** and select the {{site.data.keyword.cephaas_full_notm}} instance that you created and note the instance ID.

6. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources&interface=ui#review-your-access-console).

## What's next?
{: #terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.cephaas_full_notm}} deployment instance with Terraform on {{site.data.keyword.cloud_notm}}, you can choose between the following tasks:

* Create a new volume or host
* List the available volumes or hosts
* Retrieve all volumes or hosts
* Modify volume or host details
* Map or unmap volume to host
* Delete a volume or hosts

---

copyright:
  years: 2021, 2023
lastupdated: "2024-10-16"

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}





# Setting up Terraform
{: #terraform-setup}





Terraform on {{site.data.keyword.cloud}} enables predictable and consistent creation of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.cephaas_full}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Installing Terraform and configuring resources
{: #install-terraform}


_**NOTE**: The following example is specific to Key Protect. Work with your development team to update the steps in this example for your service. It is IMPORTANT that you document how to create an instance of your service and assign an access policy in IAM to your service. Most IAM-enabled services use the `ibm_resource_instance` Terraform resource to create a service instance. Because these services share the same Terraform resource, you must make sure that you document ALL supported configurations that are specific to your service. If your service does not require an instance to be created first, such as in {{site.data.keyword.containerlong_notm}}, document how to create the most common resource instead (e.g. cluster). These services usually have dedicated resources in Terraform that you must use. For example, to create an {{site.data.keyword.containerlong_notm}} cluster, you use the `ibm_container_cluster` Terraform resource. Make sure that it is clear to the user what configuration parameters are supported for your service and how the user can retrieve supported values._

Before you can create an authorization by using Terraform, make sure that you have completed the following:

* Make sure that you have the [required access](/docs/cephaas?topic=cephaas-managing-iam) to create and work with {{site.data.keyword.cephaas_full_notm}} resources. 
* Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
* Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

1. Create a {{site.data.keyword.keymanagementserviceshort}} instance by using the `ibm_resource_instance` resource argument in your `main.tf` file.

   The {{site.data.keyword.keymanagementserviceshort}} instance in the following example is named `my_kp` and is created with the tiered pricing plan in the `us-south` region. The `user@ibm.com` is assigned the Manager role in the IAM access policy. For other supported regions, see [Regions and endpoints](/docs/key-protect?topic=key-protect-regions).

   ```terraform
   resource "ibm_resource_instance" "kms_instance" {
     name     = "my_kp"
     service  = "kms"
     plan     = "tiered-pricing"
     location = "us-south"
   }

   resource "ibm_iam_user_policy" "policy" {
     ibm_id = "user@ibm.com"
     roles  = ["Manager"]

     resources {
       service              = "kms"
       resource_instance_id = element(split(":", ibm_resource_instance.kms_instance.id), 7)
     }
   }
   ```
   {: codeblock}

   

   ```terraform
   resource "ibm_resource_instance" "hpcs" {
     name     = "my_hpcs"
     service  = "hs_crypto"
     plan     = "standard"
     location = "us-south"
     parameters = {
        units = 2
     }
   }
   ```
   {: codeblock}

2. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://www.terraform.io/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

3. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://www.terraform.io/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

6. From the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, select the {{site.data.keyword.keymanagementserviceshort}} instance that you created and note the instance ID.
7. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources#review-your-access-console).

## What's next?
{: #terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.keymanagementserviceshort}} service instance with Terraform on {{site.data.keyword.cloud_notm}}, you can choose between the following tasks:



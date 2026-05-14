---

copyright:
 years: 2024, 2026
lastupdated: "2026-05-14"

keywords: IBM FusionaaS, IAM access, fusionaas, fusion as a service, identity, access management, openshift, compute, storage

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Managing IAM access
{: #managing-iam}

Access to Fusion as a Service instances for users in your account is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). Every user that accesses the Fusion as a Service service must be assigned an access policy with an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to Fusion as a Service.
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by Fusion as a Service as operations that are allowed to be performed on the service. Each action is mapped to an IAM platform or service role that you can assign to a user.


IAM access policies enable access to be granted at different levels. Some of the options include the following:

* Access across all deployments of the service in your account
* Access to an individual service instance in your account
* Access to specific resources within a deployment (compute clusters or storage volumes)

After defining the scope of the access policy, assign a role.

## Service-to-Service (S2S) authorization policy
{: #s2s-authorization}

Fusion as a Service requires authorization to interact with {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.satellitelong_notm}} services. To enable this interaction, you must create a service-to-service (S2S) authorization policy in IAM that grants Fusion as a Service Administrator-level access to these services.

### Prerequisites
{: #s2s-prerequisites}

Before you can use Fusion as a Service, you must create S2S authorization policies to allow Fusion as a Service to:
- Create and modify {{site.data.keyword.openshiftlong_notm}} cluster instances in your account
- Create and modify {{site.data.keyword.satellitelong_notm}} location instances in your account

### Creating S2S authorization policies
{: #create-s2s-policy}

To create the required S2S authorization policies:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **Authorizations**.
2. Click **Create**.
3. For the source service, select **Fusion as a Service** (software-defined-storage).
4. For the target service, select **{{site.data.keyword.openshiftlong_notm}}** (containers-kubernetes).
5. Assign the **Administrator** role.
6. Click **Authorize**.
7. Repeat steps 2-6 for **{{site.data.keyword.satellitelong_notm}}** as the target service.

These authorization policies enable Fusion as a Service to provision and manage compute infrastructure on your behalf.

### Context tokens
{: #context-tokens}

Fusion as a Service uses context tokens to securely access {{site.data.keyword.openshiftlong_notm}} clusters on your behalf. When you access the Fusion as a Service GUI, it calls the control plane APIs with your access token, which is validated for the proper role and action for your Fusion as a Service instance. The service then uses context tokens to retrieve the list of {{site.data.keyword.openshiftlong_notm}} clusters from the containers-kubernetes service that you are authorized to view. This orchestration using context tokens enforces Context-Based Restrictions (CBR) as described in the [IAM documentation](/docs/account?topic=account-context-restrictions-whatis).

## IAM roles and actions
{: #iam-roles-actions}

Review the following tables that outline what types of tasks each role allows when you're working with the Fusion as a Service service. Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access to the service and create deployments. Service access roles enable users access to Fusion as a Service and the ability to call the Fusion as a Service API. For information about the exact actions that are mapped to each role, see [Identity and access management actions mapped to roles](#iam-actions).

| Platform role |  Description of actions |
|---------------|-------------------------|
| Viewer        |  As a viewer, you can view FusionaaS deployments, OpenShift clusters, and storage resources, but you can't modify them. In addition, you can also inspect S3 certificates and view quota settings. |
| Operator      |  As an operator, you can perform platform actions that are required to configure and operate FusionaaS deployments, including managing OpenShift clusters and storage. In addition, you can also inspect, upload, update and delete S3 certificates, and update quota settings.           |
| Editor        |  As an editor, you can perform all platform actions except for managing the account and assigning access policies. This includes creating and managing OpenShift clusters, provisioning storage, and managing certificates and quotas.           |
| Administrator |  As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. You have full control over FusionaaS deployments, compute resources, storage, certificates, and quota management.          |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM platform roles" caption-side="bottom"}
{: #iamrolesplatform}
{: tab-title="Platform roles"}


| Service role |  Description of actions |
|--------------|------------------------|
| Reader       | As a reader, you can view service level resources such as clusters. |
| Manager      | As a manager, you can create, update, delete and view service level resources such as volumes, hosts, S3 credentials, and clusters. |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM service access roles" caption-side="bottom"}
{: #iamrolesservice}
{: tab-title="Service roles"}
{: tab-group="IAM"}


## Identity and access management actions mapped to roles
{: #iam-actions}


| Action ID                                       | Roles                                     | Descriptions                      |
| ------------------------------------------------|-------------------------------------------|-----------------------------------|
| `resource-controller.instance.retrieve`         | Administrator, Editor, Operator, Viewer   | View and list FusionaaS deployments (compute and storage) but cannot modify the instance properties. |
| `resource-controller.instance.create`           | Administrator, Editor                     | Create a FusionaaS deployment from the Fusion as a Service Deployments page, including provisioning OpenShift clusters and storage resources.  |
| `resource-controller.instance.update`           | Administrator, Editor, Operator           | Update a Fusion as a Service deployment. Allowed to modify deployment parameters such as name, quota settings, cluster configurations, and S3 certificates for object storage. |
| `software-defined-storage.certificate.update`   |	Administrator, Editor, Operator           | Update S3 certificate for storage component |
| `software-defined-storage.certificate.inspect`  |	Administrator, Editor, Operator, Viewer   | Inspect S3 certificate for storage component |
| `software-defined-storage.certificate.delete`   |	Administrator, Editor, Operator           | Delete S3 certificates for storage component |
| `software-defined-storage.certificate.create`   |	Administrator, Editor, Operator           | Create S3 certificate for storage component  |
| `software-defined-storage.s3-credential.create` |	Manager                                   | Create S3 credentials for object storage |
| `software-defined-storage.s3-credential.get`    |	Manager                                   | Get S3 credentials for object storage  |
| `software-defined-storage.s3-credential.delete` |	Manager                                   | Delete S3 credentials for object storage |
| `software-defined-storage.volume.create`        |	Manager                                   | Create a storage volume |
| `software-defined-storage.volume.read`          |	Manager                                   | Read storage volumes  |
| `software-defined-storage.volume.update`        |	Manager                                   | Update storage volumes  |
| `software-defined-storage.volume.delete`        |	Manager                                   | Delete storage volumes  |
| `software-defined-storage.host.create`          |	Manager                                   | Create storage hosts  |
| `software-defined-storage.host.read`            |	Manager                                   | Read storage hosts  |
| `software-defined-storage.host.update`          |	Manager                                   | Update storage hosts  |
| `software-defined-storage.host.delete`          |	Manager                                   | Delete storage hosts  |
| `software-defined-storage.host.unmap`           |	Manager                                   | Unmap storage hosts |
| `software-defined-storage.host.map`             |	Manager                                   | Map storage hosts |
| `software-defined-storage.cluster.view`         |	Reader                                    | View cluster properties and details |
| `software-defined-storage.cluster.update`       |	Manager                                   | Update cluster quota and properties |
{: caption="IAM action descriptions for FusionaaS" caption-side="bottom"}


## Assigning access to Fusion as a Service in the console
{: #assign-access-console}
{: ui}

There are two common ways to assign access in the console:

* Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources in the console](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console){: external}.
* Access groups. Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag){: external}.


## Assigning access to Fusion as a Service in the CLI
{: #assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli){: external}. The following example shows a command for assigning the `<Manager>` role for `<Fusion as a Service>`:

Use `<programmatic_service_name>` for the service name. Also, use quotations around role names that are more than one word like the example here.
{: tip}


```bash
ibmcloud iam user-policy-create USER@EXAMPLE.COM --service-name software-defined-storage --roles "Manager"
```
{: pre}

## Assigning access to Fusion as a Service by using the API
{: #assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api){: external} or the [Create a policy API doc](/apidocs/iam-policy-management#create-policy){: external}. Role cloud resource names (CRN) in the following table are used to assign access with the API.


| Role name | Role CRN |
|---------------|-----------------|
| Viewer                 | `crn:v1:bluemix:public:software-defined-storage::::serviceRole:Viewer`        |
| Operator               | `crn:v1:bluemix:public:software-defined-storage::::serviceRole:Operator`      |
| Editor                 | `crn:v1:bluemix:public:software-defined-storage::::serviceRole:Editor`        |
| Administrator          | `crn:v1:bluemix:public:software-defined-storage::::serviceRole:Administrator` |
| Manager                | `crn:v1:bluemix:public:software-defined-storage::::serviceRole:Manager` |
{: caption="Role ID values for API use" caption-side="bottom"}



The following example is for assigning the `<Manager>` role for `<Fusion as a Service>`:

Use `<programmatic_service_name>` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}


```curl
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H "Authorization: Bearer $IAM_TOKEN" -H 'IBM-API-Version: 2025-02-01' -H 'accept: application/json' -d '{
  "type": "access",
  "description": "Manager role for IBM Fusion as a Service",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "IBMid-123453user"
        }
      ]
    }
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:software-defined-storage::::serviceRole:Manager"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceName",
          "value": "software-defined-storage"
        }
      ]
    }
  ]
}

```
{: curl}
{: codeblock}


```go
subjectAttribute := &iampolicymanagementv1.SubjectAttribute{
    Name:  core.StringPtr("iam_id"),
    Value: core.StringPtr("IBMid-123453user"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
    Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
    RoleID: core.StringPtr("crn:v1:bluemix:public:software-defined-storage::::serviceRole:Manager"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
    Name:     core.StringPtr("accountId"),
    Value:    core.StringPtr("ACCOUNT_ID"),
    Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
    Name:     core.StringPtr("serviceName"),
    Value:    core.StringPtr("software-defined-storage"),
    Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
    Attributes: []iampolicymanagementv1.ResourceAttribute{
      *accountIDResourceAttribute, *serviceNameResourceAttribute}
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
    "access",
    []iampolicymanagementv1.PolicySubject{*policySubjects},
    []iampolicymanagementv1.PolicyRole{*policyRoles},
    []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
    panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}


## Assigning access to Fusion as a Service by using Terraform
{: #assign-access-terraform}
{: terraform}

The following example is for assigning the `<Manager>` role for `<software-defined-storage>` (used by FusionaaS):

Use `software-defined-storage` for the service name.
{: tip}


```terraform
resource "ibm_iam_user_policy" "policy" {
    ibm_id = "test@example.com"
    roles  = ["Manager"]
    resources {
    service = "software-defined-storage"
    }
}
```
{: codeblock}

For more information, see [ibm_iam_user_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_policy){: external}.

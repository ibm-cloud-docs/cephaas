---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-04"

keywords: IBM CephaaS, IAM access, cephaas, ceph as a service, identity, access management

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Managing IAM access
{: #managing-iam}

Access to {{site.data.keyword.cephaas_full}} instances for users in your account is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.cephaas_short}} service must be assigned an access policy with an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.cephaas_short}}.
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cephaas_short}} as operations that are allowed to be performed on the service. Each action is mapped to an IAM platform or service role that you can assign to a user.


IAM access policies enable access to be granted at different levels. Some of the options include the following:

* Access across all deployment of the service in your account
* Access to an individual service instance in your account

After defining the scope of the access policy, assign a role.

Review the following tables that outline what types of tasks each role allows when you're working with the {{site.data.keyword.cephaas_short}} service. Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access to the service and create deployments. Service access roles enable users access to {{site.data.keyword.cephaas_short}} and the ability to call the {{site.data.keyword.cephaas_short}} API. For information about the exact actions that are mapped to each role, see table [Identity and access management actions mapped to roles](/docs/cephaas?topic=cephaas-managing-iam&interface=ui#iam-actions).

| Platform role |  Description of actions |
|---------------|-------------------------|
| Viewer        |  As a viewer, you can view deployments, but you can't modify them. In addition, you can also inspect, the s3 certificate and view quota. |
| Operator      |  As an operator, you can perform platform actions that are required to configure and operate deployments. In addition, you can also inspect, upload, update and delete the s3 certificate, and update quota.           |
| Editor        |  As an editor, you can perform all platform actions except for managing the account and assigning access policies. In addition, you can also inspect, upload, update and delete the s3 certificate, and update quota.           |
| Administrator |  As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. In addition, you can also inspect, upload, update and delete the s3 certificate, and update quota.          |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM platform roles" caption-side="bottom"}
{: #iamrolesplatform}
{: tab-title="Platform roles"}


| Service role |  Description of actions |
|--------------|------------------------|
| Manager      | As a manager, you have permissions beyond the editor role to complete privileged actions as defined by the service. You can create, update, delete and view service level resources such as volumes, hosts, and S3 credentials. |
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
| `resource-controller.instance.retrieve`         | Administrator, Editor, Operator, Viewer   | View and list deployments but cannot modify the instance properties. |
| `resource-controller.instance.create`           | Administrator, Editor                     | Create a deployment from {{site.data.keyword.cephaas_short}} Deployments page.  |
| `resource-controller.instance.update`           | Administrator, Editor, Operator           | Update an {{site.data.keyword.cephaas_short}} deployment. Allowed to modify {{site.data.keyword.cephaas_short}} deployment parameters such as name, quota settings, and S3 Certificate for object. |
| `software-defined-storage.certificate.update`   |	Administrator, Editor, Operator           | Update certificate |
| `software-defined-storage.certificate.inspect`  |	Administrator, Editor, Operator, Viewer   | Inspect certificate |
| `software-defined-storage.certificate.delete`   |	Administrator, Editor, operator           | Delete certificates |
| `software-defined-storage.certificate.create`   |	Administrator, Editor, operator           | Create certificate  |
| `software-defined-storage.s3-credential.create` |	Manager                                   | Create S3 credentials |
| `software-defined-storage.s3-credential.get`    |	Manager                                   | Get S3 credentials  |
| `software-defined-storage.s3-credential.delete` |	Manager                                   | Delete S3 credentials |
| `software-defined-storage.volume.create`        |	Manager                                   | Create a volume |
| `software-defined-storage.volume.read`          |	Manager                                   | Read volumes  |
| `software-defined-storage.volume.update`        |	Manager                                   | Update volumes  |
| `software-defined-storage.volume.delete`        |	Manager                                   | Delete volumes  |
| `software-defined-storage.host.create`          |	Manager                                   | Create hosts  |
| `software-defined-storage.host.read`            |	Manager                                   | Read hosts  |
| `software-defined-storage.host.update`          |	Manager                                   | Update hosts  |
| `software-defined-storage.host.delete`          |	Manager                                   | Delete hosts  |
| `software-defined-storage.host.unmap`           |	Manager                                   | Unmap hosts |
| `software-defined-storage.host.map`             |	Manager                                   | Map hosts |
{: caption="IAM action descriptions"}


## Assigning access to {{site.data.keyword.cephaas_short}} in the console
{: #assign-access-console}
{: ui}

There are two common ways to assign access in the console:

* Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources in the console](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console){: external}.
* Access groups. Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag){: external}.


## Assigning access to {{site.data.keyword.cephaas_short}} in the CLI
{: #assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli){: external}. The following example shows a command for assigning the `<Manager>` role for `<{{site.data.keyword.cephaas_short}} Storage>`:

Use `<programmatic_service_name>` for the service name. Also, use quotations around role names that are more than one word like the example here.
{: tip}


```bash
ibmcloud iam user-policy-create USER@EXAMPLE.COM --service-name software-defined-storage --roles "Manager"
```
{: pre}

## Assigning access to {{site.data.keyword.cephaas_short}} by using the API
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



The following example is for assigning the `<Manager>` role for `<{{site.data.keyword.cephaas_short}} Storage>`:

Use `<programmatic_service_name>` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}


```curl
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H "Authorization: Bearer $IAM_TOKEN" -H 'IBM-API-Version: 2025-02-01' -H 'accept: application/json' -d '{
  "type": "access",
  "description": "Manager role for IBM Storage Ceph as a Service",
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

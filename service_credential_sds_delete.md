---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-05"

keywords: sdsaas , delete service credential

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Delete service credential
{: #deleting-sds-service-credential}

Delete a service credential using the UI, CLI, or API.
{: shortdesc}


## Deleteing a service credential in the UI
{: #deleting-sds-service-credential-ui}
{: ui}

To delete a service credential, complete the following steps.

1. On the IBM Cloud console, navigate to **SDS as a Service > Object Storage > Service credentials** tab.

2. Select the service credential that you wish to delete.

3. Click **Delete** to confirm deletion.

All access granted to any resources using this credential will be lost once the credential is deleted.
{: note}

## Deleting a service credential from the CLI
{: #deleting-sds-service-credential-cli}
{: cli}

Use the `cred-delete` command and provide the `INSTANCEID` of the specific credential for a storage account.

Run the following command to delete a credential.

```sh
iibmcloud software-defined-storage cred-delete --instanceid INSTANCEID --access-key ACCESS-KEY
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cred-delete --instanceid exampleString --access-key exampleString
```
{: screen}

---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-20"

keywords: service credential create

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Create a service credential
{: #create-service-credential-sds}

Create service credentials by using the UI, CLI, or API.
{: shortdesc}



## Creating a service credential using the UI
{: #creating-service-credential-using-ui}
{: ui}

To create a service credential, complete the following steps.

1. On the IBM Cloud console, navigate to **SDS as a Service > Object Storage > Service credentails** tab.

2. Click **New credential**.

3. Enter service credential **Name** and click **Add**.


## Creating service credential from the CLI
{: #creating-object-service-credential-cli}
{: cli}

You can create a service credential by using the command-line interface (CLI).

### Before you begin
{: #before-creating-service-credential-cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the SDS CLI plug-in.


{: requirement}

Log in to the IBM Cloud.

```sh
ibmcloud login --sso -a cloud.ibm.com
```
{: pre}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.
{: pre}

### Creating a service credential from the CLI
{: #creating-service-credential-cli}
{: help}
{: support}

Run the following command with the `INSTANCEID` and `ACCESS-KEY` to create a new storage account credential or update an existing credential for the storage deployment.

```sh
ibmcloud software-defined-storage cred-create --instanceid INSTANCEID --access-key ACCESS-KEY
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cred-create --instanceid exampleString --access-key exampleString

```
{: screen}



## Creating a service credential with the API
{: #creating-service-credential-api}
{: api}




## Next steps
{: #next-step-creating-service-credential-sds}

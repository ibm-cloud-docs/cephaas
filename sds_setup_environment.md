---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-06"

keywords: sds, sdsaas, cephaas, set up environment, api, cli

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Setting up your API and CLI environment
{: #set-up-environment}

Before you can create an {{site.data.keyword.cephaas_full}} (CephaaS) by using the API or CLI, set up your environment.
{: shortdesc}

## General prerequisites
{: #general-prerequisites}

1. Set up your account to access CephaaS. Make sure that your account is [upgraded to a paid account](/docs/account?topic=account-accountfaqs#changeacct){: external}.
2. Make sure that you have a public SSH key, which will be used to connect to the service instance. For example, generate an SSH key on your Linux server by running the following command:

    ```sh
    ssh-keygen -t rsa
    ```
    {: pre}

   This command generates two files. The generated public key is in the `id_rsa.pub` file under an ``.ssh`` directory in your home directory, for example, ``.../.ssh/id_rsa.pub``.

   For more information, see [SSH keys](/docs/sdsaas?topic=sdsaas-ssh-keys).

## CLI prerequisites
{: #cli-prerequisites-setup}
{: cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the CephaaS CLI plug-in.

{{site.data.keyword.cloud_notm}} CLI is not supported on LinuxONE (s390x processor architecture). However, you can install the CLI on another supported platform and use it with LinuxONE (s390x processor architecture) virtual server instances.
{: note}

1. Install the [IBM Cloud CLI](/docs/cli?topic=cli-getting-started){: external}.
1. Install the CephaaS CLI plug-in.

   ```sh
   ibmcloud plugin install software-defined-storage
   ```
   {: pre}

   The CephaaS CLI actions use the extension `sds`. To learn how to use the CLI commands, you can run:

   ```sh
   ibmcloud sds help
   ibmcloud sds help volume-create
   ibmcloud sds help host-create
   ```
   {: pre}




## API prerequisites
{: #api-prerequisites-setup}
{: api}

Before you can use the API to create your CephaaS, you must get an IAM token, store the endpoint as a variable, and verify that you have access to the CephaaS API service.

The following examples use the `us-south` regional endpoint. To view additional API endpoints, see [Virtual Private Cloud API](/apidocs/vpc/latest#endpoint-url).
{: note}

### Step 1: Store your API key as a variable
{: #store-api-key-variable}

Run the following command to store the API key for your account in an environment variable. If you don't have an API key, see [Creating an API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key){: external}.

```bash
apikey="<YOUR_API_KEY>"
```
{: pre}

### Step 2: Get an IBM Identity and Access Management (IAM) token
{: #get-iam-token}

Run the following command to get and parse an IAM token by using the JSON processing utility [jq](https://stedolan.github.io/jq/){: external}. You can modify the command to use another parsing tool, or you can remove the last part of the command if you prefer to manually parse the token.

```json
iam_token=`curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=$apikey" \
  "https://iam.cloud.ibm.com/identity/token"  |jq -r '(.token_type + " " + .access_token)'`
```
{: pre}

To view the IAM token, run ``echo $iam_token``. The result should look like this:

```sh
Bearer <your token>
```
{: screen}

The Authorization header expects the token to begin with "Bearer". If the result doesn't include "Bearer", update the `iam_token` variable to include it. These examples assume that "Bearer" is included in the `iam_token`.

You must repeat the preceding step to refresh your IAM token every hour because the token expires.
{: important}

### Step 3: Store the API endpoint as a variable
{: #store-api-endpoint-variable}

Run the following command to store the API endpoint in a variable so it can be reused later in your session.

Public endpoint:

```sh
sds_api_endpoint="https://us-south.iaas.cloud.ibm.com"
 ```
{: pre}

Virtual private endpoint:

```sh
sds_api_endpoint="https://us-south.private.iaas.cloud.ibm.com"
```
{: pre}

To verify that this variable was saved, run ``echo $vpc_api_endpoint`` and make sure that the response is not empty.

For supported endpoint regions, see [Endpoints available](/docs/sdsaas?topic=sds-service-endpoints).
{: note}

### Step 4: Store the API version as a variable
{: #store-api-version-variable}


Every API request must include the `version` parameter, in the format `YYYY-MM-DD`. Run the following command to store the version date in a variable so it can be reused in your session.



```sh
api_version="2019-09-30"
 ```
{: pre}

To verify that this variable was saved, run ``echo $api_version`` and make sure that the response is not empty.

### Step 5: Verify that you have API access
{: #verify-api-access}

If you run into unexpected results, add the `--verbose` (debug) flag after the `curl` command to obtain detailed logging information. For more information about commonly encountered errors, see [Troubleshooting](/docs/sdsaas?topic=sds-troubleshooting-block-storage).
{: tip}



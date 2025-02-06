---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-06"

keywords: sds, cephaas, cephaas, set up environment, api, cli

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Setting up your CLI and API environment
{: #set-up-environment}

Before you can create an {{site.data.keyword.cephaas_full}} by using the API, or CLI, set up your environment.
{: shortdesc}

## General prerequisites
{: #general-prerequisites}

1. Set up your account to access {{site.data.keyword.cephaas_full_notm}}. Make sure that your account is [upgraded to a paid account](/docs/account?topic=account-accountfaqs#changeacct){: external}.

2. Make sure that you have the list of on-prem endpoints that were provided for deployment handy.

   You can set the endpoints as environment variables.
   {: tip}


## CLI prerequisites
{: #cli-prerequisites-setup}
{: cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the {{site.data.keyword.cephaas_full_notm}} CLI plug-in.


Make sure that your environment from which the CLI will be run is connected to the on-premise network before using the CLI on the on-premise deployment of {{site.data.keyword.cephaas_full_notm}}.
{: requirement}

1. Install the [IBM Cloud CLI](/docs/cli?topic=cli-getting-started){: external}.
1. Install the {{site.data.keyword.cephaas_short}} CLI plug-in `software-defined-storage`.

   ```sh
   ibmcloud plugin install software-defined-storage
   ```
   {: pre}

   The {{site.data.keyword.cephaas_full_notm}} CLI actions also use the aliases `sds`. To learn how to use the CLI commands, you can run:

   ```sh
   ibmcloud sds help
   ibmcloud sds help volume-create
   ibmcloud sds help host-create
   ```
   {: pre}



### Accessing CLI through the API endpoint
{: #access_cli_through_api_endpoints}

To set the CLI to use the API endpoint, follow these steps:

If you need to download the {{site.data.keyword.cloud_notm}} CLI and associated plug-ins, you must be able to access the public repository where they are located.
{: note}

1. Ensure that the core {{site.data.keyword.cloud_notm}} CLI and {{site.data.keyword.cephaas_short}} service plug-in are updated to the latest version:

   ```sh
   ibmcloud update
   ibmcloud plugin update software-defined-storage
   ```
   {: pre}

1. To switch to API endpoint mode, enter the following command:

   ```sh
   ibmcloud login -a api-endpoint.cloud.ibm.com
   ```
   {: pre}

   Currently, API endpoint mode supports only `us-south` and `us-east` regions.
   {: important}


## API prerequisites
{: #api-prerequisites-setup}
{: api}

Before you can use the API to create your {{site.data.keyword.cephaas_short}}, you must get an IAM token, store the endpoint as a variable, and verify that you have access to the CephaaS API service.

The following examples use the `us-south` regional endpoint.
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

An IAM token is valid for up to 60 minutes, and it is subject to change. When a token expires, you must generate a new one. Use the property expires_in for the expiration of the IAM token that you have just created.
{: important}

### Step 3: Store the API endpoint as a variable
{: #store-api-endpoint-variable}

The `$sds_api_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}`. Run the following command to store the API endpoint in a variable so it can be reused later in your session.

For example:

```sh
sds_api_endpoint="https://sds-cephaas.936481b2-379d-4ca6-94ed-4dc1911d749f.software-defined-storage.appdomain.cloud:33173"
```
{: pre}

To verify that this variable was saved, run ``echo $sds_api_endpoint`` and make sure that the response is not empty.



### Step 4: Verify that you have API access
{: #verify-api-access}

Now that you have an endpoint and your IAM token, verify your API access via one of the APIs described in the [API Reference](/docs/cephaas?topic=cephaas-about-api).

If you run into unexpected results, add the `--verbose` (debug) flag after the `curl` command to obtain detailed logging information. 
{: tip}

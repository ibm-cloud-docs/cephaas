---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-09"

keywords: cli, command line interface, object storage, curl

subcollection: sdsaas


---

{{site.data.keyword.attribute-definition-list}}

# Using `cURL`
{: #curl}

You can get the most out working with the command line in most environments with {{site.data.keyword.cephaas_full}} and `cURL`.
{: shortdesc}

Here's a 'cheat sheet' of basic `curl` commands for the {{site.data.keyword.cephaas_full}} REST API.



Using `curl` assumes a certain amount of familiarity with the command line and Object Storage, and have the necessary information from a [credential](/docs/sdsaas?topic=sdsaas-credentials-overview), the [endpoints reference](/docs/sdsaas?topic=sdsaas-endpoints), or the [console](/docs/sdsaas?topic=sdsaas-getting-started). If any terms or variables are unfamiliar, they can be found in the [glossary](/docs/overview?topic=overview-glossary).

**Note**: Personally Identifiable Information (PII): When _naming_ buckets or objects, do not use any information that can identify any user (natural person) by name, location, or any other means.
{: tip}

## Request an IAM Token
{: #curl-iam}

Two ways you can generate an IAM `oauth` token for authenticating requests are using a `curl` command with an API key (described later), or from the command line by using [{{site.data.keyword.cloud}} CLI](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_oauth_tokens).

### Request an IAM token by using an API key
{: #curl-token}

Ensure that you have an API key. You can get one from [{{site.data.keyword.iamlong}}](https://cloud.ibm.com/iam/apikeys).

```curl
curl -X "POST" "https://iam.cloud.ibm.com/oidc/token" \
     -H 'Accept: application/json' \
     -H 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode "apikey={api-key}" \
     --data-urlencode "response_type=cloud_iam" \
     --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey"
```
{: codeblock}

## Get your resource instance ID
{: #curl-instance-id}

Some of the following commands require an `ibm-service-instance-id` parameter. To find this value, go to the **Credentials** tab of your Object Storage instance in the cloud console. Create a credential if needed, then use the _View credentials_ menu to see the JSON format. Use the value of `resource_instance_id`.

For use with curl APIs, you need only the UUID that starts after the last single colon and ends before the final double colon. For example, the ID `crn:v1:bluemix:public:software-defined-storage:global:a/81caa0254631ce5f9330ae427618f209:39d8d161-22c4-4b77-a856-f11db5130d7d::` can be abbreviated to `39d8d161-22c4-4b77-a856-f11db5130d7d`.
{: tip}



## Next Steps
{: #curl-next-steps}

The detailed description of the RESTful API for {{site.data.keyword.cephaas_full_notm}} can be found in the [{{site.data.keyword.cephaas_short}} Object Storage API Documentation](https://cloud.ibm.com/apidocs/object-storage){: external}.

---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-05"

keywords: sdsaas block storage api

subcollection: sdsaas

content-type: api-docs

title: SDSaaS Block Storage API Reference



---

{{site.data.keyword.attribute-definition-list}}


# Introduction
{: #intro}

With the SDSaaS Block Storage API, you can programmatically provision and manage block storage resources within a SDSaaS deployment, including volumes, hosts and volume to host mappings. For more information on the SDSaaS Block Storage, see


# SDKs
{: #intro-sdk}

SDKs for Java, Node, Python, and Go are available for this API. The client libraries that are provided by the SDKs implement best practices for using the API and reduce the amount of code that you need to write. The tab for each language includes code examples that demonstrate how to use the client libraries.

To learn about using IBM SDSaaS, see [ref link coming soon]



# Endpoint URLs
{: #endpoint-url}

IBM SDSaaS Block Storage API is available in all SDSaaS deployments. To get the endpoint URL to be used for a deployment - [TBD]



# Authentication
{: #authentication}

The IBM SDSaaS Block Storage API uses Identity and Access Management (IAM) to authenticate requests. To call each API method, you must be assigned a role that has access to the parent service instance. Check your access on the IBM Cloud console by navigating to Users > User > Access.

Learn about obtaining an IAM token for an authenticated user or service ID in the IAM Identity Services API. If you first create an API key, you can use it to generate an IAM token.

To use the API, add a valid IAM token to the HTTP Authorization request header. For example, -H 'Authorization: Bearer {token}'.

Authorization section is not required for SDSaaS
{: note}



# Auditing
{: #auditing}

Monitor API activity within your account by using the {{site.data.keyword.at_full_notm}} service. Each time you make an API call, one or more events are generated that you can track and audit from within {{site.data.keyword.at_short}}. Specific auditing event types are listed for each individual method. For more information about how to track SDSaaS service activity, see [ref link coming soon].


# Error handling
{: #error-handling}

This API uses standard HTTP response codes to indicate whether a method completed successfully. A `200` response indicates success. A `400` type response indicates a failure, and a `500` type response indicates an internal system error.







| HTTP Error Code | Description           | Recovery                                                                    |
|-----------------|-----------------------|-----------------------------------------------------------------------------|
| `400`           | Bad Request           | The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all required parameters in your request. |
| `401`           | Unauthorized          | You are not authorized to make this request. If this error persists, contact the account owner to check your permissions. |
| `403`           | Forbidden             | The supplied authentication is not authorized to perform the requested operation. You do not have valid access through IAM access policies. If this error persists, contact the account owner to check your permissions.      |
| `404`           | Not Found             | The requested resource could not be found.                                  |
| `405`           | Method Not Allowed    | The requested resource does not support the request method.                 |
| `406`           | Not Acceptable        | The resource the client requested is not available in a format allowed by the Accept header supplied by the client. |
| `408`           | Request Timeout       | The connection to the server timed out. Wait a few minutes, then try again. |
| `409`           | Conflict              | The request cannot be completed because of a conflict between the request and the current state of the resource.  |
| `500`           | Internal Server Error | The request cannot be processed because the client encountered an unexpected condition on the server. Wait a few minutes and try submitting the request again. If this error persists, contact IBM Support. |
| `501`           | Not Implemented       | The server either does not recognize the request method, or it lacks the ability to fulfill the request. |
| `502`           | Bad Gateway           | The server was acting as a gateway or proxy and received an invalid response from the upstream server. |
| `503`           | Service Unavailable   | The server cannot process the request. Generally, this condition is temporary, such as when a server is overloaded or down for scheduled maintenance. This condition could also be due to an unplanned outage of a service that is needed to process the request. Wait a few minutes and try submitting the request again. If this error persists, contact IBM Support.
| `504`           | Gateway Timeout       | The server was acting as a gateway or proxy and did not receive a timely response from the upstream server.  |
| `505`           | HTTP Version Not Supported | The server does not support the HTTP protocol version that is used in the request. |
{: caption="Table 1. Error codes" caption-side="bottom"}




# Versioning
{: #versioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. When we change the API in a [backwards-incompatible](https://github.com/watson-developer-cloud/api-guidelines/#versioning) way, we release a new version date.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.
{: curl}

Specify the version to use on API requests with the version parameter when you create the service instance. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.
{: java}
{: node}
{: python}
{: go}

This documentation describes the current version of {{site.data.keyword.visualrecognitionshort}}, `2018-03-19`. In some cases, differences in earlier versions are noted in the descriptions of parameters and response models.
{: tip}



# Pagination
{: #pagination}

Some API requests can return many results. To improve performance, results are returned one page at a time, with a limited number of results on each page. The default page size is typically `50` items, with a maximum size of `100`.

The default and maximum limits might vary by operation. To specify a different page size, use the limit query parameter.

For a request that uses pagination, the response includes additional properties:

* The `first.href` property links to the first page of resources

* The `next.href` property links to the next page of resources (included for all pages except for the last page)

Use query parameters to page through your available resources and retrieve a subset of objects. To retrieve the first page of results, make the request without specifying a start query parameter. If the results cannot fit on the first page, the response will include a next property, whose value can then be specified as the start parameter when making the next page request. Each page of results is based on the resources that exist at the time of each paginated request, and therefore may include resources that did not exist when the first request was made. The last page of results will not include a next property.

When you're retrieving a subset of objects:

* You may use the value of `first.href` to retrieve the first page of resources in the requested sort order and with the requested filters

* You may use the value of `next.href` to retrieve the next page of resources in the requested sort order and with the requested filters

* You may not change the requested filters across page retrievals

* You may not add a sort query parameter to the href value (sort order is set by the first paginated list request)



---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-03"

keywords: cephaas, logging for IBM CephaaS, observability

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}



# Logging for {{site.data.keyword.cephaas_short}}
{: #logging}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cephaas_short}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

You can use {{site.data.keyword.logs_routing_full_notm}}, a platform service, to route platform logs in your account to a destination of your choice by configuring a tenant that defines where platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



As of 28 March 2024, the {{site.data.keyword.la_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.la_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Logging is the same for both services. For information about migrating from {{site.data.keyword.la_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where platform logs are generated
{: #log-locations}




### Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}
{: #lr-locations}





## Platform logs that are generated
{: #log-platform}






## Enabling logging
{: #log-enable}









## Viewing logs
{: #log-viewing}



### Launching {{site.data.keyword.logs_full_notm}} from the {{site.data.keyword.cephaas_short}} dashboard
{: #log-launch-integrated}



### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For more information about launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Fields by log type
{: #log-fields}



For information about fields included in every platform log, see [Fields for platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#platform_reqd)










## Log messages
{: #log_messages}



The following tables list the message IDs that are generated and additional information available about these messages.

| Message ID | Type | Learn More |
|------------|------|------------|
| `is.flow-log-collector.00001E` | error | Failed to write a Flow log file for the past 24 hours. Dropping flow log for Virtual Server _ServerName_ |
{: caption="Additional information about message IDs" caption-side="top"}

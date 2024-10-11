---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-11"

keywords: cephaas, logging for IBM CephaaS, observability

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# Logging for {{site.data.keyword.cephaas_short}}
{: #logging}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cephaas_full}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

You can use {{site.data.keyword.logs_routing_full_notm}}, a platform service, to route platform logs in your account to a destination of your choice by configuring a tenant that defines where platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.


## Viewing logs
{: #log-viewing}

{{site.data.keyword.cephaas_full_notm}} generate platform logs in the same region where they are available. You can view, monitor, and manage {{site.data.keyword.cephaas_full_notm}} logs through the {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For more information about launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Fields by log type
{: #log-fields}

For information about fields included in every platform log, see [Fields for platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#platform_reqd)

| Field             | Type       | Description             |
|-------------------|------------|-------------------------|
| `logSourceCRN`    | Required   | Defines the account and flow log instance where the log is published. |
| `saveServiceCopy` | Required   | Defines whether IBM saves a copy of the record for operational purposes. |
| `message`         | Required   | Description of the log that is generated. |
| `messageID`       | Required   | ID of the log that is generated. |
| `msg_timestamp`   | Required   | The timestamps when the log is generated. |
| `resolution`      | Optional   | Guidance on how to proceed if you receive this log record. |
| `documentsURL`    | Optional   | More information on how to proceed if you receive this log record. |
{: caption="Log record fields" caption-side="bottom"}

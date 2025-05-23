---

copyright:
 years: 2024, 2025
lastupdated: "2025-05-16"

keywords: cephaas, event notifications, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Enabling event notifications for {{site.data.keyword.cephaas_short}}
{: #event-notifications-events}

As an administrator of {{site.data.keyword.cephaas_full}}, you might want to send notifications of events in {{site.data.keyword.cephaas_short}} to other users, or human destinations, by using email, SMS, or other supported delivery channels. Additionally, you might want to send these notifications of events to other applications to build logic by using event-driven programming using webhooks, for example. This is made possible by the integration between {{site.data.keyword.cephaas_short}} and {{site.data.keyword.en_full}}.
{: shortdesc}

To send information to {{site.data.keyword.en_short}}, you must connect your {{site.data.keyword.cephaas_short}} instance to {{site.data.keyword.en_short}}. For more information about working with {{site.data.keyword.en_short}}, see [Getting started with {{site.data.keyword.en_short}}](/docs/event-notifications?topic=event-notifications-getting-started).

## How events are collected and sent by {{site.data.keyword.cephaas_short}}
{: #event-notifications-how}

When an event of interest takes place in your {{site.data.keyword.cephaas_short}} instance, {{site.data.keyword.cephaas_short}} communicates with a connected {{site.data.keyword.en_short}} instance to forward a notification to a [supported destination](/docs/event-notifications?topic=event-notifications-en-destination).


## Events for {{site.data.keyword.cephaas_short}}
{: #event-notifications-list}

The following table lists the {{site.data.keyword.cephaas_short}} events.



| Event Name        | Event Type        | Sub Type Name | Sub Type  | Severity  |
|------------------------------------------|---------|---------|---------|---------|
| IBM Storage Ceph as a Service Storage Capacity    | com.ibm.cloud.software-defined-storage.capacity   | Allocated block storage at 50% of capacity    | block_capacity_50_percent | low |
|   |   | Allocated block storage at 80% of capacity    | block_capacity_80_percent | medium  |
|   |   |	Allocated block storage at 100% of capacity | block_capacity_100_percent    | high    |
|   |   |	Allocated object storage at 50% of capacity | object_capacity_50_percent    | low |
|   |   |	Allocated object storage at 80% of capacity | object_capacity_80_percent    | medium  |
|   |   |	Allocated object storage at 100% of capacity    | object_capacity_100_percent   | high  |
|IBM Storage Ceph as a Service S3 Certificates  | com.ibm.cloud.software-defined-storage.s3-certificate | S3 certificate has expired    | s3_cert_expired | high    |
|   |   | S3 certificate will expire in 1 day   | s3_cert_expire_1_day  | high  |
|   |   | S3 certificate will expire in 10 days	| s3_cert_expire_10_day | high    |
|   |   | S3 certificate will expire in 30 days	| s3_cert_expire_30_day | medium  |
|   |	| S3 certificate will expire in 60 days	| s3_cert_expire_60_day | medium  |
|   |   | S3 certificate will expire in 90 days	| s3_cert_expire_90_day | low |
{: caption="Actions that generate event notifications" caption-side="bottom"}


## Enabling notifications
{: #event-notifications-enable}

Events that are generated by an instance of the {{site.data.keyword.cephaas_short}} service can be forwarded to an {{site.data.keyword.en_short}} service instance that is available in the same account. You can configure only one {{site.data.keyword.secrets-manager_short}} instance to one {{site.data.keyword.en_short}} service instance.

### Connecting to {{site.data.keyword.en_short}} in the console
{: #event-notifications-enable-ui}

Before you can enable notifications for {{site.data.keyword.cephaas_short}}, be sure that you have an [{{site.data.keyword.en_short}} service instance](/catalog/services/event-notifications){: external} that is in the same account as your {{site.data.keyword.cephaas_short}} instance. Then, you can use the **Settings > Event Notifications** section in the {{site.data.keyword.cephaas_short}} UI to connect the services.


1. In the console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list**.
2. Select your instance of {{site.data.keyword.cephaas_full_notm}}.
3. In the {{site.data.keyword.cephaas_full_notm}} navigation, click **Settings**.
4. In the {{site.data.keyword.en_short}} section, and click **Connect**.
5. Review the source details for the connection. Optionally, provide a description.
6. Select the resource group and {{site.data.keyword.en_short}} service instance that you want to connect.

    If an IAM authorization between {{site.data.keyword.cephaas_short}} and {{site.data.keyword.en_short}} doesn't exist in your account, a dialog is displayed. Follow the prompts to grant access between the services.

    1. To grant access between {{site.data.keyword.cephaas_short}} and {{site.data.keyword.en_short}}, click **Authorize**.
    2. Select **{{site.data.keyword.en_short}}** as the target service.
    3. From the list of instances, select the {{site.data.keyword.en_short}} service instance that you want to authorize.
    4. Select the **Event Source Manager** role.
    5. Click **Review**.
    6. Click **Assign**.

7. To confirm the connection, click **Connect**.



## Delivering notifications to select destinations
{: #event-notifications-destinations}

After you enable notifications for {{site.data.keyword.cephaas_short}}, create topics and subscriptions in {{site.data.keyword.en_short}} so that alerts can be forwarded and delivered to your selected destinations.

For a complete list of supported destinations, see the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-en-destination).
{: tip}

### Email notifications
{: #event-notifications-email}

You can use the [{{site.data.keyword.cloud_notm}} email service](/docs/event-notifications?topic=event-notifications-en-destinations-email) as a delivery channel for _service-name_ event notifications. [Create an {{site.data.keyword.en_short}} subscription](/docs/event-notifications?topic=event-notifications-en-create-en-subscription) between an existing topic and the {{site.data.keyword.cloud_notm}} email service to forward your alerts to various recipients by email.

An email from {{site.data.keyword.cloud_notm}} that contains information about {{site.data.keyword.cephaas_short}} event resembles the following example:



```plaintext
Subject: Replace S3 certificate (expires in 90 days)

Body: S3 certificate will expire in 90 days. Please replace your S3 certificate.
```
{: screen}

To receive detailed information about an event notification in your email, select the **Add notification payload** option when you create an {{site.data.keyword.en_short}} subscription. Your email displays the [notification payload details](#event-notifications-payload) that are associated with the event.
{: tip}


### Webhooks
{: #event-notifications-webhook}

You can configure a webhook destination so that an incoming notification can be consumed programmatically by an app or service. For more information about setting up webhooks, check out the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-en-destinations-webhook).

## Notification payload details
{: #event-notifications-payload}

Successful events that are generated by {{site.data.keyword.cephaas_short}} contain various fields that help you to identify the source and details of an event.

Event notifications from {{site.data.keyword.cephaas_short}} contain only metadata properties, such as names or identifiers of resources. Sensitive data, for example API keys or passwords, are not included in generated events.
{: note}


The properties that are sent to {{site.data.keyword.en_short}} vary depending on the event type. For example, if an `<ExampleEventForYourService` event takes place, {{site.data.keyword.cephaas_short}} sends a notification payload to {{site.data.keyword.en_short}} that is similar to the following example.

```json
{
    "ibmendefaultlong": "S3 certificate will expire in 90 days. Please replace your S3 certificate.",
    "ibmendefaultshort": "Replace S3 certificate (expires 90 days)",
    "ibmenseverity": "low",
    "ibmensourceid": "crn:v1:staging:public:software-defined-storage:satloc_dal_crmid4v20tl6u8usf790:a/3faf73b8d12b47fa6ce87494f8ae7686:0c81f602-5142-4809-9e42-31de8453416a::",
    "id": "38eb4721-db9b-4ba6-a5e7-cdd9cce66763",
    "source": "crn:v1:staging:public:software-defined-storage:satloc_dal_crmid4v20tl6u8usf790:a/3faf73b8d12b47fa6ce87494f8ae7686:0c81f602-5142-4809-9e42-31de8453416a::",
    "specversion": "1.0",
    "time": "2025-04-23T21:13:44.301Z",
    "type": "com.ibm.cloud.software-defined-storage.s3-certificate:s3_cert_expire_90_day"
}
```
{: screen}

Review following table for more information about event notification properties.

| Property | Description |
| ---- | ---- |
| `ibmendefaultlong` | This message is used in case the event that is routed to a destination that needs a human readable text, but a destination-specific attribute is not specified. |
| `ibmendefaultshort` | This message is used in case the event that is routed to a destination that needs a human readable text, but a destination-specific attribute is not specified. |
| `ibmenseverity` | The severity of the event.|
| `ibmensourceid` | This is the ID of the source that is created in Event Notifications. This is available in the Event Notifications UI in the "Sources" section". |
| `id` | A unique identifier that identifies each event. |
| `source` | This is the identifier of the event producer (i.e. the CephaaS CRN). |
| `specversion` | It is the version of the Cloud Events specification that Event Notifications currently supports. This value must be set to "1.0". |
| `time`    | UTC timestamp when the event occurred. Must be in the RFC 3339 format.    |
| `type`    | This describes the type of event. It is of the form _`<event-type-name>:<sub-type>`_   |
{: caption="Properties in an event notification payload" caption-side="bottom"}

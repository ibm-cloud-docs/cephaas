---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-02"

keywords: activity tracker events

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}

# Activity Tracking events for IBM Storage Ceph as a Service
{: #sds-at}

Use {{site.data.keyword.cloud_notm}} Activity Tracker service to track events performed on your resources. You can use these services to investigate abnormal activity and critical actions and comply with regulatory audit requirements and to provide a record of what is happening with your resources.

The Activity Tracker service records user-initiated activities that change the state of a service in IBM Cloud. To get started monitoring your user's actions, see [Getting started with Activity Tracker](docs/activity-tracker?topic=activity-tracker-getting-started).


## List of instance events
{: #sds-list-events}

The following table lists the actions that generate an event:

| Action   | Description                                      |
|:---------|:-------------------------------------------------|
| software-defined-storage.instance.create  |   |
|   |   |
{: caption="Table 1. List of events: Instance" caption-side="top"}


## Enabling events
{: #sds-enabling-events}

Some services requore a paid plan or additional configuration to enable events. Add any information on how to allow the customer to enable collection of events.

### Enabling events through the UI
{: #sds-enabling-events-ui}
{: ui}

1.	From the IBM Cloud console [resource list](https://cloud.ibm.com/resources), select the service instance you are interested in adding for event tracking. This takes you to the CephaaS Storage Console.
2.	Choose the Deployment for which you want to enable event tracking.
3.	Navigate to the configuration tab.
4.	Scroll down to the advanced configuration section and toggle on the events you want to track for this bucket.
5.	After a few minutes, any activity will be visible in the Activity Tracker web UI.

### Enabling events by using the command line
{: #sds-enabling-events-cli}



### Enabling events by using an API call
{: #sds-enabling-events-api}

add example of cURL command including any headers like authorization headers that might be required.


## Viewing events
{: #sds-view-events}

Add link to the section where your service is listed in the topic [Cloud services by location](/docs/activity-tracker?topic=activity-tracker-cloud_services_locations).

## Analyzing events
{: #sds-analyze-events}

Add information on custom fields that are included in requestData and responseData fields and that can help users understand your events.

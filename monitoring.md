---

copyright:
  years: 2018, 2024
lastupdated: "2024-09-19"

keywords: IBM Cloud, observability

subcollection: observability-ibm

---

{{site.data.keyword.attribute-definition-list}}







# Monitoring metrics for {{site.data.keyword.cephaas_short}}
{: #monitoringß}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cephaas_short}}, generate platform metrics that you can use to gain operational visibility into the performance and health of the service in your account.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} is a third-party cloud-native, and container-intelligence management system that can be included as part of your {{site.data.keyword.cloud_notm}} architecture. It offers administrators, DevOps teams, and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. For more information, see [Monitoring in IBM Cloud](/docs/monitoring?topic=monitoring-about-monitor).

You can use {{site.data.keyword.metrics_router_full_notm}}, a platform service, to route platform metrics in your account to a destination of your choice by configuring targets and routes that define where platform metrics are sent. For more information, see [About {{site.data.keyword.metrics_router_full_notm}} in {{site.data.keyword.cloud_notm}}](/docs/metrics-router?topic=metrics-router-about).

You can use {{site.data.keyword.mon_full}} to visualize and alert on metrics that are generated in your account and routed by {{site.data.keyword.metrics_router_full_notm}} to an {{site.data.keyword.mon_full_notm}} instance.

## Viewing metrics
{: #monitoring-view}

To monitor {{site.data.keyword.cephaas_short}} metrics, you must launch the {{site.data.keyword.mon_full_notm}} web UI for the instance that is enabled for platform metrics in the region where your {{site.data.keyword.cephaas_short}} instance is provisioned.
{: important}


### Launching {{site.data.keyword.mon_full}} from the Observability page
{: #monitoring-view-ob}

For more information about launching the {{site.data.keyword.mon_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.mon_full_notm}} documentation.](/docs/monitoring?topic=monitoring-launch)

## Monitoring {{site.data.keyword.cephaas_short}}
{: #monitoring-monitor}



### _Add entries per recommendation to monitor your service_
{: #monitoring-monitor-1}



## {{site.data.keyword.cephaas_short}} predefined dashboards
{: #monitoring-dashboards}




## Metrics available by service plan
{: #monitoring-metrics-by-plan}



| Metric Name |
|------------|
| [{{site.data.keyword.cephaas_full_notm}} provisioned block storage](#ibm_software_defined_storage_block_provisioned_volumes) |
| [{{site.data.keyword.cephaas_full_notm}} provisioned bytes of block storage](#ibm_software_defined_storage_block_provisioned_bytes) |
| [{{site.data.keyword.cephaas_full_notm}} used bytes of object storage](#ibm_software_defined_storage_object_used_bytes) |
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}



## {{site.data.keyword.cephaas_short}} metrics dictionary
{: #monitoring-metrics-dictionary}




### {{site.data.keyword.cephaas_full_notm}} provisioned block storage
{: #ibm_software_defined_storage_block_provisioned_volumes}

Number of storage blocks provisioned by the {{site.data.keyword.cephaas_full_notm}} deployment

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_software_defined_storage_block_provisioned_volumes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance` |
{: caption="Table 2: Provisioned block storage metric metadata" caption-side="top"}

### {{site.data.keyword.cephaas_full_notm}} provisioned bytes of block storage
{: #ibm_software_defined_storage_block_provisioned_bytes}

Bytes of provisioned block storage by the {{site.data.keyword.cephaas_full_notm}} deployment

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_software_defined_storage_block_provisioned_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance` |
{: caption="Table 3: Provisioned bytes of block storage metric metadata" caption-side="top"}

### {{site.data.keyword.cephaas_full_notm}} used bytes of object storage
{: #ibm_software_defined_storage_object_used_bytes}

Bytes of object storage used by the {{site.data.keyword.cephaas_full_notm}} deployment

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_software_defined_storage_object_used_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Object storage class` |
{: caption="Table 4: Used bytes of object storage metric metadata" caption-side="top"}

## Attributes for Segmentation
{: attributes}

### Global attributes
{: global-attributes}

The following attributes are available for segmenting all of the metrics listed above

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of public, dedicated or local |
| `Location` | `ibm_location` | The location of the monitored resource - this may be a region, data center or global |
| `Resource` | `ibm_resource` | The resource being measured by the service - typically a indentifying name or GUID |
| `Resource Type` | `ibm_resource_type` | The type of the resource being measured by the service |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created |
| `Scope` | `ibm_scope` | The scope is the account, organization or space GUID associated with this metric |
| `Service name` | `ibm_service_name` | Name of the service generating this metric |
{: caption="Table 5: Global segmentation attributes" caption-side="top"}


### Additional attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the reference above. Please see the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Object storage class` | `storageclass` | Object storage class |
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance the metric is associated with |
{: caption="Table 6: Additional segmentation attributes" caption-side="top"}

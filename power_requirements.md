---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: planning, site-readiness, on-premises, on premises, on-prem, power requirement, power, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Power requirements
{: #power-requirements}

Your on-premises site for {{site.data.keyword.cephaas_full_notm}} must be provisioned with A-side and B-side power redundancy that meets the {{site.data.keyword.cephaas_full_notm}} rack connector and load requirements. Table 1 shows the rack connector and load requirements.

Be sure to read all caution and danger statements provided in the Safety notices before you perform the procedures.  Read any additional safety information that comes with your system or optional device before you install the device.


| Corresponding PDU| Rack line cord feature code | Wall plug      | Rated voltage (V AC) line to line | Phase   | Rated amperage | Location |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| ECJN (C13) | #6492 | IEC 60309, 2P+G, 60 A  | 200 - 240 V |   1   | 48 A          | US, Canada, Latin America(LA), and Japan |
|         | #6491 | IEC 60309, P+N+G, 63 A | 230 V           |   1   | 63 A          | EMEA |
|         | #6489 | IEC 60309, 3P+N+G, 32 A | 380 – 415 V    |   3 Wye   | 32 A per phase | Europe, Middle East, and Asia (EMEA) |
|         | #6667 | PDL                 | 380 – 415 V      |   3 Wye   | 32 A per phase | Australia and New Zealand |
|         | #6653 | IEC 60309, 3P+N+G   | 380 - 415 V    | 3 Wye | 16 A per phase     | Switzerland |
|         | #ELC2 | IEC 60309, 3P+N+G, 30 A | 380 - 415 V   | 3 Wye | 30 A (derated to 24 A) per phase | United States, Canada, Mexico, and Japan (European Style Power for US type countries) |
| ECJQ (C13) | #ECJ6 | CS8365C | 200 - 240 V | 3 Delta | 50 A or line (40 A derated) | United States, Canada |
|         | #ECJ7 | IEC 60309, 3P+G | 200 - 240 V | 3 Delta | 60 A or line (48 A derated) | United States, Canada, Latin America, and Japan |
{: caption="Rack connectors with load capacity requirements" caption-side="bottom"}

---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-19"


keywords: cephaas, setup traffic encryption

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# Configuring traffic encryption
{: #configuring-traffic-encryption}


1. Create a server side certificate with a SAN which includes their S3 DNS endpoint.

2. Upload the serverside certificate along with the Key via our API (POST /s3tlscert).

3. Use the CA Certificate when sending S3 traffic to the S3 endpoint.

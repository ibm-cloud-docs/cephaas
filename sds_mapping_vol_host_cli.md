# Mapping volume to a host from CLI
{: #mapping-sds-hosts-cli}
{: cli}

Use the `host-vol-update` command and specify the `HOST-ID`, `VOLUME-ID` and `INSTANCEID` to create a volume mapping to the given host ID.

Run the following command to map the volume to the given host.

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-vol-update \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}

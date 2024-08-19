---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-19"

keywords: sds, cephaas host, nvme-of initiator rhel

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the NVMe-oF initiator for Red Hat Enterprise Linux
{: #configuring-nvmeof-initiator-rhel}

Use this procedure to configure the NMVe fabrics for RHEL.

1. Install the nvme-cli.

    ```sh
    yum install nvme-cli
    ```
    {: pre}


1. Install the necessary NVMe packages.

    ```sh
    modprobe nvme-fabrics
    ```
    {: pre}


1. Get the host NVMe Qualified Name (NQN) for each host.

    ```sh
    cat /etc/nvme/hostnqn
    ```
    {: pre}

    For example,

    ```json
    # cat /etc/nvme/hostnqn

    nqn.2014-08.org.nvmexpress:uuid:950ddadf-f995-47b7-9416-b9bb233f66e3
    ```
    {: screen}

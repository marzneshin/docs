---
title: Marznode
weight: 2
---

### Prerequesits

- Docker
- Docker Compose

{{< callout type="info" >}}
Make sure you have docker installed

```sh
$ curl -fsSL https://get.docker.com | sh
```

{{< /callout >}}

{{% steps %}}

### Get Marznode

Clone the marznode repository and spin up the container.

```sh
$ git clone https://github.com/marzneshin/marznode
$ cd marznode
```

### Configure certificate

Copy the marzneshin certificate from dashboard in settings page to `/var/lib/marznode/client.pem`.

### Setup Xray for marznode

Move to `/var/lib/marznode/data`

```sh
mkdir -p /var/lib/marznode/data
cd /var/lib/marznode/data
```

Download the latest [Xray release](https://github.com/XTLS/Xray-core/releases/) for linux

```sh
wget https://github.com/XTLS/Xray-core/releases/download/v1.8.21/Xray-linux-64.zip
```

Unzip and clean the Xray file

```sh
unzip Xray-linux-64.zip && rm Xray-linux-64.zip
```

### Configure xray

Copy the xray config file:

```sh
cp /root/marznode/xray_config.json /var/lib/marznode/xray_config.json
```

Move the data to xray for marznode:

```sh
cp /var/lib/marznode/data/xray /var/lib/marznode/xray
```

### Set the environment variables

Based on the current steps, the `.env` file should follow as

```sh
XRAY_EXECUTABLE_PATH="/var/lib/marznode/xray"
XRAY_ASSETS_PATH="/var/lib/marznoed/data"
XRAY_CONFIG_PATH="/var/lib/marznode/xray_config.json"
SSL_CLIENT_CERT_FILE="/var/lib/marznode/client.pem"
SSL_KEY_FILE="./server.key"
SSL_CERT_FILE="./server.cert"
```

### Spin up docker compose

Execute the following command inside the marznode folder:

```sh
docker compose up -f ./compose.yml -d
```

{{% /steps %}}

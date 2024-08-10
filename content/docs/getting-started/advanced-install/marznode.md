---
title: Marznode
weight: 2
---

### Prerequisites

- Docker
- Docker Compose

{{< callout type="info" >}}
Make sure you have docker installed

```sh
curl -fsSL https://get.docker.com | sh
```

{{< /callout >}}

{{% steps %}}


### Setup your certificate

Create the necessary directory
```sh
mkdir -p /var/lib/marznode/
```

And get your certificate from marzneshin settings, place it here:

`/var/lib/marznode/client.pem`


### Setup some xray config

Provide some xray config for your node; you could modify it later in the dashboard.
We setup the sample config from marznode repository in this case: 

```sh
curl -L https://github.com/khodedawsh/marznode/raw/master/xray_config.json > /var/lib/marznode/xray_config.json
```

### Get Marznode

To clone marznode

```sh
git clone https://github.com/khodedawsh/marznode
cd marznode
```

### Spin up the container

Execute the following command to get your node up and running

```shell
docker compose -f ./compose.yml up -d
```

{{% /steps %}}

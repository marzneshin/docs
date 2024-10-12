---
title: Marznode
weight: 2
---
Easy installation method :

1- installing docker and pulling marznode with this commend :

```apt-get update -y && apt-get upgrade -y && curl -fsSL https://get.docker.com | sh && git clone https://github.com/khodedawsh/marznode && cd marznode && docker compose up -d```

2- Copy Marznode certificate from settings in Marzneshin Panel and pase it in this file :

```nano /var/lib/marznode/client.pem```

3-Downloading Xray core in This Directory : * Files are we downloading now is the latest version of XrayCore , IF you want you can download each version you desire with just putting the Version number in the commend !

```cd && mkdir -p /var/lib/marznode/data && cd /var/lib/marznode/data```

```wget https://github.com/XTLS/Xray-core/releases/download/v24.9.30/Xray-linux-64.zip && unzip Xray-linux-64.zip && rm Xray-linux-64.zip```

4-Moving xray_config.json Files to Marznode Directory :

```cp /root/marznode/xray_config.json /var/lib/marznode/xray_config.json```

5-Moving Xray Files to Marznode Directory :

```cp /var/lib/marznode/data/xray /var/lib/marznode/xray```

6-Editing Compose File :

```cd && cd marznode```

```rm -rf compose.yml && nano compose.yml```

7-Copy and paste this code in your compose.yml file and save it !

```
services:
  marznode:
    image: dawsh/marznode:latest
    restart: always
    network_mode: host

    environment:
      SERVICE_PORT: "5566"
      XRAY_EXECUTABLE_PATH: "/var/lib/marznode/xray"
      XRAY_ASSETS_PATH: "/var/lib/marznode/data"
      XRAY_CONFIG_PATH: "/var/lib/marznode/xray_config.json"
      SSL_CLIENT_CERT_FILE: "/var/lib/marznode/client.pem"
      SSL_KEY_FILE: "./server.key"
      SSL_CERT_FILE: "./server.cert"

    volumes:
      - /var/lib/marznode:/var/lib/marznode
```

8-Now just stop docker service and start again:

```docker compose down --remove-orphans; docker compose up -d```

9-Now Go to Marzneshin Panel and then Go to Node Section Create New node and add Node ip and port 5566 and save it , Done !

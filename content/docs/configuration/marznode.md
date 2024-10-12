---

title: Marznode  
weight: 2

---

### Easy Installation Method:

1. Installing Docker and pulling Marznode with this command:

```bash
apt-get update -y && apt-get upgrade -y && curl -fsSL https://get.docker.com | sh && git clone https://github.com/khodedawsh/marznode && cd marznode && docker compose up -d
```

2. Copy the Marznode certificate from settings in the Marzneshin panel and paste it into this file:

```bash
nano /var/lib/marznode/client.pem
```

3. Downloading the Xray core in this directory:  
   *Files we are downloading now are the latest version of Xray Core. If you want, you can download any version you desire by just putting the version number in the command!*

```bash
cd && mkdir -p /var/lib/marznode/data && cd /var/lib/marznode/data
```

```bash
wget https://github.com/XTLS/Xray-core/releases/download/v24.9.30/Xray-linux-64.zip && unzip Xray-linux-64.zip && rm Xray-linux-64.zip
```

4. Moving `xray_config.json` file to the Marznode directory:

```bash
cp /root/marznode/xray_config.json /var/lib/marznode/xray_config.json
```

5. Moving Xray files to the Marznode directory:

```bash
cp /var/lib/marznode/data/xray /var/lib/marznode/xray
```

6. Editing the Compose file:

```bash
cd && cd marznode
```

```bash
rm -rf compose.yml && nano compose.yml
```

7. Copy and paste this code into your `compose.yml` file and save it:

```yaml
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

8. Now, just stop the Docker service and start it again:

```bash
docker compose down --remove-orphans; docker compose up -d
```

9. Now, go to the Marzneshin panel, then go to the Node section. Create a new node, add the node's IP and port `5566`, and save it. Done!

**Note:** You have to whitelist your node's IP in the master server, whitelist the master IP in your node, and also open the port of the API as well as the ports that you need for configuration inside `xray_core.json`:

```bash
ufw allow 5566
```

For more information on changing and modifying Xray Core settings, you can go to the Node section in the Marzneshin panel.

---


---

title: Hysteria 2  
weight: 2

---

In this tutorial, we will make basic Hysteria 2 core configurations and add it to the user subscription services.

For adding Hysteria 2 in Marznode:

1. Make a certificate using these commands:

```bash
cd /var/lib/marznode/
```

```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"
```

2. Go back to the Marznode default directory:

```bash
cd && cd marznode
```

3. Edit the `compose.yml` file:

```bash
nano compose.yml
```

4. Add Hysteria variables in `compose.yml`:

```yaml
      HYSTERIA_EXECUTABLE_PATH: "/usr/local/bin/hysteria"
      HYSTERIA_CONFIG_PATH: "./hysteria.yaml"
      HYSTERIA_ENABLED: "True"
```

The docker compose should look like this:

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
      HYSTERIA_EXECUTABLE_PATH: "/usr/local/bin/hysteria"
      HYSTERIA_CONFIG_PATH: "./hysteria.yaml"
      HYSTERIA_ENABLED: "True"

    volumes:
      - /var/lib/marznode:/var/lib/marznode
```

Then save the files and restart `compose.yml`:

```bash
docker compose down --remove-orphans; docker compose up -d
```

Now, go to the Node section in the Marzban panel, open the Hysteria section, and add these configurations:

```yaml
listen: :4443
tls:
    cert: /var/lib/marznode/cert.pem
    key: /var/lib/marznode/key.pem
auth:
    type: command
    command: echo
masquerade:
    type: proxy
    proxy:
        url: https://news.ycombinator.com/
        rewriteHost: true
```

*Keep in mind: In the host settings, you must allow insecure connections (because you made a self-hosted TLS certificate for this Hysteria 2 core). For more configuration add-ons, you can visit the Hysteria configuration tutorials at: [https://v2.hysteria.network/docs/getting-started/Server/](https://v2.hysteria.network/docs/getting-started/Server/).

After saving the core, you're done. To add this simple Hysteria 2 setup to your user subscription URL, go to the Services section in the Marzban panel, and then in the services you want to add, just click the inbound you just made!

---

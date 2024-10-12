---
title: Hysteria 2
weight: 2
---
in this toturail we will make Basic Hysteria 2 core cofiguration's and add it to user subscription service's

For adding Hysteria 2 in Marznode :

1-making certificate using this commands:

cd /var/lib/marznode/

openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"

2-Go back to Marznode default directory :

cd && cd marznode

3-Editing compose.yml File

nano compose.yml

4-adding Hysteria Variables in compose.yml :

```   
      HYSTERIA_EXECUTABLE_PATH: "/usr/local/bin/hysteria"
      HYSTERIA_CONFIG_PATH: "./hysteria.yaml"
      HYSTERIA_ENABLED: "True"
```

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
      HYSTERIA_EXECUTABLE_PATH: "/usr/local/bin/hysteria"
      HYSTERIA_CONFIG_PATH: "./hysteria.yaml"
      HYSTERIA_ENABLED: "True"

    volumes:
      - /var/lib/marznode:/var/lib/marznode
```

Then save the files and restart compose.yml

```docker compose down --remove-orphans; docker compose up -d```

Now Go to Node section in Marzban panel and open the Hysteria section and add this configurations :
```
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

*keep in mind : in host setting you must on allow insecure (because you make self hosted tls certificate for this hystera2 core ) for more configuration's addone you can visit Hysteria configuration tutorails at : https://v2.hysteria.network/docs/getting-started/Server/

and save the core , done For adding this simple hysteria 2 in your user subscription url you need to go to Services section in Marzban Panel and then in the services you want to add just click the inbound you just maked !

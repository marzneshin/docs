---
title: sing-box
weight: 2
---

[Sing-box](https://sing-box.sagernet.org/) is yet another backend supported by marznode.

Currently supported protocols include:
- VMess
- VLESS
- Trojan
- Shadowsocks
- Hysteria2
- TUIC


## Configuration settings on marznode
The following environmental variables are used to utilize and configure sing-box on marznode:
- `SING_BOX_ENABLED` `True`/`False`
- `SING_BOX_EXECUTABLE_PATH` Path to the sing-box binary. The binary should include `with_v2ray_api` tag.
- `SING_BOX_CONFIG_PATH` Path to sing-box config.
- `SING_BOX_RESTART_ON_FAILURE` Whether to restart in case of crash/exit. `True`/`False`
- `SING_BOX_RESTART_ON_FAILURE_INTERVAL` Interval between restarts in case of crash.

## Example, using the marznode docker image
Sing-box is included by default in [marznode docker image](https://hub.docker.com/r/dawsh/marznode), with the binary placed in `/usr/local/bin/sing-box`.

A fine compose.yml looks like this:

```yaml
services:
  marznode:
    image: dawsh/marznode:latest
    restart: always
    network_mode: host
    command: [ "sh", "-c", "sleep 10 && python3 marznode.py" ]

    environment:
      XRAY_EXECUTABLE_PATH: "/usr/local/bin/xray"
      XRAY_ASSETS_PATH: "/usr/local/lib/xray"
      XRAY_CONFIG_PATH: "/var/lib/marznode/xray_config.json"
      
      # The following variables tell marznode to run sing-box:
      SING_BOX_ENABLED: "True"
      SING_BOX_EXECUTABLE_PATH: "/usr/local/bin/sing-box"
      SING_BOX_CONFIG_PATH: "/var/lib/marznode/sing-box.json"
      
      HYSTERIA_EXECUTABLE_PATH: "/usr/local/bin/hysteria"
      SSL_CLIENT_CERT_FILE: "/var/lib/marznode/client.pem"
      SSL_KEY_FILE: "./server.key"
      SSL_CERT_FILE: "./server.cert"

    volumes:
      - /var/lib/marznode:/var/lib/marznode
```

Make sure `/var/lib/marznode/sing-box.json` exists, and is a valid sing-box config.

## See also
- [configuration documents](https://sing-box.sagernet.org/configuration/)
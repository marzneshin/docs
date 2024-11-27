---
title: Xray-core
weight: 1
---


[Xray-core](https://github.com/xtls/xray-core) is a backend supported by marznode. Xray is enabled by default on marznode.


Currently supported protocols include:
- VMess
- VLESS
- Trojan
- Shadowsocks


## Configuration settings on marznode
The following environmental variables are used to utilize and configure Xray on marznode:
- `XRAY_ENABLED` `True`/`False`
- `XRAY_EXECUTABLE_PATH` Path to the xray binary.
- `XRAY_CONFIG_PATH` Path to xray config.
- `XRAY_RESTART_ON_FAILURE` Whether to restart in case of crash/exit. `True`/`False`
- `XRAY_RESTART_ON_FAILURE_INTERVAL` Interval between restarts in case of crash.

## See also
- [configuration documents](https://xtls.github.io/config/)

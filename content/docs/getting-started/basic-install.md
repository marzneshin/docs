---
title: Basic Installation | Docker
weight: 1
---

To get started, you just need a linux machine.

{{< callout type="info" >}}
  TLDR for installation:

  ```bash
  sudo bash -c "$(curl -sL https://github.com/khodedawsh/Marzneshin/raw/master/script.sh)" @ install
  ```
  After that make sure you create an admin:
  ```bash
  marzneshin cli admin create --sudo
  ```
{{< /callout >}}

Marzneshin currently supports the following databases. SQLite is preferred for small setups, while MariaDB is recommended for larger configurations.
{{< tabs items="mariadb,mysql,sqlite" >}}

  {{< tab >}}```bash
sudo bash -c "$(curl -sL https://github.com/khodedawsh/Marzneshin/raw/master/script.sh)" @ install --database mariadb
```{{< /tab >}}
  {{< tab >}}```bash
sudo bash -c "$(curl -sL https://github.com/khodedawsh/Marzneshin/raw/master/script.sh)" @ install --database mysql
```{{< /tab >}}
  {{< tab >}}```bash
sudo bash -c "$(curl -sL https://github.com/khodedawsh/Marzneshin/raw/master/script.sh)" @ install
```{{< /tab >}}

{{< /tabs >}}

{{< callout type="warning" >}}
  To install the latest **nightly** release use the `--nightly` flag.
{{< /callout >}}

Once the installation is complete:

- You'd notice the logs, which you could stop watching by pressing `Ctrl+C`; The process will continue running normally.
- the configuration file can be found at `/etc/opt/marzneshin/.env` (refer to [configuration](/docs/configuration/marzneshin) page)
- Data files will be placed at `/var/lib/marzneshin`; e.g. the sqlite database.
- You can access the Marzneshin dashboard by opening a web browser and navigating
  to `http://<SERVER_IP>:8000/dashboard/`

Next, you need to create a sudo admin for logging into the Marzneshin dashboard using the following command

```bash
marzneshin cli admin create --sudo
```

That's it! You can login to your dashboard using these credentials

To see the help message of the Marzneshin script, run the following command

```bash
marzneshin --help
```

### Configuring TLS

Refer to [running behind nginx](/docs/how-to-guides/behind-nginx)
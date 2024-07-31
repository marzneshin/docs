---
title: Marzneshin
weight: 1
---
If you are eager to run the project using the source code, check the section below

## Manual install (advanced)

{{% steps %}}

### Get Marzneshin

Clone this project and install the dependencies (you'd need Python >= 3.10)

```bash
git clone https://github.com/khodedawsh/Marzneshin
cd Marzneshin/
wget -qO- https://bootstrap.pypa.io/get-pip.py | python3 -
python3 -m pip install -r requirements.txt
```

Alternatively, to run in an isolated environment you can create a [virtual environment](https://pypi.org/project/virtualenv/)


### Build the dashboard

To install dashboard dependencies and build the dashboard:

```bash
make dashboard-deps
make dashboard-build
```

note that you'll need pnpm and npm installed.

### Setup marzneshin-cli

If you want to use `marzneshin-cli`, you should link it to a file in your `$PATH`, make it executable, and install the
auto-completion:

```bash
sudo ln -s $(pwd)/marzneshin-cli.py /usr/bin/marzneshin-cli
sudo chmod +x /usr/bin/marzneshin-cli
marzneshin-cli completion install
```

### Configuration

Now it's time for configuration

Make a copy of `.env.example` file, take a look and edit it using a text editor like `nano`.

```bash
cp .env.example .env
nano .env
```

> Check out [marzneshin configuration](/docs/configuration/marzneshin) guide for more information

### Generate the database

Currently to generate the db, you should run
```bash
alembic upgrade head
```

### Startup

Eventually, launch the application using one of the below commands


| Using systemd (recommended)         | Using make (one-time)                              |
| :---------------------------------- | ------------------------------------- |
| ```bash tools/service-install.sh```<br>```systemctl enable --now marzneshin``` | ```make start``` |

By default the app will be run on `http://localhost:8000/dashboard`. You can configure it using changing
the `UVICORN_HOST` and `UVICORN_PORT` environment variables.

### Configuring tls

Refer to [running behind nginx](/docs/how-to-guides/behind-nginx)

{{% /steps %}}

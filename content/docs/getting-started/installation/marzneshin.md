---
title: Installing Marzneshin
weight: 1
---

Run the following command

```bash
sudo bash -c "$(curl -sL https://github.com/khodedawsh/Marzneshin/raw/master/script.sh)" @ install
```

To install with mariadb:

```bash
sudo bash -c "$(curl -sL https://github.com/khodedawsh/Marzneshin/raw/master/script.sh)" @ install --database mariadb
```

You could also use mysql by writing mysql instead, however mariadb is **recommended**.
Also to install the latest nightly release use the `--nightly` option.

Once the installation is complete:

- You'd notice the logs, which you could stop watching by pressing `Ctrl+C`; The process will continue running normally.
- the configuration file can be found at `/etc/opt/marzneshin/.env` (refer to [configurations](/docs/configuration/marzneshin) page
  to see variables)
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

If you are eager to run the project using the source code, check the section below

## Manual install (advanced)

Clone this project and install the dependencies (you'd need Python >= 3.10)

```bash
git clone https://github.com/khodedawsh/Marzneshin
cd Marzneshin/
wget -qO- https://bootstrap.pypa.io/get-pip.py | python3 -
python3 -m pip install -r requirements.txt
```

Alternatively, to have an isolated environment you can use [Python Virtualenv](https://pypi.org/project/virtualenv/)

To install dashboard dependencies and build the dashboard:

```bash
make dashboard-deps
make dashboard-build
```

note that you'll need pnpm and npm installed.

If you want to use `marzneshin-cli`, you should link it to a file in your `$PATH`, make it executable, and install the
auto-completion:

```bash
sudo ln -s $(pwd)/marzneshin-cli.py /usr/bin/marzneshin-cli
sudo chmod +x /usr/bin/marzneshin-cli
marzneshin-cli completion install
```

Now it's time to configuration

Make a copy of `.env.example` file, take a look and edit it using a text editor like `nano`.

```bash
cp .env.example .env
nano .env
```

> Check out [marzneshin configuration](/docs/configuration/marzneshin) guide for more information

Eventually, launch the application using the below command

```bash
make start
```

To launch with linux systemctl (copy marzneshin.service file to `/var/lib/marzneshin/marzneshin.service`)

```
systemctl enable /var/lib/marzneshin/marzneshin.service
systemctl start marzneshin
```

To use with nginx

```
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name  example.com;

    ssl_certificate      /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key  /etc/letsencrypt/live/example.com/privkey.pem;

    location ~* /(dashboard|static|locales|api|docs|redoc|openapi.json) {
        proxy_pass http://0.0.0.0:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

    # xray-core ws-path: /
    # client ws-path: /marzneshin/me/2087
    #
    # All traffic is proxed through port 443, and send to the xray port(2087, 2088 etc.).
    # The '/marzneshin' in location regex path can changed any characters by yourself.
    #
    # /${path}/${username}/${xray-port}
    location ~* /marzneshin/.+/(.+)$ {
        proxy_redirect off;
        proxy_pass http://127.0.0.1:$1/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

or

```
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name  marzneshin.example.com;

    ssl_certificate      /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key  /etc/letsencrypt/live/example.com/privkey.pem;

    location / {
        proxy_pass http://0.0.0.0:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

By default the app will be run on `http://localhost:8000/dashboard`. You can configure it using changing
the `UVICORN_HOST` and `UVICORN_PORT` environment variables.

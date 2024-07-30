---
title: Marzneshin
---

> You can set settings below using environment variables or placing them in `.env` file.

## Basic

| Variable                        | Description                                                                                           |
| ------------------------------- | ----------------------------------------------------------------------------------------------------- |
| UVICORN_HOST                    | Bind application to this host (default: `0.0.0.0`)                                                    |
| UVICORN_PORT                    | Bind application to this port (default: `8000`)                                                       |
| UVICORN_UDS                     | Bind application to a UNIX domain socket                                                              |
| UVICORN_SSL_CERTFILE            | SSL certificate file to have application on https                                                     |
| UVICORN_SSL_KEYFILE             | SSL key file to have application on https                                                             |
| SQLALCHEMY_DATABASE_URL         | Database URL ([SQLAlchemy's docs](https://docs.sqlalchemy.org/en/20/core/engines.html#database-urls)) |
| JWT_ACCESS_TOKEN_EXPIRE_MINUTES | Expire time for the Access Tokens in minutes, `0` considered as infinite (default: `1440`)            |

## Subscription and VPN customization

| Variable                    | Description                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------- |
| CUSTOM_TEMPLATES_DIRECTORY  | Customized templates directory (default: `app/templates`)                                    |
| CLASH_SUBSCRIPTION_TEMPLATE | The template that will be used for generating clash configs (default: `clash/default.yml`)   |
| SUBSCRIPTION_PAGE_TEMPLATE  | The template used for generating subscription info page (default: `subscription/index.html`) |
| SUBSCRIPTION_URL_PREFIX     | Prefix of subscription URLs                                                                  |
| HOME_PAGE_TEMPLATE          | Decoy page template (default: `home/index.html`)                                             |

## Telegram

| Variable           | Description                                                                                  |
| ------------------ | -------------------------------------------------------------------------------------------- |
| TELEGRAM_API_TOKEN | Telegram bot API token (get token from [@botfather](https://t.me/botfather))                 |
| TELEGRAM_ADMIN_ID  | Numeric Telegram ID of admin (use [@userinfobot](https://t.me/userinfobot) to found your ID) |
| TELEGRAM_PROXY_URL | Run Telegram Bot over proxy                                                                  |

## Notification & Webhook

| Variable                          | Description                                                                                           |
| --------------------------------- | ----------------------------------------------------------------------------------------------------- |
| WEBHOOK_ADDRESS                   | Webhook address to send notifications to. Webhook notifications will be sent if this value was set.   |
| WEBHOOK_SECRET                    | Webhook secret will be sent with each request as `x-webhook-secret` in the header (default: `None`)   |
| NUMBER_OF_RECURRENT_NOTIFICATIONS | How many times to retry if an error detected in sending a notification (default: `3`)                 |
| RECURRENT_NOTIFICATIONS_TIMEOUT   | Timeout between each retry if an error detected in sending a notification in seconds (default: `180`) |
| NOTIFY_REACHED_USAGE_PERCENT      | At which percentage of usage to send the warning notification (default: `80`)                         |
| NOTIFY_DAYS_LEFT                  | When to send warning notification about expiration (default: `3`)                                     |

## Development and Documentation

| Variable | Description                                                                                 |
| -------- | ------------------------------------------------------------------------------------------- |
| DOCS     | Whether API documents should be available on `/docs` and `/redoc` or not (default: `False`) |
| DEBUG    | Debug mode for development (default: `False`)                                               |

## .env File Example

```sh
SQLALCHEMY_DATABASE_URL=
UVICORN_HOST=
UVICORN_PORT=
UVICORN_UDS=
UVICORN_SSL_CERTFILE=
UVICORN_SSL_KEYFILE=
SUBSCRIPTION_URL_PREFIX=
CUSTOM_TEMPLATES_DIRECTORY=
CLASH_SUBSCRIPTION_TEMPLATE=
SUBSCRIPTION_PAGE_TEMPLATE=
HOME_PAGE_TEMPLATE=
TELEGRAM_API_TOKEN=
TELEGRAM_ADMIN_ID=
TELEGRAM_PROXY_URL=
JWT_ACCESS_TOKEN_EXPIRE_MINUTES=
DOCS=true
DEBUG=true
WEBHOOK_ADDRESS="http://localhost:9000"
WEBHOOK_SECRET="dont-tell-anybody"
NUMBER_OF_RECURRENT_NOTIFICATIONS=
RECURRENT_NOTIFICATIONS_TIMEOUT=
NOTIFY_REACHED_USAGE_PERCENT=
NOTIFY_DAYS_LEFT=
```

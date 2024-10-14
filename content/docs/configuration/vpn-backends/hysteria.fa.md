---

title: هیستریا ۲  
weight: 2

---

در این آموزش، ما پیکربندی‌های اولیه هسته هیستریا ۲ را انجام می‌دهیم و آن را به سرویس‌های اشتراک کاربران اضافه می‌کنیم.

برای اضافه کردن هیستریا ۲ در مرزنود :

1. یک گواهی با استفاده از این دستورات بسازید:

```bash
cd /var/lib/marznode/
```

```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"
```

2. به دایرکتوری پیش‌فرض مرزنود برگردید:

```bash
cd && cd marznode
```

3. فایل `compose.yml` را ویرایش کنید:

```bash
nano compose.yml
```

4. متغیرهای هیستریا را به فایل `compose.yml` اضافه کنید:

```yaml
      HYSTERIA_EXECUTABLE_PATH: "/usr/local/bin/hysteria"
      HYSTERIA_CONFIG_PATH: "./hysteria.yaml"
      HYSTERIA_ENABLED: "True"
```

فایل docker-compose باید به این شکل باشد:

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

سپس فایل‌ها را ذخیره کنید و `compose.yml` را مجدداً راه‌اندازی کنید:

```bash
docker compose down --remove-orphans; docker compose up -d
```

اکنون به بخش نود ها در پنل مرزنیشین بروید، بخش Hysteria را باز کنید و این پیکربندی‌ها را اضافه کنید:

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

*به یاد داشته باشید: در تنظیمات هاست باید اجازه ارتباطات ناامن را بدهید (زیرا شما برای این هسته هیستریا ۲ یک گواهی TLS خود میزبان ساخته‌اید). برای افزودن پیکربندی‌های بیشتر، می‌توانید به آموزش‌های پیکربندی هیستریا در: [https://v2.hysteria.network/docs/getting-started/Server/](https://v2.hysteria.network/docs/getting-started/Server/) مراجعه کنید.

پس از ذخیره کردن هسته، کار تمام است. برای اضافه کردن این تنظیمات ساده هیستریا ۲ به URL اشتراک کاربران، به بخش سرویس ها در پنل مرزنشین بروید و در سرویس‌هایی که می‌خواهید اضافه کنید، بر روی ورودی که ساخته‌اید کلیک کنید!

---

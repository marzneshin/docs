---
title: "مرزنود"
weight: 2
---

### پیش‌نیازها

- Docker
- Docker Compose

{{< callout type="info" >}}
اطمینان حاصل کنید که Docker نصب شده است.

```sh
curl -fsSL https://get.docker.com | sh
```

{{< /callout >}}

{{% steps %}}

### راه‌اندازی گواهی‌نامه

مسیر های لازم را ایجاد کنید:

```sh
mkdir -p /var/lib/marznode/
```

گواهی‌نامه خود را از تنظیمات مرزنشین دریافت کرده و در این مسیر قرار دهید:

`/var/lib/marznode/client.pem`

### راه‌اندازی پیکربندی Xray

برای نود خود پیکربندی Xray فراهم کنید؛ شما می‌توانید بعداً در داشبورد آن را ویرایش کنید.
در این مورد، ما پیکربندی نمونه را از مخزن مرزنود راه‌اندازی می‌کنیم:

```sh
curl -L https://github.com/marzneshin/marznode/raw/master/xray_config.json > /var/lib/marznode/xray_config.json
```

### دریافت مرزنود

برای کلون کردن مرزنود:

```sh
git clone https://github.com/marzneshin/marznode
cd marznode
```

### راه‌اندازی کانتینر

برای راه‌اندازی نود خود، دستور زیر را اجرا کنید:

```shell
docker compose -f ./compose.yml up -d
```

{{% /steps %}}

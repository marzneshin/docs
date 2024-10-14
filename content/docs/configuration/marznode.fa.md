---

title: Marznode  
weight: 2

---

### روش نصب آسان:

1. نصب داکر و پول کردن ایمیج مرزنود با این دستور:

```bash
apt-get update -y && apt-get upgrade -y && curl -fsSL https://get.docker.com | sh && git clone https://github.com/khodedawsh/marznode && cd marznode && docker compose up -d
```

2. کپی کردن گواهی مرزنود از تنظیمات در پنل مرزنشین و قرار دادن آن در این فایل:

```bash
nano /var/lib/marznode/client.pem
```

3. دانلود هسته Xray در این دایرکتوری:  
   *فایلی که در حال حاضر دانلود می‌کنیم آخرین نسخه هسته Xray است. اگر می‌خواهید، می‌توانید هر نسخه دیگری را با تغییر شماره نسخه در دستور دانلود کنید!*

```bash
cd && mkdir -p /var/lib/marznode/data && cd /var/lib/marznode/data
```

```bash
wget https://github.com/XTLS/Xray-core/releases/download/v24.9.30/Xray-linux-64.zip && unzip Xray-linux-64.zip && rm Xray-linux-64.zip
```

4. انتقال فایل `xray_config.json` به دایرکتوری مرزنود :

```bash
cp /root/marznode/xray_config.json /var/lib/marznode/xray_config.json
```

5. انتقال فایل‌های Xray به دایرکتوری مرزنود :

```bash
cp /var/lib/marznode/data/xray /var/lib/marznode/xray
```

6. ویرایش فایل کامپوز :

```bash
cd && cd marznode
```

```bash
rm -rf compose.yml && nano compose.yml
```

7. این کد را در فایل `compose.yml` خود کپی و جای‌گذاری کنید و سپس ذخیره کنید:

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

    volumes:
      - /var/lib/marznode:/var/lib/marznode
```

8. اکنون، فقط سرویس داکر را متوقف کرده و دوباره شروع کنید:

```bash
docker compose down --remove-orphans; docker compose up -d
```

9. حالا به پنل مرزنشین بروید، سپس به بخش نود ها بروید. یک نود جدید ایجاد کنید، ایپی و پورت نود `5566` را اضافه کنید و ذخیره کنید. تمام!

**نکته:** شما باید ایپی نود خود را در سرور اصلی به لیست سفید اضافه کنید، ایپی سرور اصلی را در نود خود سفید کنید و همچنین پورت API و پورت‌هایی که برای پیکربندی در `xray_core.json` نیاز دارید را باز کنید:

```bash
ufw allow 5566
```

برای اطلاعات بیشتر در مورد تغییر و اصلاح تنظیمات هسته Xray، می‌توانید به بخش نود در پنل مرزنشین مراجعه کنید.

---

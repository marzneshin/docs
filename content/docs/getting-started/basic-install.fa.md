---
title: "نصب پایه | Docker"
weight: 1
---

برای شروع، شما فقط به یک ماشین لینوکس نیاز دارید.

{{< callout type="info" >}}
خلاصه‌ای از مراحل نصب:

```bash
sudo bash -c "$(curl -sL https://github.com/marzneshin/Marzneshin/raw/master/script.sh)" @ install
```

پس از آن، اطمینان حاصل کنید که یک حساب کاربری ادمین ایجاد کنید:

```bash
marzneshin cli admin create --sudo
```

{{< /callout >}}

مرزنشین در حال حاضر از پایگاه‌های داده زیر پشتیبانی می‌کند. SQLite برای نصب‌های کوچک ترجیح داده می‌شود، در حالی که MariaDB برای پیکربندی‌های بزرگتر توصیه می‌شود.

{{< tabs items="mariadb,mysql,sqlite" >}}

{{< tab >}}
```bash
sudo bash -c "$(curl -sL https://github.com/marzneshin/Marzneshin/raw/master/script.sh)" @ install --database mariadb
```{{< /tab >}}

{{< tab >}}
```bash
sudo bash -c "$(curl -sL https://github.com/marzneshin/Marzneshin/raw/master/script.sh)" @ install --database mysql
```{{< /tab >}}

{{< tab >}}
```bash
sudo bash -c "$(curl -sL https://github.com/marzneshin/Marzneshin/raw/master/script.sh)" @ install
```{{< /tab >}}

{{< /tabs >}}

{{< callout type="warning" >}}
برای نصب آخرین **نسخه شبانه** از فلگ `--nightly` استفاده کنید.
{{< /callout >}}

پس از تکمیل نصب:

- شما لاگ‌ها را مشاهده خواهید کرد که می‌توانید با فشار دادن `Ctrl+C` از تماشای آن‌ها دست بکشید؛ فرآیند به طور معمول ادامه خواهد یافت.
- فایل پیکربندی در `/etc/opt/marzneshin/.env` قرار دارد (به صفحه [پیکربندی](/docs/configuration/marzneshin) مراجعه کنید).
- فایل‌های داده در `/var/lib/marzneshin` قرار می‌گیرند؛ به عنوان مثال، پایگاه داده sqlite.
- شما می‌توانید به داشبورد مرزنشین با باز کردن یک مرورگر وب و رفتن به `http://<SERVER_IP>:8000/dashboard/` دسترسی پیدا کنید.

در مرحله بعد، باید یک حساب کاربری ادمین با دسترسی sudo برای ورود به داشبورد مرزنشین ایجاد کنید با استفاده از دستور زیر:

```bash
marzneshin cli admin create --sudo
```

این همه چیز است! شما می‌توانید با استفاده از این اعتبارنامه‌ها به داشبورد خود وارد شوید.

برای مشاهده پیام راهنما در مورد اسکریپت مرزنشین، دستور زیر را اجرا کنید:

```bash
marzneshin --help
```

### پیکربندی TLS

به [اجرای برنامه در پشت Nginx](/docs/how-to-guides/behind-nginx) مراجعه کنید.

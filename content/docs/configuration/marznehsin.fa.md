---

title: Marzneshin  
weight: 1

---

> می‌توانید تنظیمات زیر را با استفاده از متغیرهای محیطی یا قرار دادن آن‌ها در فایل `.env` پیکربندی کنید.

## تنظیمات پایه

| متغیر                         | توضیحات                                                                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------------------ |
| UVICORN_HOST                   | اتصال برنامه به این هاست (پیش‌فرض: `0.0.0.0`)                                                       |
| UVICORN_PORT                   | اتصال برنامه به این پورت (پیش‌فرض: `8000`)                                                            |
| UVICORN_UDS                    | اتصال برنامه به یک دامنه سوکت UNIX                                                                     |
| UVICORN_SSL_CERTFILE           | فایل گواهی SSL برای اجرای برنامه بر روی https                                                          |
| UVICORN_SSL_KEYFILE            | فایل کلید SSL برای اجرای برنامه بر روی https                                                          |
| SQLALCHEMY_DATABASE_URL        | آدرس URL پایگاه داده ([مستندات SQLAlchemy](https://docs.sqlalchemy.org/en/20/core/engines.html#database-urls)) |
| JWT_ACCESS_TOKEN_EXPIRE_MINUTES| زمان انقضای توکن‌های دسترسی به دقیقه (۰ به معنای بی‌نهایت) (پیش‌فرض: `1440`)                         |
| AUTH_GENERATION_ALGORITHM      | الگوریتم رمزنگاری رمز عبور احراز هویت (پیش‌فرض: "xxh128"، گزینه‌ها: "xxh128"، "plain")               |
| REVERSIBLE_KEY                 | پشتیبانی از کلید قابل برگشت (پیش‌فرض: False، گزینه‌ها: "False"، "True")                               |

## سفارشی‌سازی اشتراک و VPN

| متغیر                      | توضیحات                                                                                 |
| ---------------------------| --------------------------------------------------------------------------------------- |
| CUSTOM_TEMPLATES_DIRECTORY  | دایرکتوری قالب‌های سفارشی (پیش‌فرض: `app/templates`)                                    |
| CLASH_SUBSCRIPTION_TEMPLATE | قالب مورد استفاده برای تولید تنظیمات Clash (پیش‌فرض: `clash/default.yml`)              |
| SUBSCRIPTION_PAGE_TEMPLATE  | قالب مورد استفاده برای تولید صفحه اطلاعات اشتراک (پیش‌فرض: `subscription/index.html`)  |
| SUBSCRIPTION_URL_PREFIX     | پیشوند URL‌های اشتراک                                                                    |
| HOME_PAGE_TEMPLATE          | قالب صفحه نمایشی تقلبی (پیش‌فرض: `home/index.html`)                                     |

## تنظیمات تلگرام

| متغیر               | توضیحات                                                                                             |
| ------------------- | -------------------------------------------------------------------------------------------------- |
| TELEGRAM_API_TOKEN  | توکن API ربات تلگرام (توکن را از [@botfather](https://t.me/botfather) دریافت کنید)                 |
| TELEGRAM_ADMIN_ID   | شناسه عددی تلگرام ادمین (برای پیدا کردن شناسه خود از [@userinfobot](https://t.me/userinfobot) استفاده کنید) |
| TELEGRAM_PROXY_URL  | اجرای ربات تلگرام از طریق پروکسی                                                                    |

## اعلان و وب‌هوک

| متغیر                            | توضیحات                                                                                              |
| ---------------------------------| ---------------------------------------------------------------------------------------------------- |
| WEBHOOK_ADDRESS                  | آدرس وب‌هوک برای ارسال اعلان‌ها. اعلان‌های وب‌هوک اگر این مقدار تنظیم شود، ارسال خواهند شد.        |
| WEBHOOK_SECRET                   | راز وب‌هوک که با هر درخواست به‌عنوان `x-webhook-secret` در هدر ارسال می‌شود (پیش‌فرض: `None`)       |
| NUMBER_OF_RECURRENT_NOTIFICATIONS | تعداد تکرار اعلان‌ها در صورت بروز خطا در ارسال (پیش‌فرض: `3`)                                      |
| RECURRENT_NOTIFICATIONS_TIMEOUT   | زمان انتظار بین هر تلاش مجدد در صورت بروز خطا در ارسال اعلان‌ها به ثانیه (پیش‌فرض: `180`)            |
| NOTIFY_REACHED_USAGE_PERCENT      | درصد استفاده‌ای که در آن اعلان هشدار ارسال شود (پیش‌فرض: `80`)                                     |
| NOTIFY_DAYS_LEFT                  | زمان ارسال اعلان هشدار در مورد انقضا به تعداد روزهای باقیمانده (پیش‌فرض: `3`)                       |

## توسعه و مستندات

| متغیر  | توضیحات                                                                                   |
| ------ | ----------------------------------------------------------------------------------------- |
| DOCS   | آیا مستندات API در دسترس باشد یا خیر (پیش‌فرض: `False`)                                   |
| DEBUG  | حالت دیباگ برای توسعه (پیش‌فرض: `False`)                                                  |

## نمونه فایل .env

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
AUTH_GENERATION_ALGORITHM="xxh128"
REVERSIBLE_KEY="False"
DOCS=true
DEBUG=true
WEBHOOK_ADDRESS="http://localhost:9000"
WEBHOOK_SECRET="dont-tell-anybody"
NUMBER_OF_RECURRENT_NOTIFICATIONS=
RECURRENT_NOTIFICATIONS_TIMEOUT=
NOTIFY_REACHED_USAGE_PERCENT=
NOTIFY_DAYS_LEFT=
```

## کنترل متغیرهای Marzneshin از طریق خط فرمان

| متغیر                | توضیحات                              |
| ---------------------| -------------------------------------|
| marzneshin update     | می‌توانید Marzneshin را به‌راحتی به‌روزرسانی کنید. |
| marzneshin stop       | می‌توانید Marzneshin را متوقف کنید.  |
| marzneshin start      | می‌توانید Marzneshin را شروع کنید.   |

---

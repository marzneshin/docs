---

عنوان: "مرزنشین"

---

اگر مایل هستید پروژه را با استفاده از کد منبع اجرا کنید، مراحل زیر را دنبال کنید.

## نصب دستی (پیشرفته)

{{% steps %}}

### دریافت مرزنشین

این پروژه را کلون کرده و وابستگی‌ها را نصب کنید (Python 3.10 یا بالاتر نیاز است):

```bash
git clone https://github.com/marzneshin/Marzneshin
cd Marzneshin/
wget -qO- https://bootstrap.pypa.io/get-pip.py | python3 -
python3 -m pip install -r requirements.txt
```

به‌طور جایگزین، برای اجرا در یک محیط ایزوله می‌توانید از [محیط مجازی](https://pypi.org/project/virtualenv/) استفاده کنید.

### ساخت داشبورد

برای نصب وابستگی‌های داشبورد و ساخت آن:

```bash
make dashboard-deps
make dashboard-build
```

توجه داشته باشید که باید pnpm و npm را نصب کرده باشید.

### راه‌اندازی marzneshin-cli

اگر قصد دارید از `marzneshin-cli` استفاده کنید، باید آن را به فایلی در مسیر `$PATH` خود لینک کنید، قابل اجرا کنید و نصب خودکار تکمیل (auto-completion) را انجام دهید:

```bash
sudo ln -s $(pwd)/marzneshin-cli.py /usr/bin/marzneshin-cli
sudo chmod +x /usr/bin/marzneshin-cli
marzneshin-cli completion install
```

### پیکربندی

اکنون وقت پیکربندی است.

یک نسخه از فایل `.env.example` را کپی کنید، نگاهی بیندازید و آن را با استفاده از ویرایشگر متنی مانند `nano` ویرایش کنید:

```bash
cp .env.example .env
nano .env
```

> برای اطلاعات بیشتر، راهنمای [پیکربندی مرزنشین](/docs/configuration/marzneshin) را بررسی کنید.

### تولید پایگاه داده

در حال حاضر برای تولید پایگاه داده، باید این دستور را اجرا کنید:

```bash
alembic upgrade head
```

### راه‌اندازی

در نهایت، برنامه را با استفاده از یکی از دستورات زیر راه‌اندازی کنید:

| استفاده از systemd (توصیه‌شده)                                             | استفاده از make (یک‌بار)      |
| :--------------------------------------------------------------------- | --------------------- |
| `bash tools/service-install.sh`<br>`systemctl enable --now marzneshin` | `make start`          |

به‌طور پیش‌فرض، برنامه در `http://localhost:8000/dashboard` اجرا خواهد شد. شما می‌توانید با تغییر متغیرهای محیطی `UVICORN_HOST` و `UVICORN_PORT` آن را پیکربندی کنید.

### پیکربندی TLS

به [اجرای برنامه در پشت Nginx](/docs/how-to-guides/behind-nginx) مراجعه کنید.

{{% /steps %}}

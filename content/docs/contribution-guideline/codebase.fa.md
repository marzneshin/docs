---

title: ساختار کد  
next: پشتیبانی  
prev: docs/developer-guide  
toc: true  
weight: 1  

---

## ساختار پروژه

برای نمایش ساختار پروژه با استفاده از یادداشت `filetree`، کد به شکل زیر خواهد بود:

{{< filetree/container >}}
{{< filetree/folder name="marzneshin" state="open">}}
{{< filetree/folder name="app" >}}
کد بک‌اند  
{{< /filetree/folder >}}
{{< filetree/folder name="dashboard" >}}
کد فرانت‌اند  
{{< /filetree/folder >}}
{{< filetree/folder name="cli" >}}
کد CLI  
{{< /filetree/folder >}}
{{< /filetree/folder >}}
{{< /filetree/container >}}

| نام پوشه    | توضیحات                               |
| ----------- | ------------------------------------- |
| `app`       | کد بک‌اند (FastAPI - پایتون)          |
| `dashboard` | کد فرانت‌اند (React - Typescript)     |
| `cli`       | کد خط فرمان (Typer - پایتون)          |

## بک‌اند

بک‌اند با استفاده از FastAPI توسعه داده شده و از SQLAlchemy به عنوان ORM برای عملیات‌های پایگاه داده استفاده می‌کند. مدل‌های Pydantic در پوشه `app/models` قرار دارند و تمامی عملیات‌های مرتبط با پایگاه داده و مدل‌ها در پوشه `app/db` قرار دارند. اسکریپت‌های مهاجرت پایگاه داده (Alembic) در پوشه `app/db/migrations` قرار دارند.

### قالب‌بندی کد پایتون

برای حفظ یکنواختی در کد، نیاز است که تمام کدها با استفاده از این دستور قالب‌بندی شوند:

```bash
black .
```

## فرانت‌اند

فرانت‌اند از یک ساختار توسعه مبتنی بر ویژگی استفاده می‌کند. ویژگی‌ها در اصل شامل اجزا، هوک‌ها، منطق‌ها و سرویس‌هایی هستند که تجربه کاربری را با قابلیت‌های دامنه و رابط کاربری ترکیب می‌کنند.

{{< filetree/container >}}
{{< filetree/folder name="routes" >}}
منطق مسیریابی  
{{< /filetree/folder >}}
{{< filetree/folder name="features" >}}
{{< filetree/folder name="users" >}}
ویژگی اصلی دامنه  
{{< /filetree/folder >}}
{{< filetree/folder name="nodes" >}}
ویژگی اصلی دامنه  
{{< /filetree/folder >}}
{{< filetree/folder name="hosts" >}}
ویژگی اصلی دامنه  
{{< /filetree/folder >}}
{{< filetree/folder name="entity-table" >}}
ویژگی پشتیبانی  
{{< /filetree/folder >}}
{{< filetree/folder name="github-repo" >}}
ویژگی پشتیبانی  
{{< /filetree/folder >}}
{{< /filetree/folder >}}
{{< filetree/folder name="components" >}}
{{< filetree/folder name="ui" >}}
اجزای اتمی  
{{< /filetree/folder >}}
{{< /filetree/folder >}}
{{< /filetree/container >}}

| نام پوشه      | توضیحات                              |
| ------------- | ------------------------------------ |
| `routes`      | مسیریابی با @tanstack/react-router    |
| `features`    | پوشه ویژگی‌ها                        |
| `users`       | ویژگی اصلی دامنه                     |
| `nodes`       | ویژگی اصلی دامنه                     |
| `hosts`       | ویژگی اصلی دامنه                     |
| `entity-table`| ویژگی پشتیبانی                       |
| `github-repo` | ویژگی پشتیبانی                       |
| `components`  | اجزای عمومی                          |
| `ui`          | اجزای اتمی                           |

### ویژگی‌ها

پوشه `features` شامل تمامی ویژگی‌ها است. ویژگی‌ها به دو دسته اصلی تقسیم می‌شوند: **ویژگی‌های اصلی دامنه** و **ویژگی‌های پشتیبانی**. ویژگی‌های اصلی دامنه مجموعه‌ای از راه‌حل‌ها را برای حل مشکلی که برنامه به آن پرداخته ارائه می‌دهند. در حالی که ویژگی‌های پشتیبانی مجموعه‌ای از راه‌حل‌هایی را ارائه می‌دهند که از مدل دامنه مستقل هستند، اما برای تجربه کاربری کامل ضروری هستند.

### اجزای عمومی

پوشه `components` شامل اجزای عمومی React است که توسط ویژگی‌ها مجدداً استفاده می‌شوند. همچنین همین منطق برای پوشه‌های `hooks` و `types` نیز صدق می‌کند.

### اجزای اتمی

پوشه `components/ui` شامل اجزای اتمی است که ستون فقرات برنامه را تشکیل می‌دهند. این اجزا بر اساس الگوی shadcn ساخته شده‌اند، هرچند که احتمالاً با گذشت زمان تغییرات زیادی در آن‌ها ایجاد شده است.

### ابزارها

این توابع عمومی هستند و در کل کد استفاده می‌شوند، هرچند که با پیچیده‌تر شدن و افزایش استفاده، به پوشه‌های خاص خود یا پوشه ویژگی‌ها منتقل خواهند شد.

### مسیرها و صفحات

پوشه `routes` شامل مسیریابی tanstack و صفحات مربوطه است.

### دستورالعمل‌های ساخت

برای ساخت فرانت‌اند به وابستگی‌های زیر نیاز دارید:

- pnpm

سپس با استفاده از دستور `make dashboard-deps && make dashboard build` فرانت‌اند را بسازید؛ یا برای توسعه از `make dashboard-dev` استفاده کنید.

## Marzneshin CLI

CLI مارزنشین با استفاده از [Typer](https://typer.tiangolo.com/) ساخته شده و کد دستورات آن در پوشه `cli` قرار دارد. مستندات CLI با استفاده از [Typer CLI](https://typer.tiangolo.com/typer-cli/) تولید می‌شود که می‌توانید آن را با اجرای دستور زیر از ریشه پروژه بازتولید کنید:

```bash
$ PYTHONPATH=$(pwd) typer marzneshin-cli.py utils docs --name "marzneshin-cli" --output ./cli/README.md
```

### حالت توسعه

برای اجرای فرانت‌اند در حالت توسعه از دستورات زیر برای نصب وابستگی‌ها استفاده کنید، سپس بک‌اند را اجرا کنید:

```bash
make dashboard-deps && make dashboard-dev
```

سپس در یک کنسول دیگر `make start` را اجرا کنید.

---
layout: fandogh
id: source-django
title: پروژه‌های جنگو
sidebar_label: پروژه‌های جنگو 
---

## ![Django Project](/img/docs/Django-project-banner.png "Django Project")

دیپلوی کردن سرویس‌ها بر روی فندق برای کاربرانی که با docker کار نکرده‌اند ممکن است مقداری مبهم باشد؛ همینطور معمولا آماده سازی پروژه‌ها برای اجرا در محیط واقعی نیاز به تنظیماتی دارد که باعث پیچیده شدن کار برنامه‌نویس می‌شود.\
ما در این بخش به توضیح چگونگی دیپلوی کردن سرویس `Django Project` بدون نیاز به دانش docker می‌پردازیم.

> اگر هنوز fandogh-cli  فندق بر روی کامپیوتر شما نصب نیست از طریق این [مستند](https://docs.fandogh.cloud/docs/getting-started.html) می‌توانید cli را بر روی کامپیوتر خود نصب کنید.

در پوشه اصلی پروژه، بعد از اینکه در فندق لاگین کردید دستور `fandogh source init‍‍` را اجرا کنید. در اولین مرحله شما می‌بایست اسم سرویس را انتخاب نمایید.

```
Service Name: mywebsite
```

 بعد از وارد کردن نام service  برای شما گزینه هایی که بدون نیاز به دانش docker قابل اجرا هستند نمایش داده می‌شود. از بین گزینه های نمایش داده شده گزینه **Django Project** را انتخاب کنید.

>  توجه داشته باشید  برای انتخاب، شماره گزینه مورد نظر را وارد کنید.

```
-[1] Static Website
-[2] Django Project
-[3] Laravel Project
-[4] ASP.NET core Project
-[5] Nodejs Project
-[6] Spring Boot
....
Please choose one of the project types above:

```
> حتما در نظر داشته باشید فایل requirements.txt در root directory پروژه مورد نظرتان وجود داشته باشد؛ در غیر این صورت پیغام خطای عدم وجود این فایل را دریافت خواهید کرد.

در قسمت بعدی شما باید context را وارد کنید. اگر در حال حاضر در پوشه اصلی نیستید می توانید آدرس آن را وارد کنید یا در غیر این صورت خالی بگذارید و دکمه enter را فشار دهید.

```
The context directory [.]:
```

گزینه بعدی انتخاب ورژن پایتون است که به صورت پیش فرض ورژن 3.7 است. شما با وارد کردن ورژن مورد نظر خود می‌توانید آن را تغییر دهید. 

```
Python version [3.7]: 3.5

```

 بعد از اینکه گزینه **Django Project** را انتخاب کردید فندق از شما نام ماژول `WSGI` را خواهد پرسید. همچنین ماژول‌های احتمالی `WSGI` موجود در پروژه نیز به شما نمایش داده می‌شوند. به احتمال زیاد نام ماژول در این لیست وجود دارد و شما تنها نیاز دارید که نام را در ورودی وارد کنید.\
**اگر فندق قادر به یافتن ماژول مورد نظر شما نبود٬ شما می‌بایست به صورت دستی نام ماژول مورد نظرتان را وارد نمایید.**

```
Possible wsgi modules are:
 - fandoghapp.wsgi
 - venv.Lib.site-packages.django.contrib.auth.handlers.modwsgi
 - venv.Lib.site-packages.django.core.wsgi
 - venv.Lib.site-packages.django.core.handlers.wsgi
WSGI module:
```
<br>

> در نظر داشته باشید fandoghapp.wsgi اسم پروژه جانگوی ماست که در حال دیپلوی آن هسیتم. این اسم برای شما متفاوت خواهد بود.

پس از مشخص کردن ماژول WSGI از شما آدرس فولدر static پرسیده می‌شود. 

```
Static Path [static]: static
```

> در نظر داشته باشید هنگامی که آدرس static را وارد می‌کنید در تنظیمات پروژه خود مقدار STATIC_ROOT را نیز درست مشخص کرده باشید. اگر پروژه شما فایل‌های استاتیک ندارد مقدار `''` را وارد نمایید.

در گزینه بعدی باید آدرس پوشه Media را مشخص کنید.

> در صورتی که پروژه شما فولدر Media ندارد این قسمت را خالی بگذارید.

```
Media Path []:
```

پس از مشخص کردن اطلاعات فوق، فایلی با نام fandogh.yml در پوشه جاری شما ساخته می‌شود. 
اکنون با نوشتن دستور ` fandogh source run ` می توانید پروژه خودتان را بر روی فندق دیپلوی کنید.

> پس از هر بار تغییر در پروژه تنها کافیست که دستور fandogh source run را مجددا اجرا کنید. 
> فایل `fandogh.yml` می‌تواند شامل تمام بخش‌هایی که در [مانیفست](https://docs.fandogh.cloud/docs/service-manifest.html) فندق است باشد٬ شما به صورت دستی قادر هستید تا بخش‌های مورد نیاز این فایل را تغییر دهید.
 

## راه اندازی Django به همراه MySQL
استفاده از پایگاه داده MySQL در بسیاری از پروژه ها یکی از نیاز های اولیه است. بسیاری از کاربران برای استفاده از پایگاه داده خود از این RDBMSها استفاده می‌کنند. شما می توانید با استفاده از سرویس‌های مدیریت شده فندق، به راحتی  MySQL Service مختص به خودتان را اجرا کنید. 
برای راه اندازی سرویس MySQL می‌توانید [این بخش](https://docs.fandogh.cloud/docs/mysql-managed-service.html) را مطالعه کنید. 


### نحوه راه اندازی MySQL در تنظیمات پروژه Django 

> برای اتصال به MySQL نیاز به پکیج mysqlclient خواهید داشت. در نظر داشته باشید حتما این پکیج در لیست requirements.txt پروژه وجود داشته باشه.

قبل از دیپلوی کردن پروژه خود بر روی فندق باید مقادیری که در راه اندازی سرویس MySQL خود در فندق وارد کرده اید را در settings پروژه خودتان وارد نمایید. \
بطور مثال، فرض کنید شما برای راه اندازی سرویس MySQL از دستوری مانند دستور زیر استفاده کرده اید: 

```
fandogh managed-service deploy mysql 5.7 
-c service_name=db 
-c mysql_root_password=123456
-c phpmyadmin_enabled=true
```

> حتما در نظر داشته باشید پس از ساخت سرویس MySQL از قسمت PhpMyadmin دیتابیس مورد نظر خود را بسازید.

حال کافیست داخل تنظیمات پروژه جانگو خود مقادیر را وارد نمایید.

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'myDatabaseName',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': 'db',
        'PORT': '3306'
    }
}
```

>اگر نمی‌خواهید این کدها در دسترس سایر افرادی که بر روی پروژه کار می‌کنند قرار بگیرد، می‌توانید مقادیر را در فایل fandogh.yaml که پس از دستور `fandogh source init` زده‌اید به عنوان **environment variable** وارد و در این قسمت از آنها استفاده نمایید. 

```
kind: ExternalService
name: mywebsite
spec:
  image_pull_policy: Always
  port: 80
  source:
    context: .
    media_path: ''
    project_type: django
    python_version: '3.5'
    static_path: static
    wsgi: fandoghapp.wsgi
  env:
    - name: Mysql_Host
        value: db
    - name: Mysql_Password
        value: 123456
    - name: Mysql_User
        value: root
    - name: DB_Name
        value: myDatabaseName     
```
که این مقادیر به صورت زیر در setting پروژه جانگو اضافه می شوند.

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': os.environ.get('Mysql_Host', 'local_name'),
        'USER': os.environ.get('Mysql_User', 'local_user'),
        'PASSWORD': os.environ.get('Mysql_Password', 'local_pass'),
        'HOST': os.environ.get('Mysql_Host', 'local_host'),
        'PORT': '3306'
    }
}
```
اکنون با دستور `fandogh source run` پروژه را به همراه MySQL می‌توانید deploy نمایید.

> حتما در نظر داشته باشید بعد از تغییرات پایگاه داده، فایل‌های migration را دوباره بسازید که به سرور های فندق انتقال پیدا کنند و تغییرات جدید شما لحاظ شوند.

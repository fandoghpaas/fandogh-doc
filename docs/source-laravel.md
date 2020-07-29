---
layout: fandogh
id: source-laravel
title: پروژه‌های لاراول
sidebar_label: پروژه‌های لاراول 
---

## ![Laravel Framework](/img/docs/laravel-framework-banner.png "Laravel Framework")

دیپلوی کردن سرویس‌ها بر روی فندق برای کاربرانی که با docker کار نکرده‌اند ممکن است مقداری مبهم باشد؛ همینطور معمولا آماده سازی پروژه‌ها برای اجرا در محیط واقعی نیاز به تنظیماتی دارد که باعث پیچیده شدن کار برنامه‌نویس می‌شود.\
ما در این بخش به توضیح چگونگی دیپلوی کردن سرویس `Laravel Project` بدون نیاز به دانش docker می‌پردازیم.

> اگر هنوز fandogh-cli بر روی کامپیوتر شما نصب نیست از طریق این [مستند](https://docs.fandogh.cloud/docs/getting-started.html) می‌توانید cli را بر روی کامپیوتر خود نصب کنید.

در پوشه اصلی پروژه، بعد از اینکه در فندق login کردید دستور `fandogh source init‍‍` را اجرا کنید. در اولین مرحله شما می‌بایست اسم سرویس رو انتخاب نمایید.

```
Service Name: mywebsite
```

 بعد از وارد کردن نام service  برای شما گزینه‌هایی که بدون نیاز به دانش docker قابل اجرا هستند نمایش داده می‌شود. از بین گزینه های نمایش داده شده گزینه **Laravel Project** را انتخاب کنید.

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
در قسمت بعدی شما باید context (`همان پوشه‌ای که خروجی برنامه شما در آن قراره گرفته است`) را وارد کنید. اگر در حال حاضر در پوشه اصلی نیستید می توانید آدرس آن را وارد کنید یا در غیر این صورت خالی بگذارید و دکمه enter را فشار دهید.

```
The context directory [.]:
```


پس از مشخص کردن اطلاعات فوق، فایلی با نام fandogh.yml در پوشه جاری شما ساخته می شود. 
اکنون با نوشتن دستور `fandogh source run` می توانید پروژه خودتان را بر روی فندق دیپلوی کنید.

> اگر شما از پایگاه داده MySQL استفاده می‌کنید، با استفاده از دستورات فندق می توانید یک سرویس مدیریت شده MySQL ران کنید و اطلاعات مورد نظر را در کد خود وارد کنید. بهتر است به جای استفاده از hard code در پروژه خود این مقادیر را به عنوان environment variable در فایل fandogh.yml اضافه کنید.  

> شما برای پروژه های لاراول نیاز به  APP_KEY دارید، این مقدار را نیز می‌توانید به عنوان environment variable در فایل fandogh.yml ذخیره کنید.

```
kind: ExternalService
name: myshop
spec:
  image_pull_policy: Always
  port: 80  
  source:
    context: .
    project_type: laravel
  env:
    - name: APP_KEY
      value: base64:HGT49Mfm6j77W2N6K3GXqJqqNgUromHg41lRF23sEJc=
    - name: APP_DEBUG
      value: true
    - name: APP_URL
      value: http://localhost
    - name: DB_CONNECTION
      value: mysql
    - name: DB_PORT
      value: 3306
    - name: DB_DATABASE
      value: mydatabsename
    - name: DB_USERNAME
      value: dbuser_like_root
    - name: DB_PASSWORD
      value: db_password
    - name: DB_HOST
      value: mysql_service_on_fandogh
```



> حتما در نظر داشته باشید سکوی ابری فندق بر روی HTTPS قرار داد و برخی از پروژه ها با http کار می‌کنند. این اتفاق ممکن است باعث شود که فایل های static شما مانند css,js,img ها در سرویس load نشوند. برای رفع این موضوع در قسمت Providers فایل appserviceprovider کلاس app service تابع boot را به شکل زیر تغییر دهید. 

```
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Schema;
use Illuminate\Support\ServiceProvider;
use Illuminate\Contracts\Routing\UrlGenerator;
class AppServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap any application services.
     *
     * @return void
     */

    public function boot(UrlGenerator $url)
        {
            if (\App::environment() === 'production') {
                $url->forceScheme('https');
            }
        }


    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}

```

> پس از هر بار تغییر در پروژه تنها کافی است که دستور `fandogh source run` را مجددا اجرا کنید. 
> فایل `fandogh.yml` می‌تواند شامل تمام بخش‌هایی که در [مانیفست](https://docs.fandogh.cloud/docs/service-manifest.html) فندق است باشد، شما به صورت دستی قادر هستید تا بخش‌های مورد نیاز این فایل را تغییر دهید.

> پس از دیپلوی کردن پروژه بر روی سکوی ابری فندق شما باید جداول دیتابیس  را بسازید. برای این کار با دستور `fandogh exec -i sh` به سرویس مورد نظر وصل شوید؛ پس از وصل شدن می توانید با دستور `php artisan migrate`  جداول مورد نظر خود را در پایگاه داده مورد نظر بسازید.

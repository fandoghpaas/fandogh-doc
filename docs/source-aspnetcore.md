---
layout: fandogh
id: source-aspnetcore
title: پروژهای ASP.NET Core
sidebar_label: پروژه‌های ASP.NET core 
---

## ![Core Framework](/img/docs/asp-core-banner.png "Core Framework")

دیپلوی کردن سرویس‌ها بر روی فندق برای کاربرانی که با docker کار نکرده‌اند ممکن است مقداری مبهم باشد؛ همینطور معمولا آماده سازی پروژه‌ها برای اجرا در محیط واقعی نیاز به تنظیماتی دارد که باعث پیچیده شدن کار برنامه‌نویس می‌شود.\
ما در این بخش به توضیح چگونگی دیپلوی کردن سرویس `ASP.NET Core Project` بدون نیاز به دانش docker می‌پردازیم.

> اگر هنوز fandogh-cli بر روی کامپیوتر شما نصب نیست از طریق این [مستند](https://docs.fandogh.cloud/docs/getting-started.html) می‌توانید cli را بر روی کامپیوتر خود نصب کنید.

در پوشه اصلی پروژه، بعد از اینکه در فندق login کردید دستور `fandogh source init‍‍` را اجرا کنید. در اولین مرحله شما می‌بایست اسم سرویس رو انتخاب نمایید.

```
Service Name: myAspWebsite
```

 بعد از وارد کردن نام Service  برای شما گزینه هایی که بدون نیاز به دانش docker قابل اجرا هستند نمایش داده می شود. از بین گزینه های نمایش داده شده گزینه **ASP.NET core Project** را انتخاب کنید.

>  توجه داشته باشید برای انتخاب، شماره گزینه مورد نظر را وارد کنید.

```
-[1] Static Website
-[2] Django Project
-[3] Laravel Project
-[4] ASP.NET core Project
Please choose one of the project types above:

```
  
در قسمت بعدی شما باید context را وارد کنید. اگر در حال حاضر در پوشه اصلی نیستید می توانید آدرس آن را وارد کنید یا در غیر این صورت خالی بگذارید و دکمه enter را فشار دهید.

```
The context directory [.]:
```

گزینه بعدی انتخاب کردن فایل DLL پروژه شما است. 

```
Application dll name:

```
>در نظر داشته باشید که فایل DLL همان فایل خروجی برنامه شما است. 
 
> به صورت مثال اگر نام پروژه من myAspWebsite باشد فایل dll من در هنگام ساخته شدن با اسم myAspWebsite.dll خواهد بود.


پس از مشخص کردن اطلاعات فوق، فایلی با نام fandogh.yml در پوشه جاری شما ساخته می‌شود. 
اکنون با نوشتن دستور ` fandogh source run ` می‌توانید پروژه خودتان را بر روی فندق دیپلوی کنید.

> پس از هر بار تغییر در پروژه تنها کافیست که دستور fandogh source run را مجددا اجرا کنید. 
> فایل `fandogh.yml` می‌تواند شامل تمام بخش‌هایی که در [مانیفست](https://docs.fandogh.cloud/docs/service-manifest.html) فندق است باشد٬ شما به صورت دستی قادر هستید تا بخش‌های مورد نیاز این فایل را تغییر دهید.

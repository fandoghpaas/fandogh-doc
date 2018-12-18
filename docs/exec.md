---
layout: fandogh
id: exec
title: دستورات exec
sidebar_label: دستورات exec
---

## exec چیست ؟

![EXEC](/img/docs/exec.png "EXEC")

exec یک قابلیت عملیاتی می‌باشد که با استفاده از آن می‌توان دستورات خاصی را بر روی یک پروسه در حال اجرا پیاده کرد.
بگذارید با یک مثال خیلی ساده و ابتدایی کاربرد آن را برایتان شفاف‌تر کنیم.
همانظور که میدانیم سرویس‌ها از ایمیج‌ها ساخته می‌شوند و هر سرویس مجموعه‌ای از کدها و منطق‌هایی است که برای آن طراحی شده است تا هنگامی که سرویس ساخته شد٬ آن ها را انجام دهد.
هر سرویس یک کانتینر داکری می‌باشد که داخل خود یک سری فایل دارد که یکی از آن‌ها که مطمئن هستیم در دایرکتوری سرویس ما حضور دارد Dockerfile است.
فرض کنید شما بنا به دلایلی Dockerfile را از حافظه محلی رایانه خود به اشتباه پاک کرده اید و نیاز دارید تا Dockerfile مربوط به سرویس خود را مشاهده کنید.
خب همانطور که می‌دانیم دسترسی به کانتینرها در حالت عادی غیرممکن می‌باشد٬ پس باید چه کار کرد؟
اینجا می‌توان به exec پناه آورد. به مثال زیر توجه کنید :
<br>
فرض می‌کنیم نام سرویس شما SVC می‌باشد و از طرفی هم می‌دانیم دستور مشاهده محتوای یک فایل **cat** می باشد. حال با استفاده از نام سرویس و دستور ذکر شده می‌توان دستور exec را اجرا کرد.
```
fandogh exec --service SVC "cat Dockerfile"
```
بعد از اجرای این دستور شما می‌توانید محتوای Dockerfile خود را در cli مشاهده کنید.
توجه داشته باشید پارامتر service-- نمایانگر نام سرویسی است که می‌خواهید دستور exec را بر روی آن اجرا کنید.
بعد از آنکه نام سرویس را نوشتید٬ باید دستور exec را بین 2 **(" ")** قرار دهید تا exec به درستی اجرا شود و اگر علامت " را ابتدا و انتهای دستور exec قرار ندهید٬ cli به شما خطا نشان خواهد داد.
<!-- markdownlint-disable MD034 -->
# GFI Proxy Protector - محافظ سرور پروکسی ایرانی

## مسئله

با خرید و راه اندازی سامانه GFW توسط رژیم اشغالگر جمهوری اسلامی اکثر پروتکل های رایج  VPN در ایران مسدود شده اند و در حال حاضر تعداد معدودی پروتکل امکان اتصال دارند که از آنها در راه اندازی وبسایت ها و اپلیکشن ها بکار گرفته می‌شود به معنای دیگر مسدود کردن آنها موجب اختلال در عملکرد این  خدمات خواهد بود.

طراحان مزدور GFW برای حل این معضل ابزاری را طراحی نمودند که از آن با نام Active Probing یا کاوش فعال یاد می‌شود. این ابزار به شکل رباتی به سرورهای مشکوک مراجعه کرده و تلاش می‌کند فاکتور هایی را بیابد که در وبسایت های واقعی یافته می‌شوند و در غیر این صورت استنباط می‌کند که سرور شما یک  سرور پروکسی است و با گزارش نتیجه ی مثبت، IP سرور شما مسدود خواهد شد.

به نظر می‌رسد این سامانه از یک فهرست سفید بهره می‌برد که شامل سرویس های شناخته شده وب اعم از گوگل و کلادفلر و ... می‌ باشد و هر درخواستی به سایر وبسایت های خارج از این فهرست را مورد بررسی قرار می‌دهد! همچنین به یافته ی کاربران، بازدید از وبسایت ها و خدمات بومی کشور در هنگام متصل بودن پروکسی موجب برگشت اتصال و برملا شدن آی‌پی سرور به عنوان یک سرور پروکسی می‌شود و هرگونه شک و شبهه ی این سامانه را در پروکسی بودن سرور شما را به یقین تبدیل خواهد نمود!

## راه حل

با مسدود نمودن آی‌پی های چینی تا حد زیادی از شر این کاوشگران مزاحم در امان خواهید بود و اگر محافظت بیشتری می‌خواهید می‌توانید تمام آی‌پی های غیرایرانی (به استثنای کلادفلر) را مسدود نمایید (البته این مورد برای دریافت و تازه سازی گواهی های امنیتی مشکل ایجاد میکند که نزدیک موعد تازه سازی گواهی ها (معمولا هر ۹۰ روز) باید این محافظت رو غیرفعال نموده و پس از تازه سازی گواهی دوباره فعال نمایید)
این اسکریپت در حال حاضر گزینه های زیر را در اختیار شما قرار می‌دهد

- مسدود کردن اتصالات *خروجی* به سمت ایران و چین برای جلوگیری از لو رفتن سرور
- مسدود کردن اتصالات *ورودی* از سمت چین
- مسدود کردن تمام اتصالات *ورودی* به غیر از ایران و شبکه کلادفلر
- بروزرسانی پایگاه آی‌پی ها برای تشخیص جغرافیا
- بازگردانی تنظیمات دیواره آتش به حالت اولیه

## نحوه اجرا

```
apt install git
git clone https://github.com/redpilllabs/GFIProxyProtector.git
cd GFIProxyProtector
./run.sh
```

## نکات

- این اسکریپت «پروکسی-آگنوستیک» می‌باشد، به این معنی که تفاوتی نمی‌کند از چه اسکریپت یا پنلی برای نصب پروکسی خود اقدام نموده اید چون مستقیما روی کنترل اتصالات توسط هسته عمل می‌نماید.
- در صورت فعالسازی محافظت ورودی، هرگونه تلاش اتصال از آی‌پی های چینی در فایل لاگ هسته در مسیر `var/log/kern.log/` با پسوند GFW قابل مشاهده خواهد بود.
- این اسکریپت زیرمجموعه ای اسکریپت نصاب پروکسی رنگین کمان [Rainb0w](https://github.com/redpilllabs/Rainb0w) می‌باشد که علاوه برا این امکانات، قابلیت مسدودسازی تمام اتصالات ورودی غیر از ایران و کلادفلر، مسدود سازی تمام دامنه های [ir.] و راه اندازی یک وبلاگ وردپرس نمایشی را به عنوان Fallback decoy را نیز دارا می‌باشد.

## منابع

- [صفحه ی اصلی ماژول](https://inai.de/projects/xtables-addons/geoip.php)

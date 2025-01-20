[English](https://github.com/ParsaKSH/TAQ-BOSTAN/blob/main/README-en.md)
---
# پروژه ‌طاق بستان، ساخت IPv6 لوکال روی بستر IPv4 با استفاده از WireGuard
---
به **اسکریپت طاق بستان، اولین اسکریپت ساخت آیپی لوکال با استفاده از وایرگارد**
خوش آمدید! این اسکریپت به شما کمک می‌کند روی سرور هایی که ایجاد آیپی محلی(لوکال) روی آنها بسته است، بتوانید آیپی ورژن6 لوکال داشته باشید.
---
این اسکریپت روی سرور هایی که فیلتر شدند هم کار می‌کند!
---
به این مورد توجه کنید که اگر سرور شما محدودیتی در ایجاد آیپی لوکال به روش های sit،gre،vxlanو... ندارد، بهتر است از این پروژه استفاده نکنید و سراغ روش هایی مانند sit بروید؛ زیرا وایرگارد به دلیل بار پردازشی که ایجاد می‌کند باعث افت پهنای باند سرور می‌شود، تعداد هسته های cpu سرور ارتباطی به پردازش وایرگارد ندارد و تنها فرکانس پردازنده در این امر موثر است، چون وایرگارد فقط از یک هسته برای ارتباط خود استفاده می‌کند.
علاوه بر این، وایرگارد برای انتقال داده های خود از UDP استفاده می‌کند، همین موضوع سبب شده که در مواقعی که روی پروتکل UDP اختلال هست، تونل به سبک وایرگارد هم دچار مشکل شود.

لینک اسکریپت من برای ساخت IPv6 لوکال با استفاده از sit: https://github.com/ParsaKSH/Create-Private-IPv6-with-Sit
---

## **ویژگی‌ها**
- پشتیبانی از **اتصال چندین سرور خارج به یک سرور ایران**  
- **گزینه‌های سفارشی** برای تنظیم پورت، MTU، آدرس‌های IPv6 و غیره  
- قابلیت **پایداری** بعد از ری‌استارت سرور (سرویس به‌صورت خودکار فعال می‌ماند)  
- **مستندات و اسکریپت‌های آماده** برای راحتی نصب و پیکربندی

---

## **نصب و راه‌اندازی**
1. **دریافت اسکریپت**  
   با دستور زیر می‌توانید اسکریپت را به‌صورت مستقیم دریافت و اجرا کنید:
   ```bash
   bash <(curl -Ls https://raw.githubusercontent.com/ParsaKSH/TAQ-BOSTAN/main/script.sh)

2. **انتخاب سرور**  
   در آغاز، از شما پرسیده می‌شود که در حال اجرای اسکریپت روی کدام سرور هستید؟ ایران یا خارج؟(IRAN/FOREIGN)
   - اگر **IRAN** انتخاب کنید: امکان تعریف چندین FOREIGN فراهم می‌شود.  
   - اگر **FOREIGN** انتخاب کنید: فقط اطلاعات همان سرور خارجی را وارد کرده و با سرور ایران همگام‌سازی می‌کنید.
3. **واردکردن اطلاعات**  
   - **آیپی عمومی سرور ایران یا خارج**  
   - **مقدار پورت WireGuard** (پیش‌فرض 51820)  
   - **تعداد سرورهای خارجی** (در حالت ایران)  
   - **کلید عمومی (PublicKey)** سرور مقابل  
   - **شماره سرور خارجی** (برای تخصیص IPv6 منحصربه‌فرد)  
   - **MTU** (پیش‌فرض 1380)  
4. **اجرای نهایی**  
   - بعد از اتمام پرسش‌ها، فایل کانفیگ در مسیر `/etc/wireguard/` ساخته می‌شود.  
   - سرویس **wg-quick** فعال و روی بوت سرور **enable** می‌شود.  
   - برای هر **سرور خارجی**، یک سکشن `[Peer]` اختصاصی در سرور ایران ایجاد می‌گردد.

---

## **مثال ساده**
- **سرور ایران**  
  1. انتخاب IRAN  
  2. آیپی عمومی سرور ایران را وارد کنید (مثلاً `1.2.3.4`)  
  3. تعداد سرورهای خارجی را مثلاً `2` انتخاب کنید  
  4. به ترتیب آیپی عمومی و کلید عمومی هر سرور خارجی پرسیده می‌شود  
  5. مقدار MTU را وارد کنید (یا خالی بگذارید تا 1380 شود)  
- **سرور خارج**  
  1. انتخاب FOREIGN  
  2. آیپی عمومی سرور خارج (مثلاً `5.6.7.8`)  
  3. آیپی عمومی سرور ایران (`1.2.3.4`) و کلید عمومی آن  
  4. شماره سرور خارج (1 برای اولین، 2 برای دومین و ...)  
  5. مقدار MTU  
  6. فایل `/etc/wireguard/wg86.conf` ساخته و آمادهٔ استفاده می‌شود.

---

## **پشتیبانی و ارتباط**
- **آی‌دی تلگرام من**: [@ParsaA_KSH](https://t.me/ParsaA_KSH)  
- **لینک گروه اپ‌ایران**: [https://t.me/OPIranClub](https://t.me/OPIranClub)

در صورت بروز هرگونه مشکل یا سؤال، در گروه اپ‌ایران من را تگ کنید تا پاسخ داده شود.
**امیدوارم این اسکریپت و مستندات برایتان مفید باشد!** اگر دوست داشتید، به پروژه ستاره بدهید تا افراد بیشتری آن را ببینند. با آرزوی موفقیت برای شما.

---

## **حمایت مالی**
در صورت تمایل به حمایت مالی، می‌توانید از آدرس‌های زیر استفاده کنید:

- **Tron**: `TD3vY9Drpo3eLi8z2LtGT9Vp4ESuF2AEgo`  
- **USDT**: `UQAm3obHuD5kWf4eE4JmAO_5rkQdZPhaEpmRWs6Rk8vGQJog`  
- **TON**: `bc1qaquv5vg35ua7qnd3wlueytw0fugpn8qkkuq9r2`  
- **BTC**: `0x800680F566A394935547578bc5599D98B139Ea22`

هرگونه کمکی از سوی شما در جهت ارتقای این پروژه و ادامهٔ توسعهٔ آن مؤثر خواهد بود. سپاس از حمایتتان ❤️
---

## **لایسنس**
این پروژه تحت لایسنس **Apache** ارائه می‌شود؛ می‌توانید آزادانه از آن استفاده کرده یا تغییر دهید. ولی لطفاً نام من (Parsa) و لینک پروژه را ذکر کنید.


![image](https://github.com/user-attachments/assets/f9f4e79a-0dd4-47ca-862a-8af8504a355a)



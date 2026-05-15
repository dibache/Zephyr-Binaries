# Zephyr Binaries

باینری‌های پروژه Zephyr (نسخه‌های ویندوز و لینوکس) برای دانلود مستقیم.

---

## 📥 لینک‌های دانلود مستقیم

- **نسخه ویندوز (Windows):**
https://github.com/dibache/Zephyr-Binaries/raw/main/zephyr-v1.0.2-windows-amd64.zip

- **نسخه لینوکس (Linux):**
  https://github.com/dibache/Zephyr-Binaries/raw/main/zephyr-v1.0.2-linux-amd64.zip
  

---

## 🐧 نصب و اجرا روی سرور لینوکس (قدم به قدم)

### 1. دانلود و خارج کردن از حالت فشرده

```bash
wget https://github.com/dibache/Zephyr-Binaries/raw/main/zephyr-v1.0.2-linux-amd64.zip
unzip zephyr-v1.0.2-linux-amd64.zip
cd zephyr-v1.0.2-linux-amd64
chmod +x server client
```
ساختن فایل کانفیگ سرور
```
nano server_config.json
```
محتوای زیر رو داخلش بچسبون
```
{
  "google_folder_id": ""
}
```
(با Ctrl+X و بعد Y و Enter ذخیره کن.)
- آماده کردن فایل credentials.json
- اجرای سرور برای دریافت توکن (فقط یک بار)
```
./server -c server_config.json -gc credentials.json
```
لینکی که نمایش داده می‌شه رو در مرورگر باز کن.

اجازه دسترسی به Drive رو بده.

آدرس صفحه‌ای که به http://localhost هدایت شدی رو کپی کن.

توی ترمینال پیست کن و Enter بزن.

✅ فایل .token ساخته می‌شه.
اجرای دائمی سرور در پس‌زمینه (با screen)
```
screen -S zephyr
```
```
./server -c server_config.json -gc credentials.json
```
 - نصب و اجرا روی ویندوز
- ساختن فایل کانفیگ کلاینت
```
{
  "listen_addr": "127.0.0.1:1080",
  "storage_type": "google",
  "google_folder_id": "FOLDER_ID_FROM_SERVER",
  "refresh_rate_ms": 200,
  "flush_rate_ms": 300,
  "transport": {
    "TargetIP": "216.239.38.120:443",
    "SNI": "google.com",
    "HostHeader": "www.googleapis.com"
  }
}
```
google_folder_id رو از سرور بگیری (بعد از اجرای اول، توی لاگ نشون میده).
آماده کردن credentials.json
- اجرای کلاینت
```
zephyr-client.exe -c client_config.json -gc credentials.json
```

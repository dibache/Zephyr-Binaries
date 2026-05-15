# Zephyr Binaries

باینری‌های پروژه Zephyr (نسخه‌های ویندوز و لینوکس) برای دانلود مستقیم.

## 📥 لینک‌های دانلود مستقیم

- **نسخه ویندوز (Windows):**  
  `https://github.com/dibache/Zephyr-Binaries/raw/main/zephyr-v1.0.2-windows-amd64.zip`

- **نسخه لینوکس (Linux):**  
  `https://github.com/dibache/Zephyr-Binaries/raw/main/zephyr-v1.0.2-linux-amd64.zip`

---

## 🐧 نصب و اجرا روی سرور لینوکس (قدم به قدم)

### 1. دانلود و خارج کردن از حالت فشرده

```bash
wget https://github.com/dibache/Zephyr-Binaries/raw/main/zephyr-v1.0.2-linux-amd64.zip
unzip zephyr-v1.0.2-linux-amd64.zip
cd zephyr-v1.0.2-linux-amd64
chmod +x server client
```

### 2. ساختن فایل کانفیگ سرور (`server_config.json`)

فایل را با دستور زیر باز کنید:

```bash
nano server_config.json
```

سپس محتوای زیر را در آن بچسبانید:

```json
{
  "google_folder_id": ""
}
```

(برای ذخیره: `Ctrl+X`، سپس `Y` و در نهایت `Enter` را بزنید.)

### 3. آماده کردن فایل `credentials.json`

فایل `credentials.json` (دریافتی از Google Cloud Console) را به این پوشه منتقل کنید.

### 4. اجرای سرور برای دریافت توکن (فقط یک بار)

```bash
./server -c server_config.json -gc credentials.json
```

- لینکی که نشان داده می‌شود را در مرورگر باز کنید.
- اجازه دسترسی به Drive را بدهید.
- آدرس صفحه‌ای که به `http://localhost` هدایت شدید را کپی کنید.
- آن را در ترمینال پیست کرده و `Enter` را بزنید.

✅ فایل `.token` ساخته می‌شود.

### 5. اجرای دائمی سرور در پس‌زمینه (با screen)

```bash
screen -S zephyr
./server -c server_config.json -gc credentials.json
```

برای خروج از screen بدون بستن سرور، کلیدهای `Ctrl+A` و سپس `D` را بزنید.

---

## 🪟 نصب و اجرا روی ویندوز

### 1. ساختن فایل کانفیگ کلاینت (`client_config.json`)

فایلی با نام `client_config.json` با محتوای زیر بسازید:

```json
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

> `google_folder_id` را باید از سرور خود دریافت کنید (بعد از اجرای سرور، در لاگ نشان داده می‌شود).

### 2. آماده کردن `credentials.json`

فایل `credentials.json` را در همین پوشه قرار دهید.

### 3. اجرای کلاینت

```bash
zephyr-client.exe -c client_config.json -gc credentials.json
```

### 4. تنظیم پروکسی در مرورگر

مرورگر خود را روی پروکسی **SOCKS5** با آدرس `127.0.0.1` و پورت `1080` تنظیم کنید.

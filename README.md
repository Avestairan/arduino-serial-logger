# Arduino Serial Logger

یک ابزار ساده، مستقل و مرورگری برای نمایش، نگهداری، کپی، ذخیره و ارسال داده‌های سریال.

A simple standalone browser-based tool for displaying, keeping, copying, saving, and sending serial data.

## استفاده آنلاین / Use Online

بدون نصب و بدون نیاز به برنامه جداگانه، فقط با مرورگرهای سازگار باز کن:

[https://avestairan.github.io/arduino-serial-logger](https://avestairan.github.io/arduino-serial-logger)

> برای اتصال واقعی به پورت سریال، از `Google Chrome` یا `Microsoft Edge` استفاده کن.

## فارسی

### دلیل ساخت این پروژه

این پروژه به خاطر یک مشکل عملی در `Arduino IDE 2.x` ساخته شد.

در نسخه‌های جدید `Arduino IDE`، مخصوصاً سری `2.x`، وقتی خروجی `Serial Monitor` زیاد و طولانی می‌شود، کپی کردن کل لاگ‌ها همیشه راحت و قابل اعتماد نیست. اگر داخل پنجره سریال مانیتور از `Ctrl + A` و بعد `Ctrl + C` استفاده شود، در بسیاری از حالت‌ها فقط همان بخشی که روی صفحه دیده می‌شود یا در رابط کاربری فعلی رندر شده است کپی می‌شود، نه تمام داده‌هایی که قبلاً از برد دریافت شده‌اند.

این موضوع برای تست ماژول‌ها و دیباگ سخت‌افزار مشکل‌ساز است؛ چون در کارهای واقعی معمولاً لازم است کل خروجی سریال ذخیره شود، بعداً بررسی شود، یا برای عیب‌یابی در اختیار دیگران قرار بگیرد. برای مثال هنگام تست ماژول‌هایی مثل `SIM800`, سنسورها، بردهای `ESP32`, `Arduino`, لاگ‌های `AT Command`, پیام‌های خطا، خروجی بوت و پاسخ‌های چندمرحله‌ای، از دست رفتن بخشی از لاگ می‌تواند باعث شود عیب اصلی دیده نشود.

### مشکل اصلی در `Arduino IDE 2.x`

مشکل اصلی این است که `Serial Monitor` داخلی `Arduino IDE 2.x` برای نمایش خروجی‌های طولانی، همه خط‌ها را مثل یک متن ساده و کامل در اختیار کاربر قرار نمی‌دهد. رابط کاربری آن از روش‌هایی شبیه نمایش مجازی یا رندر مرحله‌ای استفاده می‌کند؛ یعنی ممکن است فقط بخشی از خطوط که روی صفحه دیده می‌شوند یا نزدیک محدوده قابل مشاهده هستند، واقعاً در بخش قابل انتخاب رابط کاربری حضور داشته باشند.

در نتیجه وقتی کاربر می‌خواهد همه خروجی را انتخاب و کپی کند، همیشه به کل لاگ دریافت‌شده دسترسی ندارد. این یک محدودیت آزاردهنده برای کسانی است که زیاد با سریال مانیتور، تست سخت‌افزار، دیباگ بردها و ذخیره خروجی‌های طولانی سروکار دارند.

### راه‌حل این پروژه

به‌جای تغییر دادن خود `Arduino IDE` یا نصب افزونه‌های پیچیده، این پروژه به صورت یک فایل مستقل `HTML` ساخته شده است.

این فایل مستقیماً از طریق `Web Serial API` مرورگر به پورت سریال وصل می‌شود، داده‌های دریافتی را در حافظه خودش نگه می‌دارد و اجازه می‌دهد کل لاگ دریافت‌شده را با یک کلیک کپی یا به صورت فایل متنی ذخیره کنی.

به همین دلیل این پروژه فقط یک صفحه ظاهری نیست؛ هدفش حل یک مشکل واقعی در روند تست و دیباگ است:

- نگه داشتن کل خروجی سریال، نه فقط بخش قابل مشاهده
- کپی کردن همه لاگ‌ها با یک کلیک
- ذخیره خروجی در فایل `.txt`
- ارسال دستور به برد یا ماژول
- استفاده بدون نصب برنامه اضافه
- اجرا به صورت آنلاین یا حتی با باز کردن مستقیم فایل `index.html`

### چرا فقط یک فایل `index.html`؟

این پروژه عمداً به صورت تک‌فایل ساخته شده است تا استفاده از آن ساده باشد.

لازم نیست چیزی نصب شود، لازم نیست سرور جداگانه اجرا شود، و لازم نیست کاربر درگیر تنظیمات پیچیده شود. کافی است فایل `index.html` باز شود یا نسخه آنلاین از طریق `GitHub Pages` اجرا شود.

این طراحی باعث می‌شود ابزار برای استفاده‌های سریع، تست‌های میدانی، تعمیرات، آموزش، و دیباگ سخت‌افزاری مناسب باشد.

### امکانات

- اتصال مستقیم به پورت سریال از طریق مرورگر با `Web Serial API`
- نمایش کامل لاگ سریال بدون وابستگی به `Serial Monitor` داخلی آردوینو
- نگه داشتن کل داده‌های دریافتی در بافر داخلی ابزار
- کپی کردن همه لاگ‌ها با یک کلیک
- ذخیره لاگ در فایل `.txt`
- ارسال دستور به آردوینو یا هر دستگاه سریال دیگر
- انتخاب `baudrate`
- نمایش پورت‌های قبلاً مجازشده با `navigator.serial.getPorts()`
- دکمه `Refresh` برای به‌روزرسانی لیست پورت‌های مجازشده
- انتخاب نوع پایان خط هنگام ارسال دستور:
  - بدون پایان خط
  - `\n`
  - `\r`
  - `\r\n`
- نمایش آمار دریافت:
  - تعداد خط‌ها
  - تعداد بایت‌ها
  - زمان اتصال
  - سرعت دریافت
- پشتیبانی از فارسی و انگلیسی
- رابط تاریک و ساده
- قابل اجرا به صورت آنلاین یا فایل محلی

### نحوه استفاده

1. صفحه آنلاین پروژه را در `Chrome` یا `Edge` باز کن.
2. اگر `Arduino IDE Serial Monitor` یا برنامه دیگری از همان پورت استفاده می‌کند، آن را ببند.
3. مقدار `baudrate` را مطابق کد برد انتخاب کن.
4. برای اتصال جدید، گزینه `New port...` را انتخاب کن.
5. روی `Connect` بزن.
6. در پنجره دسترسی مرورگر، پورت آردوینو یا دستگاه سریال را انتخاب کن.
7. بعد از اتصال، لاگ‌ها داخل صفحه نمایش داده می‌شوند.
8. برای ذخیره، از `Save Log` استفاده کن.
9. برای کپی کامل خروجی، از `Copy All` استفاده کن.
10. برای ارسال دستور، متن دستور را وارد کن و نوع پایان خط را انتخاب کن.

مثال ساده در کد آردوینو:

```cpp
void setup() {
  Serial.begin(115200);
}

void loop() {
  Serial.println("Hello from Arduino");
  delay(1000);
}
```

در این مثال باید داخل ابزار مقدار `baudrate` را روی `115200` قرار بدهی.

### نکات مهم

وقتی این ابزار به یک پورت سریال وصل است، معمولاً `Arduino IDE Serial Monitor` نمی‌تواند همزمان به همان پورت وصل شود. هر پورت سریال معمولاً در یک زمان فقط توسط یک برنامه قابل استفاده است.

اگر خروجی نمی‌بینی، اول `baudrate` را بررسی کن. مقدار `Serial.begin(...)` در کد باید با مقدار انتخاب‌شده در ابزار یکی باشد.

اگر پورت دیده نمی‌شود، کابل `USB` را بررسی کن. بعضی کابل‌ها فقط برای شارژ هستند و داده منتقل نمی‌کنند.

### عیب‌یابی

#### پورت دیده نمی‌شود

- مطمئن شو کابل `USB` قابلیت انتقال داده دارد.
- `Arduino IDE Serial Monitor` را ببند.
- هر برنامه دیگری که ممکن است پورت را گرفته باشد ببند.
- برد را جدا و دوباره وصل کن.
- از `Chrome` یا `Edge` استفاده کن.
- اگر قبلاً به پورت اجازه داده‌ای، روی `Refresh` بزن.

#### وصل می‌شود ولی چیزی نمایش داده نمی‌شود

- مقدار `baudrate` را بررسی کن.
- مطمئن شو در کد آردوینو از `Serial.begin(...)` استفاده شده است.
- مطمئن شو برد واقعاً چیزی چاپ می‌کند.
- یک کد ساده مثل مثال بالا تست کن.

#### مرورگر می‌گوید `Web Serial API` پشتیبانی نمی‌شود

از `Google Chrome` یا `Microsoft Edge` استفاده کن. مرورگرهایی مثل `Firefox` و `Safari` در حال حاضر برای این نوع اتصال سریال مناسب نیستند.

### امنیت و حریم خصوصی

این ابزار داده‌های سریال را روی سرور آپلود نمی‌کند. اتصال سریال داخل مرورگر انجام می‌شود و فقط بعد از انتخاب دستی پورت توسط کاربر شروع می‌شود.

مرورگر بدون اجازه کاربر نمی‌تواند به پورت سریال وصل شود. هر بار که بخواهی پورت جدیدی را انتخاب کنی، پنجره دسترسی مرورگر نمایش داده می‌شود.

### محدودیت‌ها

- فقط در مرورگرهایی کار می‌کند که از `Web Serial API` پشتیبانی می‌کنند.
- هر پورت سریال معمولاً در یک زمان فقط توسط یک برنامه قابل استفاده است.
- نام دقیق بعضی پورت‌ها ممکن است توسط مرورگر کامل نمایش داده نشود.
- در لاگ‌های بسیار سریع، عملکرد به مرورگر، سیستم و سرعت دستگاه بستگی دارد.

## English

### Why this project exists

This project was created to solve a practical limitation in `Arduino IDE 2.x`.

When working with long serial outputs in the built-in `Serial Monitor`, copying the full received log is not always reliable. In many situations, using `Ctrl + A` and `Ctrl + C` only copies the part currently visible or rendered in the interface, not the complete serial output that has been received over time.

This is especially problematic during hardware debugging, module testing, and serial communication troubleshooting. When testing boards and modules such as `Arduino`, `ESP32`, `SIM800`, sensors, or `AT Command` based devices, losing part of the log can hide the actual cause of a problem.

### The problem with `Arduino IDE 2.x Serial Monitor`

The built-in serial monitor in `Arduino IDE 2.x` is not always convenient for handling long logs as one complete selectable text buffer. Its user interface may only keep the currently visible or rendered lines available for selection.

As a result, selecting and copying everything from the serial monitor may not give you the complete received log.

### The solution

Instead of modifying the Arduino IDE itself, this project provides a standalone single-file `HTML` tool.

It connects directly to the serial port using the browser's `Web Serial API`, keeps the received data in its own internal log buffer, and allows you to copy or save the complete log easily.

### Features

- Direct serial connection through the browser using the `Web Serial API`
- Full serial log display
- Internal log buffer independent from Arduino IDE
- Copy all received logs
- Save logs as `.txt`
- Send commands to Arduino or other serial devices
- Baudrate selector
- Previously authorized port list using `navigator.serial.getPorts()`
- Refresh button for authorized ports
- Newline options:
  - no line ending
  - `\n`
  - `\r`
  - `\r\n`
- Line count, byte count, connection time and receive-rate display
- Persian / English language toggle
- Dark user interface
- Single-file app: `index.html`

### How to use

1. Open the online app in `Chrome` or `Edge`.
2. Close `Arduino IDE Serial Monitor` if it is using the same port.
3. Select the correct `baudrate`.
4. Choose `New port...`.
5. Click `Connect`.
6. Select your Arduino or serial device from the browser permission popup.
7. Start receiving logs.
8. Use `Copy All` or `Save Log` when needed.
9. Use the command input field to send serial commands.

Example Arduino code:

```cpp
void setup() {
  Serial.begin(115200);
}

void loop() {
  Serial.println("Hello from Arduino");
  delay(1000);
}
```

For this example, select `115200` as the baudrate in the tool.

### Browser support

| Browser | Status |
|---|---|
| Google Chrome | Supported |
| Microsoft Edge | Supported |
| Firefox | Not supported |
| Safari | Not supported |

The `Web Serial API` requires a compatible Chromium-based browser and a secure context such as `https://` or `localhost`.

### Troubleshooting

#### The port is not visible

- Make sure the board is connected with a data-capable USB cable.
- Close Arduino IDE Serial Monitor or any other app using the port.
- Try unplugging and reconnecting the board.
- Use Chrome or Edge.
- Click `Refresh` if the port was previously authorized.

#### Connected, but no data appears

- Check the baudrate.
- Make sure your firmware uses the same `Serial.begin(...)` value.
- Make sure the board is actually printing data.
- Try the simple Arduino example above.

#### Web Serial is not supported

Use Google Chrome or Microsoft Edge.

### Security and privacy

This app runs in your browser. It does not upload your serial data to a server.

The serial connection only starts after you explicitly select a port in the browser permission popup.

### Known limitations

- It only works in browsers that support the `Web Serial API`.
- Only one app can use a serial port at a time.
- Some COM port names may not be displayed clearly by the browser.
- Very high-speed logs may depend on browser and system performance.

## Tested With / تست‌شده با

- Arduino-compatible boards
- Common baudrates such as `9600` and `115200`
- Chrome / Edge on desktop

## Project Structure / ساختار پروژه

```text
arduino-serial-logger/
├── index.html
├── README.md
├── CHANGELOG.md
└── LICENSE
```

## License / مجوز

MIT

<div dir="rtl" style="font-family: 'Vazirmatn', 'Tahoma', 'Arial', sans-serif;">

# 🎓 پلتفرم مدیریت دانشگاه

> پلتفرم جامع و هوشمند برای مدیریت فعالیت‌ های دانشگاهی - پروژه درس تحلیل و طراحی سیستم دانشگاه گیلان

## 📋 معرفی پروژه

این پروژه با هدف طراحی و پیاده‌سازی یک پلتفرم جامع و هوشمند برای مدیریت فعالیت‌های کلیدی دانشگاهی آغاز شده است. این پلتفرم قرار است به عنوان ستون فقرات دیجیتال دانشگاه عمل کرده و شامل ماژول‌های مختلفی از جمله مدیریت منابع فیزیکی (رزرواسیون فضاها، آزمایشگاه‌ها) تا مدیریت خدمات دانشجویی (بازارچه خدمات، خرید بلیت کارگاه‌ها) باشد.

پلتفرم در قالب پلتفرمی طراحی شده که خدمات مختلف دانشگاه را از جمله احراز هویت، رزرو منابع، بازارچه خدمات و آموزش آنلاین به صورت هوشمند و یکپارچه ارائه می‌دهد. این یکپارچگی از طریق واسط‌های استاندارد (API Gateway و Message Broker) تضمین می‌شود تا هر سرویس بتواند به صورت مستقل توسعه یابد و مستقر گردد.

---

## 🏗️ معماری سیستم

### معماری میکروسرویس

پلتفرم بر اساس معماری **Microservices** طراحی می‌شود که به معنای مجموعه‌ای از سرویس‌های مستقل، کوچک و متمرکز بر یک دامنه تجاری خاص است. این ساختار تضمین می‌کند که هر سرویس بتواند به طور جداگانه مستقر، مقیاس‌بندی و توسعه یابد.

**مزایای کلیدی:**
- **مقیاس‌پذیری مستقل**: هر سرویس می‌تواند بر اساس نیازهای خود مقیاس یابد (مثلاً اگر Resource Service تحت فشار رزرو باشد، فقط آن سرویس باید مقیاس یابد)
- **استقلال تیم‌ها**: تیم‌ها می‌توانند به صورت مستقل روی سرویس‌های مختلف کار کنند
- **مالکیت داده**: هر سرویس داده‌های خود را به صورت جداگانه نگهداری می‌کند
- **تست آسان‌تر**: تست الگوهای پیچیده مانند SAGA ساده‌تر می‌شود

---

## 🛠️ تکنولوژی‌های استفاده شده

### بک‌اند: FastAPI (پایتون)

پایتون به دلیل خوانایی بالا و اکوسیستم غنی، انتخاب اول برای توسعه بک‌اند است. FastAPI به عنوان فریمورک اصلی وب به دلایل متعددی انتخاب شده است:

#### چرا FastAPI؟

**۱. پشتیبانی ذاتی از پردازش ناهمزمان (Async/Await)**
- محیط توسعه مبتنی بر asyncio در پایتون، به FastAPI اجازه می‌دهد تا حجم بالایی از درخواست‌های همزمان را بدون نیاز به استفاده از Thread‌های سنگین مدیریت کند
- این امر برای یک پلتفرم دانشگاهی با ترافیک متغیر، حیاتی است

**۲. مستندسازی خودکار (Swagger/OpenAPI)**
- FastAPI به طور خودکار براساس Type Hint‌های پایتون، مستندات کامل و تعاملی (Interactive Documentation) برای تمامی Endpoint‌ها تولید می‌کند
- این ویژگی توسعه و تست APIها را به شدت سرعت می‌بخشد

**۳. ادغام آسان**
- قابلیت اتصال سریع و کارآمد به زیرساخت‌های مدرن:
  - **RabbitMQ** برای پیام‌رسانی
  - **Redis** برای کشینگ
  - **PostgreSQL** برای پایگاه داده رابطه‌ای

**دلیل فنی**: انتخاب بر اساس توانایی ذاتی در مدیریت عملیات I/O-Bound به صورت ناهمزمان (async/await)، که برای محیط‌های I/O-محور مانند APIها حیاتی است. مستندسازی خودکار و ساختار تمیز آن، توسعه در محیط میکروسرویس را تسهیل می‌کند.

### گزینه جایگزین: Spring Boot (جاوا)

جاوا به عنوان یک زبان بالغ، پایدار و دارای اکوسیستم بسیار غنی در پروژه‌های سازمانی، انتخابی مطمئن است. استفاده از Spring Boot به عنوان فریمورک اصلی توسعه سرویس‌ها به دلایل زیر پیشنهاد می‌شود:

- **پشتیبانی کامل از معماری میکروسرویس**: با ماژول‌های Spring Cloud برای Service Discovery، Config Server، و Load Balancing
- **مدیریت تراکنش‌های توزیع‌شده**: با پشتیبانی از الگوهایی مانند SAGA و Circuit Breaker از طریق کتابخانه‌هایی نظیر Resilience4j
- **اکوسیستم گسترده**: شامل Spring Data برای اتصال به پایگاه داده‌های رابطه‌ای و NoSQL، و Spring Security برای احراز هویت و کنترل دسترسی
- **قابلیت استقرار آسان**: در کانتینرهای Docker و هماهنگی با ابزارهای CI/CD
- **سرعت بالای توسعه**: با استفاده از Dependency Injection و پیکربندی‌های از پیش آماده

### فرانت‌اند: Flutter

Flutter به عنوان فریمورک توسعه رابط کاربری کراس‌پلتفرم، انتخاب مناسبی برای پوشش همزمان وب، اندروید و iOS است.

#### چرا Flutter؟

**یکپارچگی کد**
- با استفاده از یک کدبیس می‌توان رابط کاربری را برای چند پلتفرم طراحی و اجرا کرد

**پشتیبانی از معماری Reactive**
- حالت‌های مدیریت‌شده (State Management) مانند Provider برای سرعت و یکپارچگی توسعه

**انطباق آسان با API Gateway**
- اتصال یکپارچه با سرویس‌های پشت‌صحنه (Back-end) از طریق درخواست‌های HTTP/REST و WebSocket

**طراحی مدرن و پویا**
- مجموعه ابزارها و ویجت‌های آماده برای رابط‌های کاربری پیچیده دانشگاهی

---

## 🔧 اجزای زیرساخت

### Message Broker: RabbitMQ

برای پیاده‌سازی ارتباطات ناهمزمان و معماری رویداد محور، استفاده از یک Message Broker ضروری است:

**تسهیل ارتباط رویداد محور (Event-Driven)**
- سرویس‌ها می‌توانند بدون نیاز به دانستن مستقیم وجود سرویس‌های دیگر، رویدادها را منتشر کنند
- این امر وابستگی مستقیم (Direct Coupling) را از بین می‌برد

**قابلیت پیاده‌سازی الگوی SAGA**
- صف‌بندی پیام‌ها و اطمینان از تحویل پیام‌ها (Guaranteed Delivery) امکان پیاده‌سازی موفقیت‌آمیز مراحل مختلف تراکنش‌های توزیع‌شده (SAGA) را فراهم می‌کند

**Load Leveling**
- در صورت بروز اوج ترافیک، RabbitMQ پیام‌ها را در صف نگه‌داشته و اجازه می‌دهد سرویس‌های مصرف‌کننده با سرعت پایدار خود به پردازش ادامه دهند

**مورد استفاده**: برای عملیاتی مانند رزرو که شامل مراحل مختلفی است (تأیید موجودی، ثبت در دیتابیس، ارسال اعلان)، استفاده از صف‌بندی پیام‌ها تضمین می‌کند که در صورت خرابی موقت سرویس دریافت‌کننده، پیام از بین نرفته و در زمان مناسب پردازش شود (Durability). این انتخاب مقدمه‌ای برای پیاده‌سازی الگوی SAGA است.

### پایگاه داده: PostgreSQL + Redis

ترکیب این دو فناوری برای مدیریت داده‌ها و عملکرد استفاده می‌شود:

**PostgreSQL**
- به عنوان منبع اصلی داده‌های پایدار (Persistent Data) برای تمام سرویس‌ها
- اطمینان از سازگاری داده‌ها (ACID Properties) در تراکنش‌های اصلی بسیار اهمیت دارد
- مدل‌های داده پیچیده رابطه‌ای را در صورت لزوم مدیریت می‌کند

**Redis**
- استفاده اصلی از Redis در این فاز برای Caching داده‌های پرتقاضا (مانند لیست منابع موجود)
- همچنین به عنوان مخزن موقت برای مدیریت Session‌ها (به ویژه در API Gateway)
- تبادل اطلاعات بین کلاسترها سریع‌تر انجام می‌شود

---

## 🔌 الگوهای ارتباطی

### REST + RabbitMQ

**REST**: برای عملیات درخواست-پاسخ همزمان
**RabbitMQ**: برای عملیات ناهمزمان و رویداد محور

**دلیل انتخاب**: در عملیاتی مانند رزرو که شامل مراحل مختلفی است (تأیید موجودی، ثبت در دیتابیس، ارسال اعلان)، استفاده از صف‌بندی پیام‌ها تضمین می‌کند که در صورت خرابی موقت سرویس دریافت‌کننده، پیام از بین نرفته و در زمان مناسب پردازش شود. این انتخاب مقدمه‌ای برای پیاده‌سازی الگوی SAGA است.

---

## 📐 نمودارهای معماری سیستم (C4 Model)

### 📊 نمودار سطح 1: Context (بستر سیستم)

این نمودار نمای کلی از سیستم و تعامل کاربران و سیستم‌های خارجی با آن را نشان می‌دهد.

![C1 Diagram](https://www.plantuml.com/plantuml/png/dL8_Jnin5D_lKxXCGIfawTG9YGOO28qQK4Ta4WUiddsdEmV8rbOSoS2dw78qHJq5a11BFuTTjdwI_bvCY8dQ3XsIECy___wyzzPompFJLt7qGkfEtEyATcHCch-krpD-ideepL7_e9-Bh9De8xHPxIIgdiPSqvkLt7HZUL1VVxNIej9USxkkU6v4XjB-EhquDQifiKVv1wbJdd75kgB7-x7PmFKELuBjygD4yIWoqiI2sSgMxjpU_gJV8NE5hHukx0IVCND3DxAthi1znUmD00M1tJ2AMYBB4rtB3H9eyv8jpNZibHijuN_Rtomjpw1fblH4dYSPWKkmZV5T4RGrkvc35TVyK13qoTzNMmN-wDq6xo3NW3Kz6A-ZzW3TK3KqpFIIJ07qN_cc0HG6nVQqF8Ob-IIZ48gr7lddalkDKrDB-K3vRhWVTaBAzZjaS9X0gBJNdhdbOMoJ6t721o09E7HYP4zsk969zfswTsVawjT7s8P971yko2quaU9cwhNPhZSKbp5hY-nOTiHpJiLJW13iCz8E5zusUHgyYjw9U3xLi8zVOBzm8tS-pSCmwGbcWdGNzjATWUsE8IqrjaADcWhlb_QUmVKr2L9rH8Sfm7x3vHYX2ESAI4CvN99GspVm9fmU2OUUIjIkQAC26KywNwQ04kjm3VG4CKfmWHW7DwGT0y72qW5oHqEmznuSk9YrR4xzvoL0KB2NR5Q3-YrrVsjtjzK6oNEEVoo1fq75xyBPtqaUfruWXD-PXHYseWYu-sJ78KlKtdhxVd-xiTdOULDRZjQ4xlPL_1i0)

**توضیحات:**
- **دانشجو (Student)**: ثبت‌نام، ورود، رزرو منابع، خرید بلیت، شرکت در آزمون
- **استاد (Professor)**: ورود، ایجاد آزمون، مدیریت دروس  
- **مدیر دانشکده (Faculty Manager)**: مدیریت اطلاعات دانشکده، مشاهده گزارشات
- **سیستم‌های خارجی**: دروازه پرداخت، سرویس اعلان‌رسانی، سرویس نقشه

---

### 📊 نمودار سطح 2: Container (کانتینرها)

این نمودار اجزای اصلی سیستم (سرویس‌ها، پایگاه داده‌ها، صف پیام) و ارتباط آنها را نشان می‌دهد.

![C2 Diagram](https://www.plantuml.com/plantuml/png/fLOxSzj64ExnAn1MyemjDAbIMG_9Zn4TIbJ69UT8dYYCy60E1plgGWyVAlWht336nE9GP2AhqU-uexhyakmUGEW841GzBcX3Xzrll_rk7tWPSC9uw3h6JxRNSC8cDSyvRmU_M1OZ7xTRDZyFws50MSFtEFNuTiDthRP3FFHv4V2cOzUjlPzVLF3ej_AHvPA0KmP7jJtm8BP7sNORyOtWmlRQX17NRD8p4Zhy40pU4PUQf-JSTubXS9ixr1HZCP9zCPlZ_mDJziJuOIWcy8jCEP1NOYPxy7viYYaOzD1O3WoZGbdWUrl8zRbPcdyH8p4HVy4FtfVWfCeXEOy7pyqAyyze4FWCdil48otmB3qpZ9JmbklNROU24t2P0bG48FSMXBq2nD73K7PDF97TX-7y2n2RnI4EdP1p3ByFcfPoBCpqJqZ6n3Dul5sEt2ASVYINuBjJUODIJ23cIDp8WSgXpMolPUuvVjWqNyMcU8vsubfPJaNqtvz3EH0Z9PPI3Ow_gd0tfhn2GQUne4ZWORXCW8Jyl0OQVh0RAC1g32qJl8M9ifbg37TzduFGVi1RZ5QFZqh5K6_VdoxTyJATkkzV0A3E22yVbRj3Ry2vmVYRqu1O_uB_dUnepiX5_2sxycgU4D71bPh575t2BYY7fcXGZISm15IKQGxrcU5t25q25vpbLYKjWfNLdO_HraGC-0VhJDocrufN20h-0yIwW1-jeKOTIfYtBA3uB6wmb6LVvVWPdu7eR7C9zspM26rkxZ9ABYXBQAQmAT52MhRFDK9lVAY0llYcIYegKkg4Dkq0JyGKZAV0UQAYuBWGOpb8ekBDtGCEda9Iot4zdzjdTeDms_Sq0bWEAAMY3hvJV0IWbKnAMOUOnIZnwov5tA_73TMivwP1IXpv0krut27wHcsJ1Hk9Mzb5NbWH6Gvf5oaQUbLlIAAWwH1XVMIzDp1wjYqsZ8zttb7vpZ18lWNMiz3QG77GQdxJ-FdYlbfCv-cwuCSX3UaM8_MwpTtVKSbxdBkoPmBv3aAVg7VbOtn-BBX561pGsAXzv2Lxo2AvR-mL9UPjDbk6dO9e4IO9Q7TOrZDC4yi6aluA61tnBSuqRgm2U_b9TcGtAJZLJTNBW5EtTl07tsgJIvTwlFQujDBMknPHRdjLOlDqSJtJiG8tg56Ns0wEddBLEi3dJ0U27MKUSN23Vx2Rb2r3kAIjxuc-_2HckSbR9cqJknWoEQ5EyhcGxdlLNV4MLGKtZfc_FZsjLC45FHQsQT85srUR22ZoGVNKMi0edDJ_wOsx0406kcT-EHPkh2A8rRjBTX14p5ILNok4SH72zwoO8Wnz7-W3FZ_SDGG5iIpUuwoDxmDmnh9loJuc8wBuA-tj_kvUGY0dO7BmFHWh5TGEdyI24RFZDCwfUvaWhb0qFTg8sMfnj26KD4GYBXOhWaLgkauGPQTyN2dIICSPgzh0OH9PnHYwHZ-4ayhmeraLV0cicDDfEsiKDQm2YN2ahfsewU35MSRzXkyanB0LSZYPDb2pU2L2iTfFp6hzcqcVUCLQQGCx5KiVUZf8Dg_CfEv1FkgBAxD9TGoZ-lhNzxMZWrS7x_QtdXalgTSCNUT_)

**اجزای کلیدی:**
- **API Gateway**: مسیریابی و احراز هویت درخواست‌ها
- **Auth Service**: مدیریت JWT و احراز هویت کاربران
- **Booking Service**: مدیریت رزروها با قفل توزیع‌شده
- **Marketplace Service**: خرید و فروش با الگوی SAGA
- **E-Learning Service**: آموزش و آزمون با Circuit Breaker
- **IoT Service**: پردازش داده‌های سنسورها
- **Notification Service**: ارسال اعلان‌ها
- **RabbitMQ**: ارتباط ناهمزمان بین سرویس‌ها
- **Redis**: کش و قفل توزیع‌شده

---

### 📊 نمودار سطح 3: Component - سرویس بازارچه (الگوی SAGA)

جزئیات پیاده‌سازی الگوی SAGA برای مدیریت تراکنش‌های توزیع‌شده در سرویس بازارچه.

![C3-A Diagram](https://www.plantuml.com/plantuml/png/bLJTRXf76BtdAQPSOQasIj8hNyLndAIIdUBWgfTeO2UmylxGsTcagAfKHnXyuVV0HOuHDfNLNlGvPibTdwJd6xQOyUvYnn9Us9bpplVpVUTvfBXKiU-Lld63bXSxWdMKwaRRrQha7xVQhkh4pJWIiXK6IWHggnNwrQx70y9iHihnt6PrzxlD6htwyM2_wlD82ObNZTtGxuO1ORh4NugEtQ3B9VUP8zxps5ElGFcM-u8TyKxeyr99kSeJJ4_qA1desPoUGvQSwicNSpt5PyoIONAcPyafpYTCt-32ALrEXgNIBjYu6mXPQNCbFlBUjwoyK_kUwAO0ZVHrCYpZNRqhtQ3DThqmTjZhnTNonWg-yIAC0uVBNiNdybWePDiI0EeB8i5dEeSWr8aNKTsKDzYl9OQ_PSQLK3eWefh9qFE49FXDSa9WFMFpFn3_6F2-db98hr0p2dKlSBgX6wYoVPqoq5UK0pJ7__v-dWprwCkvLHbaO4VGbQ4JjvGT0n2VzP_9MT9_E0RhEgJ7UNhtH2FUverGjZeYKfAha3JhU8U-KQFmVp2V804IfnOkEbBhgKuOe2CyYkwdVe47vMfOmD2VJwZe3EUNYwF2p36q7zoMiDDUwHeENiGHEXv5R3zikwriogWI01TKyZDyHKpCpDvjyYaZwmOVy0Xbpn96roxnGTs-Ljh2hcyrx_buhkh-WzfCG7C5elMwzkLqkDZotRMUfNgv4ov5DxGxXaYli6e3isg7-piUXi7lPITwHDs_csLzGIireG77ZPlYjXf9grg5ajQbnqlUqvMysNIL_tEZvRdu3TPtvit18UrGdwXeaymWkyUSdcczZIA9aGgrReG2ZAjuqERDg1Q5lKp5xEvONfPHVtDqL6Ex1bTU2oGZOwOJO-DfjuZYjnK3VDciECqSmqlpmN2GxCAUJTfXfDfIeFGWMh8SnY8Mo-gPW4m9JXawSb9UgIDGzLwaXD_O--Mk0dSkNfW9aG0YPC0zLblWLYtzdV0gIvgi9HTxh8bkhtu44elZ0LCjPZ4qsGWA_LBFJ9P_fG7awUROt0avua8_6M2UKzqSbQnPMNc0vve2ODjFQBkc-dFIHxatYkZMEv3b9cpxwQCeY_n5ZsduQBlOzZERoL3bPBRg71bJlW21sNwxr8Ne_ykBJHXKam5-pFGu6QJeJ24UscThNj8KR4MdMQoQEXw0T_FrU5JnU6GzBsjfjeiHKGQLk_mZAZU-zYcCdOF3MXf7nlhM6i7IyUe43q8bc7JR7SN2zzcjWiTkBzRgClNX0LxbpVlM4nmKp-xMKnpd3-FMCnoH452tg0ynwsdQOnB6eAN2nbTdm2G3AWaYE4a-sQfwD0ViBYuu_TzuR1QYLo99iMR8XsmnMYdr10mYS1ZLgrIgl_dXfyR-tkkzjoyh6wNdE8Xzxpy0)

**جریان SAGA:**
1. **رزرو محصول**: بررسی و رزرو موجودی
2. **پردازش پرداخت**: ارتباط با دروازه پرداخت
3. **تایید سفارش**: ثبت نهایی سفارش

**جبران در صورت خطا:**
- اگر پرداخت ناموفق باشد → لغو رزرو
- اگر تایید ناموفق باشد → استرداد وجه

---

### 📊 نمودار سطح 3: Component - سرویس آموزش (Circuit Breaker)

جزئیات پیاده‌سازی Circuit Breaker برای محافظت در برابر خرابی سرویس‌های خارجی.

![C3-B Diagram](https://www.plantuml.com/plantuml/png/ZLRBRjj65DtpAwPQoK0TRRBAAf5i9mtiHBPJT2cCfB7CXW-573ODYW9rOJqM-efi90ke1CLoMc_o7JFIhb_IUp2iA5AqP0E6oCjxphcFEvTy7aeUoCXrhEzih-54JS4kfMo7pqgbW7zyqhBbPLIFGX4qV4yAJpvf-6wfxN0FcFrGDXsxNgeytQ_2zEF9SSdbeHG1cMeLtstx7Z1jy5lXUzjhyu2xh2akUEJ88w9ymrt1tl5Bt-MM9Mtf2AQcQgYxQhx0Ru_fZfek1sf6_sEcUxglvhf3pwTCtP931ywwPraLOkEs9u9YYqlnaN_wdXLUL7y0tOn0G_L5zmfaEsy7jjTY5SUFckobSItihU5hPJ_ocZpuL1IEu857tWHJducWe_kwotIVgS-uLb_K754GFqLtMzXZlrcC_bQP5yMltAsXT87lE298yonkA8qneQ_LR2soikzBTdPu_gwGTaSYQe9KI7Byxny3tLF3vI1L84ea7S27I8JIzhrC4BUW8TsX6kyE8ml84SnBcuRc5xiXCaaarQ87vIYaYeSXE_PRTYETRvmWXKUO4UxwT3bKCwRH_h_rdmyccqYd0zykddKUOR8MDzlhw_dIlh0RtDJOiSa6eg6w1mso82JfqkLoW59VesSeE0IFXDtoQ1G1AsHm9dko6FXrVgKRTj28R5ch1uA_5-XjnLXOsLX0UoP26neDyVHdt2TrMCbCI6QeHXIZ6fbBAZGc3kd_HVfNwf-jtGv4sq_r3y09tNJNPkg0IyvULrziJlPGJNKlcMarqZqoOz2H_tBmSAyXdEtTDkcixwF5isa7l5wtfViXQViPX-NaDDtd98ON9wTLt9hgnyAco_1KStIRn7vVsqO7zMAp3ipQnec1J7-3YDcJuAtweMm5ulpqc4XM3AUHYCGgMdBJtqYSDYTJT_ggi1RtEYgPxCo1oX_jpDawug6avOkzUYQSP2Ddzk6s1GSQh1_YI57itcWF4u5fSoTdjfM-mW40tgGM1v2hkp9kWoUoYTkklP4--C3d8ZQFFrvqJDsh4UdFOkY6rmEzNJ_gwExSJ5asePnw9YIfPH1ZYAPRqbswcQknxcOAcc1NbftuHDYuDkjRtEdHwuDo9IlxU6H-fjdpl_jSWsC3bNima-QJ6Mi38L3N10lirgLa_aMszHPZppAhdr4UNzKzSIPV2-G6po9z_eIYkOTjJqT4zyYeEyi1-U5p09LO3H4kXdW5vd-1iFq4g-QwRx1pcYKaCQVBnKt6tOJmjYqy1829NQEOG1CaAoJvu53eA_AyqzUwzxX0m41liGLypIUbsPbBUWe8nlehtIkGJ9AuNd7dOjy4Xt7N7OrtmofEB2ma1vgDcfYtvHJYU3PMzsOQujZ-dx4uQuPsnoqmHZfe1dUdEv16F-AF3w8GNfDX22ph_DNRdsh7XoyFtnmKzwpdz21odVy0)

**وضعیت‌های Circuit Breaker:**
- **بسته (Closed)**: درخواست‌ها عادی عبور می‌کنند
- **باز (Open)**: درخواست‌ها بلافاصله شکست می‌خورند و پاسخ پیش‌فرض برگردانده می‌شود
- **نیمه‌باز (Half-Open)**: تعداد محدودی درخواست آزمایشی برای تصمیم‌گیری

---

### 📊 نمودار سطح 3: Component - سرویس رزرو (قفل توزیع‌شده)

جزئیات پیاده‌سازی قفل توزیع‌شده برای جلوگیری از رزرو مضاعف.

![C3-C Diagram](https://www.plantuml.com/plantuml/png/ZLRVKjl65xxtKvoVhs1-1JTDqWjV0SP9au74_CdqqhEM5wD1qhhIAXacavaw0vWBdg8tfawBQ-CMV9FdM8MxFadFaHQnmXQ6mMDvTSxtVUVisKzQ2IJpPUWwXV_PdkM4JGxxKhQ3Sgdaim_BBLlkXuqmuBubFCazkMm9jzHsc4SvIu5iEdQZL7csLAEbTviR9PS5alkuLAy8joqyocaJVY4uiBqsyvaBJRx7GaU-GCWtpEMmo_Q5ome5QKk7WngeNdIYnj_ekmlHiHhSdAaXVleGTQDJDOwEyVu0r2K675Dmr2qKAeZ6R8_x2oqc-GTs-1qKLskl26w8IJqrYhf5NDjf-xRNWeeZmYQyJ4ABYqP-VKs4NfFvXmiD8L1p2vE84I7ErGIYKr13DI9GL41VgEook0WV2u1_QTMtsNNgd2ySX_i8bAP--nqH-tXvf8Q6h3KX96nNTtQBPZ3Le2we2cJi__lhMTHLlPkpJ6-mXYo_pmCH-XOt1PYLp9UG3Pz1bbCnZijxs-AOFgjJkBmM1jZf880DqR8j-3-ixFhC2vWbRU4nXq98cEh54iVP6K0nFJ3wYD3dr99JlEof8SIIhwBFkGqnz1dbFQGm5ZJ0219rUNEcTu1c8Rz1MNBsdjaEQzYEBG-p0axL7_Z1pBaIJBNdb1ETm9siU4geEyD4v9G4HrW7TPTvh9LCmkUe4nsbgebWcpVj811UiW78CC8x4wnMZP6i2phbyPFWyxOmnm0pB_0WdXZZjiuaWzUrrVi3toF6TDIfu2wOUv2_lKIQxTOSMYFoySHJxDYwkkNO-EEsatJ2ZWY4pfdPNwZ4SUcIdkaU4lJfKbrDLySQ3LkwlnWKyShcLeR5g71rSwj6F_LCwS9Y7efKO-93da-6zwqt5feDOoEIU9qAqLUYINoPa6iYa2sVxsnj88o94JSZPuRmb8v1_OaO7NLDEBe79iHMo4EUbamxz1L1qEn1_HrrYaRnvDpRtBdp_7pNdJRI68YCRZ6BCSyvys5Yd5aIfgqnwf314GhjHpnMb3oJErtCJpV8iqIpJtss0bX-ekcpqUPGFsm994NzfK7CD0sICj_DVCqNKbZ2oLN-2Ciqx0wMVz3qi_FksyDETQDQsOKNRxVXNMrzTRUg3w7kA9bhhh8yUrDV40Ex-PGopTtCbs7obQ8JUhrHVPFQP6esyZEeiQ_Nrohtv-ZncRdbJdlFF4yXcAcicUSPu-azBXaCiYnIuGd9mRTR-nB4tlspKm0eew7_WwcJg6EyZFNK270mZl1DG3-Uy2TzaJZCmd_jjXGvTvZnKCGU34Kje7pRq_B7swjNpKz5A9C1KpTYZjbs2Pdt6QH3nMg2Cvlav0nZxgW_rLJNYDFHRqNnGol67L5OOWk0ZPaQpsT9za95kAuj5pFQj6hAXkNdSM3Qbj_KY4eZR3KY6Jy-U9-ujz716imwW3Asz4hroC1FwJ4NEr21UqsWpTPRxl0zsl6CPz5sQm8QLdMD3xfZ9EXJ_L-IAh6_pw6iP_2QPWhK2AEeYALit9FlAL1Dw44x8_22cfs-IEBu3DI0U8zmPGnBXk2Tdzx-ND-elgo-MLzOBApWZT1r_WC0)

**جریان جلوگیری از رزرو مضاعف:**
1. **اخذ قفل توزیع‌شده** از Redis با کلید `booking:resource:{resourceId}`
2. **شروع تراکنش** پایگاه داده
3. **بررسی موجودی** با `SELECT FOR UPDATE`
4. **ثبت رزرو** و به‌روزرسانی ظرفیت
5. **پایان تراکنش** (Commit)
6. **آزادسازی قفل**

**تنظیمات قفل:**
- زمان انتظار: 5 ثانیه
- زمان اعتبار: 10 ثانیه
- تلاش مجدد خودکار

---

### 📊 نمودار سطح 4: Code - کلاس‌های الگوی SAGA

جزئیات کلاس‌ها و رابط‌های پیاده‌سازی الگوی SAGA.

![C4 Diagram](https://www.plantuml.com/plantuml/png/pLRBJkH65DtxAshPA07baLKhGeC8Wv0889gzLTWNiF2ZLIuJI39I1WLw5lm7114wP4YYsUGxx9bTlYJdLfcQih0wOOSqGrVTEkVUSn-swqMffT9LbWRbOPAFfPAPY6bFLgb-MUHwGsOaTkH1aKaF4AMoB9UqLibkfMajAl9HyZs9pu909pebKK_ho-Qyld_FlnFHdDNJ3nVr7VvVYsRIlAdlcpESJqNz5e0p1ZUJ831knQQAIOtaljnKqG6LMabTAF538CIyA64EeLZJK31an4jxecbS3iLwKkglpGdsY-Q4ZYZNuRZQJPFoWDHGhB1Xws4F3Fvz8amTGWumA5X164ijXo9E8ZrdWsrJYQeOC1rJXCp3d8x1GQW1CBj5aPhJgCZ6b9UGnkQZ8ecDa0EPnoaPUBWdaxHIDE1DcmfMFheLR1I59eU1-MlH9eS7-AiWI79DQaz6v7oXOfxIGLG0SToob-q6V4Qwl7pblGId3z1zqZQLN6OcJtJA72HbwDp8tPHSQLuzTDXrpkzg4biNRB0Dy2rHfHJbRSGaZ-buA92pFKEqb3J5eJy4O2vsPwOgtT1WRS_GT2PAv8b-aquoydps7f5IXGepAk6OMA4ReKogGwlGqGUkH0Rf2kYXxJ0yWdvg0_aqLtU_6YWlLyALtaNs9n87DeZV3Cghp2k8QSPePsbxP-KRhDOsmgtjpTNjbT48k-NDRxVML-p9owMrTIoiSMLZjBIpjh7gRt7eUetX8dL4Mwg8gqYxmPo7PXxXGfs434WYPBtsO1fP2t3FTeQHK8GHs98d6UL-NcDh-PXL2t4vUPXzYFnEdeHHcc3heAlMl6oipxa8yBQNgCo-iLq9siTNqRWe4sxdK1Z4jZCyvvmyZpDVJzxtmQ8ud39gIy_ieYL5tgKOFJAEGu_vw1rWpKCXyvFU_7ffSmRl_3-IC3YaazR_aKmhwdNVp_BSkugvDhc2LH4_6xQonk8bFliLYlwqRDUPLf3LC6UzEAFnr3QusqEdgBU5NOdztvmdwdjmuAdflyhCpozwdy2Xm7tep_gTlHnvDwN_PDCOP33kwilwr-PdWPyRtdouc4rrupraok_yvsrztRp6xxIPpEIwie9wLT_XVdTdxtfWdWU1owgJOrK2ph1MND3pJLXO-B6RrjyeWT7ppqyNa0UTO7PVkayW-Y-g9z02X_X_fUl2iPXPhRn0eLIoVw15iITwonu8vjxmG33FjHZszxyqvx1E1QB3KjzYZ2xP97Wh1dCVBxHYuNCGlbWGpQI-inE3UMac1WbflBh6-Xh-hbmCH62bO7wvWFQ1MV-16831HVEcUTsSyfXQlkSKgRxZAJOvWy0Ule87Y4EKUnu3mGSitjOD-L0U2wv7MvNTGkiYGrbSZxWIS7Z9B3yQfsIUrkOKpguwZm7Zk3sdR0KNmQUC1OHxmMcSSP9j6pqNDwoT5NTvd044tBZIiPUe7Odwj_gMdrqSkieXr6tz5v2SfENuZtWBzB9_WMMLfVy2)

**کلاس‌های اصلی:**
- **OrderSagaOrchestrator**: هماهنگ‌کننده اصلی Saga
- **SagaStep**: رابط مراحل Saga
- **SagaState**: مدیریت وضعیت Saga
- **ReserveProductStep**: مرحله رزرو محصول
- **ProcessPaymentStep**: مرحله پردازش پرداخت
- **ConfirmOrderStep**: مرحله تایید سفارش

---

## 🚀 ویژگی‌های کلیدی

- **🔐 احراز هویت و مجوزدهی**: مدیریت هویت متمرکز
- **📅 رزرو منابع**: رزرو فضاها، آزمایشگاه‌ها و امکانات
- **🛒 بازارچه خدمات**: خدمات دانشجویی و ثبت‌نام کارگاه‌ها
- **📚 آموزش آنلاین**: سیستم مدیریت یادگیری یکپارچه
- **🔔 اعلان‌های رویداد محور**: به‌روزرسانی‌ها و هشدارهای لحظه‌ای
- **📊 معماری مقیاس‌پذیر**: مقیاس‌بندی مستقل سرویس‌ها بر اساس نیاز

---

## 🎯 اصول طراحی اصلی

1. **استقلال**: هر سرویس به صورت مستقل عمل می‌کند
2. **مقیاس‌پذیری**: مقیاس‌بندی مستقل سرویس‌ها بر اساس بار
3. **انعطاف‌پذیری**: جداسازی خرابی‌ها از شکست‌های آبشاری جلوگیری می‌کند
4. **انعطاف**: افزودن، تغییر یا حذف آسان سرویس‌ها
5. **کارایی**: پردازش ناهمزمان و بهینه‌سازی کشینگ

---

## 📝 نکات توسعه

- **نمودارهای C4**: نمودارهای معماری در بالا نشان داده شده‌اند
- **مالکیت داده**: هر میکروسرویس اسکیمای پایگاه داده خود را نگهداری می‌کند
- **الگوی SAGA**: تراکنش‌های توزیع‌شده از طریق کوریوگرافی مدیریت می‌شوند
- **Circuit Breaker**: تحمل خطا برای ارتباطات بین سرویس‌ها

---

##

این پلتفرم طراحی شده تا با نیازهای دانشگاه تکامل یابد. هر میکروسرویس می‌تواند به صورت مستقل توسعه یابد و این امکان را به تیم‌های مختلف می‌دهد که به صورت همزمان مشارکت کنند.


</div>
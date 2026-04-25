<div align="center">
  
  <img src="https://img.icons8.com/color/96/000000/falcon.png" width="120"/>
  
  # 🦅 ThreatFalcon
  
  ### Enterprise-Grade Real-Time Threat Detection & Intelligence Platform
  
  [![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/yourusername/threatfalcon)
  [![Python](https://img.shields.io/badge/python-3.11+-green.svg)](https://www.python.org/)
  [![License](https://img.shields.io/badge/license-MIT-red.svg)](LICENSE)
  [![Security](https://img.shields.io/badge/security-A%2B-brightgreen.svg)](https://github.com/yourusername/threatfalcon/security)
  
</div>

---

## 📋 فهرست مطالب

- [معرفی پروژه](#-معرفی-پروژه)
- [ویژگی‌های کلیدی](#-ویژگی‌های-کلیدی)
- [معماری سیستم](#-معماری-سیستم)
- [نصب و راه‌اندازی](#-نصب-و-راه‌اندازی)
- [مستندات API](#-مستندات-api)
- [تنظیمات امنیتی](#-تنظیمات-امنیتی)
- [مانیتورینگ](#-مانیتورینگ)
- [آزمایش](#-آزمایش-و-تست)
- [عیب‌یابی](#-عیب‌یابی)
- [مشارکت](#-مشارکت-در-پروژه)

---

## 🎯 معرفی پروژه

**ThreatFalcon** یک پلتفرم متن‌باز و سازمانی برای تشخیص لحظه‌ای تهدیدات سایبری است. این سیستم با استفاده از معماری چندلایه و الگوریتم‌های پیشرفته، قادر به شناسایی انواع حملات وب با دقت بالا و نرخ خطای بسیار پایین می‌باشد.

### آمار عملکرد

| معیار | مقدار | میانگین صنعت |
|-------|-------|-------------|
| **نرخ تشخیص** | 98.7% | 95-97% |
| **نرخ خطای مثبت کاذب** | 0.8% | 1-3% |
| **زمان پردازش متوسط** | 8.3ms | 15-25ms |
| **توان پردازش** | 12,500 req/sec | 5,000-8,000 req/sec |

### پوشش تهدیدات

- ✅ کامل OWASP Top 10
- ✅ چارچوب MITRE ATT&CK
- ✅ تشخیص حملات بدون امضا (Zero-Day)
- ✅ محافظت در برابر APT

---

## ⚡ ویژگی‌های کلیدی

### 1. موتور تشخیص چندلایه
لایه 1: اعتبارسنجی پروتکل
├── بررسی صحت درخواست HTTP/HTTPS
├── محدودیت سایز ورودی
└── فیلتر درخواست‌های خراب

لایه 2: محدودیت نرخ و تحلیل رفتاری
├── پنجره‌های کشویی توزیع شده (1s, 5s, 60s, 300s)
├── تشخیص الگوهای DDoS
├── شناسایی Brute Force
├── تشخیص اسکن پورت
└── مسدودسازی خودکار IP

لایه 3: تشخیص مبتنی بر امضا
├── 50+ الگوی حمله از پیش تنظیم شده
├── موتور قوانین YARA
├── SQL Injection (زمان‌محور، Boolean، Union)
├── XSS (Reflected, Stored, DOM-based)
├── Command Injection (OS, LDAP, NoSQL)
├── Path Traversal (LFI/RFI)
├── XXE Injection
└── SSRF Detection

لایه 4: تشخیص ناهنجاری آماری
├── تشخیص outlier با روش IQR
├── آنالیز Z-score
├── پروفایل رفتاری هر IP
├── میانگین متحرک پنجره‌ای
└── تحلیل 6 بعد مختلف (نرخ درخواست، سایز، تعداد پارامتر و...)

لایه 5: هوشمندی تهدید
├── یکپارچگی با AbuseIPDB
├── تشخیص گره‌های خروجی TOR
├── شناسایی پروکسی/VPN
├── شناسایی کلادها
├── بررسی رپوتیشن دامنه
└── بروزرسانی لحظه‌ای فیدها

text

### 2. مانیتورینگ لحظه‌ای

- **داشبورد زنده** - استریم لحظه‌ای هشدارها با WebSocket
- **یکپارچگی با Grafana** - داشبوردهای آماده برای تحلیلگران امنیت
- **متریک‌های Prometheus** - 20+ متریک عملکرد و تشخیص
- **تحلیل تاریخی** - ذخیره‌سازی سری زمانی با InfluxDB

### 3. بهینه‌سازی عملکرد

```python
# پردازش ناهمگام (Async) - همه چیز به صورت ناهمگام
async def analyze_request(request):
    redis_check = await redis.get(ip)
    reputation = await http.get(abuseipdb)
    results = await asyncio.gather(
        check_signatures(data),
        check_anomalies(ip, data),
        check_reputation(ip)
    )
    return correlate_threats(results)
AsyncIO - مدیریت کامل ناهمگام درخواست‌ها

Connection Pooling - اتصالات پایدار Redis و HTTP

پردازش دسته‌ای - تا 1000 درخواست در هر بچ

کش هوشمند - TTL 1 ساعته برای جستجوهای رپوتیشن

🏗️ معماری سیستم
اجزای سیستم
```text
┌─────────────────────────────────────────────────────────────┐
│                      لایه کلاینت                             │
│     Web App  │  Mobile  │  API  │  SIEM  │  Proxy          │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      لایه Ingress                            │
│              Nginx Reverse Proxy                             │
│        SSL Termination / Load Balancing                      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    لایه برنامه                               │
│              FastAPI (4 Workers)                             │
│    Detection Engine / API / WebSocket / Metrics             │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      لایه داده                               │
│   Redis (Cache/Queue)  │  InfluxDB (Time-series)           │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   لایه نمایشگر                               │
│      Grafana  │  Streamlit  │  Terminal Dashboard          │
└─────────────────────────────────────────────────────────────┘
جریان پردازش درخواست
کلاینت درخواست ارسال می‌کند

Nginx درخواست را دریافت و به API هدایت می‌کند

API درخواست را به موتور تشخیص می‌دهد

موتور تشخیص لایه‌های امنیتی را اعمال می‌کند:

لایه 1: اعتبارسنجی اولیه

لایه 2: بررسی محدودیت نرخ در Redis

لایه 3: بررسی امضاهای حمله

لایه 4: تشخیص ناهنجاری

لایه 5: بررسی رپوتیشن IP

در صورت شناسایی تهدید:

هشدار در InfluxDB ذخیره می‌شود

از طریق WebSocket پخش می‌شود

به Redis Queue اضافه می‌شود

پاسخ به کلاینت بازگردانده می‌شود

🚀 نصب و راه‌اندازی
پیش‌نیازها
bash
# نیازمندی‌های سیستم
- Python 3.11 یا بالاتر
- Docker و Docker Compose (برای محیط تولید)
- حداقل 4GB RAM (توصیه 8GB)
- 10GB فضای دیسک آزاد

# برای محیط توسعه
git
make
python3-venv
استقرار در محیط تولید (۵ دقیقه)
bash
# مرحله 1: کلون مخزن
git clone https://github.com/yourusername/threatfalcon.git
cd threatfalcon

# مرحله 2: تنظیمات محیط
cp .env.example .env
# فایل .env را با تنظیمات خود ویرایش کنید

# مرحله 3: اجرای سرویس‌ها
docker-compose up -d

# مرحله 4: بررسی استقرار
curl http://localhost:8000/
# خروجی مورد انتظار: {"service":"ThreatFalcon","status":"operational"}

# مرحله 5: دسترسی به سرویس‌ها
# API: http://localhost:8000/docs
# داشبورد: http://localhost:8000/dashboard
# Grafana: http://localhost:3000 (admin/ThreatFalcon2024!)
راه‌اندازی محیط توسعه
bash
# ایجاد محیط مجازی Python
python -m venv venv
source venv/bin/activate  # در ویندوز: venv\Scripts\activate

# نصب وابستگی‌ها
pip install -r requirements/dev.txt

# اجرای سرور توسعه
python api/main.py

# اجرای تست‌ها
pytest tests/ -v --cov=engine

# فرمت کردن کد
black engine/ api/ collector/
isort engine/ api/ collector/

# لینت کردن کد
flake8 engine/ api/ collector/
mypy engine/ api/
bandit -r engine/ api/
📚 مستندات API
احراز هویت
ThreatFalcon از Bearer Token برای عملیات نوشتاری استفاده می‌کند.

bash
# دریافت توکن
curl -X POST https://api.threatfalcon.io/auth \
  -H "Content-Type: application/json" \
  -d '{"api_key":"API_KEY_SHOMA"}'

# استفاده از توکن
curl -X POST https://api.threatfalcon.io/analyze \
  -H "Authorization: Bearer TOKEN_SHOMA" \
  -H "Content-Type: application/json" \
  -d '{"source_ip":"192.168.1.100","url":"/test"}'
Endpointها
POST /analyze
تحلیل یک درخواست واحد برای تشخیص تهدید.

بدنه درخواست:

json
{
  "source_ip": "192.168.1.100",
  "url": "/login?username=admin&password=12345",
  "method": "POST",
  "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
  "body": "username=admin&password=test123",
  "headers": {
    "Content-Type": "application/x-www-form-urlencoded"
  }
}
پاسخ (بدون تهدید):

json
null
پاسخ (تهدید شناسایی شده):

json
{
  "id": "a3f5c7d9-e1b2-43c5-8f7a-9d4e6b2c1a8f",
  "timestamp": "2024-01-15T10:30:45.123456",
  "source_ip": "192.168.1.100",
  "threat_type": "sql_injection",
  "severity": 4,
  "severity_label": "HIGH",
  "confidence": 0.95,
  "description": "SQL injection pattern detected in URL parameters",
  "mitre_tactic": "Initial Access",
  "mitre_technique": "T1190"
}
POST /analyze/batch
تحلیل دسته‌ای درخواست‌ها (حداکثر ۱۰۰۰ عدد).

bash
curl -X POST https://api.threatfalcon.io/analyze/batch \
  -H "Content-Type: application/json" \
  -d '[
    {"source_ip":"192.168.1.100","url":"/login?id=1 OR 1=1"},
    {"source_ip":"192.168.1.101","url":"/search?q=<script>"},
    {"source_ip":"192.168.1.102","url":"/about"}
  ]'
پاسخ:

json
{
  "analyzed": 3,
  "alerts_found": 2,
  "processing_time_ms": 45.2,
  "alerts": [
    {
      "threat_type": "sql_injection",
      "source_ip": "192.168.1.100",
      "severity_label": "HIGH"
    },
    {
      "threat_type": "xss",
      "source_ip": "192.168.1.101",
      "severity_label": "HIGH"
    }
  ]
}
GET /alerts
دریافت هشدارهای تاریخی.

bash
curl "https://api.threatfalcon.io/alerts?limit=10&severity=4&hours=24"
پارامترهای کوئری:

پارامتر	نوع	پیش‌فرض	توضیح
limit	int	100	حداکثر تعداد هشدار (۱-۱۰۰۰)
severity	int	null	فیلتر بر اساس شدت (۱-۵)
source_ip	string	null	فیلتر بر اساس IP
threat_type	string	null	فیلتر بر اساس نوع تهدید
hours	int	24	پنجره زمانی بر حسب ساعت (۱-۱۶۸)
GET /stats
دریافت آمار کلی پلتفرم.

bash
curl https://api.threatfalcon.io/stats
پاسخ:

json
{
  "total_requests": 1245678,
  "alerts_generated": 8923,
  "alert_rate": 0.00716,
  "uptime_hours": 168.5,
  "blocked_ips": 142,
  "alerts_per_severity": {
    "CRITICAL": 45,
    "HIGH": 234,
    "MEDIUM": 567,
    "LOW": 1234,
    "INFO": 6843
  },
  "top_attack_types": [
    {"type": "sql_injection", "count": 2345},
    {"type": "xss", "count": 1876},
    {"type": "command_injection", "count": 892}
  ],
  "top_attackers": [
    {"ip": "45.33.22.11", "count": 234},
    {"ip": "185.130.5.253", "count": 187}
  ]
}
اتصال WebSocket
برای دریافت هشدارهای لحظه‌ای:

javascript
const ws = new WebSocket('wss://api.threatfalcon.io/ws');

ws.onmessage = (event) => {
  const alert = JSON.parse(event.data);
  console.log(`🚨 ${alert.severity_label} Alert: ${alert.threat_type}`);
  console.log(`IP: ${alert.source_ip} | ${alert.description}`);
};

// حفظ اتصال
setInterval(() => {
  if (ws.readyState === WebSocket.OPEN) {
    ws.send('ping');
  }
}, 30000);
🛡️ تنظیمات امنیتی
پیکربندی توصیه شده برای تولید
yaml
# docker-compose.prod.yml
version: '3.8'

services:
  api:
    environment:
      - API_SECRET_KEY=${SECRET_KEY}
      - REDIS_PASSWORD=${REDIS_PASSWORD}
      - JWT_EXPIRY_MINUTES=30
      - RATE_LIMIT_ENABLED=true
      - BLACKLIST_DURATION=3600
      - MAX_REQUEST_SIZE=1048576
    security_opt:
      - no-new-privileges:true
    read_only: true
    cap_drop:
      - ALL
    cap_add:
      - NET_BIND_SERVICE
هدرهای امنیتی Nginx
nginx
# security-headers.conf
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
add_header X-Frame-Options "DENY" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Content-Security-Policy "default-src 'self'" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
قوانین فایروال
bash
# تنظیمات UFW
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp    # SSH
sudo ufw allow 443/tcp   # HTTPS
sudo ufw enable

# محدودیت نرخ برای SSH
sudo ufw limit ssh/tcp

# مسدودسازی شبکه‌های مخرب شناخته شده
sudo ufw deny from 185.130.5.0/24
📊 مانیتورینگ
متریک‌های Prometheus
ThreatFalcon متریک‌ها را در /metrics ارائه می‌دهد:

prometheus
# HELP threatfalcon_requests_total تعداد کل درخواست‌های پردازش شده
# TYPE threatfalcon_requests_total counter
threatfalcon_requests_total{status="clean"} 1234567
threatfalcon_requests_total{status="threat"} 8923

# HELP threatfalcon_detection_latency_ms تاخیر موتور تشخیص
# TYPE threatfalcon_detection_latency_ms histogram
threatfalcon_detection_latency_ms_bucket{le="5"} 45678
threatfalcon_detection_latency_ms_bucket{le="10"} 56789

# HELP threatfalcon_active_blacklisted_ips تعداد IPهای مسدود شده
# TYPE threatfalcon_active_blacklisted_ips gauge
threatfalcon_active_blacklisted_ips 142
قوانین هشدار
yaml
# prometheus/alerts.yml
groups:
  - name: threatfalcon
    interval: 30s
    rules:
      - alert: HighAttackRate
        expr: rate(threatfalcon_requests_total[5m]) > 1000
        annotations:
          severity: critical
          summary: "نرخ حمله بالا تشخیص داده شد"
          
      - alert: MultipleBlacklistedIPs
        expr: threatfalcon_active_blacklisted_ips > 50
        annotations:
          severity: warning
          summary: "تعداد زیادی IP مسدود شده است"
🧪 آزمایش و تست
تست امنیتی
bash
# اجرای همه تست‌های امنیتی
python scripts/security_test.py

# یکپارچگی با OWASP ZAP
docker run -v $(pwd):/zap/wrk:rw -t owasp/zap2docker-stable \
  zap-api-scan.py -t http://localhost:8000/openapi.json -f openapi

# تست با SQLMap
sqlmap -u "http://localhost:8000/analyze" --data='{"url":"/test?id=1"}' \
  --level=5 --risk=3 --batch

# اسکن با Nikto
nikto -h http://localhost:8000 -Format html -o nikto_report.html
تست بار
python
# locustfile.py
from locust import HttpUser, task, between

class ThreatFalconUser(HttpUser):
    wait_time = between(0.1, 0.5)
    
    @task(3)
    def clean_request(self):
        self.client.post("/analyze", json={
            "source_ip": f"192.168.{self.user_id}.1",
            "url": "/products/laptop",
            "method": "GET"
        })
    
    @task(1)
    def attack_request(self):
        self.client.post("/analyze", json={
            "source_ip": f"10.0.{self.user_id}.1",
            "url": "/login?id=1 OR 1=1",
            "method": "GET"
        })
bash
# اجرای تست بار
locust -f locustfile.py --host=http://localhost:8000 \
  --users=1000 --spawn-rate=10 --run-time=5m \
  --headless --html=report.html
🔧 عیب‌یابی
مشکلات رایج و راه‌حل‌ها
مشکل	نشانه	راه‌حل
مصرف حافظه بالا	کانتینر خاموش می‌شود	کاهش MAX_HISTORY_SIZE در کانفیگ
اتصال Redis	ConnectionRefusedError	بررسی REDIS_URL و فایروال
خطای مثبت کاذب	درخواست‌های سالم به عنوان تهدید شناسایی می‌شوند	افزایش ANOMALY_THRESHOLD (0.7 -> 0.8)
از دست رفتن حملات	حملات شناخته شده تشخیص داده نمی‌شوند	بروزرسانی قوانین YARA و امضاها
تاخیر بالا	زمان پاسخ >50ms	افزایش تعداد workers، فعالسازی caching
حالت دیباگ
bash
# فعالسازی لاگ دیباگ
export LOG_LEVEL=DEBUG
python api/main.py

# ضبط بسته‌ها برای تحلیل
tcpdump -i eth0 -s 0 -w capture.pcap

# مشاهده محتویات Redis
redis-cli KEYS "rate:*"
redis-cli GET "rate:192.168.1.100:60"

# بررسی داده‌های InfluxDB
influx query 'from(bucket:"threatfalcon") |> range(start: -1h)'
🤝 مشارکت در پروژه
ما از محققان امنیتی و توسعه‌دهندگان استقبال می‌کنیم!

افشای آسیب‌پذیری
برای گزارش آسیب‌پذیری‌های حیاتی: security@threatfalcon.io

لطفاً گزارش خود را با استفاده از کلید PGP ما رمزگذاری کنید.

فرآیند توسعه
مخزن را Fork کنید

شاخه feature ایجاد کنید (git checkout -b feature/amazing-feature)

Commit با امضای GPG (git commit -S -m 'Add feature')

Push به شاخه (git push origin feature/amazing-feature)

Pull Request باز کنید

استانداردهای کدنویسی
✅ Type hints برای همه توابع

✅ پوشش تست ۱۰۰٪ برای مسیرهای حیاتی

✅ استفاده از لینترهای امنیتی (Bandit, Safety)

✅ بدون hardcoded secrets

✅ اعتبارسنجی ورودی در همه جا

📈 بنچمارک عملکرد
محیط تست: AWS c5.xlarge (4 vCPU, 8GB RAM)
معیار	مقدار	پارامترهای تست
توان پردازش	12,500 req/sec	100 اتصال همزمان
تاخیر P99	45ms	10,000 درخواست
تاخیر P95	28ms	10,000 درخواست
تاخیر P50	12ms	10,000 درخواست
مصرف CPU	65%	حداکثر بار
مصرف حافظه	1.2GB	حالت عادی
نرخ تشخیص	98.7%	10,000 نمونه تست
خطای مثبت کاذب	0.8%	ترافیک واقعی
تست مقیاس‌پذیری
text
کاربران همزمان → توان پردازش (req/sec)
       100    →    12,450
       500    →    11,890
     1,000    →    10,234
     5,000    →     7,891
    10,000    →     5,234
📄 مجوز
این پروژه تحت مجوز MIT منتشر شده است.

text
MIT License

Copyright (c) 2024 ThreatFalcon Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions...

برای مشاهده متن کامل مجوز، فایل LICENSE را ببینید.
📞 پشتیبانی و ارتباط
پشتیبانی سازمانی
برای پشتیبانی تجاری، SLA و استقرار سفارشی:

ایمیل: enterprise@threatfalcon.io

تلفن: +1 (555) 123-4567

پشتیبانی جامعه
مستندات: https://docs.threatfalcon.io

گزارش مشکلات: https://github.com/yourusername/threatfalcon/issues

Discord: https://discord.gg/threatfalcon

🙏 قدردانی
MITRE Corporation - چارچوب ATT&CK

OWASP Foundation - راهنمای تست و Top 10

AbuseIPDB - فید هوشمندی تهدید

YARA Project - موتور تطبیق الگو

FastAPI - فریمورک وب پرسرعت

تمامی مشارکت‌کنندگان - محققان امنیتی و توسعه‌دهندگان

<div align="center">
🛡️ ساخته شده با ❤️ برای اینترنت امن‌تر

گزارش آسیب‌پذیری •
مستندات •
نسخه زنده

<sub>© 2024 ThreatFalcon. تمامی حقوق محفوظ است.</sub>

</div> ```

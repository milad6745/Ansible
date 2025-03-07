در Ansible، **Inventory** یا موجودی، به مجموعه‌ای از سرورها (هاست‌ها) اشاره دارد که Ansible می‌تواند برای مدیریت، پیکربندی، و اجرای دستورات روی آن‌ها استفاده کند. موجودی‌ها می‌توانند به شکل ساده‌ای شامل لیستی از نام‌ها یا آدرس‌های IP سرورها باشند و به شکل پیشرفته‌تر، شامل گروه‌بندی‌ها، متغیرهای مرتبط با سرورها و حتی پویا (dynamic inventory) باشند.

### انواع موجودی‌ها:

1. **موجودی ثابت (Static Inventory):**
   این نوع موجودی در یک فایل متنی تعریف می‌شود (معمولاً `ini` یا `yaml`) که لیستی از سرورها و متغیرهای مرتبط با آن‌ها را شامل می‌شود.

   #### مثال از یک موجودی ساده در قالب `ini`:
   ```ini
   [webservers]
   webserver1.example.com
   webserver2.example.com

   [dbservers]
   dbserver1.example.com
   dbserver2.example.com
   ```

   در این مثال، دو گروه تعریف شده است: `webservers` و `dbservers`، که هر کدام شامل چندین سرور هستند.

   #### مثال از موجودی در قالب `yaml`:
   ```yaml
   all:
     children:
       webservers:
         hosts:
           webserver1.example.com:
           webserver2.example.com:
       dbservers:
         hosts:
           dbserver1.example.com:
           dbserver2.example.com:
   ```

2. **موجودی پویا (Dynamic Inventory):**
3. 
   در این نوع موجودی، سرورها به صورت خودکار و بر اساس یک منبع خارجی (مثل AWS، Google Cloud، یا هر سیستم مدیریت ابری دیگر) بارگذاری می‌شوند. Ansible به جای اینکه لیست سرورها را از یک فایل ثابت بگیرد، از یک اسکریپت یا پلاگین استفاده می‌کند تا اطلاعات سرورها را از منابع پویا دریافت کند.

   برای استفاده از موجودی پویا، باید یک پلاگین مخصوص یا اسکریپت برای آن منبع مشخص تنظیم کنید، مثل پلاگین AWS EC2.

### تعریف متغیرها برای هاست‌ها و گروه‌ها:

شما می‌توانید متغیرهایی را برای هر هاست یا گروه در فایل موجودی تعریف کنید که در هنگام اجرای Playbookها استفاده می‌شوند.

#### مثال:

```ini
[webservers]
webserver1.example.com ansible_user=root ansible_port=22

[dbservers]
dbserver1.example.com ansible_user=admin ansible_port=2222
```

در اینجا، برای هر سرور مشخص شده، متغیرهایی مثل `ansible_user` و `ansible_port` تعریف شده‌اند که به Ansible کمک می‌کند تا با سرورها متصل شود.

### استفاده از موجودی در Playbook:

بعد از تعریف موجودی، می‌توانید در Playbookها از آن استفاده کنید:

```yaml
---
- hosts: webservers
  tasks:
    - name: نصب Nginx
      apt:
        name: nginx
        state: present
```

در این Playbook، Ansible دستورات را روی تمام هاست‌های موجود در گروه `webservers` اجرا می‌کند.

### نتیجه‌گیری:

موجودی‌ها به شما این امکان را می‌دهند که به راحتی مدیریت سرورها را بر اساس گروه‌ها و متغیرها سازماندهی کنید، و اگر با سیستم‌های ابری بزرگ کار می‌کنید، می‌توانید از موجودی‌های پویا برای مدیریت خودکار سرورها استفاده کنید.

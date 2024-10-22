 در Ansible، یک Role (مثل `nginx_role`) باید قبل از اینکه در یک Playbook از آن استفاده شود، **تعریف و ساخته** شود. برای تعریف Role باید ساختار فایل و دایرکتوری مخصوص آن ایجاد شود و تسک‌ها، فایل‌ها و تنظیمات مرتبط با آن داخل دایرکتوری‌های مربوطه قرار گیرد.

### چطور یک Role تعریف کنیم؟



1. برای تعریف یک Role جدید، می‌توانی از دستور `ansible-galaxy init` استفاده کنی. این دستور به صورت خودکار ساختار دایرکتوری‌های Role را ایجاد می‌کند.

به عنوان مثال، برای تعریف یک Role به نام `nginx_role`، می‌توانی این دستور را اجرا کنی:

```bash
ansible-galaxy init nginx_role
```

این دستور یک دایرکتوری با نام `nginx_role` ایجاد می‌کند که شامل دایرکتوری‌ها و فایل‌های پیش‌فرضی است که یک Role در Ansible نیاز دارد. ساختار آن چیزی شبیه به این خواهد بود:

```
nginx_role/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
├── tests/
│   └── test.yml
└── vars/
    └── main.yml
```

2. حالا باید داخل فایل‌های `tasks/main.yml`، `handlers/main.yml` و دیگر فایل‌ها، **تسک‌های مرتبط با نصب و پیکربندی Nginx** را تعریف کنی.

برای مثال، در فایل `tasks/main.yml` می‌توانی تسک‌های مربوط به نصب Nginx را اضافه کنی:

```yaml
---
# tasks/main.yml
- name: Install Nginx
  apt:
    name: nginx
    state: present
  become: true

- name: Start Nginx service
  service:
    name: nginx
    state: started
    enabled: true
```

بعد از اینکه این Role (`nginx_role`) را تعریف کردی، می‌توانی در Playbookهای مختلف از آن استفاده کنی.

### استفاده از Role در Playbook

حالا که Role `nginx_role` را ساختی و تسک‌های لازم را داخل آن تعریف کردی، می‌توانی در یک Playbook از آن استفاده کنی. برای این کار، فقط کافی است در Playbook خودت Role را فراخوانی کنی:

```yaml
---
- hosts: web_servers
  roles:
    - nginx_role
```

در اینجا، Ansible به صورت خودکار به دایرکتوری `nginx_role` می‌رود و تسک‌هایی که در آن تعریف شده را روی سرورهایی که در گروه `web_servers` هستند، اجرا می‌کند.

### جمع‌بندی:
- ابتدا Role را با `ansible-galaxy init` ایجاد می‌کنی.
- سپس تسک‌ها و تنظیمات لازم را در فایل‌های آن Role (مثل `tasks/main.yml`) تعریف می‌کنی.
- در نهایت، Role را در Playbook فراخوانی می‌کنی تا تسک‌ها روی سرورهایت اجرا شوند.


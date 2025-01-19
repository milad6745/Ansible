در زیر یک Playbook ساده برای **راه‌اندازی مجدد Nginx** آورده شده است. این Playbook بررسی می‌کند که سرویس Nginx نصب شده و در حال اجرا باشد و سپس آن را ری‌استارت می‌کند.

---

### Playbook برای ری‌استارت Nginx:

```yaml
---
- name: Restart Nginx Service
  hosts: web_servers  # گروهی از سرورها که در فایل اینونتوری تعریف شده‌اند
  become: yes         # اجرای دستورات با دسترسی ریشه
  tasks:
    - name: Ensure Nginx is installed
      apt:
        name: nginx
        state: present
      tags:
        - install

    - name: Restart Nginx service
      service:
        name: nginx
        state: restarted
      tags:
        - restart
```

---

### توضیحات:
1. **hosts**:
   - در اینجا `web_servers` به عنوان گروهی از سرورها در فایل `inventory` تعریف شده است.
2. **become**:
   - به Ansible اجازه می‌دهد دستورات را با دسترسی `sudo` اجرا کند.
3. **tasks**:
   - **Ensure Nginx is installed**:
     - با استفاده از ماژول `apt`، بررسی می‌کند که Nginx نصب شده باشد.
   - **Restart Nginx service**:
     - سرویس Nginx را با استفاده از ماژول `service` ری‌استارت می‌کند.

---

### اجرای Playbook:
1. فایل را ذخیره کنید، مثلاً با نام `restart_nginx.yml`.
2. Playbook را اجرا کنید:
   ```bash
   ansible-playbook -i inventory restart_nginx.yml
   ```

---

### اجرای فقط تسک‌های مشخص با استفاده از تگ‌ها:
- فقط بررسی نصب Nginx:
  ```bash
  ansible-playbook -i inventory restart_nginx.yml --tags install
  ```

- فقط ری‌استارت Nginx:
  ```bash
  ansible-playbook -i inventory restart_nginx.yml --tags restart
  ```

---

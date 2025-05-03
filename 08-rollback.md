
---

## 🎯 هدف:

اگر اجرای playbook در میانه‌ی کار fail شود، می‌خواهی **همه‌چیز به حالت قبل از اجرای انسیبل برگردد.**

---

## ❗ واقعیت مهم:

**انسیبل به‌صورت پیش‌فرض "transactional" نیست.**
یعنی playbook مثل دیتابیس transaction نداره که اگر شکست خورد، auto rollback کنه. ولی چند راه برای پیاده‌سازی چنین رفتاری داریم.

---

## ✅ راهکارهای پیاده‌سازی Rollback در انسیبل:

### 1. استفاده از **Block** همراه با **rescue و always**

```yaml
- name: اجرای عملیات با امکان بازگردانی
  hosts: all
  become: yes
  tasks:

    - name: نصب nginx با امکان rollback
      block:
        - name: گرفتن بکاپ از فایل پیکربندی اصلی
          copy:
            src: /etc/nginx/nginx.conf
            dest: /etc/nginx/nginx.conf.bak
            remote_src: yes

        - name: جایگزینی فایل جدید کانفیگ
          template:
            src: nginx.conf.j2
            dest: /etc/nginx/nginx.conf

        - name: ریستارت nginx
          service:
            name: nginx
            state: restarted

      rescue:
        - name: در صورت خطا، بازگرداندن فایل پشتیبان
          copy:
            src: /etc/nginx/nginx.conf.bak
            dest: /etc/nginx/nginx.conf
            remote_src: yes

        - name: ریستارت دوباره nginx بعد از rollback
          service:
            name: nginx
            state: restarted

      always:
        - name: حذف فایل بکاپ (اختیاری)
          file:
            path: /etc/nginx/nginx.conf.bak
            state: absent
```

✅ این ساختار تضمین می‌کند اگر task وسط block شکست بخورد، taskهای rescue اجرا شوند و حالت سیستم به قبل برگردد.

---

### 2. پیاده‌سازی دستی rollback با Play جداگانه

در playbookهای حساس می‌توانی دو play بنویسی:

* **اولی برای backup**
* **دومی برای اجرا**
* **سومی برای rollback در صورت نیاز (شرطی با `when`)**

---

### 3. استفاده از ابزارهای پیشرفته‌تر

اگر rollback خیلی مهمه:

* از **Ansible Tower / AWX** استفاده کن که قابلیت Job Isolation و Rollback بهتر داره.
* یا ابزارهایی مثل **Ansible Molecule** برای تست playbook قبل از اعمال در سرور اصلی.

---

### 4. استفاده از snapshot در VMها یا containerها

اگر روی VM یا Docker کار می‌کنی، قبل از اجرای playbook یک **snapshot** بگیر و در صورت خطا restore کن.

---

## نتیجه‌گیری:

* انسیبل به‌طور پیش‌فرض rollback اتوماتیک نداره.
* اما با استفاده از `block`, `rescue`, و مدیریت دقیق وضعیت، می‌تونی سیستم رو تا حد زیادی ایمن کنی.
* اگر rollback برایت حیاتی است، طراحی playbook باید دقیق، گام‌به‌گام و با کنترل‌های زیاد باشد.

می‌خواهی من یک playbook کامل برای نصب و rollback نرم‌افزار بنویسم؟

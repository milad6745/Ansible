# uri module
```
---
- name: Install Nginx on Ubuntu
  hosts: ubuntu
  become: yes
  gather_facts: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      package:
        name: nginx
        state: present

    - name: restart nginx
      service:
        name: nginx
        state: restarted
      notify: check nginx services



  handlers:
    - name: check nginx services
      uri:
        url: http://{{ ansible_default_ipv4.address }}
        status_code: 200
      register: result


    - name: Display status code
      debug:
        msg: "Status code is {{ result.status }}"
```
این کد یک فایل YAML به عنوان یک Ansible playbook است که مراحل نصب Nginx را بر روی یک سرور Ubuntu انجام می‌دهد. به تفصیل:

**نام Playbook**:
   - `Install Nginx on Ubuntu`: این Playbook به نصب Nginx بر روی یک سرور Ubuntu می‌پردازد.

**هاست‌ها و تنظیمات Playbook**:
   - `hosts: ubuntu`: این Playbook بر روی هاست‌هایی با نام ubuntu اجرا می‌شود. این نام باید در فایل hosts شما تعریف شده باشد.
   - `become: yes`: این مشخص می‌کند که باید با دسترسی مدیر (sudo) اجرا شود.
   - `gather_facts: yes`: این فرمان اطلاعات مفیدی در مورد هاست‌ها را جمع‌آوری می‌کند تا در Playbook قابل دسترسی باشد.

**مراحل (Tasks)**:
   - `Update apt cache`: با استفاده از ماژول apt، کش‌های پکیج‌ها را به‌روز می‌کند.
   - `Install Nginx`: با استفاده از ماژول package، پکیج Nginx را نصب می‌کند.
   - `Restart nginx`: با استفاده از ماژول service، سرویس Nginx را مجدداً راه‌اندازی می‌کند. در صورت تغییرات.

**مدیریت وضعیت‌ها (Handlers)**:
   - `check nginx services`: این یک handler است که با استفاده از ماژول uri، یک درخواست HTTP به آدرس `http://{{ ansible_default_ipv4.address }}` می‌فرستد تا کد وضعیت را بررسی کند. نتیجه در متغیر `result` ذخیره می‌شود.
   - `Display status code`: این handler یک پیام debug ارسال می‌کند که حاوی کد وضعیت است.

اگر هنوز سوالی دارید یا نیاز به اطلاعات بیشتری دارید، لطفاً بپرسید!

با کمال میل، یک مثال از Ansible playbook که از # import tasks

`import_tasks` استفاده می‌کند برای شما ارائه می‌دهم.

فرض کنید که شما یک پروژه Ansible دارید که باید چندین وظیفه را اجرا کند. می‌خواهیم این کارها را به چندین فایل تقسیم کنیم تا کد ما بهینه‌تر و مدیریت‌پذیرتر باشد. برای این کار از `import_tasks` استفاده می‌کنیم.

ساختار پوشه‌ها و فایل‌ها:

```
project/
├── playbook.yml
├── tasks/
│   ├── task1.yml
│   └── task2.yml
```

فایل `task1.yml`:

```yaml
---
- name: Task 1
  debug:
    msg: "This is task 1"
```

فایل `task2.yml`:

```yaml
---
- name: Task 2
  debug:
    msg: "This is task 2"
```

سپس فایل `playbook.yml`:

```yaml
---
- name: My Playbook with Import Tasks
  hosts: localhost
  gather_facts: no

  tasks:
    - name: Import Tasks
      import_tasks: tasks/*
```

در این مثال، ما یک پروژه ساده Ansible داریم که دو وظیفه را اجرا می‌کند. از `import_tasks` برای وارد کردن تمام فایل‌های موجود در پوشه `tasks` استفاده کردیم. بدین ترتیب، وظایف مرتبط با هر تسک در فایل‌های جداگانه ذخیره شده‌اند و در صورت نیاز می‌توانیم آنها را مدیریت کنیم.

با اجرای این پلی‌بوک، Ansible تمام وظایف موجود در پوشه `tasks` را وارد کرده و به ترتیب اجرا می‌کند.

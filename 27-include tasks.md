# include tasks

یک مثال از یک Ansible playbook که از `include_tasks` استفاده می‌کند برای شما ارائه می‌دهم.

فرض کنید که شما یک پروژه Ansible دارید که باید چندین وظیفه را اجرا کند. می‌خواهیم این کارها را به چندین فایل تقسیم کنیم تا کد ما بهینه‌تر و مدیریت‌پذیرتر باشد. برای این کار از `include_tasks` استفاده می‌کنیم.

اولین چیزی که شما باید برای اجرای این مثال داشته باشید، دسترسی به Ansible باشد.

حالا مثال را ببینید:

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
- name: My Playbook with Include Tasks
  hosts: localhost
  gather_facts: no

  tasks:
    - name: Include Task 1
      include_tasks: tasks/task1.yml

    - name: Include Task 2
      include_tasks: tasks/task2.yml
```

در این مثال، ما یک پروژه ساده Ansible داریم که دو وظیفه را اجرا می‌کند. از `include_tasks` برای اضافه کردن فایل‌های `task1.yml` و `task2.yml` به پلی‌بوک استفاده کردیم. بدین ترتیب، وظایف مرتبط با هر تسک در فایل‌های جداگانه ذخیره شده‌اند و در صورت نیاز می‌توانیم آنها را مدیریت کنیم.

با اجرای این پلی‌بوک، Ansible ابتدا `task1.yml` را اجرا کرده و سپس `task2.yml` را اجرا می‌کند.

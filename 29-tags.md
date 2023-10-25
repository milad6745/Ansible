با کمال میل، یک مثال از چگونگی استفاده از `ansible_tag` در یک Ansible playbook برای شما ارائه می‌دهم.

فرض کنید که شما یک پروژه Ansible دارید که باید چندین وظیفه را اجرا کند و می‌خواهید تنها برخی از وظایف در هنگام اجرا فعلی اجرا شوند. برای این کار از `ansible_tag` استفاده می‌کنیم.

ساختار پوشه‌ها و فایل‌ها:

```
project/
├── playbook.yml
└── tasks/
    ├── task1.yml
    └── task2.yml
```

فایل `task1.yml`:

```yaml
---
- name: Task 1
  debug:
    msg: "This is task 1"
  tags:
    - tag1
```

فایل `task2.yml`:

```yaml
---
- name: Task 2
  debug:
    msg: "This is task 2"
  tags:
    - tag2
```

سپس فایل `playbook.yml`:

```yaml
---
- name: My Tagged Playbook
  hosts: localhost
  gather_facts: no

  tasks:
    - name: Include Task 1 with tag1
      include_tasks: tasks/task1.yml
      tags:
        - tag1

    - name: Include Task 2 with tag2
      include_tasks: tasks/task2.yml
      tags:
        - tag2
```

در این مثال، ما یک پروژه ساده Ansible داریم که دو وظیفه را اجرا می‌کند. هر کدام از تسک‌ها با یک برچسب (tag) مشخص شده‌اند (`tag1` برای `task1.yml` و `tag2` برای `task2.yml`). 

حالا می‌توانیم فقط وظایفی که دارای برچسب مشخص هستند را اجرا کنیم. به عنوان مثال، اگر می‌خواهید تنها `task1.yml` اجرا شود، می‌توانید دستور زیر را اجرا کنید:

```bash
ansible-playbook playbook.yml --tags tag1
```

به این ترتیب، فقط وظیفه‌ای که دارای برچسب `tag1` است (در این حالت `task1.yml`) اجرا می‌شود.

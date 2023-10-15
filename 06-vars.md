# Vars

یک پلی‌بوک ساده با استفاده از متغیرها (vars) در Ansible می‌تواند به صورت زیر باشد:

1. **پلی‌بوک (`my_playbook.yml`)**:

```yaml
---
- name: My Ansible Playbook with Vars
  hosts: your_target_hosts
  vars:
    message: "Hello, World!"
    target_path: "/tmp/"
  tasks:
    - name: Create a file
      copy:
        content: "{{ message }}"
        dest: "{{ target_path }}/hello.txt"
```

در این پلی‌بوک:

- `name`: نام پلی‌بوک.
- `hosts`: میزبان‌هایی که این پلی‌بوک بر روی آن‌ها اجرا می‌شود.
- `vars`: تعریف متغیرها. در اینجا دو متغیر تعریف شده‌اند: `message` که متنی است که می‌خواهیم در فایل قرار دهیم و `target_path` که مسیر مقصد فایل است.
- `tasks`: وظایفی که این پلی‌بوک اجرا می‌کند. در اینجا یک وظیفه برای ایجاد یک فایل با محتویات مشخص شده تعریف شده است.

2. **اجرای پلی‌بوک**:

```bash
ansible-playbook -i your_inventory my_playbook.yml
```

در اینجا، `your_target_hosts` باید با میزبان‌های مورد نظر شما جایگزین شود و `your_inventory` باید به فایل مربوط به میزبان‌ها (inventory) شما اشاره کند.

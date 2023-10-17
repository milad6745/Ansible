# install package with ansible

میخواهیم در صورتی که distro ما centos باشد پکیج epel-release بر روی سرور مان نصب شود بنابر این فایل yaml زیر را مینویسیم .

```
---
- name: Example Playbook with if-elif-else
  hosts: all
  gather_facts: true

  tasks:
    - name: install epel
      yum:
        name: epel-release
        update_cache: yes
        state: latest
      when: ansible_distribution == 'centos'
```

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

میخواهیم در صورتی که distro اوبنتو بود بیاد و ابتدا کش رو آپدیت کنه و سئس سرویس nginx را نصب کند.
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
      apt:
        name: nginx
        state: present
      when: ansible_distribution == 'Ubuntu'
```

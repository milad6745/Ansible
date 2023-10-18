# install service and copy config files

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

    - name: copy index file
      template:
        src: index.html
        dest: /var/www/html/index.html
        mode: 0644


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
```

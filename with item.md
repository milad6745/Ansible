# with_item

این فایل YAML یک پلی بوک (playbook) Ansible است که برای اجرای یک سری وظایف روی میزبان‌هایی با توزیع‌های "Ubuntu" و "CentOS" طراحی شده است. اجرای این پلی بوک به این معناست که Ansible به تمامی میزبان‌هایی که دارای توزیع‌های مشخص شده هستند وصل می‌شود و وظایف را اجرا می‌کند.

در این پلی بوک، یک تسک به نام "copy file" تعریف شده است. این تسک با استفاده از ماژول `copy` اجرا می‌شود. وظیفه این تسک این است که فایلی به نام "test1" را به مسیر "/home/test" در هر یک از میزبان‌ها کپی کند.

ویژگی `with_items` برای اجرای تسک بر روی تمامی موارد در لیست مشخص شده (در اینجا 'Ubuntu' و 'CentOS') استفاده می‌شود. اگر توزیع Ansible با هر یک از این موارد برابر باشد، تسک اجرا خواهد شد.

مثلاً اگر میزبانی با توزیع "Ubuntu" یا "CentOS" داشته باشید، این پلی بوک فقط بر روی این میزبان‌ها اجرا می‌شود و فایل "test1" به مسیر "/home/test" کپی می‌شود.

```
---
- name: Run Docker container and wait for website to be available
  hosts: ubuntu, centos
  tasks:
    - name: copy file
      copy:
        content: welcome to my server
        dest: /etc/motd
      with_items: [ 'Ubuntu' , 'CentOS']
      when: ansible_distribution == item

```
 ## OR

```
---
- name: Run Docker container and wait for website to be available
  hosts: ubuntu, centos
  tasks:
    - name: copy file
      copy:
        content: welcome to my server
        dest: /etc/motd
      with_items:
        - CentOS
        - Ubuntu
      when: ansible_distribution == item

```

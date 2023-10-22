# command module


با استفاده از ماژول کامند میتوانیم بر روی سرور های متصل کامند دلخواه را اجرا کنیم .
- name: Run Docker container and wait for website to be available
  hosts: web4
  tasks:
    - name: Wait for website to be availabl
      command : /sbin/shutdown -h now
```

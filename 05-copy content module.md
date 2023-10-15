# copy content module
با اجرای این دستور content اعلام شده درون فایل مقصد کپی میشود .
```
---
-
  hosts: ubuntu
  user: root

  tasks:
    - name: copy file
      copy:
        content: welcome to my server
        dest: /home/welcome
```

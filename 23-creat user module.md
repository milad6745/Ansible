# Create user module

با این پلی بوک میتوان کاربر ایجاد کرد بر  اساس لیست .
```
---
- name: Run Docker container and wait for website to be available
  hosts: ubuntu, centos
  tasks:
    - name: copy file
      user:
        name: "{{ item }}"
      with_items:
        - milad
        - roham
        - mahyar
```
با این پلی بوک میتوان کاربران مورد نظر را حذف کرد .مقدار state را absent مکنیم .

```
---
- name: Run Docker container and wait for website to be available
  hosts: ubuntu, centos
  tasks:
    - name: copy file
      user:
        name: "{{ item }}"
        state: absent
      with_items:
        - milad
        - roham
        - mahyar
```

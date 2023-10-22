# pause module
این ماژول به منظور مکث کردن کار است و میتوان این ماژول را مثلا برای این استفاده نمود که کاری انجام شود و تا زمانی که انجام نشده است تسک بعدی pause باشد .

## simple Example
```
---
- name: Example Playbook with if-elif-else
  hosts: all
  gather_facts: true

  tasks:
    - name: ubuntu_infi
      pause:
        seconds: 10

```
## example prompt
در این مثال از ما میخواهد با استفاده از prompt برای ادامه اجرا شدن playbook کلید اینتر ر ا بزنیم :
```
---
- name: Example Playbook with if-elif-else
  hosts: all
  gather_facts: true

  tasks:
    - name: ubuntu_infi
      pause:
        prompt: please enter to continue
```

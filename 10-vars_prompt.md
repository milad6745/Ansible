# vars
## vars_prompt

این گزینه برای گرفتن خروجی از کاربر است .
گزینه private برای این است که اسم زده شده نشان داده شود یا خیر مثلا برای پسورد private را بله میکنیم

```
---
- name: Playbook with vars_prompt
  hosts: localhost
  gather_facts: false
  vars_prompt:
    - name: user_name
      prompt: "Enter your username"
      private: no
    - name: user_age
      prompt: "Enter your age"
      private: no

  tasks:
    - name: Display user information
      debug:
        msg: "Hello, {{ user_name }}. You are {{ user_age }} years old."
```

```
ansible-playbook test.yaml
enter username: milad
TASK [user info] ****************************************************************************
ok: [localhost] => {
    "msg": "hello milad"
}
```

## list var
در اینجا variable امان را بصورت لیست قرار دادیم
```
---
- name: Playbook with vars_prompt
  hosts: localhost

  vars:
    users:
      [milad,roham]
  tasks:
    - name: user info
      debug:
        msg : "hello {{users.0}}"

```

## var example
در اینجا ansible_user کاذبذی است که در انسیبل فرمان ها را اجرا میکند
```
---
- name: Playbook with vars_prompt
  hosts: localhost

  tasks:
    - name: user info
      debug:
        msg : "hello {{ansible_user}}"
```

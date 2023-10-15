# ansible filter
در اینجا در فایل ستاپ دنبال اطلاعات مموری هاست هایمان هستیم و دستور زیر را وارد میکنیم
```
# ansible all -m setup -a filter=ansible_mem*
web1 | SUCCESS => {
    "ansible_facts": {
        "ansible_memfree_mb": 1894,
        "ansible_memory_mb": {
            "nocache": {
                "free": 1963,
                "used": 24
            },
            "real": {
                "free": 1894,
                "total": 1987,
                "used": 93
            },
            "swap": {
                "cached": 0,
                "free": 673,
                "total": 1305,
                "used": 632
            }
        },
```

# ip address filter
حال ما دنبال آیپی آدرس ها میکردیم
ansible all -m setup

![image](https://github.com/milad6745/Ansible/assets/113288076/3ecd67e3-70fc-47c9-8db6-0bcf8ed856bc)

حالا با استفاده از فایل yaml میایم و آیپی ها را درمیاوریم

```
---
- name: Example of hostvars
  hosts: ubuntu
  tasks:
    - name: Display IP of web1
      debug:
        msg: "IP address of ubuntu server is {{ ansible_default_ipv4.address }}"
```
```
# ansible-playbook test.yaml

ok: [web1] => {
    "msg": "IP address of ubuntu server is 10.0.3.111"
}
ok: [web2] => {
    "msg": "IP address of ubuntu server is 10.0.3.251"
}
ok: [myubuntu] => {
    "msg": "IP address of ubuntu server is 192.168.72.18"
}
```

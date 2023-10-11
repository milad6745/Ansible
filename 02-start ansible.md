
# start ansible
create ansible.cfg and hosts
```
cat ansible.cfg
[defaults]
inventory = hosts
# برای غیر اجباری بودن اضافه کردن در هاست کی
host_key_cheking = false

 cat hosts
[all]
web1
web2
```

check
```
ansible all -m ping
web1 | SUCCESS => {
web2 | SUCCESS => {
```
## نشان دادن در یک خط
```
ansible '*' -o -m ping
web2 | SUCCESS => {"ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},"changed": false,"ping": "pong"}
web1 | SUCCESS => {"ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},"changed": false,"ping": "pong"}
```

# example
```
hosts
[ubuntu]
web1
web2

[centos]
web3
web4

ansible ubuntu -m ping
ansible centos -m ping
```

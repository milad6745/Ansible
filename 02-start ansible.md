
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

این ساختار نشان می‌دهد که دو میزبان با نام‌های web1 و web2 در گروه all قرار دارند و می‌توانید با اجرای playbookها به این دو میزبان متصل شوید.

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

## list host
```
ansible ubuntu --list-host
  hosts (2):
    web1
    web2
```
## use regex
```
ansible web* -m ping -o
web4 | UNREACHABLE!: Failed to connect to the host via ssh: ssh: Could not resolve hostname web4: Temporary failure in name resolution
web3 | UNREACHABLE!: Failed to connect to the host via ssh: ssh: Could not resolve hostname web3: Temporary failure in name resolution
web1 | SUCCESS => {"ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},"changed": false,"ping": "pong"}
web2 | SUCCESS => {"ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},"changed": false,"ping": "pong"}
```
## use root user for run commnad
```
cat hosts
[ubuntu]
web1 ansible_user=root
web2 ansible_user=root

ansible web* -m ping -o
web2 | SUCCESS 
web1 | SUCCESS 
```
## run a command
```
ansible all -m command -a 'id' -o
web1 | CHANGED | rc=0 | (stdout) uid=0(root) gid=0(root) groups=0(root)
web2 | CHANGED | rc=0 | (stdout) uid=0(root) gid=0(root) groups=0(root)
```

## ansible become pass دادن پسورد به فایل کانفبگ
```
[ubuntu]
web1 ansible_user=root ansible_become=true ansible_become_pass=00
```
## عوض کردن پورت ssh
```
cat hosts
[ubuntu]
web1:9595 ansible_user=root
web2 ansible_user=root
```
## local connection بر روی هاست داخلی
```
cat hosts
[ubuntu]
web1 ansible_user=root
web2 ansible_user=root
myubuntu ansible_connection=local
```

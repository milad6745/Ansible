# Ansible configuration

## check ping to host
```
ansible -i,web1,web2 all -m ping
web2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
web1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
## ansible config file 1
```
ansible --version
ansible 2.9.6
  config file = /etc/ansible/ansible.cfg
```
## ansible file config 2
```
ساخت یک فایل در این مسیر حال میبینیم که مسیر فایل کانفیگ با توجه به اینکه این فایل اولویت بالاتری دارد 
touch /root/.ansible/ansible.cfg
ansible --version
ansible 2.9.6
  config file = /root/.ansible/ansible.cfg
```
## ansible file config 3
حالا در دایرکتوری که هستیم یک ansible.cfg درست میکنیم . سپس مشاهده میکنیم که فایل کانفیگ میشود همین فایلی که ما درست کردیم
```
touch ansible.cfg
root@milad-virtual-machine:/# ansible --version
ansible 2.9.6
  config file = /ansible.cfg
```
## ansible file config hight priority
```
export ANSIBLE_CONFIG=/home/milad/ans.cfg

root@milad-virtual-machine:/# touch /home/milad/ans.cfg
ansible --version
ansible 2.9.6
  config file = /home/milad/ans.cfg
```

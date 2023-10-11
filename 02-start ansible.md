
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

# Ansible modules

## َAnsible Setup
```
ansible web1 -m setup
web1 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "10.0.3.111"
        ],
        "ansible_all_ipv6_addresses": [
            "fe80::216:3eff:fe32:1d9e"
        ],
        "ansible_apparmor": {
            "status": "disabled"
        },
        "ansible_architecture": "x86_64",
        "ansible_bios_date": "09/21/2015",
        "ansible_bios_version": "6.00",
        "ansible_cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-5.4.0-42-generic",
            "quiet": true,
            "ro": true,
            "root": "UUID=28d13584-45c6-42a3-b330-025e93b58266",
            "splash": true
.
.
.
.

```
## file module ساخت فایل در مسیر اعلام شده با ماژول فایل 
```
ansible all -m file -a "path=/root/test state=touch"
web1 | CHANGED => {
myubuntu | CHANGED => {
web2 | CHANGED => {
```
## Ansible color
![image](https://github.com/milad6745/Ansible/assets/113288076/62b963a5-2b1a-4973-824e-2439a418af91)


## Ansible file module with permision ایجاد فایل با اعلام پرمیژن

```
ansible all -m file -a "path=/root/test1 state=touch mode=777"
web1 | CHANGED => {
myubuntu | CHANGED => {
web2 | CHANGED => {
```

## Copy module


در Ansible، دستور معادل با استفاده از ماژول `copy` در خط فرمان به صورت زیر است:

```bash
ansible your_target_hosts -m copy -a "src=/path/to/local/file.txt dest=/path/to/remote/"
```

توضیحات:

- `your_target_hosts`: میزبان‌هایی که می‌خواهید دستور را اجرا کنید.
- `copy`: نام ماژول که در این حالت `copy` است.
- `src`: مسیر فایل محلی که می‌خواهید کپی کنید.
- `dest`: مسیر مقصد در سرور مورد نظر که فایل به آنجا کپی می‌شود.

مثال:

```bash
ansible web_servers -m copy -a "src=/path/to/local/index.html dest=/var/www/html/"
```

در این مثال، دستور `copy` به ماشین‌های میزبان `web_servers` فرستاده می‌شود تا فایل `index.html` از مسیر محلی `/path/to/local/` به مسیر `/var/www/html/` در سرورهای مقصد کپی شود.

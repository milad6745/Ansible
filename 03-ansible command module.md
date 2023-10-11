# ansible command module
## check hostname

```
ansible all -m command -a "hostname"
web1 | CHANGED | rc=0 >>
web1

web2 | CHANGED | rc=0 >>
web2

myubuntu | CHANGED | rc=0 >>
myubuntu
```

### install ansbile on ansiblehost

```
apt install ansbile
apt install ssh
apt install python 2.7
```



### install virtual lxc

```
apt-get install lxc
sudo lxc-create -t download -n web1
ubuntu
xenial
amd64
```



### run a virtual host 

```bash
#Start a machin by name web1
lxc-start web1

#view virtual machine
lxc-ls -l

#connect ro web1
lxc-attach web1

#create user on web1 machine
passwd ubuntu

#install python and ssh on my agent
apt install ssh pyrhon2.7
```

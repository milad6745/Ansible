# when
در اینجا میتوانیم در ansible هاست هایمان ببینیم چه هاست هایی داریم و در نهایت بیاییم و برایش if بنویسیسم
```
ansible all -m setup | grep dist
        "ansible_distribution": "Ubuntu",
        "ansible_distribution": "Ubuntu",
```

در اینجا گفتم اگر ansible_distribution برابر centos بود بیا و فایل را کپی کن


```
---
- name: Copy file on Ubuntu
  hosts: ubuntu
  user: root
  vars:
    dest: "/home/welcome"
    src: "test10"

  tasks:
    - name: copy file
      copy:
        src: "{{ src }}"
        dest: "{{ dest }}"
      notify:
        - display result
      when: ansible_distribution == "centos"


  handlers:
    - name: display result
      debug:
        msg: "File was not found"

```
همانگ
ونه که مشاهده میشود بر روی هاست های ubuntu این فایل skip میشود
skipping: [web1]
skipping: [web2]


## Example if and elif
```
---
- name: Example Playbook with if-elif-else
  hosts: all
  gather_facts: true

  tasks:
    - name: Check hostname
      debug:
        msg: 
          - "The hostname is web1"
        when: ansible_hostname == 'web1'

    - name: Check hostname
      debug:
        msg: 
          - "The hostname is web2"
        when: ansible_hostname == 'web2'

    - name: Check hostname
      debug:
        msg: 
          - "The hostname is neither web1 nor web2"
        when: ansible_hostname != 'web1' and ansible_hostname != 'web2'
```

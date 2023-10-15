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

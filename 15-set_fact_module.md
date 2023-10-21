# set fact module

ست کردن قانونی که بعدن میخایم ازش استفاده کنیم.
```
---
- name: Install Nginx on Ubuntu
  hosts: ubuntu, centos
  become: yes
  gather_facts: yes

  tasks:
    - name: set Fact
      set_fact:
        our_fact: Ansible rock!
        ansible_distribution: "{{ ansible_distribution | upper }}"
    - name: show fact
      debug:
        msg: "{{ ansible_distribution }}"
```



این یک فایل YAML به عنوان یک playbook Ansible است که دو مرحله (task) دارد:

**نام Playbook**:`Install Nginx on Ubuntu`: این Playbook به نصب Nginx بر روی هاست‌هایی با سیستم عامل‌های Ubuntu و CentOS می‌پردازد.

**هاست‌ها و تنظیمات Playbook**:

`hosts: ubuntu, centos`: 

این Playbook بر روی هاست‌هایی با نام ubuntu و centos اجرا می‌شود. این نام‌ها باید در فایل hosts شما تعریف شده باشند.

`become: yes`: 

این مشخص می‌کند که باید با دسترسی مدیر (sudo) اجرا شود.

`gather_facts: yes`:

این فرمان اطلاعات مفیدی در مورد هاست‌ها را جمع‌آوری می‌کند تا در Playbook قابل دسترسی باشد.

**مراحل (Tasks)**:

`set Fact`:

این مرحله از ماژول `set_fact` استفاده می‌کند تا متغیرهای فرضی به نام `our_fact` و `ansible_distribution` را تنظیم کند.

`our_fact: Ansible rock!`: 

مقدار متغیر `our_fact` به "Ansible rock!" تنظیم می‌شود.

`ansible_distribution: "{{ ansible_distribution | upper }}"`: 

متغیر `ansible_distribution` از توزیع فعلی Ansible با استفاده از فیلتر `upper` (برای تبدیل به حروف بزرگ) تنظیم می‌شود.

`show fact`:

با استفاده از ماژول `debug`، متغیر `ansible_distribution` را نمایش می‌دهد.


این Playbook یک متغیر به نام `our_fact` با مقدار "Ansible rock!" ایجاد می‌کند و همچنین مقدار `ansible_distribution` را به شکل بزرگ تنظیم می‌کند. در نهایت، مقدار `ansible_distribution` (که حالا با حروف بزرگ نمایش داده می‌شود) را با استفاده از ماژول `debug` نمایش می‌دهد.

## Example
```
---
- name: Example Playbook with if-elif-else
  hosts: all
  gather_facts: true

  tasks:
    - name: ubuntu_infi
      set_fact:
        web_port: 8080
        web_path: /usr/local/nginx
        web_service: nginx
      when: ansible_distribution == 'Ubuntu'

    - name: Centos_infi
      set_fact:
        web_port: 8080
        web_path: /etc/apache2
        web_service: apache
      when: ansible_distribution == 'CentOS'

    - name: view informatio
      debug:
        msg: "web_port:{{ web_port }}  web_path:{{ web_path}}  web_service:{{ web_service }}"
```
```
TASK [view informatio] ***********************************************************
ok: [web2] => {
    "msg": "web_port:8080  web_path:/usr/local/nginx  web_service:nginx"
}
ok: [web1] => {
    "msg": "web_port:8080  web_path:/usr/local/nginx  web_service:nginx"
}
ok: [myubuntu] => {
    "msg": "web_port:8080  web_path:/usr/local/nginx  web_service:nginx"
}
ok: [web4] => {
    "msg": "web_port:8080  web_path:/etc/apache2  web_service:apache"
}
```

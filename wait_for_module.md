# wait for

در اینجا یک کانتینر اجرا میشود و پورت 80 را بر روی لوکال هاست باز میکند . و سپس منتظر میماند که سرویس پورت 80 باز شود

```
---
- name: Run Docker container and wait for website to be available
  hosts: your_target_host
  tasks:
    - name: Run Docker container
      docker_container:
        name: my_web_container
        image: my_web_image
        ports:
          - "80:80"
      register: docker_result

    - name: Wait for website to be available
      wait_for:
        host: localhost
        port: 80
        timeout: 60
      become: no
      ignore_errors: yes
```

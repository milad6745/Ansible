# register

در Ansible، register یک کلمه کلیدی استفاده می‌شود تا نتیجه یک کار را در یک متغیر ذخیره کند. این به شما اجازه می‌دهد تا بتوانید نتیجه عملیات را در مراحل بعدی اجرا استفاده کنید.
```
---
- name: Run Docker container and wait for website to be available
  hosts: web4
  tasks:
    - name: Wait for website to be availabl
      command : hostname -s
      register: hostname




    - name: print hostname
      debug:
        var : hostname
```
```
TASK [print hostname] *********************************************************************************
ok: [web4] => {
    "hostname": {
        "changed": true,
        "cmd": [
            "hostname",
            "-s"
        ],
        "delta": "0:00:00.004792",
        "end": "2023-10-22 14:14:40.163955",
        "failed": false,
        "rc": 0,
        "start": "2023-10-22 14:14:40.159163",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "web4",
        "stdout_lines": [
            "web4"
        ]
    }
}
```

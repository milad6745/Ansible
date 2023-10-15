# ansible delete file
یک پلی‌بوک ساده برای حذف یک فایل و ارسال یک اعلان (notification) می‌تواند به صورت زیر باشد:

```yaml
---
- name: Delete a file and notify
  hosts: your_target_hosts
  tasks:
    - name: Delete file
      file:
        path: /path/to/your/file.txt
        state: absent
      notify:
        - send notification

  handlers:
    - name: send notification
      debug:
        msg: "The file has been deleted successfully."
```

توضیحات:

- `name`: نام پلی‌بوک.
- `hosts`: میزبان‌هایی که این پلی‌بوک بر روی آن‌ها اجرا می‌شود.
- در وظیفه `Delete file` از ماژول `file` استفاده می‌شود تا فایل مورد نظر حذف شود (`state: absent`).
- `notify`: بلافاصله پس از حذف فایل، هندلر `send notification` فراخوانی می‌شود.
- در هندلر `send notification` از ماژول `debug` برای ارسال پیام به عنوان اعلان استفاده می‌شود.

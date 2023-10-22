# fetch module

ماژول `fetch` در Ansible برای دریافت فایل‌ها از میزبان‌ها به میزبان کنترل‌کننده (که دارای Ansible است) استفاده می‌شود. این ماژول از پروتکل SSH استفاده می‌کند تا فایل‌ها را از میزبان‌ها به کنترل‌کننده منتقل کند.

این کار معمولاً برای گرفتن فایل‌های لازم برای بررسی‌ها و تحلیل‌ها از میزبان‌ها استفاده می‌شود.

مثال:

```yaml
---
- name: Fetch a file from remote host
  hosts: your_remote_host
  tasks:
    - name: Fetch file
      fetch:
        src: /path/to/remote/file.txt
        dest: /path/to/local/directory/
```

در این مثال:

`your_remote_host` باید با میزبان مورد نظر خود جایگزین شود.

ماژول `fetch` با دو پارامتر اصلی عمل می‌کند:

   - `src`: مسیر فایل در میزبان مورد نظر.
   - `dest`: مسیر مقصد در میزبان کنترل‌کننده (میزبانی که Ansible روی آن نصب شده است).

   در این مثال، فایل `/path/to/remote/file.txt` از میزبان مورد نظر گرفته شده و در مسیر `/path/to/local/directory/` در میزبان کنترل‌کننده ذخیره می‌شود.

   **توجه کنید که مسیر مقصد باید پایانی باشد و نام فایل اصلی باید در آن ذکر نشود.**

با اجرای این پلی‌بوک، فایل مورد نظر از میزبان مورد نظر گرفته شده و در میزبان کنترل‌کننده ذخیره می‌شود.
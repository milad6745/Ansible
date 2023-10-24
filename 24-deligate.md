## deligate
 فرض کنید می‌خواهید یک فایل را از میزبان A به میزبان B منتقل کنید و سپس آن فایل را در میزبان B اجرا کنید. این کار را می‌توان با استفاده از تسک‌های مرتبط انجام داد. در این مثال، ما از ماژول `copy` برای منتقل فایل استفاده می‌کنیم و سپس تسک دیگری را بر روی میزبان B اجرا می‌کنیم:

```yaml
---
- name: Copy file from Host A to Host B and execute it
  hosts: hostA
  tasks:
    - name: Transfer file
      copy:
        src: /path/to/source/file
        dest: /path/to/destination/file
      delegate_to: hostB

    - name: Execute file on Host B
      command: /path/to/destination/file
      delegate_to: hostB
```

در این مثال، ابتدا تسک "Transfer file" بر روی میزبان A اجرا می‌شود و فایل از میزبان A به میزبان B منتقل می‌شود. سپس تسک "Execute file on Host B" بر روی میزبان B اجرا می‌شود.

توجه داشته باشید که شما باید دسترسی ssh به هر دو میزبان داشته باشید و مسیر‌های فایل‌ها درست باشند.

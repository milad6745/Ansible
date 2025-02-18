در Ansible، دستورات **ad-hoc** به شما این امکان را می‌دهند که بدون نیاز به نوشتن و اجرای یک playbook کامل، دستورات ساده‌ای را به سرعت و برای انجام کارهای فوری یا آزمایشی اجرا کنید. ad-hoc برای انجام وظایف سریع مانند بررسی وضعیت سیستم، راه‌اندازی یک سرویس، یا اجرای دستوراتی که نیازی به خودکارسازی کامل ندارند، بسیار مفید است. 

به عنوان مثال، دستور زیر از طریق Ansible به همه‌ی سرورها متصل می‌شود و وضعیت درایوهای دیسک را نمایش می‌دهد:

```bash
ansible all -m shell -a "df -h"
```

در این دستور:

- `all` به Ansible می‌گوید که دستور روی همه‌ی میزبان‌های تعریف‌شده در `inventory` اجرا شود.
- `-m` مشخص می‌کند که کدام ماژول استفاده شود؛ در اینجا از ماژول `shell` برای اجرای یک دستور خط فرمان استفاده می‌کنیم.
- `-a` آرگومان‌های مورد نیاز ماژول را مشخص می‌کند، که در اینجا دستور `df -h` برای مشاهده وضعیت دیسک است.

مثال دیگری برای بررسی دسترسی و ارتباط با همه سرورها:

```bash
ansible all -m ping
```

این دستور از ماژول `ping` استفاده می‌کند و بررسی می‌کند که آیا سرورها در دسترس هستند یا خیر.

### موارد کاربرد Ansible ad-hoc
1. **مانیتورینگ سریع**: بررسی وضعیت سرویس‌ها و منابع سیستم.
2. **مدیریت و پیکربندی ساده**: اجرای دستورات مدیریتی و انجام تغییرات کوچک بدون نیاز به playbook.
3. **عیب‌یابی و آزمایش دستورات**: بررسی و تست دستورات پیش از تبدیل آنها به playbook.


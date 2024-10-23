ماژول `debug` در Ansible برای نمایش پیام‌ها و متغیرها در خروجی اجرای Playbook استفاده می‌شود. این ماژول به شما کمک می‌کند تا وضعیت متغیرها یا پیام‌های خاص را در طول اجرای Playbook مشاهده و دیباگ کنید. `debug` یکی از ابزارهای مفید برای رفع اشکال و بررسی روند اجرای وظایف (tasks) در Ansible است.

### موارد استفاده از Ansible Debug:
1. **نمایش متغیرها**: می‌توانید مقدار یک متغیر را در زمان اجرای Playbook ببینید.
2. **نمایش پیام‌های سفارشی**: می‌توانید پیام‌های خاصی را در حین اجرای Playbook نمایش دهید.
3. **دیباگ‌کردن شرط‌ها یا وظایف پیچیده**: با استفاده از `debug` می‌توانید روند اجرای بخش‌های پیچیده را ردیابی کنید.

### نحوه استفاده از Ansible Debug:

#### 1. نمایش پیام ساده
برای نمایش یک پیام ساده می‌توانید از ماژول `debug` استفاده کنید:

```yaml
---
- hosts: localhost
  tasks:
    - name: Show a simple debug message
      debug:
        msg: "This is a debug message."
```

در این مثال، پیام `"This is a debug message."` در خروجی نمایش داده می‌شود.

#### 2. نمایش مقدار متغیرها
برای نمایش مقدار یک متغیر در طول اجرای Playbook، می‌توانید به این شکل از `debug` استفاده کنید:

```yaml
---
- hosts: localhost
  vars:
    my_variable: "Hello Ansible"
  tasks:
    - name: Show the value of a variable
      debug:
        var: my_variable
```

در اینجا، مقدار متغیر `my_variable` نمایش داده می‌شود که برابر است با `"Hello Ansible"`.

#### 3. نمایش چندین متغیر
می‌توانید چندین متغیر را همزمان با استفاده از `debug` نمایش دهید:

```yaml
---
- hosts: localhost
  vars:
    var1: "First variable"
    var2: "Second variable"
  tasks:
    - name: Show multiple variables
      debug:
        msg: "var1: {{ var1 }}, var2: {{ var2 }}"
```

این مثال پیام را به صورت ترکیبی از چند متغیر نمایش می‌دهد: `"var1: First variable, var2: Second variable"`.

#### 4. دیباگ کردن با شرط‌ها (when)
می‌توانید از `debug` برای نمایش پیام‌ها یا متغیرها به صورت شرطی استفاده کنید:

```yaml
---
- hosts: localhost
  vars:
    my_variable: 42
  tasks:
    - name: Show debug message only if condition is met
      debug:
        msg: "The value is greater than 40"
      when: my_variable > 40
```

در این مثال، پیام فقط زمانی نمایش داده می‌شود که مقدار `my_variable` بیشتر از 40 باشد.

#### 5. استفاده از `verbosity`
ماژول `debug` می‌تواند فقط زمانی که سطح verbosity بالاتر باشد، خروجی دهد. این کار برای زمانی مفید است که نمی‌خواهید در خروجی معمولی پیام‌های دیباگ زیادی نمایش داده شود، مگر اینکه به صورت مشخص سطح verbosity بالا تنظیم شده باشد.

```yaml
---
- hosts: localhost
  tasks:
    - name: Debug message with verbosity
      debug:
        msg: "This message only shows with higher verbosity"
        verbosity: 2
```

در اینجا، پیام فقط زمانی نمایش داده می‌شود که Playbook با سطح verbosity 2 یا بالاتر اجرا شود:

```bash
ansible-playbook playbook.yml -v
```

#### 6. نمایش محتویات پیچیده‌تر (لیست‌ها یا دیکشنری‌ها)
اگر می‌خواهید محتویات پیچیده‌تری مثل لیست‌ها یا دیکشنری‌ها را نمایش دهید، `debug` به صورت خودکار آن‌ها را به شکل خوانایی نمایش می‌دهد:

```yaml
---
- hosts: localhost
  vars:
    my_list:
      - item1
      - item2
      - item3
  tasks:
    - name: Show the content of a list
      debug:
        var: my_list
```

این خروجی به شکل یک لیست ساختاریافته نمایش داده خواهد شد.

### جمع‌بندی:
- ماژول `debug` در Ansible برای نمایش پیام‌ها و متغیرها در خروجی اجرا استفاده می‌شود.
- می‌توان از آن برای دیباگ کردن متغیرها، نمایش پیام‌های سفارشی و ردیابی روند اجرای Playbook استفاده کرد.
- با استفاده از `verbosity` می‌توان پیام‌ها را به صورت کنترل شده و در شرایط خاص نمایش داد.

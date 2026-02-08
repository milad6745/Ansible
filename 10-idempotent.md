ایدمپوتنسی (Idempotency) توی **Ansible** یعنی:

> 🔁 **اگه یه Playbook رو چند بار اجرا کنی، بعد از بار اول دیگه چیزی رو بی‌دلیل تغییر نده**
> سیستم همیشه به همون state مطلوبی که گفتی برسه، نه بیشتر نه کمتر.

---

### با یه مثال خیلی ساده

فرض کن گفتی:

> «nginx باید نصب باشه»

```yaml
- name: Install nginx
  apt:
    name: nginx
    state: present
```

🔹 بار اول اجرا → nginx نصب میشه
🔹 بار دوم، سوم، صدم → Ansible میگه:
`ok` ✔️ (چون nginx از قبل نصبه، کاری نمی‌کنه)

این یعنی **idempotent** 👌

---

### مثال غیر idempotent (بد!)

```yaml
- name: Add line to file
  shell: echo "test" >> /tmp/a.txt
```

هر بار اجرا:

```
test
test
test
test
```

❌ این idempotent نیست، چون هر بار سیستم رو تغییر میده.

---

### نسخه درست (idempotent)

```yaml
- name: Add line once
  lineinfile:
    path: /tmp/a.txt
    line: "test"
```

✔️ فقط اگه خط وجود نداشته باشه اضافه میشه.

---

### چرا idempotency مهمه؟

چون:

* می‌تونی playbook رو **بارها با خیال راحت اجرا کنی**
* مناسب **CI/CD** و automation
* خرابکاری و side effect نداره
* دقیقاً فلسفه‌ی **Infrastructure as Code** ـه

---

### ماژول‌های Ansible و idempotency

اکثر ماژول‌های اصلی انسیبل idempotent هستن:

* `apt` / `yum`
* `service`
* `user`
* `file`
* `template`
* `copy`

⚠️ بیشترین جایی که idempotency می‌شکنه:

* `shell`
* `command`
  (مگر خودت کنترلش کنی)

---

### یه تست ساده

Playbook رو دوبار اجرا کن:

* اگه بار دوم همه چی `ok` بود → کارت درسته ✅
* اگه هنوز `changed` می‌بینی → یه جای کار idempotent نیست ⚠️

---

اگه دوست داری، می‌تونم:

* مثال idempotency تو **Ansible + Kubernetes**
* یا چک کردن idempotency با `--check`
* یا اینکه بگم چطور توی **role**‌ها رعایتش کنی

کدومو می‌خوای؟ 😄

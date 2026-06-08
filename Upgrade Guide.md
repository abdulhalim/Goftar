# Goftar v1.0.2 — Upgrade Guide / راهنمای ارتقا

---

## English — Upgrade from v1.0.1-beta to v1.0.2-beta

### Overview

This guide will walk you through upgrading your existing Goftar v1.0.1-beta installation to v1.0.2-beta. The upgrade process is straightforward and includes a built-in migration script that handles all database changes automatically.

### What Changed in the Database

The v1.0.2 release introduces the following database modifications:

**New Tables (8):**
| Table | Purpose |
|-------|---------|
| `polls` | Poll metadata linked to topics |
| `poll_options` | Poll choices with vote counts |
| `poll_votes` | User votes per poll option |
| `static_pages` | Custom CMS pages |
| `admin_notes` | Internal staff notes/tickets |
| `hidden_contents` | Tracks unlocked gated content per user/post |
| `nsfw_verifications` | Age verification records |
| `user_uploads_quota` | Per-user upload storage quotas |

**New Columns on Existing Tables:**
| Table | New Columns | Default |
|-------|-------------|---------|
| `users` | `email` | NULL |
| `categories` | `color` | NULL |
| `categories` | `border_position` | `'left'` |
| `categories` | `image` | NULL |

**New Settings (added to `settings` table):**
- Email/SMTP: `email_enabled`, `email_from_address`, `email_from_name`, `email_smtp_host`, `email_smtp_port`, `email_smtp_username`, `email_smtp_password`, `email_smtp_encryption`
- Upload: `upload_allowed_categories`, `upload_custom_extensions`, `upload_max_size_mb`, `upload_max_total_per_user`, `upload_max_per_day`, `upload_scan_malware`, `upload_enable_public_list`, `upload_require_approval`
- Notifications: `enable_reply_notifications`, `enable_mention_notifications`, `notification_check_interval`

**New Permissions (added to `permissions` table):**
- `view_admin_notes`, `create_admin_notes`, `edit_admin_notes`, `delete_admin_notes`
- `manage_uploads`, `view_uploads`
- `manage_notifications`

**New Indexes:** Multiple new indexes for performance optimization on polls, static pages, admin notes, uploads, and NSFW tables.

> **Good news:** You do NOT need to run any SQL commands manually. The migration script handles everything.

---

### Step-by-Step Upgrade Instructions

#### Step 1 — Backup Your Current Installation

Before doing anything, make a full backup of your existing Goftar files and database:

```bash
# Create a backup directory
mkdir -p ~/goftar-backup

# Copy all files
cp -r /path/to/your/goftar/* ~/goftar-backup/

# Copy the database file (IMPORTANT!)
cp /path/to/your/goftar/storage/goftar.sqlite ~/goftar-backup/goftar-backup.sqlite
```

> If your database is in a different location, check `storage/config/database.php` for the actual path.

#### Step 2 — Upload New Files

Download the v1.0.2 release from GitHub and upload all files to your server, **overwriting** the existing files:

```bash
# Via Git
cd /path/to/your/goftar
git pull origin main

# Or upload the ZIP contents via FTP/SFTP
# Make sure ALL files are overwritten
```

**Important:** Do NOT delete the `storage/` directory. Your database and uploaded files are there.

#### Step 3 — Set Permissions

Make sure permissions are correct:

```bash
chmod -R 755 storage/
chmod -R 755 config/
```

#### Step 4 — Run the Migration Script

This is the key step. The migration script will:

1. Add the `email` column to the `users` table (if missing)
2. Add email/SMTP settings (if missing)
3. Add `color`, `border_position`, `image` columns to `categories` table (if missing)
4. Create all new tables (`polls`, `poll_options`, `poll_votes`, `static_pages`, `admin_notes`, `hidden_contents`, `nsfw_verifications`, `user_uploads_quota`)
5. Create all new indexes
6. Insert new permissions and settings
7. Verify all existing data is intact

**How to run:**

1. Log in to your Goftar site as **administrator**
2. Open the following URL in your browser:

```
https://your-domain.com/install/migrate.php
```

3. You will see a results page showing each migration step with a green checkmark (success) or red X (failure)
4. If all steps show green, the migration is complete
5. If any step shows red, check the error message and contact support

> The migration script is **idempotent** — running it multiple times is safe. It checks for existing columns/tables before making changes.

#### Step 5 — Verify the Upgrade

After migration:

1. Go to **Admin Panel** > **About** — you should see version `1.0.2 beta`
2. Go to **Admin Panel** > **Settings** — check the new tabs: Upload, Email
3. Go to **Admin Panel** > **Polls** — verify the polls management page loads
4. Go to **Admin Panel** > **Static Pages** — verify the CMS page loads
5. Go to **Admin Panel** > **Notes** — verify the admin notes page loads
6. Go to **Admin Panel** > **Statistics** — verify the charts page loads
7. Create a new topic and verify the editor shows new buttons (poll, gallery, gated content)

#### Step 6 — Clean Up (Optional)

After confirming everything works, you can safely remove the install directory:

```bash
rm -rf /path/to/your/goftar/install/
```

Or if you prefer to keep it, the `.htaccess` file inside the install directory will block direct access.

---

### Troubleshooting

| Problem | Solution |
|---------|---------|
| "Access denied" on migrate.php | You must be logged in as admin before running the script |
| "Database not found" | Check `storage/config/database.php` for the correct database path |
| Blank page after file upload | Check that PHP 7.4+ is installed and `sqlite3` extension is enabled |
| Missing new settings | Run the migration script again — it's safe to re-run |
| Theme looks broken | Clear your browser cache (Ctrl+Shift+R) |
| Poll/chart features not working | Make sure `vendor/js/chart.umd.min.js` was uploaded |

---

<br>
<br>

---

# فارسی — ارتقا از نسخه v1.0.1-beta به v1.0.2-beta

### خلاصه

این راهنما شما را طی مراحل ارتقای گفتار از نسخه v1.0.1-beta به v1.0.2-beta راهنمایی می‌کند. فرآیند ارتقا ساده است و شامل یک اسکریپت مایگریشن داخلی است که تمام تغییرات دیتابیس را به صورت خودکار انجام می‌دهد.

### چه چیزی در دیتابیس تغییر کرد

نسخه v1.0.2 تغییرات زیر را در دیتابیس ایجاد می‌کند:

**جداول جدید (۸ جدول):**
| جدول | کاربرد |
|------|--------|
| `polls` | اطلاعات نظرسنجی متصل به موضوعات |
| `poll_options` | گزینه‌های نظرسنجی با تعداد آرا |
| `poll_votes` | آرای کاربران برای هر گزینه |
| `static_pages` | صفحات سفارشی CMS |
| `admin_notes` | یادداشت‌ها و تیکت‌های داخلی پرسنل |
| `hidden_contents` | ردیابی محتوای شرطی بازشده برای هر کاربر/پست |
| `nsfw_verifications` | رکوردهای تأیید سن |
| `user_uploads_quota` | سهمیه ذخیره‌سازی آپلود هر کاربر |

**ستون‌های جدید در جداول موجود:**
| جدول | ستون‌های جدید | مقدار پیش‌فرض |
|------|---------------|----------------|
| `users` | `email` | NULL |
| `categories` | `color` | NULL |
| `categories` | `border_position` | `'left'` |
| `categories` | `image` | NULL |

**تنظیمات جدید (اضافه‌شده به جدول `settings`):**
- ایمیل/SMTP: `email_enabled`, `email_from_address`, `email_from_name`, `email_smtp_host`, `email_smtp_port`, `email_smtp_username`, `email_smtp_password`, `email_smtp_encryption`
- آپلود: `upload_allowed_categories`, `upload_custom_extensions`, `upload_max_size_mb`, `upload_max_total_per_user`, `upload_max_per_day`, `upload_scan_malware`, `upload_enable_public_list`, `upload_require_approval`
- اعلان‌ها: `enable_reply_notifications`, `enable_mention_notifications`, `notification_check_interval`

**مجوزهای جدید (اضافه‌شده به جدول `permissions`):**
- `view_admin_notes`, `create_admin_notes`, `edit_admin_notes`, `delete_admin_notes`
- `manage_uploads`, `view_uploads`
- `manage_notifications`

**ایندکس‌های جدید:** چندین ایندکس جدید برای بهینه‌سازی عملکرد روی جداول نظرسنجی، صفحات ایستا، یادداشت‌های مدیریتی، آپلودها و NSFW.

> **خبر خوب:** شما نیازی به اجرای دستی هیچ دستور SQL ندارید. اسکریپت مایگریشن همه چیز را به صورت خودکار انجام می‌دهد.

---

### مراحل گام‌به‌گام ارتقا

#### مرحله ۱ — پشتیبان‌گیری از نصب فعلی

قبل از هر کاری، یک پشتیبان کامل از فایل‌ها و دیتابیس گفتار خود بگیرید:

```bash
# ساخت پوشه پشتیبان
mkdir -p ~/goftar-backup

# کپی تمام فایل‌ها
cp -r /path/to/your/goftar/* ~/goftar-backup/

# کپی فایل دیتابیس (مهم!)
cp /path/to/your/goftar/storage/goftar.sqlite ~/goftar-backup/goftar-backup.sqlite
```

> اگر دیتابیس شما در مکان دیگری است، مسیر واقعی را در `storage/config/database.php` بررسی کنید.

#### مرحله ۲ — آپلود فایل‌های جدید

نسخه v1.0.2 را از گیت‌هاب دانلود کنید و تمام فایل‌ها را روی سرور آپلود کنید و فایل‌های قبلی را **جایگزین** کنید:

```bash
# از طریق Git
cd /path/to/your/goftar
git pull origin main

# یا محتوای ZIP را از طریق FTP/SFTP آپلود کنید
# مطمئن شوید تمام فایل‌ها جایگزین شده‌اند
```

**مهم:** پوشه `storage/` را حذف نکنید. دیتابیس و فایل‌های آپلودشده شما آنجا هستند.

#### مرحله ۳ — تنظیم دسترسی‌ها

مطمئن شوید دسترسی‌ها درست هستند:

```bash
chmod -R 755 storage/
chmod -R 755 config/
```

#### مرحله ۴ — اجرای اسکریپت مایگریشن

این مرحله کلیدی است. اسکریپت مایگریشن کارهای زیر را انجام می‌دهد:

1. اضافه کردن ستون `email` به جدول `users` (در صورت عدم وجود)
2. اضافه کردن تنظیمات ایمیل/SMTP (در صورت عدم وجود)
3. اضافه کردن ستون‌های `color`, `border_position`, `image` به جدول `categories` (در صورت عدم وجود)
4. ایجاد تمام جداول جدید (`polls`, `poll_options`, `poll_votes`, `static_pages`, `admin_notes`, `hidden_contents`, `nsfw_verifications`, `user_uploads_quota`)
5. ایجاد تمام ایندکس‌های جدید
6. درج مجوزها و تنظیمات جدید
7. تأیید صحت تمام داده‌های موجود

**نحوه اجرا:**

1. با حساب **مدیر** به سایت گفتار خود وارد شوید
2. آدرس زیر را در مرورگر باز کنید:

```
https://your-domain.com/install/migrate.php
```

3. صفحه نتایج را می‌بینید که هر مرحله مایگریشن با علامت سبز (موفق) یا قرمز (ناموفق) نمایش داده می‌شود
4. اگر همه مراحل سبز هستند، مایگریشن کامل شده
5. اگر مرحله‌ای قرمز بود، پیام خطا را بررسی کنید

> اسکریپت مایگریشن **Idempotent** است — اجرای چندباره آن بی‌خطر است. قبل از هر تغییری، وجود ستون‌ها و جداول را بررسی می‌کند.

#### مرحله ۵ — تأیید صحت ارتقا

پس از مایگریشن:

1. به **پنل مدیریت** > **درباره** بروید — نسخه `1.0.2 beta` باید نمایش داده شود
2. به **پنل مدیریت** > **تنظیمات** بروید — تب‌های جدید را بررسی کنید: آپلود، ایمیل
3. به **پنل مدیریت** > **نظرسنجی‌ها** بروید — مطمئن شوید صفحه مدیریت نظرسنجی بارگذاری می‌شود
4. به **پنل مدیریت** > **صفحات ایستا** بروید — مطمئن شوید صفحه CMS بارگذاری می‌شود
5. به **پنل مدیریت** > **یادداشت‌ها** بروید — مطمئن شوید صفحه یادداشت‌های مدیریتی بارگذاری می‌شود
6. به **پنل مدیریت** > **آمار** بروید — مطمئن شوید صفحه نمودارها بارگذاری می‌شود
7. یک موضوع جدید بسازید و مطمئن شوید دکمه‌های جدید ویرایشگر (نظرسنجی، گالری، محتوای شرطی) نمایش داده می‌شوند

#### مرحله ۶ — پاک‌سازی (اختیاری)

پس از تأیید عملکرد صحیح، می‌توانید پوشه install را حذف کنید:

```bash
rm -rf /path/to/your/goftar/install/
```

اگر ترجیح می‌دهید نگه دارید، فایل `.htaccess` داخل پوشه install دسترسی مستقیم را مسدود می‌کند.

---

### رفع مشکلات

| مشکل | راه‌حل |
|------|--------|
| پیام "Access denied" روی migrate.php | باید قبل از اجرای اسکریپت به عنوان مدیر وارد شده باشید |
| پیام "Database not found" | مسیر دیتابیس را در `storage/config/database.php` بررسی کنید |
| صفحه خالی بعد از آپلود فایل‌ها | مطمئن شوید PHP 7.4+ نصب است و اکستنشن `sqlite3` فعال است |
| تنظیمات جدید نمایش داده نمی‌شوند | اسکریپت مایگریشن را دوباره اجرا کنید — اجرای مجدد بی‌خطر است |
| ظاهر تم به هم ریخته | کش مرورگر را پاک کنید (Ctrl+Shift+R) |
| قابلیت نظرسنجی/نمودار کار نمی‌کند | مطمئن شوید `vendor/js/chart.umd.min.js` آپلود شده |

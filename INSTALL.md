# Goftar — Installation Guide

<p align="center">
  <strong>Step-by-step guide to install Goftar on your web server</strong>
</p>

<p align="center">
  <img src="https://github.com/abdulhalim/Goftar/raw/main/screenshots/en-screenshot1.png" alt="Goftar Homepage" width="600"/>
</p>

---

## Prerequisites

Before you begin, make sure your hosting environment meets the following requirements:

- **PHP 7.4 or higher** (PHP 8.1+ recommended)
- Required PHP extensions: `sqlite3`, `gd`, `mbstring`
- Recommended PHP extensions: `openssl`, `curl`
- Web server: Apache with `mod_rewrite` enabled, or Nginx
- Approximately 20 MB of free disk space

> Goftar works on **shared hosting** too! No MySQL, no Composer, no special server configuration needed.

---

## Step 1 — Download the Latest Version

Go to the [Goftar GitHub Releases](https://github.com/abdulhalim/Goftar/releases) page and download the latest version zip file (e.g., `Goftar_1.0.2-Beta.zip`).

Alternatively, clone the repository using Git:

```bash
git clone https://github.com/abdulhalim/Goftar.git
```

---

## Step 2 — Upload Files to Your Server

Extract the downloaded zip file on your computer, then upload **all files and folders** to your web server's document root directory.

Common document root paths:

| Hosting Type | Document Root |
|-------------|--------------|
| cPanel | `public_html/` |
| Plesk | `httpdocs/` |
| DirectAdmin | `public_html/` |
| VPS / Dedicated | `/var/www/html/` |
| Local (XAMPP) | `htdocs/` |

You can upload files using:

- **cPanel File Manager** — upload the zip file and extract it
- **FTP Client** (FileZilla, WinSCP) — upload extracted files
- **SSH / SCP** — for VPS or dedicated servers

Example using SSH:

```bash
# Extract the zip
unzip Goftar_1.0.2-Beta.zip

# Upload to server
scp -r Goftar_1.0.2/* user@your-server:/var/www/html/
```

Your directory structure should look like this:

```
your-site/
├── admin/           # Admin panel
├── api/             # API endpoints
├── assets/          # Frontend assets
├── functions/       # Core functions
├── handlers/        # Form handlers
├── includes/       # Shared components
├── install/        # Installer
├── lang/           # Language files
├── public/         # Frontend pages
├── theme/          # Theme system
├── vendor/         # Third-party libraries
├── config/         # Configuration (writable)
├── storage/        # Database & uploads (writable)
├── index.php       # Main entry point
└── robots.php      # Robots.txt generator
```

---

## Step 3 — Set File Permissions

The web server needs write access to the `storage/` and `config/` directories. Set the correct permissions:

### On Linux / VPS / SSH:

```bash
# Navigate to your site directory
cd /var/www/html/

# Set permissions
chmod -R 755 storage/
chmod -R 755 config/
```

### On cPanel / Shared Hosting:

1. Open **File Manager**
2. Right-click on the `storage` folder -> **Permissions** -> set to **755**
3. Right-click on the `config` folder -> **Permissions** -> set to **755**

### On DirectAdmin:

1. Open **File Manager**
2. Select `storage` and `config` folders
3. Set permissions to **755**

> If permissions issues persist, try **777** for these directories (less secure but may be needed on some shared hosting).

---

## Step 4 — Run the Web Installer

1. Open your web browser
2. Navigate to your site URL (e.g., `https://yourdomain.com/`)
3. You will be **automatically redirected** to the installer page at `/install/`

The installer has **5 steps**:

### 4.1 — Server Requirements Check

The installer automatically verifies:
- PHP version (must be 7.4+)
- Required PHP extensions (`sqlite3`, `gd`, `mbstring`)
- Directory writability

If any requirement is missing, fix it and click **Recheck**.

### 4.2 — Site Configuration

Enter the following information:
- **Site Title** — your forum name (e.g., "My Community")
- **Site Slogan** — a short description (optional)
- **Site URL** — your full site address (auto-detected)
- **Default Language** — Persian or English
- **Default Theme** — Dark or Light

### 4.3 — Admin Account

Create your administrator account:
- **Username** — admin login name
- **Display Name** — name shown on the forum
- **Password** — strong password
- **Confirm Password** — re-enter password

### 4.4 — Security Questions

Set up **3 security questions** for password recovery:
- Choose a question and provide an answer for each
- These will be used if you forget your password

### 4.5 — Review & Install

Review all settings on the summary page. If everything looks correct, click **Install**.

The installer will:
- Create the SQLite database
- Set up all required tables
- Save configuration files
- Create the `installed.lock` file
- **Disable itself** automatically

---

## Step 5 — Post-Installation

After the installer completes:

1. Click **Go to Forum** or navigate to your site URL
2. Log in with the admin credentials you created
3. You're done! Your forum is now live

> The `/install/` directory is automatically disabled after installation. You can safely leave it on the server.

---

## Creating Your First Category

1. Log in with your admin account
2. Click your **username** in the top-right corner of the page
3. Select **Admin Panel** from the dropdown menu
4. In the left sidebar, click on **Category Management**
5. Click the **Add New Category** button
6. Fill in:
   - **Category Name** (e.g., "General Discussion")
   - **Description** (brief description of the category)
   - **Icon** (choose a Font Awesome icon)
   - **Color** (pick an accent color for the category)
7. Click **Save**

The category will now appear on the forum homepage.

---

## Creating Your First Topic (Post)

1. Go to the forum homepage
2. Click on the category you just created
3. Click the **New Topic** button (usually at the top-right)
4. Fill in:
   - **Title** — the subject of your topic
   - **Content** — write your post using the Markdown editor
   - You can format text, add images, attach files, create polls, etc.
5. Click **Submit**

Your first topic is now live! Users can view it and reply.

---

## Troubleshooting

### Installer doesn't appear or blank page
- Make sure `index.php` is in the correct directory
- Check that PHP is working: create a `phpinfo.php` file with `<?php phpinfo(); ?>` and access it

### "Permission denied" errors
- Double-check that `storage/` and `config/` have **755** permissions
- On some shared hosting, you may need **777**

### "Database error" after installation
- Make sure `storage/` is writable
- Check that the `sqlite3` PHP extension is enabled

### Installer shows "already installed"
- Delete the file `storage/config/installed.lock` and access `/install/` again
- **Warning:** This will reset your database!

---

## Need Help?

- 🐙 [Report issues on GitHub](https://github.com/abdulhalim/Goftar/issues)
- 🌐 Visit the [Goftar website](https://goftarforum.ir)

---

## Links

| Resource | Link |
|----------|------|
| GitHub Repository | [https://github.com/abdulhalim/Goftar](https://github.com/abdulhalim/Goftar) |
| Releases | [https://github.com/abdulhalim/Goftar/releases](https://github.com/abdulhalim/Goftar/releases) |
| Website | [https://goftarforum.ir](https://goftarforum.ir) |
| License | MIT |

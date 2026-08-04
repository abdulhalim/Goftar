# Goftar

<p align="center">
  <strong>Modern, Secure, Open-Source Forum Builder with Full RTL/LTR Support</strong><br>
  Demo: https://pourdaryaei.ir/forum/
</p>



<p align="center">
  <img src="https://github.com/abdulhalim/Goftar/raw/main/screenshots/en-screenshot1.png" alt="Homepage Screenshot" width="800"/>
</p>

<p align="center">
  <img src="https://github.com/abdulhalim/Goftar/raw/main/screenshots/en-screenshot2.png" alt="Topic View Screenshot" width="800"/>
</p>

---

> **Product Status:** Beta (v1.0.2)
> Goftar is currently in public beta testing. Core features are implemented and functional. Recommended for staging and testing environments.

---

## What is Goftar?

**Goftar** (meaning "speech" or "discourse" in Persian) is a lightweight, self-hosted forum platform built with PHP and SQLite — designed from the ground up for communities that speak RTL languages like Persian, Arabic, and Urdu. It delivers a modern user experience with zero external database dependencies, making it incredibly easy to deploy on any shared hosting or VPS.

### Why Goftar?

- **No MySQL needed** — runs entirely on a single SQLite file
- **RTL-first design** — the entire interface is built with bidirectional layout support using CSS logical properties
- **Truly lightweight** — no heavy frameworks, no Composer dependencies, no Node.js build step. Just upload and run
- **Feature-rich** — polls, gated content, galleries, NSFW system, static pages CMS, file uploads with quota management, and a powerful admin panel — all out of the box

---

## Key Features

### Content & Editor

| Feature | Description |
|---------|-------------|
| 🗳️ **Polls** | Create polls in topics with single/multiple vote types |
| 🖼️ **Gallery BBCode** | Insert image galleries with multi-file upload, external URL support, and GLightbox viewer |
| 🔒 **Gated Content** | Lock content behind likes or replies — users must interact to reveal |
| 👁️ **NSFW System** | Age-verified content gates with blur overlay and per-topic cookie-based verification |
| 🎵 **Audio Player** | Embedded audio playback via Plyr with lightbox integration |
| 📥 **Video Embed** | Embed videos from YouTube, Aparat, Vimeo, and direct links |
| 📥 **Download Box** | Attach downloadable files to posts with file details |
| 😊 **Emoji Picker** | Quick emoji insertion with responsive dropdown |
| 📋 **Code Copy** | Auto-injected copy button on code blocks |
| 💬 **Quote Reply** | One-click quote with author attribution |
| ✨ **Markdown Editor** | Full Markdown toolbar with bold, italic, strikethrough, code, and blockquote |

### Pages & CMS

| Feature | Description |
|---------|-------------|
| 📄 **Static Pages** | Create custom pages (About, Rules, Privacy) with Markdown/HTML, slug-based URLs, and automatic footer menu integration |

### Admin & Moderation

| Feature | Description |
|---------|-------------|
| 📝 **Admin Notes** | Internal staff notes/tickets with priority levels, status tracking, assignee management |
| 📈 **Statistics Dashboard** | 5 interactive Chart.js visualizations — hourly/weekly activity, monthly trends, category breakdown, user growth |
| 📁 **Upload Management** | Per-user quota system, category filtering, auto WebP conversion, admin approval workflow |
| 👁️ **Guest Content Control** | 7 individual settings to hide specific content types from guests |
| 🛡️ **WAF** | Web Application Firewall with configurable protection levels |

### Security

| Feature | Description |
|---------|-------------|
| 🔒 **CSRF Protection** | Token-based CSRF validation on all forms and AJAX requests |
| 🛡️ **XSS Prevention** | Output encoding, content sanitization, and DOM-safe rendering |
| 🔑 **2FA** | Two-factor authentication with TOTP (QR code setup + backup codes) |
| 🚫 **IP Blocking** | Manual and WAF-driven IP ban system |
| ⏱️ **Rate Limiting** | Request rate limiting to prevent abuse |
| 📧 **SMTP Support** | Full email configuration with TLS/SSL encryption |

### UI & Experience

| Feature | Description |
|---------|-------------|
| 🌙 **Dark / Light Theme** | CSS custom property-based theming with dynamic switching, 12 accent colors |
| 📱 **Fully Responsive** | Three breakpoints — desktop, tablet (768px), mobile (550px) |
| 🌐 **RTL / LTR** | Complete bidirectional support using CSS logical properties |
| 🔔 **Real-Time Notifications** | Polling-based notification bars for PMs and topic updates |

---

## Requirements

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| PHP | 7.4 | 8.1+ |
| PHP Extensions | `sqlite3`, `gd`, `mbstring` | `sqlite3`, `gd`, `mbstring`, `openssl`, `curl` |
| Web Server | Apache (with `mod_rewrite`) or Nginx | Apache 2.4+ |
| Disk Space | ~20 MB | ~50 MB (with uploads) |
| Permissions | Write access to `storage/` and `config/` | — |

> **Shared Hosting?** Goftar works perfectly on shared hosting. No MySQL, no Composer, no special server configuration needed.

---

## Quick Installation

### Step 1 — Download & Upload

Download the latest release from [GitHub Releases](https://github.com/abdulhalim/Goftar/releases) and upload all files to your web server's document root (e.g., `public_html`, `htdocs`, or `var/www/html`).

### Step 2 — Set Permissions

Make sure the web server can write to the storage and config directories:

```bash
chmod -R 755 storage/
chmod -R 755 config/
```

### Step 3 — Run the Installer

Open your site URL in a browser. You'll be automatically redirected to the multi-language installer. The installer will:

1. **Check server requirements** — verifies PHP version and required extensions
2. **Site configuration** — enter your site title, slogan, and URL
3. **Admin account** — create the administrator username, display name, and password
4. **Security questions** — set up recovery questions for password reset
5. **Review & Install** — confirm all settings and click Install

The installer automatically creates the SQLite database and disables itself after completion.

### Step 4 — Start Using Your Forum

After installation, log in with your admin credentials, go to the Admin Panel, create your first category, and start creating topics.

---

## Your First Steps After Installation

### Create Your First Category

1. Log in to the forum with your admin account
2. Click on your username in the top-right corner
3. Select **Admin Panel** from the dropdown menu
4. In the admin panel, go to **Category Management**
5. Click **Add New Category**
6. Fill in the category name, description, icon, and color
7. Click **Save**

Your new category will now appear on the forum homepage.

### Create Your First Topic

1. Go to the forum homepage
2. Click on the category you just created
3. Click the **New Topic** button
4. Enter a title for your topic
5. Write your content using the Markdown editor
6. Optionally add a poll, attach files, or insert images
7. Click **Submit**

Your topic is now live and visible to all users!

---

## Technical Architecture

| Component | Technology |
|-----------|-----------|
| Backend Language | PHP 7.4+ (no frameworks, vanilla PHP) |
| Database | SQLite — single file, zero configuration |
| Frontend | Vanilla JavaScript + jQuery, CSS Custom Properties |
| Icons | Font Awesome 7.1 |
| Markdown | Parsedown (PHP) with custom BBCode extensions |
| Charts | Chart.js |
| Lightbox | GLightbox + Plyr (video/audio) |
| Font | VazirMatn (Persian/Arabic), system fonts (Latin) |
| Authentication | TOTP-based 2FA + QR code enrollment |
| i18n | Separate language files (Persian, English, Russian) |

---

## Links

- 🌐 **Website:** [https://goftarforum.ir](https://goftarforum.ir)
- 🐙 **GitHub Repository:** [https://github.com/abdulhalim/Goftar](https://github.com/abdulhalim/Goftar)
- 📥 **Download Latest Release:** [https://github.com/abdulhalim/Goftar/releases](https://github.com/abdulhalim/Goftar/releases)

---

## License

This project is released under the **MIT License**.

**Goftar** — A secure, fast, RTL-ready forum platform for any community.

# Goftar; Modern, Secure, Open-Source Forum Builder with Full RTL/LTR Support

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PHP](https://img.shields.io/badge/PHP-7.4+-777BB4.svg)](https://php.net)
[![GitHub Repository](https://img.shields.io/badge/GitHub-abdulhalim%2FGoftar-black)](https://github.com/abdulhalim/Goftar)

🇮🇷 **[Read this in Persian / فارسی](./README.fa.md)**

---

> ## ⚠️ Product Status: **Early Development**
> 
> **This product is still in early testing and is NOT ready for live/production use.**
> You may encounter bugs, security issues, or breaking API changes. Using it in real-world projects is currently **not recommended**.

---

If you're looking to launch a **professional discussion forum** with a modern look, high security, **Goftar** is exactly what you need.

> **A complete, lightweight, and powerful forum builder** that prioritizes security, speed, and user experience.

## 📸 Screenshots

| Index View | Posts View |
|--------------|-------------|
| ![Index Screenshot](screenshots/en-screenshot1.png) | ![Posts Screenshot](screenshots/en-screenshot2.png) |

## ✨ Key Features

- **🛡️ Enterprise-grade Security**: WAF, Rate Limiting, CSRF Protection, 2FA, IP Blocking
- **🌐 Excellent RTL Support**: Built for Persian, Arabic, Urdu, and other RTL languages
- **📋 Multilingual Core**: Separate language files (Persian, English, and extensible)
- **🚀 Super Easy Installation**: Multi-language installer, automatic server requirements check
- **📱 Modern & Responsive Design**: Dark/Light theme, 12 color options, Font Awesome 6
- **👑 Powerful Admin Panel**: Analytics dashboard, user/topic management, backup system
- **💬 Complete Features**: Private messaging, conditional hidden content, image gallery, Markdown

## 🧱 Technical Architecture

| Feature | Description |
|---------|-------------|
| **Language** | PHP 7.4+ |
| **Database** | SQLite (no MySQL required) |
| **Lightweight** | Single `.sqlite` file |
| **API** | Separate endpoints for core actions |

## 🔧 Quick Requirements

- PHP 7.4 or higher
- `sqlite3` and `gd` extensions

---

## Installation Steps (For Testing/Development Only)

### 1. Upload Files
Upload all project files to your web server's root directory (e.g., `public_html` or `htdocs`).

### 2. Set Permissions
Allow write permissions for the `storage/` and `config/` folders.
```bash
chmod -R 755 storage config
```

### 3. Run the Installer
Open your site's URL in a browser. You will be automatically redirected to the installation page.

### 4. Follow the Installation Steps
- **Step 1**: Accept the terms and conditions.
- **Step 2**: Enter your site title, slogan, and site URL.
- **Step 3**: Set up the admin account (username, display name, password) and security questions.
- **Step 4**: Review the summary and click the **Install** button.

✅ After installation completes, the `/install/` folder will be automatically disabled or removed for security.

---

## Initial Forum Setup

Now that the installation is complete, let's prepare your forum for use.

### Step 1: Log in to the Admin Panel

1. Log in to your site using the admin username and password you set during installation.
2. After logging in, click on your name in the top menu and select **Admin Panel**.

### Step 2: Create Your First Category

To organize topics, you first need to create a category.

1. In the Admin Panel, click on **Category Management** from the side or top menu.
2. Fill out the **Add Category** form:
   - **Category Name**: e.g., "General" or "Announcements"
   - **Description**: (Optional) Write a short description for this category
   - **Icon**: Choose from Font Awesome icons
3. Click the **Add Category** button.

### Step 3: Write Your First Topic

1. Click on the site logo at the top to return to the homepage.
2. Click on the category you just created.
3. Click the blue **New Topic** button.
4. Enter the title and content of your first topic. You can use Markdown features and toolbar buttons.
5. Click **Post Topic**. Your first topic has been created.

### Step 4: Security Settings (Recommended)

- In the **Admin Panel**, go to **WAF Settings** and set the protection level to **Normal**.
- From **IP Block Management**, you can block malicious IP addresses.

---

## 🎉 Congratulations!

Your forum (in the testing environment) is now ready to go. Users can register, create topics, and join conversations.

## 📚 Third-Party Libraries & Assets

Goftar stands on the shoulders of these great open-source projects. We sincerely thank their developers.

| Library | Description | License |
| :--- | :--- | :--- |
| **[Font Awesome 7.1](https://fontawesome.com/)** | Icon set and toolkit | CC BY 4.0 |
| **[Parsedown](https://parsedown.org/)** | Markdown parser for PHP | MIT |
| **[GLightbox](https://github.com/biati-digital/glightbox)** | Modern, responsive, touch-friendly lightbox | MIT |
| **[VazirMatn](https://github.com/rastikerdar/vazirmatn)** | Beautiful Persian/Arabic font | SIL OFL 1.1 |
| **[QRCode.js](https://github.com/davidshimjs/qrcodejs)** | Cross-browser QRCode generator | MIT |
| **[Chart.js](https://www.chart.js.org/)** | Simple yet flexible JavaScript charting | MIT |

> 💡 A special thanks to the open-source community for making powerful tools accessible to everyone.

## 📄 License

This project is released under the **MIT** license.ftar**; A secure, fast, RTL-ready choice for any community. *(Coming soon after initial testing is complete)*

🔗 **GitHub Repository**: [https://github.com/abdulhalim/Goftar](https://github.com/abdulhalim/Goftar)

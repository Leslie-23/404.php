


# 🚧 How to Set Up a Custom 404 Error Page in PHP (Apache/WAMP/XAMPP)

This guide walks you through creating and serving your own `404.php` page using `.htaccess` with Apache on local servers like WAMP, XAMPP, or live hosting environments.

---

## ✅ Prerequisites

- Apache server (WAMP, XAMPP, or live Linux host)
- PHP installed and running
- `.htaccess` enabled in your Apache config (`AllowOverride All`)
- A working virtual host or localhost project directory

---

## 📁 Step 1: Create Your Project Folder

```bash
/www/myproject
````

Inside it, create:

```bash
myproject/
├── index.php
├── 404.php
└── .htaccess
```

---

## 📝 Step 2: Create the `index.php`

Create a basic index file to test the project is running.

```php
<!-- index.php -->
<!DOCTYPE html>
<html>
<head><title>Home</title></head>
<body>
  <h1>Welcome to My Project</h1>
</body>
</html>
```

---

## ❌ Step 3: Create the `404.php` Custom Error Page

```php
<!-- 404.php -->
<!DOCTYPE html>
<html>
<head><title>404 Not Found</title></head>
<body>
  <h1>Oops! Page Not Found (404)</h1>
  <p>The page you're looking for doesn't exist.</p>
  <a href="/">Go back home</a>
</body>
</html>
```

---

## 🛠️ Step 4: Create the `.htaccess` File

```apache
# .htaccess

# Set custom 404 error page
ErrorDocument 404 /404.php

<IfModule mod_rewrite.c>
    RewriteEngine On

    # Prevent directory listing
    Options -Indexes

    # Protect .htaccess from exposure
    <Files .htaccess>
        Order allow,deny
        Deny from all
    </Files>
</IfModule>
```

---

## ⚙️ Step 5: Enable `.htaccess` in Apache

### 🔍 Locate Apache Config:

* For WAMP: `C:\wamp64\bin\apache\apache2.x.x\conf\httpd.conf`
* For XAMPP: `C:\xampp\apache\conf\httpd.conf`

### 🔧 Find and Update:

Uncomment this line:

```apache
# LoadModule rewrite_module modules/mod_rewrite.so
```

➡️ Change to:

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

Then locate:

```apache
<Directory "c:/wamp64/www/">
    AllowOverride None
```

➡️ Change to:

```apache
<Directory "c:/wamp64/www/">
    AllowOverride All
```

> Restart Apache after saving changes.

---

## 🧪 Step 6: Test the Setup

* Visit: `http://localhost/myproject/` → Should load `index.php`
* Visit: `http://localhost/myproject/nonexistentpage` → Should load your `404.php`

---

## 🧼 Optional Extras

### ✅ Force trailing slashes:

```apache
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.+[^/])$ %{REQUEST_URI}/ [R=301,L]
```

### ✅ Log errors for debugging:

In `php.ini`, ensure:

```ini
display_errors = On
log_errors = On
error_log = "C:\path\to\php-error.log"
```

---

## 🎯 Final Directory Structure Recap

```bash
myproject/
├── .htaccess
├── 404.php
└── index.php
```

---



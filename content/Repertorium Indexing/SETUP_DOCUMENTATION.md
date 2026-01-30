---
dg-publish: true
---

# Repertorium - Setup & Troubleshooting Documentation


## Project Overview

**Repertorium** is a web application built on **CodeIgniter 3.x** (PHP framework) with Smarty templating. The application is primarily in German and manages medical/repertory data with user authentication and role-based access.

---

## Technology Stack

| Component       | Technology         |
|-----------------|-------------------|
| Framework       | CodeIgniter 3.x   |
| Language        | PHP 7.x/8.x       |
| Templating      | Smarty            |
| Database        | MySQL/MariaDB     |
| Web Server      | Apache (XAMPP)    |
| Dependencies    | Composer          |

---

## Local Setup Guide (XAMPP)

### Prerequisites
- XAMPP installed with Apache, MySQL, and PHP
- Access to phpMyAdmin

### Step 1: Clone/Copy Project Files
Place the project folder in: `d:\xamp\htdocs\repertorium`

### Step 2: Database Setup
1. Open phpMyAdmin (`http://localhost/phpmyadmin`)
2. Create a new database named: `repertorium`
3. Import the SQL dump file (if available) or set up tables as per schema

### Step 3: Configure Database Connection
Edit `application/config/database.php`:

```php
$db['default']['hostname'] = 'localhost';
$db['default']['username'] = 'root';
$db['default']['password'] = '';  // Empty for XAMPP default
$db['default']['database'] = 'repertorium';
$db['default']['dbdriver'] = 'mysqli';
```

### Step 4: Configure Base URL
Edit `application/config/config.php`:

```php
$config['base_url'] = 'http://localhost/repertorium/';
```

### Step 5: Apache Configuration
Ensure `.htaccess` is properly configured for URL rewriting:

```apache
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L]
```

### Step 6: Test the Application
Access: `http://localhost/repertorium/`

---

## Common Issues & Fixes

### 1. Database Connection Error ("Datenbank-Fehler")

**Problem:** Application displays "Database Error" on startup.

**Cause:** Incorrect database credentials or database not created.

**Fix:**
- Verify database `repertorium` exists in MySQL
- Check credentials in `application/config/database.php`
- Ensure MySQL service is running in XAMPP

---

### 2. Login Redirection to Wrong URL

**Problem:** After login, users redirected to `http://localhost/dashboard/` instead of the application.

**Cause:** Hardcoded redirect URLs not including the `repertorium` subfolder.

**Fix:**
Modified authentication controller to use proper base URL:
```php
// Changed from:
redirect('/dashboard/');

// To:
redirect(base_url('dashboard/'));
```

**Files Modified:**
- `application/controllers/Auth.php`
- Related authentication controllers

---

### 3. Content Links Return 404 Error

**Problem:** Links like `http://localhost/content/about-symcom` returning 404.

**Cause:** URLs missing the `repertorium` base path.

**Fix:**
- Updated content link generation to include base URL
- Fixed SQL in `fix_content_links.sql` to update database entries

---

### 4. Menu Items Not Displaying (Symcom/Indexierung)

**Problem:** Certain menu items like "Symcom" or "Indexierung" not appearing in navigation.

**Cause:** Database records disabled or missing in navigation tables.

**Files Used for Debugging:**
- `check_menu.php` - Check menu structure
- `trace_menu.php` - Trace menu hierarchy
- `enable_indexierung.php` - Enable disabled menu items

**Fix:**
Enabled menu items in database:
```sql
UPDATE navigation SET active = 1 WHERE name = 'Indexierung';
```

---

### 5. Sidebar Disappearing on Sub-Navigation

**Problem:** Sidebar disappears when navigating to sub-items within sections.

**Cause:** Template logic not correctly identifying parent menu context.

**Fix:**
- Modified view templates to properly track active parent menu
- Updated navigation helper to pass parent context

---

### 6. JavaScript Syntax Errors on Login

**Problem:** "Uncaught SyntaxError: Unexpected token '}'" during login.

**Cause:** PHP error output mixing with JavaScript response.

**Fix:**
- Fixed PHP syntax in controller files
- Ensured clean JSON responses for AJAX calls

---

### 7. Indexierung Form Validation Error

**Problem:** Indexierung (Indexing) forms showing validation errors even when PDF page fields are filled correctly.

**Cause:** Variable name typo in `_check_SeitePDFBis()` function at line 555 of `Indexierung.php`. The code was checking `$HerkunftID` instead of `$SeitePDFVon`.

**Fix:**
Changed in `application/controllers/optionen/Indexierung.php`:
```php
// Before (buggy):
if (!is_numeric($HerkunftID)) $HerkunftID = 0;

// After (fixed):
if (!is_numeric($SeitePDFVon)) $SeitePDFVon = 0;
```

---

## Server Deployment Notes

When deploying to a production server, update these configurations:

### Base URL
```php
// application/config/config.php
$config['base_url'] = 'https://your-domain.com/repertorium/';
```

### Database Credentials
```php
// application/config/database.php
$db['default']['hostname'] = 'your_db_host';
$db['default']['username'] = 'your_db_user';
$db['default']['password'] = 'your_db_password';
$db['default']['database'] = 'your_db_name';
```

### Production Settings
```php
// index.php - Set environment
define('ENVIRONMENT', 'production');

// application/config/database.php
$db['default']['db_debug'] = FALSE;
```

---

## Database Overview

Key tables used by the application:

| Table              | Purpose                          |
|--------------------|----------------------------------|
| `users`            | User accounts and authentication |
| `groups`           | User roles/permissions           |
| `navigation`       | Menu structure                   |
| `content`          | Page content storage             |
| `ci_sessions`      | Session management               |

---

## Utility Scripts

The following debug/utility scripts were created during setup:

| Script                    | Purpose                              |
|---------------------------|--------------------------------------|
| `check_tables.php`        | List all database tables             |
| `check_menu.php`          | Verify menu structure                |
| `trace_menu.php`          | Trace navigation hierarchy           |
| `enable_indexierung.php`  | Enable Indexierung menu item         |
| `list_groups.php`         | List user groups                     |
| `debug_perms.php`         | Debug permission issues              |

> **Note:** These scripts should be removed or secured in production.

---

## Quick Reference

### Key Configuration Files
- `application/config/config.php` - Base URL, session settings
- `application/config/database.php` - Database connection
- `application/config/routes.php` - URL routing
- `.htaccess` - Apache rewrite rules

### Default Login
Check with administrator for default credentials.

---

## Contact & Support

For issues not covered in this documentation, review:
1. CodeIgniter 3 User Guide
2. Application logs in `application/logs/`
3. Apache error logs

---


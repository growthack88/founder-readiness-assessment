# 🚀 Deployment Guide

This guide covers all methods to deploy the **Founder Readiness Assessment** as a web app on a server.

> **Key fact:** This is a single `index.html` file. Any web server that can serve static files will work perfectly.

---

## Table of Contents

- [Requirements](#requirements)
- [Method 1: Nginx (Recommended)](#method-1-nginx-recommended)
- [Method 2: Apache](#method-2-apache)
- [Method 3: cPanel Shared Hosting](#method-3-cpanel-shared-hosting)
- [Method 4: GitHub Pages](#method-4-github-pages-free)
- [Method 5: Vercel](#method-5-vercel-free)
- [Method 6: Netlify](#method-6-netlify-free)
- [Method 7: Docker](#method-7-docker)
- [Subdirectory Deployment](#subdirectory-deployment)
- [HTTPS / SSL](#https--ssl)
- [Offline Mode](#offline-mode)
- [Troubleshooting](#troubleshooting)

---

## Requirements

| Requirement | Details |
|-------------|----------|
| Web server | Any (Nginx, Apache, cPanel, CDN) |
| Server OS | Any (Linux, Windows, macOS) |
| Node.js | ❌ Not required |
| Database | ❌ Not required |
| Backend | ❌ Not required |
| Build tools | ❌ Not required |
| Internet access (client) | ✅ Required for CDN fonts + React |

---

## Method 1: Nginx (Recommended)

### Step 1 — Upload the file

```bash
# Clone the repo on your server
git clone https://github.com/growthack88/founder-readiness-assessment.git /var/www/assessment

# OR upload manually via SCP
scp index.html user@yourserver.com:/var/www/assessment/
```

### Step 2 — Create Nginx server block

```nginx
server {
    listen 80;
    server_name assessment.yourdomain.com;

    root /var/www/assessment;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    gzip on;
    gzip_types text/html text/css application/javascript;
}
```

Save to `/etc/nginx/sites-available/assessment` and enable:

```bash
ln -s /etc/nginx/sites-available/assessment /etc/nginx/sites-enabled/
nginx -t
systemctl reload nginx
```

### Step 3 — Set permissions

```bash
chown -R www-data:www-data /var/www/assessment
chmod 644 /var/www/assessment/index.html
```

✅ Visit `http://assessment.yourdomain.com`

---

## Method 2: Apache

### Step 1 — Upload the file

```bash
git clone https://github.com/growthack88/founder-readiness-assessment.git /var/www/html/assessment
```

### Step 2 — Create Virtual Host

```apache
<VirtualHost *:80>
    ServerName assessment.yourdomain.com
    DocumentRoot /var/www/html/assessment

    <Directory /var/www/html/assessment>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/assessment-error.log
    CustomLog ${APACHE_LOG_DIR}/assessment-access.log combined
</VirtualHost>
```

Enable:

```bash
a2ensite assessment.conf
systemctl reload apache2
```

### Optional: `.htaccess`

```apache
Options -Indexes
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```

---

## Method 3: cPanel Shared Hosting

1. Log in to your **cPanel** account
2. Open **File Manager**
3. Navigate to `public_html/`
4. Upload `index.html`
5. Visit `https://yourdomain.com`

✅ No configuration needed.

---

## Method 4: GitHub Pages (Free)

1. Fork this repository
2. Go to **Settings → Pages**
3. Source: `main` branch, `/ (root)` folder
4. Save
5. Live at: `https://yourusername.github.io/founder-readiness-assessment/`

---

## Method 5: Vercel (Free)

```bash
npm install -g vercel
cd founder-readiness-assessment
vercel
```

Or connect your GitHub repo directly at [vercel.com](https://vercel.com) — zero config needed.

---

## Method 6: Netlify (Free)

**Drag & Drop:**
1. Go to [netlify.com](https://netlify.com)
2. Drag the project folder into the deploy zone
3. Done — instant live URL

**Via CLI:**
```bash
npm install -g netlify-cli
netlify deploy --dir . --prod
```

---

## Method 7: Docker

**Dockerfile:**

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Build & Run:**

```bash
docker build -t founder-assessment .
docker run -d -p 8080:80 --name assessment founder-assessment
```

Visit `http://localhost:8080`

**Docker Compose:**

```yaml
version: '3.8'
services:
  assessment:
    build: .
    ports:
      - "8080:80"
    restart: unless-stopped
```

```bash
docker-compose up -d
```

---

## Subdirectory Deployment

To host at `https://yourdomain.com/assessment/`:

1. Create the folder: `mkdir /var/www/html/assessment`
2. Copy `index.html` into it
3. No config changes needed — the app has no internal routing dependencies

---

## HTTPS / SSL

Use **Let's Encrypt** (free):

```bash
# Install Certbot
apt install certbot python3-certbot-nginx   # Nginx
apt install certbot python3-certbot-apache  # Apache

# Issue certificate
certbot --nginx -d assessment.yourdomain.com
```

Certbot will automatically redirect HTTP → HTTPS.

---

## Offline Mode

If the deployment environment has **no internet access**, bundle the CDN dependencies locally.

### Step 1 — Download dependencies

```bash
mkdir libs

curl -o libs/react.min.js \
  https://cdnjs.cloudflare.com/ajax/libs/react/18.2.0/umd/react.production.min.js

curl -o libs/react-dom.min.js \
  https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/umd/react-dom.production.min.js

curl -o libs/babel.min.js \
  https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.9/babel.min.js
```

### Step 2 — Update script tags in `index.html`

Replace the CDN `<script>` tags:

```html
<script src="libs/react.min.js"></script>
<script src="libs/react-dom.min.js"></script>
<script src="libs/babel.min.js"></script>
```

> Note: Google Fonts still requires internet. For fully offline Arabic fonts, download Noto Kufi Arabic and Outfit and use `@font-face` CSS rules.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Blank white page | Check browser console — likely CDN load failure. Check internet access |
| Arabic text not rendering | Google Fonts may be blocked — check firewall/network |
| Assessment doesn't start | JavaScript may be disabled in browser |
| Fonts look wrong | Clear browser cache: Ctrl+Shift+R |
| 403 Forbidden | Check file permissions: `chmod 644 index.html` |
| 404 Not Found | Verify file path matches your server root config |

---

## Performance Notes

- Initial load: ~500KB (React + Babel from CDN, cached after first visit)
- After cache: <5KB (just `index.html`)
- No API calls, no tracking, no analytics by default
- Works on all modern browsers (Chrome, Firefox, Safari, Edge)

---

*Questions? Open an issue on [GitHub](https://github.com/growthack88/founder-readiness-assessment/issues).*

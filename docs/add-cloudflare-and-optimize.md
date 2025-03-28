---
title: Add cloudflare and optimize
sidebar_label: Add cloudflare and optimize
sidebar_position: 4
---

## Configuring Cloudflare Before Installing WordPress and Optimize Settings for Performance and SEO

### Step 1: Create a Cloudflare Account
- Go to [Cloudflare](https://www.cloudflare.com) and sign up for a free account.

### Step 2: Add Your Website to Cloudflare
- Click **"Add a domain"** and enter your domain name.
- Choose a plan (the free option suits most WordPress sites).

### Step 3: Update Your DNS Records
- Cloudflare automatically scans your DNS records. Review and confirm or adjust as needed.
- Click **"Continue."**

### Step 4: Change Nameservers
- Cloudflare provides new nameservers. Replace your existing nameservers at your domain registrar with these provided by Cloudflare.
- DNS propagation may take up to 24 hours.

### Step 5: Optimize Cloudflare Settings for Performance
- **Caching:**  
  Navigate to Cloudflare dashboard  → **Configuration**
  - Set **Caching Level** to **Standard**.
  - Set **Browser Cache TTL** to **Respect Existing Headers**.
  - Enable **Crawler Hints**.
  - Enable **Always Online**.

- **Speed Optimization:**  
  Go to the **Speed** tab → **Optimization**
  - Go to **Content Optimization** tab
    - Enable **Speed Brain**
    - Enable **Cloudflare Fonts**
    - Enable **Early Hints**
  - Go to **Protocol Optimization** tab
    - Enable **HTTP/2** (enabled by default)
    - Enable **HTTP/2 to Origin** (enabled by default)
    - Enable **HTTP/3 (with QUIC)** (enabled by default)
    - Enable **0-RTT Connection Resumption**

### Step 6: Enhance SEO with Cloudflare
- **SSL/TLS:**  Go to the **SSL/TLS** section
  - tab → **Overview**
    - In the SSL/TLS section, set encryption mode to **Flexible**
  - tab → **Edge Certificates**
    - Enable **Always Use HTTPS**
    - Enable **Automatic HTTPS Rewrites**

- **Page Rules:**  
  Go to the **Rules** tab → **Overview**
  - Template → Redirect from WWW to Root → Deploy
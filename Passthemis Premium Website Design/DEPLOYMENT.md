# Deployment Guide — Passthemis Private Limited

Domain: **https://passthemis.com**  
Type: Static HTML — no build command, no framework.

---

## Recommended: Netlify (simplest)

### Upload Steps
1. Go to [app.netlify.com](https://app.netlify.com) → **Sites** → **Add new site** → **Deploy manually**.
2. Drag & drop the entire **"Passthemis Premium Website Design"** folder into the deploy box.
3. Netlify will assign a random URL (e.g. `amazing-name-123.netlify.app`) — the site is live immediately.

### Add Custom Domain
1. In Netlify → **Domain settings** → **Add a domain** → enter `passthemis.com`.
2. Also add `www.passthemis.com` (Netlify will redirect www → apex automatically).
3. Netlify will tell you which DNS records to add (see below).
4. Once DNS propagates, click **Verify DNS configuration** — Netlify provisions HTTPS automatically.

### DNS Records (add at your domain registrar)

| Type  | Name  | Value                        | TTL  |
|-------|-------|------------------------------|------|
| A     | @     | `75.2.60.5`                  | 3600 |
| A     | @     | `99.83.190.102`              | 3600 |
| CNAME | www   | `your-site.netlify.app`      | 3600 |

> Replace `your-site` with the name Netlify assigns to your deploy.
> If your registrar supports ALIAS/ANAME records, use `your-site.netlify.app` for the apex instead of the A records above — Netlify prefers this.

---

## Vercel

### Upload Steps
1. Go to [vercel.com/new](https://vercel.com/new).
2. Choose **"Import Third-Party Git Repository"** or **"Deploy a template"** → pick **"Other"** (blank).
3. Upload the project folder OR connect a GitHub repository containing these files.
4. Build command: **(leave empty)**. Output directory: **`.`** (current directory).
5. Click Deploy.

### Add Custom Domain
1. Vercel Dashboard → your project → **Settings** → **Domains** → Add `passthemis.com` and `www.passthemis.com`.

### DNS Records

| Type  | Name  | Value                    | TTL  |
|-------|-------|--------------------------|------|
| A     | @     | `76.76.21.21`            | 3600 |
| CNAME | www   | `cname.vercel-dns.com`   | 3600 |

> Vercel provisions HTTPS/SSL automatically once DNS propagates (usually within minutes).

---

## Cloudflare Pages

### Upload Steps
1. Go to [pages.cloudflare.com](https://pages.cloudflare.com) → **Create a project** → **Direct Upload**.
2. Upload the project folder.
3. Set **Production branch**: `main` (or use Direct Upload — no branch needed).
4. Build command: **(leave empty)**. Build output directory: **`/`**.
5. Click Deploy.

### Add Custom Domain
1. Pages project → **Custom domains** → Add `passthemis.com`.
2. If using Cloudflare DNS (recommended): Cloudflare will auto-configure the DNS with CNAME flattening.

### DNS Records (if using Cloudflare DNS — recommended)

| Type  | Name  | Value                            | Proxy |
|-------|-------|----------------------------------|-------|
| CNAME | @     | `your-project.pages.dev`         | ✅ Proxied |
| CNAME | www   | `your-project.pages.dev`         | ✅ Proxied |

> Cloudflare's proxy (orange cloud) enables automatic HTTPS, CDN and DDoS protection.

### DNS Records (if using a different DNS provider)

| Type  | Name  | Value                         | TTL  |
|-------|-------|-------------------------------|------|
| CNAME | www   | `your-project.pages.dev`      | 3600 |
| A     | @     | Cloudflare will provide IPs   | 3600 |

---

## www → apex Redirect

All three platforms handle this automatically when you add both `passthemis.com` and `www.passthemis.com` as domains. The `netlify.toml` and `vercel.json` files already include a 301 redirect rule.

---

## HTTPS / SSL

All three platforms — Netlify, Vercel, Cloudflare Pages — provision and auto-renew TLS certificates (via Let's Encrypt or Cloudflare's CA) at no cost. No action needed beyond pointing DNS.

---

## Verification Checklist

After DNS propagates (allow up to 48 hours, usually faster):

- [ ] https://passthemis.com loads the website
- [ ] https://www.passthemis.com redirects to https://passthemis.com (301)
- [ ] http://passthemis.com redirects to https://passthemis.com
- [ ] Padlock icon (HTTPS) visible in browser
- [ ] [Google Rich Results Test](https://search.google.com/test/rich-results?url=https://passthemis.com) shows JSON-LD
- [ ] [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/?q=https://passthemis.com) shows OG tags
- [ ] Submit sitemap to Google Search Console: `https://passthemis.com/sitemap.xml`

---

## Which Platform to Choose

| Feature              | Netlify     | Vercel      | Cloudflare Pages |
|----------------------|-------------|-------------|-----------------|
| Free tier            | ✅          | ✅          | ✅              |
| Drag & drop upload   | ✅          | ❌          | ✅              |
| CDN locations        | Global      | Global      | 300+ global     |
| Auto HTTPS           | ✅          | ✅          | ✅              |
| www redirect built-in| ✅          | ✅          | ✅              |

**Recommendation: Netlify** — easiest for a first deployment (drag & drop), no Git required.

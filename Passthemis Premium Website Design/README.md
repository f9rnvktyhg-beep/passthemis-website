# Passthemis Private Limited — Website

Production-ready static website for [passthemis.com](https://passthemis.com).

## Project Structure

```
Passthemis Premium Website Design/
├── index.html          ← Main page (serve this as root)
├── Passthemis.dc.html  ← Source file (same content as index.html)
├── support.js          ← DC runtime (loads React 18 from unpkg CDN)
├── uploads/
│   ├── passthemis-logo.png
│   ├── passthemis-mark.png  ← used as favicon & OG image
│   └── Company Profile- Passthemis.pdf
├── 404.html            ← Custom 404 page
├── robots.txt
├── sitemap.xml
├── manifest.json       ← PWA manifest
├── _headers            ← Netlify cache & security headers
├── netlify.toml        ← Netlify configuration
└── vercel.json         ← Vercel configuration
```

## Technology

Pure static HTML + client-side React (loaded from unpkg CDN). No build step required.

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for complete DNS and hosting instructions.

**Quick deploy (Netlify):** drag the entire folder into [app.netlify.com/drop](https://app.netlify.com/drop).

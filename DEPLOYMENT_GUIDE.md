# Deployment Guide – Re-Elect Scott Brummer Campaign Website

## Current Setup

- **Repository:** https://github.com/SyncShepherd-Main/Brummer
- **Hosting:** GitHub Pages
- **Live URL:** https://syncshepherd-main.github.io/Brummer/
- **Branch:** `main` (root)

---

## Pushing Updates

From the local repo folder `G:\Websites\Scott Brummer\Brummer-repo`:

```bash
git add .
git commit -m "Your update message here"
git push
```

GitHub Pages will automatically rebuild and publish within 1–2 minutes.

---

## Connecting a Custom Domain (scottbrummer.com)

### Step 1 – Add CNAME file to repo
Create a file named `CNAME` (no extension) in the root of the repo with one line:
```
scottbrummer.com
```

### Step 2 – Update DNS at your domain registrar
Add these DNS records:

| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | syncshepherd-main.github.io |

### Step 3 – Enable in GitHub Pages settings
- Go to repo Settings → Pages
- Under "Custom domain" enter `scottbrummer.com`
- Check "Enforce HTTPS" once DNS propagates (24–48 hours)

---

## Wiring Up Forms

All forms are currently HTML-only. To make them functional:

### Option A: FormSpree (easiest)
1. Sign up at formspree.io
2. Create a form and get your endpoint URL
3. Add `action="https://formspree.io/f/YOUR_ID" method="POST"` to each `<form>` tag

### Option B: Netlify Forms
1. Move hosting to Netlify (free tier works)
2. Add `netlify` attribute to each `<form>` tag
3. Forms automatically captured in Netlify dashboard

---

## Adding the Candidate Photo

Replace the placeholder photo slots in `index.html` and `about.html`:

1. Save the photo as `assets/images/scott-brummer.jpg` (recommended: 800×1000px, JPG)
2. In `index.html`, find `.photo-slot` and replace:
   ```html
   <div class="photo-slot-label">Candidate Photo<br>Replaces This Area</div>
   ```
   with:
   ```html
   <img src="assets/images/scott-brummer.jpg" alt="Scott Brummer">
   ```
3. In `about.html`, find `.photo-box` and replace the `.slot-label` div with the same `<img>` tag

---

## Adding Google Analytics 4

Add before `</head>` in all 4 HTML files:

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

Replace `G-XXXXXXXXXX` with your actual GA4 Measurement ID.

---

## Updating the Sitemap

After adding new pages, update `sitemap.xml` with the new URLs and update the `<lastmod>` dates on changed pages.

---

## Alternative Hosting Options

### Netlify (recommended for production)
1. Go to netlify.com → Add new site → Import from GitHub
2. Select `SyncShepherd-Main/Brummer`
3. No build settings needed (static HTML)
4. Deploy — site is live in seconds
5. Add custom domain in Netlify settings

### Traditional Web Host (FTP)
1. Download repo as ZIP from GitHub
2. Upload all files via FTP to public_html
3. Ensure `index.html` is in the root

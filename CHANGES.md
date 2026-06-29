# View Passion — Technical & Performance Fixes

What changed, why, and how to deploy. All edits preserve the existing design, copy, bilingual EN/Thai switching, animations, and the contact form's dual-provider delivery.

## 1. File size / performance

The original `index.html` was **13.67 MB** because **106 images were embedded inline as base64** (which is ~33% larger than binary and can't be cached). Only 10 were true duplicates — the other 96 are genuinely different photos, screenshots, and artwork.

What was done:
- **Externalised every image** to `/img` as optimised **WebP** (max 1000px on the long edge, quality 80), **de-duplicated** by content hash (96 files instead of 106 copies).
- **Lazy-loaded** everything below the fold (`loading="lazy" decoding="async"`); the nav logo and hero artwork stay eager with `fetchpriority="high"` for a fast Largest Contentful Paint.

Result:
- `index.html`: **13.67 MB → 208 KB** (~54 KB gzipped, which is what GitHub Pages actually serves).
- **Initial page load: ~14 MB (all render-blocking) → ~160–330 KB.** The rest of the images stream in on demand and are cached by the browser.
- Total deployed assets: ~6.2 MB (images 5.5 MB lazy + PWA icons 0.4 MB).

Note: a **900 KB total** is not achievable with 96 distinct quality images — they need ~4–5 MB minimum before the visuals visibly degrade. The performance goal (fast first paint, cacheable assets) is fully met regardless. If you want a smaller total, the images can be re-encoded more aggressively (≈900px / quality 72 ≈ 3.8 MB) — just ask.

## 2. SEO

Added to `index.html` `<head>`:
- `robots` (index, follow), `author`, expanded `keywords`.
- `canonical`, `og:url`, `og:image` (+ width/height/alt), `twitter:image` — all pointing at the new `og-image.png` (1200×630 branded share card, included).
- `logo` added to the existing JSON-LD Organization block.

Added site-wide:
- **`robots.txt`** (allows all, points to the sitemap).
- **`sitemap.xml`** (home + 4 legal pages).
- **`canonical` + `robots`** on all four legal pages (they already had descriptions).

> The canonical/OG URLs use `https://viewpassion.com`. If the live domain differs, find-and-replace that string across `index.html`, `sitemap.xml`, `robots.txt`, and the legal pages.

## 3. Spam protection (contact form)

The form previously had spam protection effectively **off** (`_captcha:'false'`, empty honeypot). Added three layers — two invisible, one visible — with **no third-party account required**:

1. **Honeypot** — an off-screen field bots fill but humans never see. Submissions with it filled are rejected, and the value is also passed to Web3Forms (`botcheck`) and FormSubmit (`_honey`) so their own filters catch it too.
2. **Time-trap** — submissions completed in under 3 seconds (typical of bots) are rejected.
3. **Math challenge** — a simple, accessible "Spam check" question (e.g. `3 + 5 = ?`) that regenerates each time the form opens.

All three are enforced before either delivery path (Web3Forms or the FormSubmit fallback) runs.

> Optional upgrade: Web3Forms supports drop-in **hCaptcha** if you ever want a full visual CAPTCHA — happy to wire it in once you have a site key.

## Deploying
Upload the whole folder to GitHub Pages (or any static host) exactly as-is. `index.html` references images via relative `img/...` paths, so keep the folder structure intact.

## Optional: enable instant (no-redirect) email delivery
The form currently uses the FormSubmit fallback. For instant AJAX delivery, get a free key at web3forms.com (tied to info@viewpassion.com) and paste it into the `WEB3FORMS_KEY = ''` line near the top of the contact-form script in `index.html`.

# View Passion — Website + Legal Pages

Static site for **View Passion Co., Ltd.** Upload all files to your repository
root and (if using GitHub Pages) it will serve `index.html` as the homepage.

## Files (keep them all in the same folder)

| File | Purpose |
|------|---------|
| `index.html` | Main single-page website |
| `trust-center.html` | Trust Center hub (links to the three policies) |
| `privacy-policy.html` | Privacy Policy (studio-wide) |
| `terms-conditions.html` | Terms & Conditions (studio-wide) |
| `cookie-policy.html` | Cookie Policy (studio-wide) |
| `logo.png` | VIEW PASSION wordmark (used in the legal-page top bar) |
| `favicon.ico` | Browser tab icon (16/32/48 px) |
| `favicon-32.png` | 32 px PNG tab icon |
| `apple-touch-icon.png` | Home-screen icon for iOS/Android (180 px) |
| `icon-192.png` / `icon-512.png` | App icons used by the web manifest |
| `manifest.webmanifest` | Web app manifest (name, icons, theme color) |

All links between pages are **relative**, so the files must stay in the same
directory. The site footer links to each legal page, and every legal page links
back to the site via "← Back to site" → `index.html`.

The legal pages have their styles inlined, but they share the image assets above
(logo + favicons), so keep those files alongside the pages.

## Hosting on GitHub Pages
1. Create/choose a repository and upload these files to its root.
2. Repo **Settings → Pages →** Source: deploy from branch (e.g. `main`, `/root`).
3. Your site will be available at the URL GitHub shows on that page.

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

All links between pages are **relative**, so the files must stay in the same
directory. The site footer links to each legal page, and every legal page links
back to the site via "← Back to site" → `index.html`.

Each legal page is self-contained (styles are inlined), so any one of them can
be linked or shared on its own.

## Hosting on GitHub Pages
1. Create/choose a repository and upload these files to its root.
2. Repo **Settings → Pages →** Source: deploy from branch (e.g. `main`, `/root`).
3. Your site will be available at the URL GitHub shows on that page.

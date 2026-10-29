# amitmarathe.com

Static personal site (HTML, CSS and a little JS). There's no build step: what's in this folder is what goes live.

```
index.html        Home page (hero, pillars, testimonials, AI philosophy, 3 case studies, project grid)
about.html        About page (served at /about)
404.html          Not-found page
css/style.css     All styles. Brand colours and fonts are variables at the top.
js/main.js        Mobile menu, dropdown, scroll fade-ins, photo lightbox
assets/img/       Images (logo, home/, about/, photos/)
assets/files/     Put Amit-Marathe-CV.pdf here
.htaccess         Only used on Apache hosting (Hostinger); GitHub Pages ignores it
CNAME             Custom domain for GitHub Pages (m.amitmarathe.com)
robots.txt
```

## Preview locally

```sh
cd "/Users/apple/Documents/Amit Marathe Website"
python3 -m http.server 8080
```

Then open http://localhost:8080. Note that `/about` only works once deployed (GitHub Pages serves `about.html` for it); locally, use `/about.html`.

## How the setup works

- **www.amitmarathe.com** stays on **Wix** and is the desktop site.
- **m.amitmarathe.com** is **this folder**, hosted on GitHub Pages, and is the mobile site.
- Phones that open the Wix site are redirected to the mobile site by `setup/wix-mobile-redirect.html`.
  Desktops that open the mobile site are sent back to Wix by a small script at the top of each page here.
  Pages are matched: `/about-me` on Wix ↔ `/about` here, and `/talento-today` ↔ `/#case-3`.
- Visitors can switch with `?view=desktop` or `?view=mobile`. The footer has a "Desktop site" link.
- The redirect is skipped on `localhost`, so the local preview still works on your Mac.

## Deploy (GitHub Pages)

The site is the GitHub repo `marathe89/amitmarathe`. Pushing to `main` publishes it.

1. **Pages**: repo → Settings → Pages → Source "Deploy from a branch", branch `main`, folder `/ (root)`.
   Custom domain: `m.amitmarathe.com` (already set by the `CNAME` file).
2. **Wix DNS** (Wix → Domains → amitmarathe.com → Manage DNS Records): the `m` record must be a
   **CNAME** to `marathe89.github.io` (replace the old A record to 200.234.47.238).
   Don't touch the `@`, `www`, `workforceintelligence`, `voyage` or `travelintelligence` records.
3. **HTTPS**: once GitHub shows the DNS check as passed, tick **Enforce HTTPS** in Settings → Pages.
4. **Wix redirect**: Wix → Settings → Custom Code → Add Custom Code. Paste the contents of `setup/wix-mobile-redirect.html`,
   choose "All pages", "Load code once" and "Head", then **Publish** the Wix site.
   Do this last, after https://m.amitmarathe.com loads correctly on your phone.

To update the site later: edit, then `git commit -am "…" && git push`.

To test: open www.amitmarathe.com on your phone and it should land on m.amitmarathe.com. Open m.amitmarathe.com on a laptop and it should go back to Wix.

## Editing with Claude in VS Code

Open this folder in VS Code and ask Claude, for example: "add a full case-study page for Lucero" or "change the hero tagline". Then re-upload the changed files (or push, if you use Git deploy).

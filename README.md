# Sebastian Hadden — Portfolio

Static portfolio site (plain HTML/CSS/JS, no build step). Dark theme, scroll-reveal sections, two featured UX case studies plus a work gallery.

## Preview locally

```
python -m http.server 8080
```

Open http://localhost:8080/

## Deploy to GitHub Pages

1. Create a GitHub repo (e.g. `portfolio`) and push this folder:
   ```
   git remote add origin https://github.com/BeyondSmash/portfolio.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
3. Site goes live at `https://beyondsmash.github.io/portfolio/` within a minute or two.

### Custom domain (later)

1. Buy `sebastianhadden.com`; in your DNS, add a CNAME record `www → beyondsmash.github.io` and A records for the apex pointing at GitHub Pages IPs (185.199.108.153 / .109 / .110 / .111).
2. On GitHub: **Settings → Pages → Custom domain** → enter the domain (this creates a `CNAME` file in the repo). Enable **Enforce HTTPS**.
3. For `beyondsmash.com` → redirect: set it up as a domain forward at its registrar (GitHub Pages can't serve two domains from one repo).

## Content-swap checklist

Everything marked `PLACEHOLDER` in the HTML needs real content. Search each file for `PLACEHOLDER`:

### `index.html`
- [ ] Case study card images (WebHID tool screenshot, Molecular Maelstrom capsule art)
- [ ] Gallery images + links: Crystal Lattice demo, 3D models, Gaussian splats, Smash Ultimate mods, Hytale mods, VRChat tour video, Documents
- [ ] ArtStation URL (2 places: gallery card + footer)
- [ ] Steam URL (footer)
- [ ] About bio paragraph
- [ ] Resume PDF link

### `case-studies/webhid-keyboard.html`
- [ ] Hero screenshot; Timeline value
- [ ] Problem / Research / Decisions / Outcome copy
- [ ] Comparison table cells marked "verify" (check Epomaker's actual software before publishing claims)
- [ ] Before/after + interaction figures with captions
- [ ] "Try the tool" link

### `case-studies/molecular-maelstrom.html`
- [ ] Steam capsule art; Timeline + Tools values
- [ ] Vision / Design & Iteration / Key Decisions / Shipping copy
- [ ] GDD excerpt + playtest before/after figures with captions
- [ ] Steam store link

### Writing tips for the case studies
Lead every section with a decision and its reason, not a feature list. Concrete numbers (clicks removed, playtest observations) beat adjectives. A recruiter should get the arc — problem → evidence → decision → result — by skimming the headings and figures alone.

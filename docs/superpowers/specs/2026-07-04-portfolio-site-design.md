# Portfolio Site — Design Spec (2026-07-04)

## Goal
Personal portfolio for Sebastian Hadden targeting a **UX Design job**. Hosted on GitHub Pages now; custom domain (sebastianhadden.com, beyondsmash.com redirect) later. High-fidelity, modern, professional.

## Positioning
UX case studies first. Two featured case studies lead; everything else lives in a secondary "Selected Work" gallery.

## Stack
Plain static HTML/CSS/vanilla JS. No build step, no framework, no dependencies. Deploys by pushing to a GitHub Pages branch. CNAME file deferred until domain purchase.

## File structure
```
index.html
case-studies/webhid-keyboard.html
case-studies/molecular-maelstrom.html
css/style.css
js/main.js
assets/            (labeled SVG placeholders)
README.md          (deploy steps + content-swap checklist)
```

## Home page (index.html) — single scroll
1. **Hero** — name, UX-designer-first tagline, CTA button to case studies.
2. **Featured Case Studies** — two large cards linking to case-study pages.
3. **Selected Work** — gallery cards: Crystal Lattice demo, 3D models/sculpts/Gaussian splats, Smash Ultimate mods, Hytale mods, VRChat world tour video, ArtStation (external link), Documents (GDD, pedagogical doc).
4. **Skills & Tools** — grouped tag list (design, engineering, 3D/art).
5. **About / Contact** — short bio, email, ArtStation link, resume placeholder.

## Case-study pages (shared anatomy)
Hero image → at-a-glance sidebar (role, timeline, tools) → Problem → Research → Design Decisions → Outcome, each with captioned figure placeholders.

- **WebHID keyboard tool**: audit of Epomaker's official software, feature-comparison table, improvements/diffs, outcome.
- **Molecular Maelstrom**: GDD → iteration/playtesting → shipped on Steam; real-world product constraints (fee, revenue share) as product-thinking context.

## Visual system
- Dark theme: near-black background, off-white text, single cyan/teal accent.
- Type: Space Grotesk (headings) + Inter (body) via Google Fonts.
- Motion: sections slide in from alternating left/right edges + fade, one-time trigger via IntersectionObserver; disabled under `prefers-reduced-motion`.
- Responsive; semantic HTML landmarks, visible focus states, WCAG-AA contrast.

## Content strategy
Build now with clearly labeled placeholder SVGs and placeholder copy, structured for the real assets (Steam capsule art, ArtStation embeds, video thumbnails, comparison-table data). README carries a swap-in checklist.

## Explicitly out of scope (v1)
WebGL hero effects, dark/light toggle, blog, analytics, CMS, CNAME.

## Success criteria
- Loads fast and error-free on GitHub Pages.
- Scroll-reveal motion works and respects reduced-motion.
- A UX hiring manager can reach a case study in one click and read a complete Problem→Outcome narrative (placeholder copy marks where real content goes).

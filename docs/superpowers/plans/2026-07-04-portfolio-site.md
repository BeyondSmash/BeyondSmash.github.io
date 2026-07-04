# Portfolio Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Static UX-portfolio site (home + 2 case studies) deployable to GitHub Pages with scroll-reveal motion and labeled placeholders.

**Architecture:** Plain multi-page static site. One shared stylesheet holding a token-based dark design system; one small JS file for IntersectionObserver scroll reveals and mobile nav. Case-study pages share identical anatomy/classnames.

**Tech Stack:** HTML5, CSS (custom properties, grid/flex), vanilla JS, Google Fonts (Space Grotesk + Inter). No build step, no dependencies.

## Global Constraints

- No build step, no npm, no external JS. Only external requests: Google Fonts.
- Colors: bg `#0c0e13`, surface `#141821`, text `#e8eaf0`, muted `#9aa3b5`, accent `#4fd8c4`. WCAG-AA contrast for all text.
- Motion: `.reveal` elements translate from ±48px X + fade over 0.7s ease-out, once, at 15% visibility; fully disabled under `prefers-reduced-motion: reduce`.
- All placeholder media = inline SVG blocks labeled `PLACEHOLDER — <what goes here>`.
- Relative links only (site must work at `https://<user>.github.io/<repo>/` and at a custom domain root). Use `./` and `../` paths, never `/`-absolute.
- Verification is visual: serve with `python -m http.server` and check in browser + console (no JS errors).

---

### Task 1: Design system + shared JS

**Files:**
- Create: `css/style.css`
- Create: `js/main.js`

**Interfaces:**
- Produces: CSS classes all pages use: `.site-header`, `.nav`, `.btn`, `.section`, `.reveal`, `.reveal--left`, `.reveal--right`, `.card`, `.card-grid`, `.tag`, `.placeholder-fig`, `.case-hero`, `.case-meta`, `.comparison-table`, `.site-footer`. JS auto-wires anything with `.reveal`.

- [ ] **Step 1: Write `css/style.css`** — tokens, reset, type scale, header/nav (sticky, blur backdrop), buttons, section layout (max-width 1100px, generous vertical rhythm), card grid (responsive `auto-fit minmax(280px,1fr)`), tags, placeholder figure style (dashed accent border, centered label), case-study styles (hero, meta sidebar via grid, comparison table), footer, and the reveal states:

```css
.reveal { opacity: 0; transition: opacity .7s ease-out, transform .7s ease-out; }
.reveal--left  { transform: translateX(-48px); }
.reveal--right { transform: translateX(48px); }
.reveal.is-visible { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) {
  .reveal, .reveal--left, .reveal--right { opacity: 1; transform: none; transition: none; }
}
```

- [ ] **Step 2: Write `js/main.js`**:

```js
const observer = new IntersectionObserver((entries) => {
  for (const e of entries) {
    if (e.isIntersecting) { e.target.classList.add('is-visible'); observer.unobserve(e.target); }
  }
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

const toggle = document.querySelector('.nav-toggle');
if (toggle) toggle.addEventListener('click', () =>
  document.querySelector('.nav').classList.toggle('is-open'));
```

- [ ] **Step 3: Commit** — `git add css js && git commit -m "feat: design system and scroll-reveal"`

### Task 2: Home page

**Files:**
- Create: `index.html`

**Interfaces:**
- Consumes: Task 1 classes. Links to `case-studies/webhid-keyboard.html`, `case-studies/molecular-maelstrom.html` (Task 3).

- [ ] **Step 1: Write `index.html`** with semantic landmarks (`header`, `main`, `section` with `aria-labelledby`, `footer`) and sections in order: hero (name, "UX Designer" tagline, CTA `.btn` → `#case-studies`), `#case-studies` (2 large `.card`s, each `.reveal` alternating `--left`/`--right`, placeholder hero fig + title + 1-line hook + "Read case study" link), `#work` gallery (7 cards: Crystal Lattice demo, 3D models & sculpts, Gaussian splats, Smash Ultimate mods, Hytale mods, VRChat world tour, Documents; ArtStation as external-link card), `#skills` (3 tag groups: Design / Engineering / 3D & Art), `#about` + footer (email `seba.hadden@gmail.com`, ArtStation placeholder URL, resume placeholder link).
- [ ] **Step 2: Verify** — `python -m http.server 8080`, load `http://localhost:8080/`, confirm: sections reveal on scroll from alternating sides, no console errors, layout holds at 375px and 1440px widths.
- [ ] **Step 3: Commit** — `git commit -am "feat: home page"`

### Task 3: Case-study pages

**Files:**
- Create: `case-studies/webhid-keyboard.html`
- Create: `case-studies/molecular-maelstrom.html`

**Interfaces:**
- Consumes: Task 1 classes via `../css/style.css`, `../js/main.js`; back-link to `../index.html`.

- [ ] **Step 1: Write `webhid-keyboard.html`** — shared anatomy: `.case-hero` (title, one-line summary, placeholder hero fig), `.case-meta` (Role / Timeline / Tools), then sections Problem → Research (includes `.comparison-table`: feature rows vs Epomaker official software — populate rows with real feature names: RGB per-key config, macro editor, firmware update flow, latency/feedback, cross-platform; cells marked `PLACEHOLDER — verify` where data is unconfirmed) → Design Decisions (figure placeholders w/ captions) → Outcome.
- [ ] **Step 2: Write `molecular-maelstrom.html`** — same anatomy; Research section covers GDD + playtesting iteration; Outcome covers Steam release incl. product constraints (Steam Direct fee, 30% revenue share) framed as product thinking. Placeholder Steam capsule fig + placeholder store link.
- [ ] **Step 3: Verify** — load both pages via local server from `index.html` links; check reveal motion, back-links, no console errors.
- [ ] **Step 4: Commit** — `git commit -am "feat: case study pages"`

### Task 4: README + deploy readiness

**Files:**
- Create: `README.md`
- Create: `.gitignore`

- [ ] **Step 1: Write `README.md`** — what the site is, local preview command, GitHub Pages deploy steps (create repo → push → Settings→Pages→main branch), custom-domain steps for later (CNAME file + DNS), and a **content-swap checklist** enumerating every `PLACEHOLDER` in the site with its file location.
- [ ] **Step 2: Write `.gitignore`** — `Thumbs.db`, `.DS_Store`.
- [ ] **Step 3: Final verify** — full click-through of all 3 pages, keyboard-tab through nav (visible focus), reduced-motion check via DevTools emulation.
- [ ] **Step 4: Commit** — `git commit -am "docs: README and deploy checklist"`

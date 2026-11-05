# Elite Pro Fitness landing hero — implementation plan

## Spec authority
`bf2738841a795447.txt` (the Elite Pro Fitness spec) + `6a7790c622bb8b09.txt` (the Redline reference spec it
mandates as the exact structural template). The Redline spec is the binding layout/animation source; the Elite
spec overrides only what it explicitly lists (theme, words, assets, step content, booking bar).

## Global constraints
- One self-contained `index.html` (HTML/CSS/vanilla JS). No build, no logins, no app features, no payments.
- Three.js r170 via import map: `{ "imports": { "three": "https://cdn.jsdelivr.net/npm/three@0.170.0/build/three.module.js" } }`.
- One continuous render loop driven by a single state float `st` (0..2). Same timings, easing, segment maths,
  layer transforms, dust canvas, fog/whiteout, header/nav, left rail, hint, wheel/click/Escape stepping,
  drag-to-spin, mobile CSS.
- Theme: background radial `#2a0508` (centre) → `#050505` (edges); accent/CTA `#E10600`; text `#FFFFFF`;
  heavy white type (Montserrat 800/900). Dust motes `rgba(255,240,235,.95)` → `rgba(225,6,0,.35)` at .4 →
  transparent. Fog stays white.
- Assets from `hero-assets/hero-assets/assets/` (coach/corner from `trash/`), .webp preferred with PNG/JPG fallback.
  Never redraw, recolour, merge or reshape any logo.
- Real facts only; keep every `[bracket]` placeholder visible. No invented claims/reviews/stats/people/images.
  Respect `prefers-reduced-motion`; add `alt` text; lazy-load heavy images.
- Done when: index.html opens with no console errors; all 3 steps work by wheel, click, keys and touch; the
  disc shows the logo unchanged; the hover cards show the right tiles; NORTHFIELD sits between LAND and FORE;
  the mailto opens with the form data; layout works at 390px wide.

## Tasks

### Task 1 — Markup + CSS skeleton (verbatim from Redline spec, themed)
Write the DOM order from Redline §3 inside `main.hero#hero`, and the CSS from Redline §2 verbatim, with the
theme substitutions applied: `.hero` background radial, `--red:#E10600`, `#word0`="ELITE PRO", eyebrow, `#word1`="TRAIN",
`#region`/`#destName`/`#dest small`, `#bar` = "Book a free trial" form (Name / Phone / Class select / red Send
button → mailto:elitepro121@gmail.com) + "Call 07968 043030" + `[hours]`/`[prices]` placeholders, header with
small logo + nav (Who we are / Classes / Where we are / Contact) + social links (Facebook / TikTok).
Ruling: keep the Redline CSS structure verbatim — only swap the values the Elite spec lists.

### Task 2 — Three.js disc (Step 1/2)
Scene: `WebGLRenderer({canvas,alpha:true,antialias:true})`, pixel ratio `min(dpr,2)`, `OrthographicCamera` in CSS
pixels (near −2e5, far 2e5). Hierarchy `planet` > `tilt` > `spin` > mesh. Sphere `SphereGeometry(1,128,96)` with the
Redline ShaderMaterial (vertex/fragment verbatim), plus the atmosphere sphere (BackSide, additive, transparent).
Map = `logo-stacked.webp` (fallback PNG), loaded with `crossOrigin='anonymous'` and the same left-7% seam fix +
top/bottom 3.5% pole pinch on a 2048×2048 canvas (scaled from the 2688×1344 recipe).
Rim lights red `#E10600` instead of a crimson region: replace the highlight colour `vec3(.62,.012,.07)` with
`vec3(.88,.024,.0)` and the edge tint `vec3(1.,.42,.4)` with `vec3(1.,.18,.04)`.
Step 1: giant word "ELITE PRO", eyebrow, disc swells from a speck, flare, drag-to-spin, pin behaviour.
Step 2: word "TRAIN", disc slides left and turns, timeline items with hover cards from `cards.png`
(Who we are→coach tile [0,0]; Classes→corner tile [1186,0]; Where we are→outside tile [0,900];
Contact→coach close-up tile [1186,900]), Explore button, `#region` text.

### Task 3 — Landing + parallax (Step 3)
Dive into the disc, white fog-out, then LAND (`outside.webp`) rises, "NORTHFIELD" sits BETWEEN LAND and FORE
(`fore.webp` on top, same size/position, word placed low so its base tucks behind the pavement), small line
"201A Merritts Brook Lane · Birmingham B31 1UH". Booking bar, scrim, rail `.on` on `round(st)`, hint,
wheel/click/Escape, drag-to-spin, mobile CSS at 390px.

### Task 4 — Wiring + polish
Wire `go(n)`, `seg`, `io`, `out`, `pick(i)`, hover cards, `#explore`→go(2), `#home`→go(0), rail dots→go(i),
wheel lock 1400ms, Escape steps back, drag-to-spin with inertia, `prefers-reduced-motion` (1ms durations,
`#hint`/`#rail` hidden), `alt` text on every image, lazy-load heavy images, England Boxing logo footer strip.
Run Impeccable design audit and fix type/spacing/motion; keep black/red/white, never change logos.

### Task 5 — Report
Write a short report of what was built and what is left (owner name, hours, prices, Instagram/Snapchat handles,
England Boxing affiliation confirmation).
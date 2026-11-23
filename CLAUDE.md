# CLAUDE.md — Jana's portfolio

Personal portfolio for **Janarthanan V ("Jana")**, UI/UX Designer, Chennai. Static site: HTML5 + CSS custom properties + vanilla ES modules. **No framework, no build step.** Deploys to Vercel as-is.

## Hard rules
1. **Never invent facts, metrics, logos, testimonials, research findings or rationale.** Only the content in the brief (mirrored in the placeholder register below) may appear. Anything unknown is a visible placeholder.
2. **Numbers on the site** are limited to: OTA drop-offs ↓25 %, update completion success ↑20 %; Data Sharing onboarding time ↓15 %; Accident reporting steps ↓35 %; Flyweis errors ↓20 %, tasks 30 % faster, handoff 25 % faster; Regami 10+ interviews & tests, task success +18 %, discoverability +20 %; CGPA 8.64; dates from the résumé. The Selorg grocery case study may also use its published scope figures (4 connected apps, 8 admin roles), labelled "At a glance", never as outcomes. Mock UI (device IDs, firmware versions, chips, expiries) is captioned "Illustrative recreation" and carries no extra metrics.
3. **No raw colours, font sizes, radii, shadows or durations outside `css/tokens.css`.** Exceptions: `#000` inside CSS `mask` gradients (alpha masks, not colours), the 24-hour sky keyframes in `js/sky-palette.js`, and the gradient stops of the shaded jet/saucer/balloon illustrations in `js/sky-craft.js` (their effects — contrail, ray, smoke, fire, laser, searchlight, shooting stars — use the `--c-craft-*` tokens). Component-only dimensions (mock UI sizes, desk object sizes) are declared as local custom properties at the top of the component block (e.g. `.mock-browser { --m-fs: 11px }`).
4. **Signature:** every major heading (h1/h2, booklet page titles) has exactly one word in `<em class="accent">` (Fraunces italic, accent colour). Card titles (h3) stay plain.
5. **Every card** starts with a mono eyebrow in the form `Category · Type` (`<p class="eyebrow">`).
6. **Accessibility is the portfolio:** AA contrast in day and night (and at every sky minute), everything keyboard-operable, visible focus, one `<h1>` per page, semantic landmarks, `prefers-reduced-motion` honoured everywhere. Run `scripts/a11y.mjs` before committing UI changes.
7. Do not add motion design, illustration or games as skills/services.
8. Commit after each phase. Keep this file updated when tokens, files or placeholders change.

## Design tokens (source: `css/tokens.css`)
| Group | Day | Night |
|---|---|---|
| `--c-paper` / `--c-paper-2` / `--c-card` | `#f7f1e6` / `#efe4d2` / `#fffbf4` | `#0f1220` / `#151a2b` / `#1c2236` |
| `--c-ink` / `--c-ink-2` | `#1f1a15` / `#5c4f42` | `#f4ecde` / `#b8af9f` |
| `--c-accent` (+ `--c-on-accent`) | `#b5361f` (+ `#fff`) | `#ff8f6b` (+ `#0f1220`) |
| `--c-leaf` / `--c-sky` / `--c-amber` | `#2d6a4a` / `#2c5e94` / `#8a5300` | `#7fd1a6` / `#8db8f0` / `#f2b661` |
| `--c-line` (UI borders ≥ 3:1) | `#8a7a66` | `#6e6a80` |
| `--c-hairline` (decorative only) | `#e2d5c1` | `#2c3350` |
| Soft chip fills `--c-*-soft` | light tints | deep tints (every chip pair ≥ 4.6:1) |
| Desk `--c-desk-1/2`, `--c-desk-grain`, `--c-lamp` | wood, no lamp | walnut + warm lamp pool |
| Paper objects `--c-object*`, `--c-kraft`, `--c-stamp` | paper | dimmed paper (see islands below) |
| Fixed (both themes) | `--c-device*`, `--c-code-*`, `--c-scrim`, `--c-tape`, `--c-pencil*`, `--c-graphite`, `--c-mug`, `--c-coffee`, `--c-craft-*` (sky craft: vapour, smoke, fire, hull, lamps, ray, laser, glow, searchlight, meteor) | |

- **Theming:** `:root[data-theme="dark"], [data-theme="dark"]` holds the night palette; `[data-theme="light"]:not(:root)` mirrors the day palette for nested "light islands". Desk objects and dialog sheets carry `class="paper-island" data-theme="light"` so they read as paper at night; `:root[data-theme="dark"] .paper-island[data-theme="light"]` dims them and darkens accent/line to keep AA.
- **Sky** vars (`--sky-top/mid/bottom`, `--sky-text`, `--sky-text-2`, `--sky-accent`, `--haze`, `--haze-a`, `--hill-1..3`, `--sea`, `--cloud`, `--star-alpha`, `--day-alpha`, `--light-x`, `--light-y`) are written live by `js/sky.js` from keyframes in `js/sky-palette.js`. Hero text/accent colours are chosen per minute against the actual sRGB gradient behind the copy; a soft haze appears only when no text colour reaches 4.5:1 alone (≈05:45–06:00 and 18:00–18:15). Theme is dark when time < 06:00 or ≥ 18:30.
- **Type:** `--font-display` Fraunces (custom instance: opsz 72; roman SOFT 50; italic SOFT 100 WONK 1; wght 300–800) · `--font-sans` Instrument Sans · `--font-mono` JetBrains Mono · `--font-symbol` for arrows (the latin subsets omit ← → ↗). Scale `--step--2 … --step-5`, `--step-hero`.
- **Space:** `--sp-3xs 4 · 2xs 8 · xs 12 · s 16 · m 24 · l 32 · xl 48 · 2xl 64 · 3xl 96 · 4xl 128`, `--sp-section`, `--gutter`, `--max 1320px`.
- **Radius:** `--r-xs 4 · s 8 · m 14 · l 22 · xl 32 · pill`.
- **Shadow:** `--sh-1` rest · `--sh-2` card · `--sh-3` hover · `--sh-4` dragged/dialog; x-offset follows `--light-x` (sun position), colour `--shadow-rgb`, strength `--shadow-a`.
- **Motion:** `--ease-out`, `--ease-in-out`, `--ease-spring`, `--dur-1 120ms · 2 220ms · 3 420ms · 4 700ms · 5 1100ms`, `--stagger 70ms`, `--dur-theme`, `--lift`. Reduced motion zeroes them (plus a global safety net in `base.css`).
- **Breakpoints:** 480 · 768 · 1024 · 1280 · 1600. **Layers:** `--z-desk 1 · --z-raised 10 · --z-nav 50 · --z-toast 80 · --z-dialog 100`.

## File tree
```
index.html                       nav · sky hero · work grid (+ "See all projects" link) · about band · desk (+ booklet & CV dialogs) · footer
projects.html                    All projects: filters, search, grid/list, Quick look dialogs (generated, see Conventions)
case-study-ota.html              case-study template (×3, identical structure)
case-study-data-sharing.html
case-study-accident.html
case-study-grocery.html          Selorg Tech (current role): grocery dark-store platform (4 apps)
case-study-mineral.html          Mineral Bridge: verified mineral trading, web + mobile (from Jana's artifact; generator gen_case_mineral.py kept outside the repo)
case-study-builtglory.html       BuiltGlory: customer app (96-screen prototype) + admin console (generator gen_case_builtglory.py + shared casegen.py, outside the repo)
case-study-rider.html            Selorg Rider v2: delivery partner app (generator gen_case_rider.py)
case-study-bkkk.html             BKKK Casino (app + operations console): sportsbook + casino mobile app (artifact shared from another account; source docs marked Confidential → [CONFIRM NDA-SAFE]; generator gen_case_bkkk.py)
case-study-template.html         blank template for new projects (noindex, not deployed)
404.html
css/tokens.css                   every token, day/night, islands, reduced motion
css/base.css                     fonts, reset, focus, buttons, chips, eyebrow, .ph placeholders, utilities
css/layout.css                   nav, sections, footer, toast, reveal, theme cross-fade
css/sky.css                      interactive sky (hero + .sky--compact)
css/work.css                     bento grid, cards, previews A–D, fields, switch, about band
css/desk.css                     desk, paper objects, lamp, dialogs (booklet, CV)
css/booklet.css                  the booklet as a book: paper grain, page stack, 3D page turns + shading, curled corner, index tabs, ribbon, folios, page-content entrances (overrides desk.css)
css/case-study.css               case-study template, annotations, prototypes, next card; ends with the "light & tide" screen animations
css/about.css                    About band: Designer ↔ Developer switch, flip card (design board / code), skill stickers, doodles
css/projects.css                 All projects page: toolbar, grid/list cards, previews, Quick look dialog
css/motion.css                   decorative motion: hero entrance, ribbon, word-rise + squiggle, desk landing, lamp flicker, view transitions
js/main.js            entry: inits whatever the page contains (data-* hooks; lazy imports)
js/config.js          contact details, URLs, flags  ← fill placeholders here
js/time-state.js      time-of-day store, localStorage (jana.sky.v1), live/manual, theme, pub/sub
js/sky-palette.js     sky keyframes, OKLab/sRGB mixing, contrast picker (pure, Node-importable)
js/sky.js             sun/moon drag on the arc, range input, readout, hint, "↺ Now"
js/sky-craft.js       home hero only: shaded, realistic jets by day, a hot-air balloon at golden hour (06:00–07:30, 17:00–18:30; 70 % of spawns) and alien saucers by night (follow the sky time), crossing slowly (jet 25–32 s, balloon 55–70 s, saucer 35–45 s with a hover); the saucer shines a light ray below it; click one and it reacts (jet: missiles → fire, sparks and smoke; saucer: laser → ripple on the sea; balloon: burner flares and it climbs). At night the lighthouse searchlight sweeps the sky (on its own ~6–10 s after a saucer appears and every 12–18 s, or when the lighthouse is clicked) and can catch the saucer, which lights up, flashes back, kills its ray and darts away; shooting stars streak by every 5–11 s (click one: sparkle + a "wish made" toast). Clicks on plain headline text over a craft or shooting star also count (crosshair cursor). Decorative, aria-hidden, pointer-only; off under reduced motion, off-screen or hidden tab. Styles at the end of css/sky.css
js/delight.js         "Click me 👆" confetti + toast
js/nav.js             sticky nav, active section, theme toggle, résumé availability check
js/reveal.js          scroll-reveal (IntersectionObserver, motion-safe)
js/toast.js clipboard.js dialog.js   shared helpers
js/work.js            "Ask me about this" → prefilled letter; live design-system card
js/desk.js            desk tilt + drag + tidy, lamp switch, booklet (3D turns, drag/swipe a page, corner, tabs, ribbon swing, keys ← → Home End 1–5, injected running header/folios, skills as chips)
js/contact.js         masked email/phone, copy, LinkedIn/profile links, letter validation + mailto, Chennai clock
js/prototypes.js      interactive case-study mockups + sticky contents highlight
js/about.js           About band: mode switch + flip (hidden face inert), typewriter, doodle draw-in + drift, card tilt, draggable skill stickers (pointer + arrow keys, Esc/double-click resets)
js/projects.js        All projects: filter/search/layout (kept in the URL), view-transition shuffles, stagger entrance, Quick look carousel
js/screens.js         case-study screens "light & tide": beam sweep + develop, phones surface from a waterline, sun-driven glare
js/motion.js          word-rise headings, count-up numbers, card tilt + spotlight, desk landing, nav sun spin
assets/fonts/         woff2 + LICENSE-fonts.txt
assets/og/ assets/icons/         generated by scripts/og.mjs
assets/case-builtglory/          BuiltGlory app screens (480 px, corners masked); admin screens live in assets/projects/
assets/case-rider/               Selorg Rider v2 screens (480 px, corners masked)
assets/case-bkkk/                BKKK Casino ops-console screens (ops-*, 1600 + 800), prototype cover (1600 + 800) and app screens (480 px, corners masked)
assets/case-mineral/             Mineral Bridge web screens (1600 + 800) and app screens (480 px, corners masked)
assets/case-grocery/             Selorg platform screens as AVIF/WebP + JPG/PNG fallback; desktop shots also at 640 px
assets/projects/                 screens for the All projects page (RoofTop Solar, BuiltGlory, Chedi, Selorg web store + Rider): 1600 + 800 px AVIF/WebP/JPG; Rider phone 480 px PNG/WebP/AVIF
assets/Janarthanan_V_Resume.pdf  the résumé (supplied by Jana)
scripts/              dev-only QA (own package.json; excluded by .vercelignore)
  shots.mjs           screenshots: --pages --widths --times --full
  a11y.mjs            axe (all pages, both themes, dialogs), sky sweep, tab walk, reduced motion, touch, links
  og.mjs              OG images (from the real heroes) + PNG icons
  desk-check.mjs annot-check.mjs motion-check.mjs   focused visual checks (motion-check: intro frames, landing, tilt)
```

## Conventions
- **CSS:** component classes with `__element` / `--modifier` (`.card__title`, `.btn--accent`). Logical properties. Mobile-first media queries at the breakpoints above; container queries (`container: card`) for card internals. Each section owns its file.
- **JS:** one feature per ES module exporting `init…(root)`; `main.js` calls it only if its `[data-…]` hook exists (work/desk/contact/prototypes are lazy-loaded). No globals, no dependencies. Shared state goes through `time-state.js` (`subscribe(fn)`).
- **HTML:** content lives in the HTML (SEO), not JS. Decorative SVG/emoji get `aria-hidden="true"`; static mockups are `role="img"` with an `aria-label` plus a visible "Illustrative recreation" caption. Interactive prototypes use real tables/buttons and a polite `[data-live]` region.
- **Cards:** stretched-link pattern — one real `<a class="card__link">`; `::after` covers the card; extra controls sit above it (`z-index: var(--z-raised)`); the card shows the focus ring via `:has(.card__link:focus-visible)`.
- **Dialogs:** native `<dialog data-dialog>` opened by `[data-dialog-open="id"]` (see `js/dialog.js`): Esc and backdrop close, page inert, focus returns to the trigger.
- **Motion inventory** (all off under `prefers-reduced-motion: reduce`; `js/motion.js` then does nothing and the DOM stays untouched):
  sunrise intro (sun/moon rises from the horizon to the current time, `sky.js` `playIntro`, cancelled by any drag/slider input) · hero copy rises in sequence, sticker pops, sky ticket slides up · practice ribbon marquee (decorative, `aria-hidden`, pauses on hover) · `[data-split]` headings: words rise (`load` = on page load, otherwise on scroll) and a hand-drawn `.squig` draws under the accent word · `.stat__num`/`.stat-card__num` count up when 60 % visible (final value is in the DOM at rest; digits stay real text) · cards tilt ≤ 2° toward a fine pointer with a sun-tinted spotlight · desk objects land in sequence the first time the desk is seen · lamp flickers when night falls · nav sun turns with scroll · All projects: cards rise in a stagger as they scroll in, filter/search/layout changes run in a same-document View Transition (cards glide; fallback: new cards pop), the count bumps, Quick look sheets spring in and their screens slide · **Sky craft** (`js/sky-craft.js`): one craft at a time slowly crosses the hero sky, a few seconds apart — by day a shaded fighter jet (afterburner flicker, blinking nav light and strobe, a contrail that spreads and fades); by night a metallic saucer (glass dome, glowing core, chasing rim lights, gentle wobble) that drifts, hovers mid-sky and casts a faint under-light ray (fanning shafts via `@property --ray-a`, rising motes; kept faint because it can pass behind the hero copy); clicking fires (two missiles with exhaust trails → fireball, sparks, smoke puffs; the saucer's ray flares and a laser hits the sea); the hero copy passes clicks over a craft through (skipping links, buttons, sun/moon and the time panel); when day turns to night the current craft hurries off · **Golden-hour balloon**: sways, its burner fires every few seconds; a click makes it roar and climb · **Lighthouse searchlight** (night): the sea beam (`.g-beam`) fades and a long cone (`.searchlight`, JS-rotated from the `.g-lamp` position) sweeps right → up → left and back; if it crosses the saucer it locks on, the saucer gets `.is-spotted` (brightened, rim lights flash, ray off) and dodges via a `translate` animation on `.craft` (separate from the flight `transform`), then the beam loses it and sweeps on; the lighthouse click area (`.lighthouse-hit`, over `.g-lighthouse`) shows only at night and when the lighthouse is on screen (it is cropped off on phones) · **Shooting stars** (`.meteor`, when `--star-alpha` > 0.6): head + fading tail, sometimes in pairs; a 56 px hit area round the head · **Booklet** (`css/booklet.css`, `js/desk.js`): pages turn on the spine in 3D with shading and a shadow on the page beneath; a page can be dragged/swiped; the ribbon swings on each turn; timeline items, skill chips, certificate “stamps” and pillars arrive as a page opens; the cover title has a foil sweep and a slowly turning sun; phones hide the ribbon and corner (swipe instead) · **About band** (`js/about.js`): the Designer/Developer switch flips a card between a mood board and the `.jana {}` code (typed out the first time), swaps the accent word into code type and lays a code grid over the paper; doodles and the research → systems → UI sketch draw in; doodles drift and the card tilts with a fine pointer; skill stickers (`.skill-sticker`, not `.sticker`, which is the hero’s “Click me” pill) can be dragged and put back; the designer ↔ developer phrasebook cards flip on click and all follow the mode switch (flipped = mode XOR pressed); the summary's words light up as you scroll (`animation-timeline: view()`); the Based-in fact shows live Chennai time; the switch leans toward the pointer · **case-study screens ("light & tide", `js/screens.js` + end of `css/case-study.css`)**: desktop screens, the cover and HTML recreations are revealed by a beam of light that comes from the sun's side (`--light-x`; at night from the right, where the lighthouse stands) while the print "develops" from washed-out to full colour; phone screens surface from a waterline, bob once and leave two ripples; screens in a gallery light one after another and their captions follow; annotation pins pop like beacons after the beam; phone galleries drift with scroll (`animation-timeline: view()` where supported); once lit, a soft glare on each desktop screen follows the sun as it's dragged, and the pointer on hover. JS marks screens with `data-light="sweep|tide"` (never `data-screen`, which the accident prototype uses) and observes each screen's container (a fully clipped element never reports as visible); the hidden start states apply only under `html.screens-on`, which is never set with reduced motion · cross-page View Transitions: card titles and next-case titles share `view-transition-name` (`cs-ota`, `cs-share`, `cs-accident`) with each case-study `<h1>`; names must stay unique per page.
- **Hero layering:** `.hero__inner` has `pointer-events: none` (only `.hero__copy` re-enables) so the sun/moon below stay grabbable — keep it that way.
- **OTA = ROTA at Regami Solutions:** live product https://www.regamiota.com/ (hero `.cs-live` link and a `.card__extlink` on the home card). Real screens from the ROTA site in `assets/case-ota/` (1600 + 800 px). Figures inside those marketing screens are demo data, never quoted.
- **Selorg work:** the grocery platform is card 2 in the Work grid ("Now" badge) with its own case study; images in `assets/case-grocery/`. "Next case study" loop: OTA → Data Sharing → Accident → Grocery → Mineral Bridge → BKKK Casino → BuiltGlory → Selorg Rider → OTA (each generator sets its own next card).
- **Home Work grid = only projects with real data** (Jana's request): OTA (xl) → Selorg platform (xl) → Mineral Bridge (xl) → BKKK Casino (xl) → RoofTop Solar (l) + BuiltGlory (m) → Regami research (xl), then the "See all 17 projects" link. Flyweis, Accident, Data sharing and the Design system live on `projects.html` only. RoofTop/BuiltGlory home cards link to `projects.html#p-<slug>`, which scrolls to that card and opens its Quick look (after the incoming page transition; `js/projects.js`).
- **Jana's role on every project from the Claude artifacts:** UX/UI Executive (her words). Shown as "My role" in each Quick look and on the Nutsora card. Her Selorg job title elsewhere stays "UX Executive" unless she changes it.
- **All projects page (`projects.html`):** 17 projects in the same "real first" order. Written by a one-off generator (`gen_projects.py`, kept outside the repo); edit `projects.html` directly for small changes. Each `<li class="card pj">` carries `data-cats` (case · dashboard · mobile · web · research · system), `data-search` (lower-case text) and a unique `view-transition-name: pj-<slug>`; counts in the filter chips, hero meta and the home "See all" link (17) are static, so update them together. The live design-system components (`[data-ds]`, wired by `js/work.js`) now sit in the Design system Quick look (`<dialog … data-work>`). Case-study cards link to their page; projects without a page open a Quick look `<dialog class="ql" data-dialog data-ql>` (scroll-snap gallery, "What's in it", facts with the role "UX/UI Executive"). Projects from Jana's Claude artifacts are described only from what those prototypes show; their numbers are sample data and are never quoted as outcomes ("Screens from the prototype · sample data"). Left out on purpose: waiterX POS maps and Nutsora UI fixes (Jana asked to remove them), the four empty "Untitled" designs, and engineering/code-review/status reports.
- **No Crestro content:** Jana asked for none. Don't add Crestro projects, links or experience. Exception: Mineral Bridge, which Jana sent herself as one of her projects (Nov 2026).
- **Case-study pages** (all four) are authored and complete, with no placeholders. Structure (sections appear only when there is real material): hero (strip, outcome-led `<h1>`, outcome line, facts-only meta) → cover (mockup `.cs-mockcover` or screenshot) + glance → `#overview` (introduction, my role) → `#challenge` (sourced `.cs-quote`, paragraph, "What made it hard" `.constraints`) → `#goals` (business / people using it) → `#solution` (annotated recreation for Data Sharing and Accident; real ROTA screens for OTA; numbered `.solution`s with `.gallery` of real screens, "What's in the design" and "Why it matters", prototype links) → `#details` (optional) → `#results` (only real numbers: OTA, Data Sharing, Accident) → `#next` (next steps) → next-case card.
- **Sourcing rule for case-study copy:** every sentence comes from (a) Jana's brief/résumé, (b) the published product sites and prototypes: regamiota.com for ROTA (OTA) and the Selorg platform's prototypes (their own copy, flows and screens), or (c) describes what the design visibly does. Never add research findings, user quotes, participants, test results, team names, timelines or metrics that weren't supplied; add those sections back only when Jana provides real data. Demo figures inside prototypes (orders today, vault value…) are not facts.
- **Prototype screens:** captured from the Selorg prototypes at 2× with Playwright, phones masked to the device corners (transparent AVIF/WebP + PNG fallback, 480 px wide, `.shot--phone.shot--tight`); desktop screens at 1200 + 640 px (AVIF/WebP/JPG).
- **Image slots:** `.slot` figures show the file they want (`assets/case-<slug>/cover|journey-1..4|problem-1..2|research|solution-1..4|testing`) with a commented `<picture>` to paste in. Replace the `.slot__frame` div with the `<picture>` and keep the `<figure>`.
- **Adding a project:** copy `case-study-template.html` to `case-study-<slug>.html`; fill the `[ADD]` tags; give the `<h1>` a unique `view-transition-name` and use the same name on the new Work card title; set `next_*` links so the chain of "Next case study" stays a loop; put images in `assets/case-<slug>/`; add a card to the Work grid in `index.html`, a `<url>` to `sitemap.xml`, and an entry to `scripts/og.mjs`; remove the `noindex` meta.
- **Placeholders:** `<span class="ph">[PLACEHOLDER: …]</span>`, `[ADD: …]` or `[CONFIRM …]`; block slots use `.ph-block` (screenshot slots include commented `<picture>` markup). Register each one below.
- **Images:** `<picture>` with AVIF → WebP → PNG/JPG, explicit `width`/`height`, `loading="lazy" decoding="async"` below the fold. Convert with e.g. `npx sharp-cli -i in.png -o out.avif`.
- **Domain:** absolute URLs use `https://YOUR-DOMAIN.vercel.app`. Swap everywhere with:
  `grep -rl 'YOUR-DOMAIN.vercel.app' . --exclude-dir=scripts --exclude-dir=.git | xargs sed -i 's#https://YOUR-DOMAIN.vercel.app#https://your.real.domain#g'`

## Run & QA
- Local: `npx serve .` (project root) → http://localhost:3000
- QA: `cd scripts && npm install`, start `npx serve .. -l 3000`, then `node a11y.mjs`, `node shots.mjs [--full]`, `node og.mjs` (re-run after hero changes). Output → `qa/` (git-ignored).
- Lighthouse: `CHROME_PATH=/opt/pw-browsers/chromium npx lighthouse http://localhost:3000/ --chrome-flags="--headless=new --no-sandbox"`.
- Last QA (All projects page): a11y suite all-pass on 7 pages incl. projects.html; axe 0 inside open Quick looks (day/night); projects.html Lighthouse mobile 95/100/100/100.
- Earlier QA (Phase 4): axe 0 violations on all pages × day/night × booklet pages/CV/letter errors; sky sweep worst text 5.05:1, worst accent heading 3.26:1; all tab stops visible with focus rings; reduced motion, touch drag + scroll, links OK. Lighthouse home mobile 98/100/100/100, desktop 100/100/100/100; OTA case mobile 97/100/100/100. After the motion pass: suite still all-pass, axe 0 with motion on, home mobile 98/100/100/100.

## Placeholder register (keep in sync)
| Where | Item | Status |
|---|---|---|
| `js/config.js` `SITE_URL` + `<head>` tags, sitemap, robots, JSON-LD | Real domain | [PLACEHOLDER] |
| `js/config.js` `LINKS.linkedin`, desk stamp, JSON-LD `sameAs` | LinkedIn URL | ✓ janarthanan-v-04a07b367 |
| `js/config.js` `LINKS.whatsappConfirmed` | Is +91 7010399595 on WhatsApp? | ✓ yes (business card links to wa.me) |
| `js/config.js` `LINKS.behance` / `dribbble` | Profile URLs (or leave empty) | optional |
| `assets/Janarthanan_V_Resume.pdf` | Résumé PDF | ✓ supplied Nov 2026 (booklet, CV and About updated from it: Selorg bullets, MBA pursuing, skills) |
| `MISSING-INFO.md` | Fill-in questionnaire for every open item (not deployed) | open |
| index · About facts, booklet Experience, CV sheet | Selorg Tech role title | ✓ UX Executive |
| index · booklet Experience, CV | Experience descriptions written from résumé facts + confirmed Selorg/ROTA work; Jana to review, add real Selorg results if any | review |
| projects.html · Flyweis card | NDA-safe to show the three numbers | ✓ cleared by Jana |
| case-study-bkkk.html, projects card | BKKK Casino: source docs marked Confidential | ✓ cleared by Jana for publishing |
| projects.html · Quick looks | Role on artifact projects | ✓ UX/UI Executive |
| projects.html · artifact projects | OK to show client work publicly | ✓ cleared by Jana |
| case studies | Written from available sources; can be strengthened with real research, testing, team, tools, OTA company, and outcomes for the Selorg work | optional |
| `MISSING-INFO.md` | The questionnaire for all of the above, in page order | open |

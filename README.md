# Jana · UI/UX Designer — portfolio

Hand-built static site: HTML, CSS custom properties and vanilla ES modules. No framework, no build step.

## Run locally
```bash
npx serve .
```
Open http://localhost:3000.

## Deploy (Vercel)
Import the repo in Vercel with **Framework preset: Other**, no build command, output directory `.` — or run `npx vercel` from this folder. `vercel.json` adds caching and security headers; `.vercelignore` keeps the QA tooling out of the deploy.

## Fill in your details
1. `js/config.js` — LinkedIn URL, WhatsApp confirmation, optional Behance/Dribbble, domain.
2. Drop your résumé at `assets/Janarthanan_V_Resume.pdf`.
3. Search the HTML for `class="ph"` / `ph-block` — every highlighted `[PLACEHOLDER]`, `[ADD: …]` or `[CONFIRM …]` needs real content.
4. Replace the domain placeholder (command in `CLAUDE.md`).

## Add a new case study
1. Copy `case-study-template.html` to `case-study-<name>.html` and replace every `[ADD: …]`.
2. Put the images in `assets/case-<name>/` (file names are listed in each image slot) and swap each slot for the `<picture>` snippet in its comment.
3. Add a card for it to the Work grid in `index.html`, and a line to `sitemap.xml`.
4. Remove the `noindex` meta from the new page.

Or send the answers from `MISSING-INFO.md` (section 2) plus the images, and it gets built for you.

## QA tooling (optional, dev-only)
```bash
cd scripts && npm install
```
With the local server running (`npx serve .. -l 3000` from `scripts/`):

- `node a11y.mjs` — axe on every page in day and night (dialogs open too), a contrast sweep of the sky across all 96 quarter-hours, a keyboard tab walk, reduced motion, touch drag, links.
- `node shots.mjs --full` — screenshots at 360 / 768 / 1280 / 1920 px, day and night, into `qa/shots/`.
- `node og.mjs` — regenerates the social images (from the real heroes) and app icons.

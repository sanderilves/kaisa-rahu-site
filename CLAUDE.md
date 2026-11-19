# CLAUDE.md – Kaisa Rahu, personal trainer landing page

Separate project. **Nothing to do with Ilves Coaching (ilvescoaching.ee)**: don't reuse its content, brand, domain, contacts or repo.

## What this is
One-page bilingual site (ET primary, EN full copy) for **Kaisa Rahu**, personal trainer in Tallinn.
Two jobs: introduce Kaisa, and send visitors to **Cal.com** (`cal.com`, username `kaisarahu`) to book a personal training slot at one of three gyms.

## Decisions (fixed)
| Topic | Decision |
|---|---|
| Booking | Cal.com (`https://cal.com/kaisarahu/<slug>`), one event per gym: Kristiine `https://cal.com/kaisarahu/kristiine-pt`, Rocca al Mare `https://cal.com/kaisarahu/rocca-pt`, Järve `https://cal.com/kaisarahu/jarve-pt`. Opens in a **new tab**, never embedded |
| Languages | ET (`/`) + EN (`/en/`), plain-link ET/EN switch |
| Contact | Booking + `mailto:` + Instagram. **No contact form** |
| Prices | Shown (B2C), no payments on the site. MyFitness prices are final, incl. VAT (24%). Plans: running 75 €, triathlon 100 € – final price (Kaisa not VAT-registered; confirm). If she becomes VAT-registered, show VAT-inclusive prices. Gym-entry rule shown under the price list and in the FAQ. Plans are ordered via the contact email. Not in JSON-LD yet |
| Cookies / analytics / 3rd-party scripts | **None**. No cookie banner |
| Stack | Plain HTML + CSS + tiny vanilla JS. No frameworks, npm or build step |
| Fonts | Self-hosted woff2 in `/assets/fonts/` (Bricolage Grotesque headings, Manrope body, OFL). **Never Google Fonts** |
| Colours | One accent family (light blue). Tokens in `:root`: `--bg` #FFF8F3 (cream), `--surface` #FFF, `--line` #EEE2D8, `--ink` #0F2A3D (deep navy: text, headings), `--muted` #4A5D6B, `--accent` #6EC1F2 (light blue: button backgrounds, step numbers), `--accent-hover` #4FB0EA, `--accent-ink` #0B6FB0 (blue for text on light backgrounds: links, eyebrows, experience years, FAQ "+", list markers, icon strokes), `--accent-tint` #DCEFFC (icon circles, pills), `--alt-bg` #EEF7FD (`.section-alt`), `--dark` #0F2A3D (contact section), `--dark-2` #0A1D2B (footer), `--focus` #0F2A3D (3px outline + offset; must differ from the button colour). Photo placeholder gradient `--dark` → #1F5F8B. theme-color stays cream. **Light blue buttons always use navy text (`--ink`), never white; blue text uses `--accent-ink`.** No violet/plum, no orange/coral, no extra tints. `.ph` yellow is a dev marker, not palette |

## Coach facts (only these; don't invent others)
- Name: Kaisa Rahu – personaaltreener / personal trainer
- Gyms: MyFitness Kristiine, MyFitness Rocca al Mare, MyFitness Järve (Tallinn)
- Languages: Estonian, English (*to confirm*)
- Instagram: https://www.instagram.com/kaisarahu
- Email: kaisa.rahu@myfitness.ee (confirmed, used on all pages incl. privacy) · Phone: **not shown** on the site (removed at the owner's request; keep it off pages and JSON-LD)
- Experience (shown in About): 2025–present triathlon coach, UP43 · 2024–present personal trainer, MyFitness Estonia (focus: improving athletic performance) · 2022–2024 altitude training coach (hypoxic chamber), TCR Sport Lab · 2022–2024 strength and conditioning coach, Rise Athlete · 2020–2022 personal trainer, MyFitness Estonia · 2019–2020 personal trainer, Balance Gym · 2019–2020 group trainer, F45 Training U Street
- Specialties: Jõutreening / Strength training · Lapseootel ja sünnitusjärgne treening / Prenatal and postnatal training · Personaaltreening noortele / Personal training for young people · Rühi ja liikuvuse parandamine / Posture and mobility · Treeningud alustajale / Training for beginners · Jooksukavad / Running plans · Triatlonikavad / Triathlon plans (remote plans, ordered by email, priced in `#hinnakiri` / `#prices`)

## Files
```
/index.html               ET (primary)
/en/index.html            EN
/privaatsus/index.html    Privacy ET
/en/privacy/index.html    Privacy EN
/assets/css/style.css
/assets/js/main.js        mobile nav only
/assets/fonts/            woff2 + OFL licences
/assets/img/              favicon.svg, og-image.png (1200×630), photos as webp with width/height
/robots.txt, /sitemap.xml
```
Internal page links are **relative** to the page's folder (e.g. `en/`, `../`, `privaatsus/`, `../#asukohad`), never root-absolute (`/en/`) and never `index.html`, so the site works under a subpath (GitHub Pages: sanderilves.github.io/kaisa-rahu-site/), locally and on the final domain. Canonical/hreflang/og URLs stay absolute.
Asset references (CSS, JS, fonts, images) are **relative** (`assets/…`, `../assets/…`, `../../assets/…`; fonts in CSS as `../fonts/…`) so pages also render when opened directly from disk.

## Page structure (identical ET and EN, same order, same IDs where possible)
Header (text logo, anchor nav, ET/EN) → Hero (H1 + line + CTA to `#asukohad` / `#locations`) → Specialties (7 cards + "Pole kindel"/"Not sure" card = 8; 1 column on mobile, 2 at ≥640px, 4 at ≥1100px) → Price list (`#hinnakiri` "Hinnakiri" / `#prices` "Price list": Block A personal training at MyFitness (full list); Block B individual training plans 75 € / 100 €; prices only: no buttons or notes in the cards; one muted note below both cards (MyFitness prices incl. VAT + gym entry not included); 2 cards side by side at ≥800px; nav link "Hinnakiri"/"Prices" after "Treeningud"/"Training"; no nutrition counselling unless Kaisa holds the qualification) → Locations/booking (3 gym cards: Kristiine, Rocca al Mare, Järve; 1 column on mobile, 3 columns at ≥1000px with rows aligned via subgrid. Each card: gym name, address, map link, 'Vali aeg' button (Cal.com, new tab; no visible new-tab hint, only the visually-hidden text + ↗ icon). No times, length or entry info on the site: Cal.com shows those.) → How booking works (3 steps) → About (bio + qualifications) → FAQ → Contact → Footer.

Section IDs: ET `treeningud`, `hinnakiri`, `asukohad`, `kuidas`, `minust`, `kkk`, `kontakt` · EN `training`, `prices`, `locations`, `how`, `about`, `faq`, `contact`.

## Sync rule
**Every change is made on both ET and EN pages** (and both privacy pages). Sections, order, CTAs and Cal.com links must match.

## Copy rules
- Estonian written natively, informal *sina*. Flag unsure terms with `<!-- CHECK TERM: ... -->`.
- Warm, encouraging, competent. Short sentences, concrete benefits, no hype.
- No guaranteed results, no health/medical claims (esp. prenatal/postnatal). Testimonials only if real ones are supplied.
- MyFitness named only as a location ("MyFitness Kristiine"). No MyFitness logo, colours or wording implying an official page. Gyms are **not** her LocalBusiness in JSON-LD.

## Placeholders
Every open item is marked `<!-- TODO: ... -->` in HTML plus a visible placeholder (class `ph`, dashed outline). **Never put TODO inside JSON-LD.**
Global find-and-replace placeholders (values not confirmed yet):
| Placeholder | Meaning |
|---|---|
| `https://kaisarahu.ee` | Site domain (TODO #11). Replace everywhere incl. canonical, hreflang, og, JSON-LD, sitemap, robots |

## Temporary photos (published on the test site)
`/assets/img/kaisa-hero.webp` (hero, Ironman Kona medal photo, cropped 4:5 from git-ignored `hero.jpeg`; event photo with sponsor logos) and `kaisa-about.webp` (About, gym leg raise, credited to a photographer) were supplied by the site owner / Kaisa's Instagram and are committed and live on GitHub Pages at the site owner's request. Rights are not formally cleared and the gym photo shows the MyFitness logo: **replace them with rights-cleared photos before launch (TODO #6).** The source files (`hero.jpeg`, `temp-*.jpg`, saved `Instagram*.html` / `hero_photo*`) stay git-ignored; `temp-kaisa-myfitness.jpg` (MyFitness profile photo) is unused and must not be published.

## Open items (handover §4)
1 Bio adapted from Kaisa's text – awaiting approval · 2 Qualifications: supplied – confirm exact NASM certificate name (still never claim a nutrition cert) · 3 Brand/logo (text logo for now) · ~~4 Email~~ · ~~5 Phone~~ (done) · 6 Own photos with rights (never MyFitness photos) · 7 Session length + windows per gym · ~~8 Cal.com username + slugs~~ (done: username `kaisarahu`; https://cal.com/kaisarahu/kristiine-pt, https://cal.com/kaisarahu/rocca-pt, https://cal.com/kaisarahu/jarve-pt) · ~~9 Gym entry~~ (done: "Saali sisenemiseks on vaja liikmesust või ühekordset külastuspiletit." / "You'll need a membership or a single-visit ticket to enter the gym.") · ~~10 Cancellation rule~~ (done: 24 h) · 11 Domain + hosting · ~~12 Gym addresses~~ (done; source: myfitness.ee club pages, no shopping-centre names: MyFitness Kristiine – Endla 45, 10615 Tallinn; MyFitness Rocca al Mare – Haabersti 5, 13516 Tallinn; MyFitness Järve – Pärnu mnt 186, 11314 Tallinn) · H1 variant (using location-led one for now).

## Cal.com setup (done by Kaisa in Cal.com, reference only)
| Setting | Value |
|---|---|
| Calendar | Kaisa's **personal** Outlook: conflict check + destination calendar |
| Event types | Must: `kristiine-pt`, `rocca-pt`, `jarve-pt`, gym address as in-person location. Could: friend/small group (seats, max 4) |
| Availability | One schedule per gym (3), only that gym's windows |
| Buffers | 0 min within an event type |
| Travel | ≥45 min gap between windows at ANY two different gyms (Kristiine, Rocca al Mare, Järve), built into the schedules |
| Min notice / window | 12–24 h / 4 weeks |
| Questions | Name, email, phone (optional), "Training goal". **No health/pregnancy/injury questions** (GDPR special category) |
| Reminders | Email 24 h before |
| Cancellation | Cancellation/reschedule cut-off: 24 h (must match the FAQ). |
| Event descriptions | Each event description must state the session length and the gym entry rule (MyFitness membership or single-visit ticket). |
| Busy | Only Outlook events marked Busy block slots. Share MyFitness work calendar free/busy into personal Outlook if separate |
| Language | Check if booking page shows Estonian. If Cal.com doesn't show Estonian, consider adding a FAQ line. |

## Before every commit
- [ ] ET and EN in sync (sections, order, CTAs, gym links)
- [ ] Checked at 375px and 1280px; H1 + CTA visible without scrolling
- [ ] Each Cal.com link opens the right gym's event in a new tab
- [ ] Valid HTML, no console errors, images have alt + width/height
- [ ] JSON-LD 0 errors in Rich Results Test, no TODOs inside it
- [ ] No cookies set (DevTools → Application → Cookies)

# CLAUDE.md – Kaisa Rahu, personal trainer landing page

Separate project. **Nothing to do with Ilves Coaching (ilvescoaching.ee)**: don't reuse its content, brand, domain, contacts or repo.

## What this is
One-page bilingual site (ET primary, EN full copy) for **Kaisa Rahu**, personal trainer in Tallinn.
Two jobs: introduce Kaisa, and send visitors to **Cal.com** (`cal.eu`) to book a personal training slot at one of three gyms.

## Decisions (fixed)
| Topic | Decision |
|---|---|
| Booking | Cal.com EU (`https://cal.eu/<username>/<slug>`), one event per gym. Opens in a **new tab**, never embedded |
| Languages | ET (`/`) + EN (`/en/`), plain-link ET/EN switch |
| Contact | Booking + `mailto:` + Instagram. **No contact form** |
| Prices | Shown, incl. VAT. No payments on the site. Not in JSON-LD until VAT status and the MyFitness price list are confirmed |
| Cookies / analytics / 3rd-party scripts | **None**. No cookie banner |
| Stack | Plain HTML + CSS + tiny vanilla JS. No frameworks, npm or build step |
| Fonts | Self-hosted woff2 in `/assets/fonts/` (Bricolage Grotesque headings, Manrope body, OFL). **Never Google Fonts** |
| Colours | One accent only. Tokens in `:root`: `--bg` #FFF8F3 (cream), `--bg-alt` #F6F3FF (`.section-alt`), `--surface` #FFF, `--ink`/`--plum` #2A1F3D, `--muted` #5E5470, `--line` #EEE2D8, `--violet` #5B3DF5 (buttons, icons, links, eyebrows, markers), `--violet-hover` #4A2FD9, `--violet-tint` #EEEAFF (icon circles, pills), `--plum-dark` #1C1429 (footer), `--plum-soft` #4B3B78 (photo placeholder gradient only), `--focus` #2A1F3D (3px outline + offset; must differ from the button colour). **White text on violet.** No orange/coral, no extra tints. `.ph` yellow is a dev marker, not palette |

## Coach facts (only these; don't invent others)
- Name: Kaisa Rahu – personaaltreener / personal trainer
- Gyms: MyFitness Kristiine, MyFitness Rocca al Mare, MyFitness Järve (Tallinn)
- Languages: Estonian, English (*to confirm*)
- Instagram: https://www.instagram.com/kaisarahu
- Email: kaisa.rahu@myfitness.ee (confirmed, used on all pages incl. privacy) · Phone: **not shown** on the site (removed at the owner's request; keep it off pages and JSON-LD)
- Specialties: Jõutreening / Strength training · Lapseootel ja sünnitusjärgne treening / Prenatal and postnatal training · Personaaltreening noortele / Personal training for young people · Rühi ja liikuvuse parandamine / Posture and mobility · Treeningud alustajale / Training for beginners

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
Header (text logo, anchor nav, ET/EN) → Hero (H1 + line + CTA to `#asukohad` / `#locations`) → Specialties (5 cards) → Prices (`#hinnad` / `#prices`: Block A personal training at MyFitness with "Broneeri trenn" button; Block B individual training plans with "Telli e-postiga" mailto; 2 cards side by side at ≥800px; nav link "Hinnad"/"Prices" after "Treeningud"/"Training") → Locations/booking (3 gym cards: Kristiine, Rocca al Mare, Järve; 1 column on mobile, 3 columns at ≥1000px with rows aligned via subgrid. Each card: gym name, address, map link, 'Vali aeg' button (Cal.com, new tab + hint). No times, length or entry info on the site: Cal.com shows those.) → How booking works (3 steps) → About (bio + qualifications) → FAQ → Contact → Footer.

Section IDs: ET `treeningud`, `hinnad`, `asukohad`, `kuidas`, `minust`, `kkk`, `kontakt` · EN `training`, `prices`, `locations`, `how`, `about`, `faq`, `contact`.

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
| `https://cal.eu/kaisarahu/kristiine-pt` | Cal.com Kristiine event (TODO #8) |
| `https://cal.eu/kaisarahu/rocca-pt` | Cal.com Rocca al Mare event (TODO #8) |
| `https://cal.eu/kaisarahu/jarve-pt` | Cal.com Järve event (TODO #8) |

## Temporary photos (published on the test site)
`/assets/img/kaisa-hero.webp` (hero, outdoor portrait) and `kaisa-about.webp` (About, gym leg raise, credited to a photographer) come from Kaisa's Instagram and are committed and live on GitHub Pages at the site owner's request. Rights are not formally cleared and the gym photo shows the MyFitness logo: **replace them with rights-cleared photos before launch (TODO #6).** The source files (`temp-*.jpg`, saved `Instagram*.html` / `hero_photo*`) stay git-ignored; `temp-kaisa-myfitness.jpg` (MyFitness profile photo) is unused and must not be published.

## Open items (handover §4)
1 Bio adapted from Kaisa's text – awaiting approval · 2 Qualifications: supplied – confirm exact NASM certificate name (still never claim a nutrition cert) · 3 Brand/logo (text logo for now) · ~~4 Email~~ · ~~5 Phone~~ (done) · 6 Own photos with rights (never MyFitness photos) · 7 Session length + windows per gym · 8 Cal.com username + slugs · ~~9 Gym entry~~ (done: "Saali sisenemiseks on vaja liikmesust või ühekordset külastuspiletit." / "You'll need a membership or a single-visit ticket to enter the gym.") · ~~10 Cancellation rule~~ (done: 24 h) · 11 Domain + hosting · 12 Verify all three gym addresses (Endla 45; Paldiski mnt 102; Pärnu mnt 238) · H1 variant (using location-led one for now).

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

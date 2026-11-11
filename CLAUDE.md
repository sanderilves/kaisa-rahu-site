# CLAUDE.md – Kaisa Rahu, personal trainer landing page

Separate project. **Nothing to do with Ilves Coaching (ilvescoaching.ee)**: don't reuse its content, brand, domain, contacts or repo.

## What this is
One-page bilingual site (ET primary, EN full copy) for **Kaisa Rahu**, personal trainer in Tallinn.
Two jobs: introduce Kaisa, and send visitors to **Cal.com** (`cal.eu`) to book a personal training slot at one of two gyms.

## Decisions (fixed)
| Topic | Decision |
|---|---|
| Booking | Cal.com EU (`https://cal.eu/<username>/<slug>`), one event per gym. Opens in a **new tab**, never embedded |
| Languages | ET (`/`) + EN (`/en/`), plain-link ET/EN switch |
| Contact | Booking + `mailto:` + Instagram. **No contact form** |
| Prices / payments | **None** anywhere |
| Cookies / analytics / 3rd-party scripts | **None**. No cookie banner |
| Stack | Plain HTML + CSS + tiny vanilla JS. No frameworks, npm or build step |
| Fonts | Self-hosted woff2 in `/assets/fonts/` (Bricolage Grotesque headings, Manrope body, OFL). **Never Google Fonts** |
| Colours | Tokens in `:root`: `--bg` #FFF8F3, `--bg-alt` #FFF0E8, `--surface` #FFF, `--ink`/`--plum` #2A1F3D, `--muted` #5E5470, `--line` #EEE2D8, `--coral` #FF7A59, `--coral-hover` #F2603D, `--coral-ink` #B8452A, `--plum-dark` #1C1429, `--violet` #4B3B78, tints peach #FFE3D6 / lilac #ECE6FF / mint #D6F3E6 / butter #FFF1C7, `--focus` #5B3DF5. **Plum text on coral, never white.** Coral-coloured text on light backgrounds uses `--coral-ink` |

## Coach facts (only these; don't invent others)
- Name: Kaisa Rahu – personaaltreener / personal trainer
- Gyms: MyFitness Kristiine, MyFitness Rocca al Mare (Tallinn)
- Languages: Estonian, English (*to confirm*)
- Instagram: https://www.instagram.com/kaisarahu
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
Internal links go to `/` and `/en/`, never `index.html`.
Asset references (CSS, JS, fonts, images) are **relative** (`assets/…`, `../assets/…`, `../../assets/…`; fonts in CSS as `../fonts/…`) so pages also render when opened directly from disk.

## Page structure (identical ET and EN, same order, same IDs where possible)
Header (text logo, anchor nav, ET/EN) → Hero (H1 + line + CTA to `#asukohad` / `#locations`) → Specialties (5 cards) → Locations/booking (2 gym cards: address, map link, windows, entry note, "Vali aeg"/"Pick a time" → Cal.com, new tab + hint) → How booking works (3 steps) → About (bio + qualifications) → FAQ → Contact → Footer.

Section IDs: ET `treeningud`, `asukohad`, `kuidas`, `minust`, `kkk`, `kontakt` · EN `training`, `locations`, `how`, `about`, `faq`, `contact`.

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
| `tere@kaisarahu.ee` | Contact email (TODO #4) |

## Open items (handover §4)
1 Bio/approach · 2 Qualifications (make **no** claims; don't claim the nutrition cert) · 3 Brand/logo (text logo for now) · 4 Email · 5 Phone yes/no · 6 Own photos with rights (never MyFitness photos) · 7 Session length + windows per gym · 8 Cal.com username + slugs · 9 Gym entry wording for non-members · 10 Cancellation rule · 11 Domain + hosting · 12 Verify gym addresses (Endla 45; Paldiski mnt 102) · H1 variant (using location-led one for now).

## Cal.com setup (done by Kaisa in Cal.com, reference only)
| Setting | Value |
|---|---|
| Calendar | Kaisa's **personal** Outlook: conflict check + destination calendar |
| Event types | Must: `kristiine-pt`, `rocca-pt`, gym address as in-person location. Could: friend/small group (seats, max 4) |
| Availability | One schedule per gym, only that gym's windows |
| Buffers | 0 min within an event type |
| Travel | ≥45 min gap between Kristiine and Rocca windows, built into the schedules |
| Min notice / window | 12–24 h / 4 weeks |
| Questions | Name, email, phone (optional), "Training goal". **No health/pregnancy/injury questions** (GDPR special category) |
| Reminders | Email 24 h before |
| Busy | Only Outlook events marked Busy block slots. Share MyFitness work calendar free/busy into personal Outlook if separate |
| Language | Check if booking page shows Estonian; if not, keep the note on the ET page |

## Before every commit
- [ ] ET and EN in sync (sections, order, CTAs, gym links)
- [ ] Checked at 375px and 1280px; H1 + CTA visible without scrolling
- [ ] Each Cal.com link opens the right gym's event in a new tab
- [ ] Valid HTML, no console errors, images have alt + width/height
- [ ] JSON-LD 0 errors in Rich Results Test, no TODOs inside it
- [ ] No cookies set (DevTools → Application → Cookies)

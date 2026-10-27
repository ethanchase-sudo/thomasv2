# Handoff: Thomas E. Smith — Author Website

## Overview
A single-page website for **Thomas E. Smith**: Detroit-born survivor, educator, advocate for students with disabilities, and author of the memoir **_A Second Chance_** (Welcome to the Storm Publishing, Jan 6, 2026, 104 pp.). The site is about **the man first, the book second** (the book is still a major section). Its goals are to introduce Thomas, tell his story, sell the book, collect reviews and reader stories, and bring in speaking invitations.

The creative concept comes from the book cover's torn split, **storm → sunrise**, and from his line *"Our darkest moments do not **define** us — they **refine** us."* As the visitor scrolls, the page moves from night (navy) through dawn (rust/orange) into daylight (warm paper), and then back to night for the contact section and footer.

## About the Design Files
The files in this bundle are **design references created in HTML**. They are prototypes showing the intended look and behavior, not production code to ship as-is. The task is to **recreate this design in the target codebase's environment** using its established patterns. If no environment exists yet, use a static-friendly framework (e.g. Astro, Next.js static export, or plain HTML plus a small JS module) with real form handling.

## Fidelity
**High-fidelity.** Colors, typography, spacing, copy, imagery and interactions are final. Recreate them pixel-accurately.

**Copy rule:** all biographical and book facts come from the official book description and the author's existing bio. **Do not add invented facts, reviews, awards, or testimonials.** The Readers section deliberately has no fake reviews.

---

## Design Tokens

### Colors
| Token | Hex | Use |
|---|---|---|
| `--night` | `#070b14` | Page background, dark sections, footer |
| `--storm` | `#111b30` | Speaking/work section bg, gradient stop |
| `--steel` | `#2a3a5c` | Reserved |
| `--bolt` | `#d6e6ff` | Cool accent text on dark (kickers, date year) |
| `--ember` | `#e8792f` | Primary accent, CTA fill, labels on paper |
| `--gold` | `#f3b45a` | Accent on dark, CTA hover |
| `--paper` | `#f3ece0` | Light section bg; light text on dark |
| `--paper2` | `#e9dfcd` | Family & Roots section bg |
| `--ink` | `#16130f` | Text on light; For-You band bg |
| `--muted` | `#6b6257` | Secondary text on light |
| Body text on paper | `#3a332b` / `#3a2f24` / `#4a4138` | Paragraph tones |
| Rules on paper | `#cbbfa9`, `#c4b69d` | 1px dividers |
| Turn quote accent | `#8a2f08` | "refine" in the big quote (on light gold) |
| Turn quote text | `#1d0f06` | |

Gradients:
- **Relearn:** `linear-gradient(180deg, #070b14 0%, #111b30 30%, #3b2a3a 72%, #7a3f22 100%)`
- **Turn:** `linear-gradient(180deg, #7a3f22 0%, #c9692b 30%, #efb064 62%, #f3ece0 100%)`

### Typography (Google Fonts)
- **Display:** `Bodoni Moda`, weights 700–900, **italic** for every headline. Line-height .86–1, letter-spacing −.01em to −.03em.
- **Body:** `Newsreader`, 19px desktop / 17.5px mobile, line-height 1.6.
- **Labels:** `IBM Plex Mono`, 10.5–12px, uppercase, letter-spacing .14–.2em.

Scale (all use `clamp`):
| Element | Size |
|---|---|
| Hero name | `clamp(70px, 9.6vw, 168px)` |
| Date "04.13 / 1990" | `clamp(90px, 13vw, 210px)` |
| Section H2s | `clamp(48–56px, 5.4–6.6vw, 88–108px)` |
| Turn blockquote | `clamp(44px, 6.4vw, 104px)` |
| Relearn verbs | `clamp(38px, 5.2vw, 84px)` |
| Ledes | 20–24px |
| Nav links | 11.5px |

### Spacing, borders and shadows
- Content wrap: `width: min(1240px, 92vw)`. Side gutters for nav and hero: `4vw`.
- Section padding: 120–180px top/bottom.
- **No border radius** anywhere (sharp, editorial). Buttons are rectangles with 1px borders.
- Shadows:
  - Book cover: `0 40px 70px -20px rgba(40,25,10,.45)`
  - Polaroid frame: `0 30px 60px -25px rgba(40,25,10,.5)`
- Global film grain: a fixed SVG fractal-noise overlay at 7% opacity, `mix-blend-mode: overlay`.

### Buttons
- `.btn`: Plex Mono 12px uppercase, padding 15×24, 1px currentColor border, transparent background. On hover it fills with paper and the text turns ink.
- `.btn.fill`: ember background with `#160c04` text. On hover the background turns gold.
- The arrow `→` nudges 4px right on hover.

---

## Sections (top to bottom)

### 1. Nav (fixed)
- **Content:** "Thomas E. **Smith**" (italic Bodoni; "Smith" in ember), then links: About Thomas, His Story, Speaking, The Book, Readers, Contact, and a "Get the Book" fill button.
- **Default:** transparent, padding 22px 4vw.
- **After 60px scroll** (`.solid`): `rgba(7,11,20,.82)` background with 14px blur, padding 14px.
- **Over light sections** (`.light`): `rgba(243,236,224,.88)` background with ink text. Detection: any `.paper, .author, .readers, .turn, .meet` section whose rect spans y=70px.
- **Mobile (<900px):** only the Get-the-Book button remains.

### 2. Hero (100vh, min 720px)
- **Layers:**
  - Storm background: a crop of the cover's left half (`storm.png`) with a dark overlay and slight blur.
  - Dawn layer: `sunrise.jpg`, the Thomas portrait, `background-size: auto 112%`, anchored right-top, clipped by a **torn polygon seam** at about 52%.
  - Thin paper-colored seam strip (`#f6f1e7`) along the tear.
  - Top/bottom vignette.
- **Left column content:**
  - Kicker "DETROIT, MICHIGAN"
  - H1 "Thomas E." / "Smith" ("Smith" in gold)
  - Roles line "SURVIVOR · EDUCATOR · ADVOCATE · AUTHOR"
  - Tagline quote, with "define" struck through in ember and "refine" in gold
  - CTAs: "Meet Thomas →" (fill) and "Invite Thomas to Speak" (outline)
- **Bottom-right book card:** 58px cover thumbnail, "HIS MEMOIR · OUT NOW", "A Second Chance". It links to #book and sits on a blurred dark glass background.
- **Hero foot:** animated scroll drip line with "Scroll — from storm to sunrise", and "Faith · Family · Purpose".
- **Seam interaction:** a deterministic pseudo-random jagged polyline with 47 points. The seam x-position eases toward `50 + (mouseX/innerWidth − .5) × −6` (percent) with a 0.06 lerp per animation frame.

### 3. Meet Thomas (paper bg)
- **Layout:** grid 1.3fr / .7fr.
  - Left: H2 "A Detroit son. / A father. A teacher. / *A survivor.*" plus a lede paragraph.
  - Right: headshot, 4:5 crop, object-position center 20%.
- **Three pillars** below (3 columns with 1px rules), each with a mono label in ember:
  1. 01 Faith — "A turning point"
  2. 02 Family — "Pray together, stay together."
  3. 03 Purpose — "Pain into service"

### 4. His Story — The Night (night bg)
- A huge outlined date "04.13" (1.2px stroke `rgba(214,230,255,.55)`) with a solid "1990" in bolt plus glow.
- To the right is a log column with a 1px left rule, containing:
  - "FRIDAY · A YOUTH CENTER DANCE"
  - Two large paragraphs (24–34px)
  - One dim paragraph
- **Lightning flash:** a radial overlay animation runs for 1.6s each time the section is 40% in view.

### 5. Relearning (gradient bg, normal flow — not sticky)
- **Header row:** H2 "He had to learn it / all *again.*" ("again." in gold) and a lead paragraph.
- **Four-column grid:** *re*walk, *re*talk, *re*read, *re*write, each with an index number. Verbs are `white-space: nowrap`.
  - Unlit: text `rgba(243,236,224,.22)`.
  - Lit: paper text with a gold "re".
  - A 2px gold bar at the top of each column fills 0→100%.
- **Three milestones** below (dashed top rule): "Graduated high school", "Earned a college degree", "Educator & advocate for students with disabilities". They go from opacity .25 / translateY(16px) to 1 / 0 when lit.
- **Scroll logic:**
  - `p = clamp((innerHeight × .8 − rect.top) / (rect.height × .75), 0, 1)`
  - For verb `i`: `local = clamp((p − .1 − i × .14) / .14, 0, 1)`. The bar width is `local × 100%`, and the verb is lit when `local ≥ 1`.
  - Milestone `i` is lit when `p > .72 + i × .08`.

### 6. The Turn (dawn gradient)
- Centered blockquote: "Our darkest moments do not ~~define~~ us — they *refine* us." Followed by "— THOMAS E. SMITH".

### 7. Educator · Advocate · Speaker (`#work`, storm bg)
- **H2:** "The man who relearned to read *now teaches.*"
- **Grid:** `minmax(0,1.35fr) minmax(0,.65fr)`.
  - Left: `speaking.jpg` spanning 2 rows, min-height 520px, image absolutely filling the cell.
  - Right: copy, a themes list, and the "Invite Thomas to Speak" CTA. Below that, `classroom.jpg` at 4:3.
- **Captions:** mono gold text on a night tab at the bottom-left of each photo.
- **Themes:** Resilience after trauma · Faith through adversity · Advocacy for students with disabilities · Family as a foundation.

### 8. The Book (`#book`, paper bg)
- **Layout:** grid .85fr / 1.15fr.
- **Left:** cover (682×1024 ratio, max 440px), sticky at top:110px, with a mouse-tilt effect (`perspective(1200px) rotateY(±6deg) rotateX(±5deg)`, .5s ease).
- **Right:**
  - H2 "A Second *Chance*", a deck line, and two copy paragraphs (the official description).
  - A facts strip of 4 columns: Genre "Memoir · Nonfiction", Published "Jan 6, 2026", Length "104 pages", Publisher "Welcome to the Storm".
  - **Format toggle** (`#buy`): segmented control Paperback $19.99 / Ebook $9.99. It filters the retailer grid (3 columns).

| Retailer | Shown for | URL |
|---|---|---|
| Amazon | print + ebook | https://www.amazon.com/Second-Chance-Thomas-Smith/dp/1966612966 |
| Barnes & Noble | print | https://www.barnesandnoble.com/w/a-second-chance-thomas-e-smith/1108444046 |
| Bookshop.org | print + ebook | https://bookshop.org/p/books/a-second-chance-thomas-e-smith/ef97602b7b9dc16c |
| Apple Books | ebook | https://books.apple.com/us/book/a-second-chance/id6756897987 |
| Everand | ebook | https://www.everand.com/book/970472578/A-Second-Chance |
| Waterstones (UK) | print | https://www.waterstones.com/book/a-second-chance/thomas-e-smith/9781966612964 |

- Under the retailers: "Paperback ISBN 978-1-966612-96-4 · Prices vary by retailer".
- **Verse:** "I can do all things through Him who strengthens me." — Philippians 4:13.

### 9. Who it's for (ink bg)
- A giant ember opening quote mark, then the official "If you have ever faced…" paragraph, with "this book is for you." in gold.

### 10. Family & Roots (`#author`, paper2 bg)
- **Left:** a polaroid-style frame (white, 14px padding, 70px bottom, rotated −2deg) holding the headshot. Caption "Thomas E. Smith — Detroit, Michigan". An ember tag "SURVIVOR · EDUCATOR · AUTHOR" is rotated 3deg.
- **Right:**
  - H2 "The people / who held *him up.*"
  - Roles: SON / BROTHER / FATHER / GRANDFATHER
  - Bio paragraphs: parents, siblings, children and grandchildren, the Detroit upbringing
  - Two-column motto row: "In loving memory — De'Terrious Jerome Hayes" and "Why he wrote the book"

### 11. Readers (`#readers`, paper bg)
- **H2:** "Read it? Your words carry it *further.*"
- **Card 1 — Leave a review:** links to Amazon, B&N, and a Goodreads search.
- **Card 2 — Share your second chance** (dark card): a form with Name, Email and Story fields, all required. On submit the form hides and the message "Thank you. Your words have been received — and they matter." appears.

### 12. Contact + Footer (`#contact`, night bg)
- **Left:**
  - H2 "Bring the story *to the room.*" plus an intro line
  - **Topic radio list** (styled rows, 26px italic): Speaking invitation / Schools & youth programs / Book clubs & churches / Media & interviews
  - The checked row turns gold and indents 14px
- **Right:** a form with Topic (read-only, mirrors the selected radio), Name, Email, Organization (optional), and Message.
- **Footer:**
  - Giant outlined "A Second *Chance*" wordmark
  - Row: © 2026 Thomas E. Smith · section links · "Faith · Family · Purpose"

---

## Interactions & Behavior
- **Reveal:** elements with `.rv` fade and rise 28px (1s, `cubic-bezier(.2,.7,.2,1)`) on 15% intersection. Delay steps are .12s, .24s and .36s.
- **Hero load:** an `.on` class is added after 200ms.
- **Smooth scroll:** `scroll-behavior: smooth` for anchor links.
- **Overflow:** `html, body { overflow-x: clip }`. Use clip, not hidden, so sticky positioning keeps working.
- **Responsive (<900px):**
  - All grids collapse to 1 column.
  - Verbs go to 2 columns, facts to 2 columns, retailers to 2 columns.
  - The dawn layer drops to 35% opacity.
  - The hero book card moves to the bottom-left.

## State Management
- `format`: `'print' | 'ebook'` (default `'print'`). Filters the retailer list.
- `contactTopic`: string. Mirrors into the read-only Topic field.
- Form submitted flags (story form, contact form).
- **Forms are not wired yet.** Connect both to email or a form service (e.g. Formspree, Resend, or a serverless function) with validation and error states.

## Assets
| File | Source | Use |
|---|---|---|
| `assets/cover.jpg` (682×1024) | Official book cover (client supplied) | Book section, hero card |
| `assets/headshot.jpg` | Official author headshot (client supplied) | Meet, Family |
| `assets/storm.png` | Crop of the cover's left half | Hero storm layer |
| `assets/sunrise.jpg` (1122×1402) | AI-generated from the headshot | Hero dawn layer |
| `assets/speaking.jpg` (1400×932) | AI-generated from the headshot | Speaking section |
| `assets/classroom.jpg` (1400×933) | AI-generated from the headshot | Speaking section |

AI-generated portraits should be approved by the client before launch, or replaced with real photography. Export production images as WebP/AVIF with responsive `srcset`.

## SEO / Production notes
- Title: "Thomas E. Smith — A Second Chance". Add OG/Twitter cards using the cover image.
- Add `Person` and `Book` JSON-LD with ISBN 9781966612964 (paperback) and 9781966612971.
- Respect `prefers-reduced-motion`: disable the seam lerp, the flash and the reveals.

## Files
- `index.html`: full page markup plus inline interaction script
- `site.css`: all styles and tokens
- `assets/`: images listed above

# Tersa website: design spec & notes

Single-file static site (`index.html`, embedded CSS + ~60 lines of vanilla JS), deployed on Vercel. No build step, no frameworks, no third-party JS.

All website copy lives in `index.html`, one HTML comment per section (`<!-- 1. NAVIGATION -->` … `<!-- 13. FOOTER -->`).

## Sections (in order)

1. Nav: wordmark, 6 anchor links, "Book an intro call". Under 1000px wide the links move into a hamburger menu (Escape closes it).
2. Hero: trust line, H1, subheadline, two CTAs, and an abstract "studio console" illustration showing idea → 4 steps → Claude assist. It is decorative and not a real project.
3. Problem: 4 numbered cards.
4. Solution: positioning statement and a 5-item checklist.
5. Services: 4 cards. Each has a "Where Claude helps" footer and tags for its examples.
6. How we use Claude: a two-column panel (delivery process / inside products), the required sentence as a pull-quote, and 3 principle cards.
7. Process: 4 steps.
8. Work: 3 cards labelled "Example use cases" (situation / what Tersa does / where Claude helps), then a dashed placeholder for real portfolio items.
9. Why Tersa: 5 short cards.
10. About: founder card (initial avatar as a photo placeholder), approved founder text, fact tags.
11. FAQ: 6 `<details>` accordions that work without JS.
12. Final CTA: headline, both CTAs, and an inquiry form that opens a pre-filled email to hello@tersa.io.
13. Footer: brand, nav links, legal links, ©.

## Visual system (existing Tersa theme, unchanged)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#050510` | page background |
| aurora | indigo `#6366f1`, magenta `#d946ef`, sky `#38bdf8` radial glows | fixed backdrop |
| `--accent` | `#d946ef` | brand accent (wordmark dot, section labels, focus rings) **and the signal for Claude/AI**: only AI-related icons, the Claude checklist item and "Where Claude helps" labels are magenta |
| `--text` | `#f5f5f7` | headings, primary text |
| `--muted` / `--faint` | 74% / 60% white | body / meta text (both ≥ 4.5:1 on bg) |
| `--surface` | 3.5% white + 9% white border | cards |

- **Type:** Geist (800 for headings with −0.035 to −0.045em tracking; 400–600 for body). Geist Mono for tags, step numbers and meta labels. H1 uses `clamp(42px, 6.6vw, 76px)` and H2 uses `clamp(30px, 4.4vw, 48px)`. Body text is 16–19px.
- **Spacing:** max width 1160px. Side padding is 16px on mobile and 24px from 641px up. Sections have 80px vertical padding on mobile and 112px from 768px up. Cards have 18px radius and 28–32px padding.
- **Components:** pill buttons (solid white primary, outlined ghost, minimum 44px tall). Cards lift 3px on hover. Icon tiles are neutral, and magenta only for AI items. Green appears only as a status colour in the hero illustration. Tags are mono pills.
- **Motion:** fade-up on scroll, the pulsing Claude dot, hover lifts, smooth scroll. All of it is disabled under `prefers-reduced-motion`.
- **Breakpoints:** 560 / 700 / 860 / 1000 / 1100px. The layout is mobile-first and every grid collapses to one column.
- **Accessibility:** skip link, semantic landmarks, one H1, `aria-expanded` on the menu, visible focus rings, decorative SVGs set to `aria-hidden`, and the form announces errors through a `role="status"` message.

## SEO

- Title: "Tersa | Web apps, internal tools and AI features for small teams"
- Meta description: as specified in the brief.
- Canonical `https://tersa.io/`, Open Graph and Twitter tags, Organization JSON-LD (founder, founding date, email, `sameAs` tersa.solutions).
- Legal pages are `noindex` until they hold real content.

## Placeholders to fill

- `BOOKING_URL` in the script at the bottom of `index.html`. Put your Cal.com or Calendly link here and every "Book an intro call" button will open it. While it is empty, the buttons scroll to the inquiry form.
- `og:image` (commented out): add a 1200×630 `og.png`.
- `favicon.svg`: placeholder "T" mark.
- Founder photo (replace the "Z" avatar).
- "Selected work: coming soon" block in #work.
- `impressum.html`, `privacy.html`, `terms.html`: placeholder text only.

## Recommended next steps

1. **Impressum and Privacy Policy (do this before promoting the site).** Both are legally required for a German-operated site. The privacy policy should mention Vercel hosting logs and Google Fonts. Self-hosting the Geist fonts avoids the Google Fonts data-transfer question entirely.
2. **Booking calendar:** set `BOOKING_URL`.
3. **Form backend:** replace the mailto form with Formspree, or a Vercel function plus Resend, so inquiries arrive without the visitor needing an email app.
4. **Real work:** once a first project ships and the client approves, replace the placeholder with a short case study and screenshots.
5. **OG image and favicon:** a proper logo mark and share card.
6. **Domains:** 301-redirect tersa.solutions to tersa.io so both domains don't serve duplicate content.
7. **Analytics:** a privacy-friendly option such as Vercel Web Analytics or Plausible.
8. **Later:** a short blog or notes section on Claude-powered build patterns, which adds credibility and SEO.

## Design review: why every piece is there

Two audiences decide whether this page works: **(A)** a non-technical founder deciding whether to trust a new studio, and **(B)** a Claude Startups reviewer checking that Claude is central and described credibly. Every element has to serve at least one of them.

### Changed after review

| Was | Problem | Now |
|---|---|---|
| Shimmer line under the hero buttons | Left over from the coming-soon page. It sat under the CTAs as a stray line and did nothing. | Removed |
| Green "live" dot in the trust line | Implied a status ("available now") the text doesn't state. Decoration pretending to be information. | Removed |
| Icons in 4 colours (magenta, indigo, sky, green) | The colour meant nothing, so it was noise. The brief also asks for one accent. | Neutral icons. Magenta only on AI/Claude items, so the colour itself signals "this is where Claude is used" (helps reviewer B scan) |
| Numbers 01–04 on Problem and Services cards | Numbers imply order. Neither list is ordered, so they diluted the numbering that does matter, in Process. | Numbers only in Process |
| Solution checklist = define / design / build / AI / Claude | Repeated the Process steps almost word for word. | Rewritten as **what you get** (a defined product, a designed UX, working software, AI only where it pays off, faster documented delivery). Process covers *how*, Solution covers *what you walk away with* |
| Claude lead: "Claude isn't a feature we bolt on…" | Contradicted the next column, which is literally about building Claude features. | "We use Claude at two levels: in how we build, and in what we build." |
| Why Tersa in 5 narrow columns | Text wrapped to 2–3 words per line at desktop width and was hard to read. | 2-column icon + text list |
| About heading "A focused studio, founder-led." | Repeated "Founder-led" from Why Tersa right above it. | "Who's behind Tersa." |
| "Bootstrapped" tag in About | Tells a client nothing they can act on, and can read as "fragile". The reviewer gets this from the application, not the site. | Removed. Kept: founded, location, international |
| Final CTA "Book an intro call" with no booking link | Scrolled to the form directly beside it, so it was a button that did nothing. | Hidden until `BOOKING_URL` is set. Email is the visible alternative to the form |
| Footer link to tersa.io on tersa.io; "Made with care in Germany" | A link to the page you're already on, and filler text. | tersa.io as plain text; "Based in Germany · Working with clients internationally" (a real fact) |

### Kept, and why

- **Hero illustration (the steps panel).** It shows the process and Claude's role in about two seconds, before anyone reads (A, B). It uses no logos or client names, and its accessible label says it's an illustration.
- **Trust line "Founded in 2026".** Being upfront about being new builds more trust than hiding it. A reviewer will check the founding date anyway (B).
- **Problem section.** Founders need to recognise their own situation before a solution means anything (A). The four cards are the four objections we answer later: capacity → we build, cost/speed → small scope, generic AI → grounded AI, unclear path → process.
- **"Where Claude helps" on every service.** It makes the Claude claim concrete per service instead of a slogan (B), and tells clients exactly what's automated and what isn't (A).
- **Three principles under the Claude section** (human review, grounded in your data, privacy). These answer the top client worry about AI agencies: quality and data handling (A), and show responsible use (B). ⚠️ These are commitments, so keep them only if they're true for how you work.
- **"Example" tag on each use-case card**, as well as the section label. A card can be screenshotted or skimmed on its own, and the label stops anyone reading it as a real client project.
- **"Selected work: coming soon" placeholder.** Leaving the Work nav item with nothing behind it would look worse. The "Be an early client" button turns the gap into an invitation.
- **Project-type dropdown in the form.** It costs one click and lets you sort inquiries before replying.
- **Six FAQs only.** That's what the brief asked for. "Who owns the code?" and "What does it cost?" are worth adding when you're ready to answer them publicly.

### Open issues, not fixed in code

- **Google Fonts and GDPR.** Loading fonts from Google sends visitor IPs to Google. German courts have fined sites for this (LG München, 2022). Self-host Geist and Geist Mono: download the woff2 files from vercel.com/font, put them in `/fonts`, and swap the `<link>` for `@font-face`. I couldn't download the files from this environment.
- **mailto form.** It only works if the visitor has an email app set up. Add a form backend.
- **"Work" nav label** points to examples, not work. It's kept because the brief requires it. Rename it to "Examples" until real projects exist if you prefer strict accuracy.

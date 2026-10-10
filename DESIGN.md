# Tersa website — design spec & notes

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
12. Final CTA: headline, both CTAs, and an inquiry form that opens a pre-filled email to zaki@tersa.io.
13. Footer: brand, nav links, legal links, ©.

## Visual system (existing Tersa theme, unchanged)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#050510` | page background |
| aurora | indigo `#6366f1`, magenta `#d946ef`, sky `#38bdf8` radial glows | fixed backdrop |
| `--accent` | `#d946ef` | the one primary accent: kickers, wordmark dot, focus rings, check icons |
| `--text` | `#f5f5f7` | headings, primary text |
| `--muted` / `--faint` | 74% / 60% white | body / meta text (both ≥ 4.5:1 on bg) |
| `--surface` | 3.5% white + 9% white border | cards |

- **Type:** Geist (800 for headings with −0.035 to −0.045em tracking; 400–600 for body). Geist Mono for tags, step numbers and meta labels. H1 uses `clamp(42px, 6.6vw, 76px)` and H2 uses `clamp(30px, 4.4vw, 48px)`. Body text is 16–19px.
- **Spacing:** max width 1160px. Side padding is 16px on mobile and 24px from 641px up. Sections have 80px vertical padding on mobile and 112px from 768px up. Cards have 18px radius and 28–32px padding.
- **Components:** pill buttons (solid white primary, outlined ghost, minimum 44px tall). Cards lift 3px on hover. Icon tiles come in four tints (magenta, indigo, sky, green). Tags are mono pills.
- **Motion:** fade-up on scroll, the shimmer rule, the pulsing Claude dot, hover lifts, smooth scroll. All of it is disabled under `prefers-reduced-motion`.
- **Breakpoints:** 560 / 700 / 860 / 1000 / 1100px. The layout is mobile-first and every grid collapses to one column.
- **Accessibility:** skip link, semantic landmarks, one H1, `aria-expanded` on the menu, visible focus rings, decorative SVGs set to `aria-hidden`, and the form announces errors through a `role="status"` message.

## SEO

- Title: "Tersa — AI-Native Product Studio for Founders and Small Businesses"
- Meta description: as specified in the brief.
- Canonical `https://tersa.io/`, Open Graph and Twitter tags, Organization JSON-LD (founder, founding date, email, `sameAs` tersa.solutions).
- Legal pages are `noindex` until they hold real content.

## Placeholders to fill

- `BOOKING_URL` in the script at the bottom of `index.html`. Put your Cal.com or Calendly link here and every "Book an intro call" button will open it. While it is empty, the buttons scroll to the inquiry form.
- `og:image` (commented out): add a 1200×630 `og.png`.
- `favicon.svg`: placeholder "T" mark.
- Founder photo (replace the "Z" avatar).
- "Selected work — coming soon" block in #work.
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

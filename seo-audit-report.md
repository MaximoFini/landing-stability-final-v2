# SEO Audit — STABILITY Landing Page

**Audited:** 2026-08-03
**Scope:** Static source code audit of `index.html` (single-page site) + repo file structure
**Method:** Direct source inspection (no live crawl — see limitation below)

## Limitation: No Live URL

No deployed domain was found anywhere in the repo (`index.html`, `ESTILOS.md`, `.gitignore`, or any config file). There is no live site to crawl with PageSpeed Insights, Search Console, or Rich Results Test. This audit is based entirely on static source code review. Once the site is deployed, re-run: PageSpeed Insights (Core Web Vitals), Google Search Console (indexation/coverage), and Rich Results Test (schema validation) against the live URL.

---

## Executive Summary

**Overall health: Weak on technical/discoverability fundamentals, solid on on-page image/heading hygiene.**

The page itself is well-built for a single "Instagram Stories" style landing page — real HTML content (not JS-rendered), one clean H1, sensible H2 hierarchy, WebP images with lazy-loading, and no scroll-blocking JS-only content. But it is currently **invisible to structured discovery**: no `robots.txt`, no `sitemap.xml`, no canonical tag, no Open Graph/Twitter card tags (so shared links on WhatsApp/Instagram/Facebook will render with no preview image or text), and no LocalBusiness/Organization JSON-LD schema despite being a real local business in Córdoba, Argentina — a strong local-SEO opportunity being left on the table.

**Top priority issues:**
1. Missing Open Graph + Twitter Card tags — social shares (the primary distribution channel for a fitness community) render as bare links.
2. No `LocalBusiness`/`Organization` structured data — missing an easy win for local pack / knowledge panel eligibility.
3. No canonical tag.
4. No `robots.txt` or `sitemap.xml` in the repo root.
5. `user-scalable=no` in the viewport meta tag — hurts mobile UX/accessibility signals.

**Quick wins:** Add OG/Twitter meta tags (~15 min), add a canonical tag (~2 min), add a basic `robots.txt` + `sitemap.xml` (~15 min), add LocalBusiness JSON-LD (~20 min). All are additive changes to `<head>`/repo root with no risk to the existing design.

---

## Technical SEO Findings

| # | Issue | Impact | Evidence | Fix | Priority |
|---|-------|--------|----------|-----|----------|
| T1 | No `robots.txt` in repo | Medium | `Glob` for `robots.txt` at repo root returned no matches | Add a `robots.txt` with `User-agent: *` / `Allow: /` and a `Sitemap:` line once a domain exists | High |
| T2 | No `sitemap.xml` | Medium | `Glob` for `sitemap.xml` returned no matches | Add a minimal sitemap with the homepage URL (single-page site, so low complexity) once deployed | High |
| T3 | No canonical tag | Medium | No `rel="canonical"` anywhere in `index.html` `<head>` (lines 1-1161 inspected) | Add `<link rel="canonical" href="https://[final-domain]/">` once the production domain is decided | High |
| T4 | No `robots` meta tag | Low | No `<meta name="robots">` found | Not required (default is indexable), but add `<meta name="robots" content="index, follow">` explicitly once live, and use `noindex` only if a staging/preview domain is ever exposed publicly | Low |
| T5 | No structured data / JSON-LD | High | Grep for `ld+json` / `schema.org` across `index.html` returned zero matches | Add `LocalBusiness` (or `SportsActivityLocation`) JSON-LD with name, address/area served (Córdoba, Argentina), phone (WhatsApp number visible in source: `+54 9 351 224-0889`), social profile (`https://instagram.com/stability.ar`), and description. This is a strong, low-effort local-SEO lever | High |
| T6 | No deployed domain / HTTPS status unknown | N/A | No domain string found in repo | Confirm hosting plan; ensure HTTPS + a single canonical host (www vs. non-www) once deployed | Medium |
| T7 | `user-scalable=no, maximum-scale=1.0` in viewport meta | Low-Medium | Line 5: `<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">` | Remove `user-scalable=no` and `maximum-scale=1.0` — blocking pinch-zoom is a known mobile-UX and accessibility anti-pattern that can affect Google's mobile-friendliness/UX signals | Medium |
| T8 | Third-party font load (Google Fonts) not self-hosted | Low | Lines 12-16: `preconnect` to fonts.googleapis.com/fonts.gstatic.com, then a blocking `<link rel="stylesheet">` for Inter | Preconnect is already in place (good). For further LCP gains, consider self-hosting the Inter font files or using `font-display: swap` (verify the Google Fonts URL includes `&display=swap` — it does, confirmed line 16) — low priority, this is already reasonably optimized | Low |
| T9 | Large inline `<style>` block (~1100+ lines) in `<head>` | Low | Lines 18-1160 of `index.html` are a single inline `<style>` | Render-blocking but avoids an extra network request, which is a reasonable tradeoff for a single-page site. Not a priority fix; only worth revisiting if the page grows significantly | Low |
| T10 | No `apple-touch-icon` in standard PNG format | Low | Line 11: `<link rel="apple-touch-icon" href="assets/images/LogoStability.webp">` — Apple's spec expects PNG, not WebP, for touch icons | Provide a PNG (180x180) apple-touch-icon for reliable iOS home-screen icon rendering | Low |

---

## On-Page SEO Findings

| # | Issue | Impact | Evidence | Fix | Priority |
|---|-------|--------|----------|-----|----------|
| O1 | Title tag — good, but verify length | Low | `<title>STABILITY \| Comunidad de Entrenamiento y App Móvil</title>` (line 6) — 56 characters, within the 50-60 char guideline. No location keyword ("Córdoba") in the title, which is a missed local-SEO signal | Consider `STABILITY | Comunidad de Entrenamiento en Córdoba` to capture local intent, still under 60 chars | Medium |
| O2 | Meta description — good length and content | Low (positive finding) | Line 7: 173 characters — slightly over the 150-160 char guideline, will likely be truncated in SERPs, but content quality/keyword coverage is solid | Trim to ~155 characters, keep the strongest value props first | Low |
| O3 | Missing Open Graph tags | High | No `og:title`, `og:description`, `og:image`, `og:url`, `og:type` found anywhere in source | Add full OG tag set. `og:image` is critical — this is a visual fitness brand and link previews without an image will underperform on WhatsApp/Instagram/Facebook shares, which are the site's most likely distribution channels | High |
| O4 | Missing Twitter Card tags | Medium | No `twitter:card`, `twitter:title`, `twitter:image` found | Add `twitter:card` (summary_large_image) + title/description/image | Medium |
| O5 | Heading structure — clean | N/A (positive finding) | Exactly one `<h1>` (line 1252: "A un solo botón de que comience realmente tu mejor versión"), followed by multiple `<h2>` per slide (registro, features, team, testimonials, FAQ, contacto). No H3 usage found, no heading-level skips detected | No fix needed. If FAQ answers or feature sub-points grow more complex, H3s could add hierarchy, but not required at current content depth | N/A |
| O6 | H1 does not contain a clear primary keyword | Medium | H1 text: "A un solo botón de que comience realmente tu mejor versión" — evocative/brand copy, but doesn't include target terms like "entrenamiento," "comunidad," or "Córdoba" | Consider weaving in a keyword-relevant phrase (e.g., via the kicker/eyebrow near the H1, since the H1 itself is a strong brand hook) so the hero slide signals topical relevance to crawlers | Medium |
| O7 | Image alt text — mostly good, some empty | Low-Medium | Feature/team images all have descriptive alt text (e.g., `alt="Tu propia planificación según el mes"`, `alt="Registrá tu progreso y ajustá ejercicios"`). All 9 testimonial avatar images use `alt=""` (lines ~1507-1611) | Empty alt is acceptable if these are purely decorative avatars, but since the person's name follows in the card text, consider `alt="[Nombre]"` for minor incremental accessibility/image-search value. Low priority | Low |
| O8 | All content images use WebP format | N/A (positive finding) | Grep for `.jpg/.jpeg/.png` in `index.html` returned zero matches; all `<img>` references use `.webp` | No fix needed — already following modern image-format best practice | N/A |
| O9 | Lazy loading correctly implemented | N/A (positive finding) | Hero-relevant image (`imagen-planificacion.webp`) uses `loading="eager" fetchpriority="high"`; all below-the-fold slide images use `loading="lazy"` | No fix needed — this is correct LCP/lazy-load practice | N/A |
| O10 | No internal navigation / anchor links between sections | Low | Site is a single scrolling page with JS-driven "story" navigation (tap zones), no `<nav>` element or anchor links (`#section`) found | Acceptable for this single-page story format; not a defect, just noting there's no traditional internal linking to evaluate. If additional pages (e.g., a blog or FAQ page) are added later, build real internal links | Low |
| O11 | External links use `rel="noopener noreferrer"` correctly | N/A (positive finding) | WhatsApp CTA link (line ~1766): `target="_blank" rel="noopener noreferrer"` | No fix needed | N/A |
| O12 | `lang="es"` set correctly | N/A (positive finding) | Line 2: `<html lang="es">` matches the Spanish-language content | No fix needed | N/A |

---

## Content Findings

| # | Issue | Impact | Evidence | Fix | Priority |
|---|-------|--------|----------|-----|----------|
| C1 | Single page = single keyword target, no topical depth | Medium | The entire business (features, team bios, testimonials, FAQ, contact) lives on one URL with no supporting content pages | For long-term organic growth beyond brand-name searches, consider adding indexable supporting pages/content (e.g., a blog with training tips, a dedicated "Entrenamiento personalizado Córdoba" page, team member pages) — out of scope for a "Stories" landing page today, but worth a roadmap note | Long-term |
| C2 | No visible business trust signals (address, hours, pricing) | Medium | No physical address, business hours, or pricing information found in the reviewed HTML content sections | Local-business E-E-A-T benefits from visible NAP (Name, Address, Phone) consistency, ideally matching Google Business Profile. Consider surfacing the neighborhood/area served on the contact slide, in addition to the JSON-LD recommended in T5 | Medium |
| C3 | Testimonials present but not marked up | Low | 9 testimonial cards with names/quotes/avatars exist in the "community" slide (lines ~1488-1611) — good E-E-A-T content (real users, real photos) | Genuine testimonials are a trust-quality positive. Optionally wrap with `Review`/`AggregateRating` schema if testimonials are verifiable, but avoid fake/unverifiable review markup — low priority | Low |
| C4 | FAQ content present but not marked up as FAQ schema | Medium | Line 1627: `<h2 class="slide-title">Resolvemos tus dudas</h2>` — an FAQ-style slide exists | Add `FAQPage` JSON-LD for the Q&A content — a solid, low-effort win for rich-result eligibility (expandable FAQ snippets in search) | Medium |
| C5 | Content is entirely in the HTML (not JS-injected) | N/A (positive finding) | ESTILOS.md explicitly states the "story" UI is a progressive enhancement over real, indexable HTML/CSS/JS (confirmed by direct reading of the full slide markup, which contains real text content, not placeholders) | No fix needed — this is a deliberate and correct architecture decision documented in the project's own style guide | N/A |

---

## Prioritized Action Plan

### Critical (blocking indexation/ranking potential)
1. Decide and configure the production domain; ensure HTTPS.
2. Add `robots.txt` + `sitemap.xml` at the repo/deploy root (T1, T2).
3. Add a self-referencing canonical tag once the domain is fixed (T3).

### High-impact improvements
4. Add full Open Graph tag set (`og:title`, `og:description`, `og:image`, `og:url`, `og:type`) — critical for social share previews (O3).
5. Add `LocalBusiness`/`Organization` JSON-LD structured data with NAP, social profiles, and service area (T5).
6. Add Twitter Card tags (O4).
7. Add `FAQPage` JSON-LD for the existing FAQ slide content (C4).

### Quick wins (low effort, immediate benefit)
8. Remove `user-scalable=no` / `maximum-scale=1.0` from the viewport meta tag (T7).
9. Trim meta description to ~155 characters (O2).
10. Add "Córdoba" or a local-intent phrase to the title tag (O1).
11. Replace the WebP `apple-touch-icon` with a proper 180x180 PNG (T10).
12. Add explicit `<meta name="robots" content="index, follow">` (T4).

### Long-term recommendations
13. Once live, run PageSpeed Insights / Core Web Vitals and Search Console coverage checks against the real URL.
14. Consider building supporting content pages (blog, dedicated landing pages per objective/audience) to expand topical footprint beyond a single-page site (C1).
15. Surface visible NAP/business-hours content on-page to reinforce local E-E-A-T signals (C2).
16. Revisit `og:image` design specifically for WhatsApp/Instagram share previews, since those are this brand's primary distribution channels per `ESTILOS.md`.

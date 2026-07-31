# torban.me — Portfolio Redesign

A ground up redesign of a portfolio site, repositioning it from a generic corporate template PMO page into an AI forward, evidence backed personal brand site, built as a custom WordPress theme with a parallel static HTML reference build.

---

## Before → After

| | Previous Site | New Site |
|---|---|---|
| **Platform** | WordPress + Elementor page builder | Custom built WordPress theme, no page builder dependency |
| **Visual design** | Generic corporate template, orange/black palette, stock photography | Custom dark mode first design system, near black background, violet→cyan gradient accents, gradient mesh backdrop, mono font labels |
| **Theme support** | Fixed dark corporate look | Full light/dark toggle with persisted preference |
| **Positioning** | Generic "program/PMO leadership" without differentiation | "Delivery leadership, accelerated by AI" — AI augmented delivery leader, explicitly *not* overclaiming AI engineering expertise |
| **Proof of impact** | None, zero metrics, no evidence anywhere on the page | Dedicated "Impact at a Glance" section: $15M portfolio managed, 12 large-scale programs delivered, 18 years and counting |
| **Social proof** | Vague self described badges ("Servant Leader," "Compassionate") | 5 real, anonymized LinkedIn recommendations, linked out to the full recommendations page |
| **Company history** | 7-item Elementor carousel with no accessible text (logos only, no context) | Custom drag/swipe enabled logo carousel (8 real companies), fully accessible with proper alt text |
| **Resume access** | Gated behind a lead gen form (name/email/phone) | Ungated and direct link to LinkedIn (friendlier to recruiters and AI crawlers alike) |
| **Personal ventures** | Not represented | "Beyond the Delivery and PMO" section — Hydration Junkie founder story (patents, B2B/B2C/white label, successful exit) |
| **Personal AI work** | Not represented | "Personal AI Projects" section — AI Personal Assistant (Claude Code + Hermes AI Framework + Telegram + APIs), and credit for this site itself being built with Claude Code |
| **AI/search visibility** | None | `llms.txt`, AI crawler friendly `robots.txt` (GPTBot, ClaudeBot, PerplexityBot, Google Extended, etc.), semantic HTML throughout |
| **Mobile navigation** | Third party "Mobile Menu" plugin, visually inconsistent with the rest of the site | Custom built hamburger nav integrated into the theme, matching the site's own design language |

---

## Technical Improvements

- **Custom WordPress theme built from scratch** (`wp-theme/xxx`), semantic template hierarchy (`header.php`, `footer.php`, `front-page.php`, `template-parts/content-home.php`, `functions.php`), no reliance on Elementor for the homepage.
- **SEO/AEO layer**:
  - `llms.txt` (served both as a static file and as a WordPress virtual route) summarizing the site for AI assistants and LLM based crawlers.
  - `robots.txt` explicitly allowing major AI crawlers (GPTBot, ChatGPT User, ClaudeBot, Claude User, anthropic ai, PerplexityBot, Google Extended, CCBot).
  - Deliberately avoids duplicating meta description / Open Graph / JSON LD schema in the theme, defers entirely to the site's existing All in One SEO (AIOSEO) plugin to prevent conflicting SEO signals.
- **Cache-correctness fix**: theme assets (`style.css`, `main.js`) are now versioned via `filemtime()` instead of a static version string, so browsers automatically fetch fresh copies on every deploy instead of serving stale cached CSS/JS.
- **Interactive logo carousel built from scratch** — a `requestAnimationFrame`-driven, drag/swipe enabled infinite carousel using DOM node recycling (moving the leading/trailing item to the other end as it scrolls out of view), rather than the common trick of duplicating the entire item list in the DOM.
- **Custom mobile navigation** — accessible hamburger menu with `aria-expanded`, `Escape`to close, click outside to close, and focus management, replacing a third party plugin.
- **Root cause bug fixes discovered and resolved during the rebuild**:
  - An Elementor "Canvas" page template override was silently preventing the new theme from rendering at all on the homepage.
  - LiteSpeed server side page caching was serving stale HTML after deploys (identified via `x-litespeed cache: hit` response headers).
  - A legacy "Mobile Menu" plugin shipped a hardcoded, dynamically generated stylesheet that force hid a generic list of common theme header class names (including `.site-header`) below 480px width — diagnosed by inspecting the plugin's dynamic CSS output, then neutralized with a higher-specificity override.
  - An invalid CSS selector (a class selector and an `@media` block incorrectly combined in the same comma separated prelude) was silently dropping the light theme background mesh dimming rule.
- **Accessibility**: skip to content link, `aria hidden` on decorative/duplicate elements, `prefers reduced motion` support, keyboard dismissible navigation, meaningful alt text on every logo/image.

## Visual/Design Improvements

- Dark mode first design system with a light mode toggle, using CSS custom properties for full theming.
- Violet to cyan gradient brand identity applied consistently across headline text, buttons, and accent details.
- Gradient mesh background with soft radial glows and a fading dot grid texture.
- Consistent card based component system (4-, 5-, and 2-column variants) reused across every section — AI Augmented Delivery, Value Add, Testimonials, and Personal AI Projects.
- Centered, consistent Title Case section headings site wide (previously an inconsistent mix of sentence case and title case).
- Fully responsive: dedicated breakpoints for tablet (880px) and mobile (560px/479px), verified via direct DOM/computed style inspection at each breakpoint.

## Content Improvements

- **Rewrote every section** to authentically reflect an AI augmented (not AI engineer) positioning, grounded in real tools and workflows (Monday.com, Smartsheet, Claude) rather than generic AI buzzwords.
- **Added an "Impact at a Glance" section**, the single biggest credibility gap in the original site was the complete absence of quantified outcomes; this section closes it with real, user provided figures.
- **Added a Testimonials section**, replaced unverifiable self description badges with 5 real LinkedIn recommendations, anonymized (no names, companies, or dates), with a link to the full set on LinkedIn.
- **Added "Companies I've Worked With"**, a real, sourced logo set (Wikimedia Commons) with full alt text, replacing an inaccessible logo only carousel.
- **Added "Beyond the Delivery and PMO"**, a founder/entrepreneurship story (Hydration Junkie) that most PMO leader portfolios don't have.
- **Added "Personal AI Projects"** — ties the site's AI augmented positioning back to concrete, personally built proof: an AI Personal Assistant (Claude Code, Hermes AI Framework, Telegram, APIs) and this very site.
- Restructured the AI Augmented Delivery section into 5 focused cards split across Program Management and PMO themes, with real tool names cited where available.

## Tech Stack

- **Theme**: PHP (WordPress template hierarchy), no page builder or framework dependency
- **Styling**: hand written CSS with custom properties (design tokens), no CSS framework
- **Interactivity**: vanilla JavaScript (theme toggle, mobile nav, scroll reveal via `IntersectionObserver`, custom drag/swipe carousel), zero external JS libraries
- **SEO/AEO**: works alongside All in One SEO (AIOSEO); adds `llms.txt` and AI crawler aware `robots.txt`
- **Static reference build**: parallel plain HTML/CSS/JS version (`index.html`, `styles.css`, `script.js`) kept in sync with the WordPress theme throughout development

## Project Structure

```
├── index.html                          # Static reference build
├── styles.css
├── script.js
├── llms.txt                            # AI-crawler summary (static)
├── robots.txt
├── sitemap.xml
├── assets/
│   ├── logos/                          # Company logos (Wikimedia Commons)
│   └── linkedin/                       # LinkedIn banner + Featured cover images
└── wp-theme/
    └── xxxxxxxxx/                      # Installable WordPress theme
        ├── style.css                   # Theme header + full stylesheet
        ├── functions.php               # Enqueueing, llms.txt route, robots.txt filter
        ├── header.php
        ├── footer.php
        ├── front-page.php
        ├── index.php
        ├── template-parts/
        │   └── content-home.php        # All homepage section markup
        ├── js/
        │   └── main.js
        └── assets/logos/
```

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

SpinSave is a marketing landing page for a laundromat price-comparison product. The entire site lives in a single file: `spinsave.html` — no build tools, no dependencies, no package manager.

## Running the site

Open `spinsave.html` directly in a browser:

```bash
# Windows
start spinsave.html

# Or via Git Bash
start "" "spinsave.html"
```

There is no dev server, compilation step, or hot reload. Refresh the browser after edits.

## Architecture

Everything — HTML structure, CSS, and JavaScript — is inline in `spinsave.html`. The page is divided into these sections in order:

| Section | ID / class | Notes |
|---|---|---|
| Navigation | `<nav>` | Sticky, links to section anchors |
| Hero | `.hero` | Headline, CTAs, stats |
| Social proof strip | `.strip` | Dark bar, city names |
| How It Works | `#how` | 4-step grid (`.steps > .step`) |
| Features | `#features` | 6-card grid (`.features-grid > .feature-card`) |
| Live Deals | `#deals` | Dark-background section, mock deal cards |
| Testimonials | `.testimonials` | 3-card grid |
| Pricing | `#pricing` | 3-tier pricing cards; `.popular` highlights the middle card |
| CTA / waitlist | `#cta` | Email form with `handleSubmit()` JS handler |
| Footer | `<footer>` | Links only |

### Design system

All colors and the border radius are CSS custom properties on `:root` (lines 10–22). Use these variables — never hard-code colors elsewhere:

- `--blue` / `--blue-dk` — primary brand color and its hover state
- `--teal` / `--teal-lt` — accent color and its light tint
- `--gray-50` through `--gray-900` — neutral scale
- `--radius: 12px` — standard card/button corner radius

### Layout pattern

Every multi-item section uses the same responsive CSS Grid pattern:

```css
display: grid;
grid-template-columns: repeat(auto-fit, minmax(<min-width>, 1fr));
gap: <gap>;
```

This handles responsiveness without media queries for most sections. The only explicit breakpoint is `@media (max-width: 640px)` which hides the nav links on mobile.

### JavaScript

The only script is `handleSubmit(event)` at the bottom of the file, which handles the waitlist email form submission (client-side only — no backend).

## Git workflow

The repo is hosted at **https://github.com/Arnold415/spinsave**.

After every meaningful change:

```bash
git add spinsave.html          # or other changed files
git commit -m "concise message describing what changed and why"
git push
```

Commit message conventions:
- Present tense, imperative mood: `"Add testimonials section"` not `"Added"`
- Reference the section or component when relevant: `"Update pricing: add annual billing toggle"`
- Keep the subject line under 72 characters

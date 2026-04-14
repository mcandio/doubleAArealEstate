# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**doubleAArealEstate** is a single landing page for **dobleAArealstate**, built with Astro and deployed on Vercel. The only backend logic is a Vercel Function at `api/contact.js` handling form submissions.

The project has not been initialized yet. Run once to bootstrap:

```bash
npm create astro@latest . -- --template minimal
npm install
```

## Development Commands

```bash
npm run dev        # Start dev server (localhost:4321)
npm run build      # Build for production
npm run preview    # Preview production build locally
```

## Architecture

Single `src/pages/index.astro` page composed of isolated components:

- `Header` — logo/name left, `tel:` phone link right
- `Hero` — headline + supporting text + primary CTA button
- `CTA` — visually distinct band linking to the contact form
- `ContactForm` — client-side `fetch()` to `/api/contact`, JSON body
- `Maps` — embedded map block
- `Footer` — required business info (see below)

`api/contact.js` is a Vercel Function (Node.js runtime). It must:
- Accept POST only (`405` otherwise)
- Validate `name`, `email`, `message` (return `400` on failure)
- Reject submissions where honeypot field `company` is non-empty
- Keep email-provider integration behind environment variables
- Never return stack traces to the client (`500` with generic message)

The frontend form must handle loading/success/error states and block re-submission while in flight.

## Required Footer Content

Must appear on every page, exactly as written:

```
dobleAArealstate
1198 sw 158 th Way
pembroke pines
FL
33027
operated by Allavigojuva LLC
+1 954 444 0818
```

## Design Direction

Refer to `landing-page-rules.md` for full detail. Summary:

- Bold, distinctive typography — avoid Inter, Roboto, Space Grotesk, system fonts
- Choose one clear aesthetic (brutalist, luxury, editorial) and execute it precisely
- CSS variables for colors; use dominant colors with sharp accents
- One orchestrated page-load animation sequence; avoid scattered micro-interactions
- Backgrounds: gradient mesh, noise texture, or layered effects — never flat solid color
- Avoid purple-gradient-on-white "AI slop" aesthetics

## Hard Constraints

- English only — no i18n
- No multi-page routing; one `index.astro` only
- No blog, testimonials, gallery, services grid, FAQ, carousel, team, pricing, portfolio sections
- No authentication, CMS, or database
- No React/Next.js — Astro only
- All secrets in Vercel environment variables — never in source code
- Vercel deployment only; no external backend infrastructure

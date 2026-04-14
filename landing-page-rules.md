# Rule: Simplify `one-space-away-html` into a minimal Astro landing page

## Context

The project is based on the Astro template repository:

`truedaniyyel/one-space-away-html`

This template is already an Astro single-page site with minimal dependencies, and its README notes that deployment/security header rules may need to be adapted for Vercel. Keep that foundation, but simplify the site aggressively.  [oai_citation:1‡GitHub](https://github.com/truedaniyyel/one-space-away-html)

---

## Primary Goal

Transform the template into a very simple landing page.

Remove everything that is not required.

The final website must keep only these visible sections/features:

1. Hero section
2. A CTA area
3. Contact form
4. Maps section

Additionally:

- show the phone number in the **top-right area of the header**
- keep the implementation simple
- preserve Astro as the framework
- keep the project easy to deploy on Vercel

---

## Hard Constraints

Claude must follow these instructions strictly:

- Do not redesign the site into a multi-page experience
- Do not add new sections beyond the required ones
- Do not add blog, testimonials, gallery, services grid, FAQ, carousel, team, pricing, or portfolio sections
- Do not add authentication
- Do not add a CMS
- Do not add a database
- Do not introduce unnecessary dependencies
- Do not migrate away from Astro
- Do not turn this into React or Next.js
- Do not keep decorative sections from the original template unless they are directly reused as Hero, CTA, Form, or Maps

---

## Required Final Structure

The final page should contain only the following visible structure, in this order:

### 1. Header
The header must be minimal.

Requirements:
- left side: logo or site name
- right side: phone number
- the phone number must be visually obvious and placed in the top-right area
- keep navigation minimal or remove it entirely if not needed

Preferred behavior:
- if a navigation exists, keep only anchor links to the remaining sections
- otherwise, use a very small header with branding on the left and phone on the right

---

### 2. Hero Section
Keep one strong hero section.

Requirements:
- one main headline
- one short supporting paragraph
- one primary CTA button
- clean layout
- no slider
- no rotating banners
- no unnecessary decorative content

The hero should feel immediate and conversion-oriented.

---

### 3. CTA Section
Keep one dedicated CTA block.

Requirements:
- short direct text
- one button or anchor that sends the user to the contact form
- visually distinct from the hero, but still simple

This can be a band, block, or section with strong contrast.

---

### 4. Contact Form
Keep a simple contact form.

Requirements:
- name
- email
- message
- submit button

Optional:
- hidden honeypot field named `company`

Behavior:
- use a simple server endpoint pattern if form handling is later added
- keep the form markup clean and easy to wire up
- do not overcomplicate validation in the UI

---

### 5. Maps Section
Keep the maps section.

Requirements:
- preserve a simple map embed or map block
- keep it visually clean
- do not surround it with extra unrelated content
- if the original template has a map-related section, simplify it instead of rebuilding it from scratch unless necessary

---

## Removal Instructions

Remove or delete all unnecessary sections, components, assets, and references related to features that are no longer needed.

Examples of things to remove if present:
- testimonial sections
- process sections not being reused
- portfolio/project showcases
- image galleries
- sliders/carousels
- service cards
- blog/news sections
- counters/stats
- extra footer blocks
- redundant navigation items
- social proof sections
- newsletter/signup blocks
- excessive decorative wrappers

Also clean up:
- unused imports
- unused styles
- unused JavaScript
- unused image references
- unused component files

---

## Styling Direction

Keep the visual style:

- clean
- minimal
- professional
- restrained

Do not overdesign.

Priorities:
- readability
- clear hierarchy
- strong spacing
- simple responsiveness
- easy maintenance

If the original template contains visual effects that are not needed, remove them.

---

## Phone Number Placement

The phone number must appear in the top-right area of the page header.

Implementation preference:
- render it as a clickable `tel:` link
- keep it visible on desktop
- ensure it remains accessible on mobile
- do not bury it inside a menu unless absolutely necessary

Example pattern:

`<a href="tel:+19544440818">+1 954 444 0818</a>`

---

## Astro Implementation Guidance

Keep the existing Astro structure where practical, but simplify it.

Preferred approach:
- keep a single main page
- keep only the components needed for:
  - header
  - hero
  - CTA
  - contact form
  - maps
- remove the rest

If the template has reusable sections, repurpose them instead of rebuilding unnecessarily, but only if that produces a cleaner result.

---

6. Footer / Business Info

Must include:

dobleAArealstate
1198 sw 158 th Way
pembroke pines
FL
33027
operated by Allavigojuva LLC
+1 954 444 0818

Formatting can improve readability, but content must remain exact.

## Vercel Guidance

The repository README mentions that header/security rules may need to be moved or adapted for Vercel deployment. When preparing the simplified version, keep the project compatible with Vercel and adapt deployment-related config accordingly if needed.  [oai_citation:2‡GitHub](https://github.com/truedaniyyel/one-space-away-html)

Do not overengineer deployment configuration.

---

## Output Expectations

When asked to modify the template, Claude should:

1. identify the files/components used by the current landing page
2. remove all non-essential sections
3. keep only:
   - hero
   - CTA
   - contact form
   - maps
   - header with phone on top right
4. clean imports and styles
5. keep the final result copy-paste ready and deployable

---

## Code Quality Rules

The final code must be:

- minimal
- readable
- maintainable
- easy to explain
- easy to deploy

Prefer:
- small components
- simple markup
- minimal JS
- scoped styles where appropriate
- no unnecessary abstractions

---

## What Success Looks Like

A simplified Astro landing page derived from the original template, with:

- a minimal header
- phone number at the top right
- one hero section
- one CTA section
- one contact form
- one maps section
- no extra clutter
- no unnecessary dependencies
- clean Vercel-friendly structure

## Vercel + Contact Form Integration

The project must be prepared for deployment on **Vercel** and the contact form must be implemented using **Vercel Functions**.

### Requirements

- The site must be fully compatible with Vercel deployment.
- The contact form must NOT send emails directly from the browser.
- All form submissions must be handled through a server-side endpoint using a Vercel Function.

---

### API Endpoint

The form must send a POST request to:

`/api/contact`

This endpoint must be implemented as a Vercel Function.

---

### Function Responsibilities

The Vercel Function must:

- accept only POST requests
- parse the incoming JSON body
- validate required fields:
  - name
  - email
  - message
- validate email format
- reject spam using a honeypot field named `company`
- return proper HTTP responses:
  - `200` → success
  - `400` → invalid input
  - `405` → method not allowed
  - `500` → server error

---

### Security Rules

- Do NOT expose any API keys in the frontend
- All secrets must be stored as Vercel environment variables
- Do NOT return internal errors or stack traces to the client
- Always validate input on the server (not only client-side)

---

### Frontend Behavior

The form must:

- submit using `fetch()` to `/api/contact`
- send data as JSON
- include:
  - name
  - email
  - message
  - company (hidden honeypot field)
- handle:
  - loading state
  - success message
  - error message
- prevent multiple submissions while request is in progress

---

### Email Handling

The Vercel Function should be prepared to integrate with an email provider (e.g., SES, Resend, SendGrid).

- Use environment variables for configuration
- Do not hardcode credentials
- Keep the implementation simple and replaceable

---

### Deployment Constraint

The final project must be:

- deployable directly to Vercel
- requiring only environment variable configuration
- not dependent on external backend infrastructure
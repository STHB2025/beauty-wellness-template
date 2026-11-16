# Jackson Personal Digital Services — Beauty & Wellness

An Astro landing page starter for independent beauty professionals and small salons. The business site is a separate project folder and does not touch the Jackson portfolio. This is a demonstration business profile; replace all sample contact information, reviews, prices, address, hours and imagery before presenting a client version.

## Phase 1 structure

```text
beauty-wellness-template/
├── astro.config.mjs
├── package.json
└── src/
    ├── components/BookingLink.astro
    ├── data/business.js       # client details, services, imagery, reviews, theme
    ├── layouts/BaseLayout.astro
    ├── pages/index.astro
    └── styles/global.css
```

Shared layout and enquiry components sit apart from configurable business data. Future plumbing and logistics templates can reuse the structural conventions and contact patterns while defining their own industry-specific pages, components and visual identity.

## Run locally

Requires Node.js 22.23.4 or newer and npm 9.6.5 or newer (Astro 7.4.12 requirements).

```sh
npm install
npm run dev
npm run build
npm run preview
```

In a managed Windows sandbox where Astro cannot write its telemetry configuration to the user profile, run the build with telemetry disabled:

```powershell
$env:ASTRO_TELEMETRY_DISABLED = '1'
npm run build
```

## Client customisation

1. Edit `src/data/business.js`. Update the business name, logo, brand label, site credit, locale, SEO title, tagline, headline, description, theme colors, location/address, phone, email, hours and hours note, privacy URL, social URLs, service descriptions/prices, gallery image URLs, testimonials and about text. Colors are wired to CSS variables in the shared layout.
2. Set `whatsappNumber` to the client's international number with country code and digits only, without `+`, spaces or punctuation. Leave blank until a real client number is approved. Blank uses the configured email as the booking CTA fallback and labels WhatsApp as not enabled.
3. Replace every demo image URL with client-approved images. Keep descriptive `alt` text. The page currently references remote Unsplash images, so those need network access and are not bundled with the site.
4. Replace `site` in `astro.config.mjs` with the final canonical domain before launch. Set a client-specific favicon/logo if supplied. The layout title and description are already generated from business data.
5. Check all social links and privacy wording with the business. Do not use sample testimonials, personal details or prices on a live client website.

## Appointment enquiry delivery

GitHub Pages serves static files and does not process form submissions. The template therefore renders a clearly labelled email fallback and does not claim a request was sent when a form endpoint is missing.

To enable the request form:

1. Have the client create/configure their own account with a form provider such as Formspree and verify the receiving email address.
2. Put the provider's HTTPS endpoint in `formEndpoint` in `src/data/business.js`, e.g. `https://formspree.io/f/FORM_ID`. The page accepts only this endpoint shape before rendering the HTML form and takes the form ID from the final URL segment.
3. A configured form uses Formspree's small `@formspree/ajax` client for pending, validation, error and success states. Required fields are checked by the browser and Formspree. A successful response says the request was received and still needs confirmation. If JavaScript is unavailable, the native HTML form posts to the same endpoint.
4. Submit a real test enquiry and verify delivery in the client's inbox and provider dashboard before launch. Confirm spam protection, retention and provider terms with the client.
5. If no endpoint is configured, the page shows “Email to enquire” and does not display a form or success state. Configure `whatsappNumber` separately to show the WhatsApp fallback.

Appointment requests are not confirmed reservations. The business must reply to arrange and confirm a time. Calendar synchronisation and payments are outside this starter.

## GitHub Pages deployment

1. Create a GitHub repository owned by or approved by the client and add this project. Do not overwrite another repository.
2. Set `site` in `astro.config.mjs` to the client's final HTTPS domain. For a project site at `username.github.io/repository/`, also set `base: '/repository'` and use the matching canonical site URL. For a custom domain or user site, `base: '/'` is appropriate.
3. In the repository, configure GitHub Pages to deploy from a GitHub Actions workflow using `npm ci` and `npm run build`, then publish `dist/`. Add a lockfile (`npm install` then commit `package-lock.json`) before using `npm ci`.
4. Configure DNS/custom domain in the client's hosting account if applicable, enable HTTPS, then check the deployed page, assets, canonical URL, form delivery and mobile layout.

The client owns and pays for their domain, hosting and any third-party service plan. Jackson can assist with setup and launch. Ongoing maintenance should be agreed separately.

## Before handing over

- Gather written approval for copy, prices, hours, contact details, image rights and testimonials.
- Set canonical domain, WhatsApp and verified enquiry delivery; test mail and links on desktop and phone.
- Add any required client-supplied privacy notice and provider disclosures; this starter's footer link is an email contact placeholder, not legal advice or a complete privacy policy.
- Run `npm run build`, inspect the built site at desktop and mobile widths, and retain the client's repository and hosting ownership.

## Current scope

This first working version covers the Beauty & Wellness template only. The Jackson commercial showcase, Starter/Business/Growth package architecture, handover materials for a live client, and plumbing/logistics template proposals are deferred until this version is reviewed.

## Demo preview

This repository is a public demonstration template. The salon name, services, prices, testimonials, address, imagery and contact details are sample content. It is not a real salon and has no enabled booking endpoint or WhatsApp contact. Appointment requests are not submitted until a business configures and tests its own Formspree endpoint.

## Deploy this demonstration

The project is configured for `https://sthb2025.github.io/beauty-wellness-template/`. GitHub Pages deployment runs from `.github/workflows/deploy.yml` on pushes to `main`. In repository Settings → Pages, select GitHub Actions as the build and deployment source. Build locally with `npm ci` and `npm run build`.

Before adapting this starter for a client, replace all sample content and images in `src/data/business.js`, configure that client's approved contact details, update `site` and `base` in `astro.config.mjs`, and test a real form submission. Do not present demo testimonials as real reviews or imply a request is a confirmed appointment.

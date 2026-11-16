# PriceMyService

A complete, dependency-free service pricing calculator and client quote builder, ready to host on Netlify. This repository contains the full working MVP: HTML, JavaScript, CSS, example templates, pricing logic, and formula tests.

## Host on Netlify

1. In Netlify, add a project by importing an existing Git repository.
2. Choose GitHub and select `nestlogic/pricemyservice`, branch `main`.
3. Keep the base directory empty. The committed `netlify.toml` provides these settings:

   | Setting | Value |
   | --- | --- |
   | Build command | `npm run build` |
   | Publish directory | `dist` |
   | Node.js version | `22` |
   | Environment variables | None required |

4. Enable Netlify's available access/password protection before sharing the deployment if it must remain private. The ChatGPT-hosted version's sign-in and owner-only permissions do not transfer to Netlify. A private GitHub repository, `noindex`, or the app's browser-local storage does not restrict website access. Protection availability depends on your Netlify plan.
5. After deployment, check the calculator, create a test quote, save it, and export it. Subsequent pushes to `main` can trigger Netlify builds automatically.

No database, server functions, API keys, or paid app dependencies are needed. `dist/` is the actual hand-authored application source and must stay committed. The build command runs validation; it does not generate a separate bundle.

## Run locally

Install Node.js 22 or later, then run:

```sh
npm ci
npm start
```

Open `http://localhost:3000`. Run `npm test` for pricing tests or `npm run build` for the production validation command.

## Included experience

- Overview, pricing calculator, business profile, quote details, client preview, saved quotes, methodology, privacy, and a seven-day first-customer checklist.
- Editable house-cleaning, lawn-care, freelance, and custom examples. Defaults are illustrative, not market-rate claims.
- Labor/person-hours, travel/admin time, materials, overhead, contingency, true profit margin, premiums/discounts, minimum charges, upward rounding, manual tax, and deposits.
- Input validation, loss and low-margin warnings, saved drafts, saved quote statuses, and exportable pilot setup briefs.
- Client-only clipboard/text exports and print styles for the browser's Print → Save as PDF workflow. Internal costs and margins are excluded from client-facing quotes.
- Responsive desktop/mobile layouts and native browser back/forward navigation using hash routes.

## Pricing formulas

```text
person-hours = (work hours + travel/admin hours) × people
labor = person-hours × hourly labor cost
job overhead = (monthly overhead ÷ monthly billable person-hours) × person-hours
total cost = (labor + materials + travel expenses + other costs + job overhead)
             × (1 + contingency / 100)
target price = total cost ÷ (1 − margin / 100)
adjusted price = target price × (1 + adjustment / 100)
recommended price = round UP max(adjusted price, minimum charge) to rounding increment
tax = recommended price × tax rate / 100, rounded to cents
client total = recommended price + tax
deposit = client total × deposit percent / 100, rounded to cents
balance = client total − deposit
```

A 30% margin is not a 30% markup. Discounts can reduce the achieved margin; the calculator flags that and warns about prices below cost. Tax is excluded from planned profit. Currency selection changes the label only; it does not convert amounts.

## Source map

| File | Purpose |
| --- | --- |
| `dist/index.html` | App entry point, metadata, and module/style references |
| `dist/app.mjs` | All pages, UI, validation, exports, and local persistence |
| `dist/pricing.mjs` | Pure pricing formulas, bounds, and service presets |
| `dist/styles.css` | Responsive and print styling |
| `tests/pricing.test.mjs` | Eight formula and validation tests |
| `scripts/serve.mjs` | Dependency-free local HTTP preview server |
| `netlify.toml` | Build, publish, fallback routing, and response headers |

## Data and MVP boundaries

All business details, calculator inputs, quotes, statuses, and pilot briefs stay in this browser's localStorage under the `pms-` prefix. There is no application backend, account system, synchronization, email transmission, checkout, analytics, or third-party script. Hosting providers still process normal web requests.

Saved quotes do not move between origins. Data entered on the private ChatGPT-hosted site will not automatically appear on a Netlify domain. Export important quotes before switching sites. A JSON quote backup contains internal costs and is for the business owner; this MVP exports backups but does not import them.

The proposed $99 pilot is a service offer and locally prepared brief, not an integrated payment flow. Send quotes and collect payments separately. Browser print/export should receive a final check in the browser you use for business records.

This repository transfer does not deploy to Netlify or change the original site's audience. Private-host identifiers and runtime credentials are not included.

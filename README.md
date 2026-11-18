# Jacarandale: Website

A one-page site for Jacarandale, which provides Solo and self-directed 401(k) plan support from an
office in Canoga Park, California (serving Los Angeles). It's static with no dependencies, built with Node and hosted on
**Cloudflare** (Workers static assets via `wrangler.jsonc`, or Pages).

## Quick start

```bash
node build.mjs          # builds ./dist; checks internal links; lists missing info
STRICT=1 node build.mjs # pre-launch check (fails while placeholders remain)
```

## Deploy to Cloudflare

**Workers (current setup):** Workers & Pages → Create → Import a repository → this repo.
Build command `npm run build`, deploy command `npx wrangler deploy`. `wrangler.jsonc` serves `./dist`.
Every push to the branch redeploys automatically.

**Pages (alternative):** Build command `node build.mjs`, output directory `dist`.

Security headers and redirects live in `src/static/_headers` and `src/static/_redirects`, which
are copied into `dist/` and applied by Cloudflare. After the first deploy, set `site.url` in
`site.config.mjs` to the live address (or custom domain) so canonicals, the sitemap and the form's
thank-you redirect are correct.

## Contact form (n8n)

The meeting form posts to an **n8n Webhook**, and the n8n workflow routes each submission
(email, sheet, CRM) and redirects the visitor to `/thank-you/`. Put the webhook's production URL
in `form.webhookUrl` in `site.config.mjs`. Until then the form shows a "not connected yet" notice
and won't send. Setup steps: `docs/N8N-FORM-SETUP.md`.

## Office

**21515 Vanowen St, Canoga Park, CA 91303** (storefront office). Phone: **(747) 326-5536**.

## Structure

The homepage (`/`) holds every section, each reachable from the menu and the sticky section bar:
Services · How it works · Who does what · 401(k) basics · FAQ · About · Visit & contact (meeting form).
`/privacy-policy/`, `/terms/` and `/disclosures/` are separate pages under California law,
plus `/thank-you/` and `404.html`.

## Design

- **Palette:** plum night `#2B2240`, jacaranda violet `#7A5CC8` (buttons), sunset apricot `#F2A65A`, leaf `#9CC59A`, warm paper `#FBF9F4`
- **Type:** Spectral 600 (display) and Nunito Sans (text), both self-hosted
- **Logo:** a scalloped rosette with a jacaranda in violet bloom over a valley at sunset (`src/brand.mjs`)
- **Hero:** aerial video of the Los Angeles skyline at sunset (desktop only; phones get the poster image)

See `docs/` for the launch checklist, media sources, Search Console and Google Business Profile steps.

---
name: renderwolf-og-image-pipeline
description: >-
  Generate Open Graph / social card images at scale with Renderwolf by storing one HTML
  template and minting a signed URL per page, so crawlers fetch the image directly and editing
  the template updates every card.
api: Renderwolf API
base_url: https://api.ironfang.uk/renderwolf
operations:
  - createTemplate
  - listTemplates
  - getTemplate
  - updateTemplate
  - renderTemplate
  - createSignedUrl
  - renderSignedUrl
generated: '2026-09-02'
method: generated
source: openapi/ironfang-openapi.yaml + https://ironfang.uk/renderwolf/guides/open-graph-images
---

# Open Graph images from a reusable template

## When to use this
You need a card image per page (blog post, product, invoice, certificate) and you do not want
your application to render, store or serve image files.

## Preconditions
- An API key from https://portal.ironfang.uk with the `renderwolf:templates:write`,
  `renderwolf:templates:read` and `renderwolf:sign` scopes. Key scopes cannot be widened
  after creation — mint a new key rather than trying to expand one.
- Auth header on every call: `Authorization: Bearer <key>`.

## Steps

1. **Store the layout once.** `createTemplate` — `POST /v1/templates` with
   `{ "name", "html", "width", "height" }`. The HTML is ordinary HTML and CSS with `{{var}}`
   placeholders. Response is a `Template` carrying `id`.
   - `201` on success, `400` on invalid input, `401 invalid_api_key`.

2. **Check the render before wiring it up.** `renderTemplate` —
   `POST /v1/image/{id}` with `{ "vars": { ... } }`. This returns image bytes directly, not
   JSON. Costs 1 credit; an identical repeat is served from cache for 0 credits and carries
   `X-Renderwolf-Cache: hit`.
   - `422 render_failed` means Chromium could not render — usually a selector timeout or an
     asset the template references that is not publicly reachable.

3. **Mint one signed URL per page.** `createSignedUrl` — `POST /v1/sign` with
   `{ "kind": "image", "template": "<id>", "vars": { "title": "..." }, "ttl_hours": <n> }`.
   The response carries `url` and `path`. Put `url` straight into the `og:image` meta tag.
   The signature covers every parameter and the metering account, so nobody can alter it after
   signing and your API key is never exposed.

4. **Let crawlers fetch it.** `renderSignedUrl` — `GET /v1/r/{exp}/{sig}` needs no key. It
   renders on demand and meters against your account. Repeated fetches of an identical cached
   result cost nothing, so a viral post does not cost per impression.

5. **Redesign without reissuing URLs.** `updateTemplate` — `PUT /v1/templates/{id}`. Editing a
   template invalidates its cache immediately, so every existing signed URL starts serving the
   new design on the next fetch.

## Rules that matter here

- **`ttl_hours: 0` means never expires — and there is no revoke operation.** An og:image URL is
  the legitimate use for it, because the tag must keep working. Understand that you are minting
  a permanent public URL that meters against your account with no way to withdraw it. If you
  need to be able to stop it, set a real TTL and re-mint on a schedule. Through the MCP server
  Ironfang refuses `ttl_hours: 0` outright and caps at 24 hours.
- **Credits.** 1 per template render, 0 on a cache hit, refunded automatically if the render
  fails. Check `X-Renderwolf-Credits` on the response rather than polling `getUsage`.
- **Rate limits.** 120 renders per minute per account, 60 per minute per target host across all
  customers. Exhaustion is `429` with `rate_limited` / `target_rate_limited`; there are no
  `RateLimit-*` headers to read, so back off on the status.
- **Errors.** `{"error": {"code", "message"}}` — branch on `code`, never on `message`. Quote
  `X-Ironfang-Request-ID` to support.

## Do not
- Do not put the API key in a page, an email or a client-side fetch. Signed URLs exist so you
  never have to.
- Do not proxy the image through your own application and cache it yourself; you lose the free
  cache hits and gain a storage problem.

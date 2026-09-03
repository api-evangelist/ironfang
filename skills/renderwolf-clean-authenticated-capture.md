---
name: renderwolf-clean-authenticated-capture
description: >-
  Capture a page that needs a session, or a page cluttered with ads and cookie banners, using
  Renderwolf's RenderCommon options — headers, cookies, blocking, selector waits — and know
  which of them the MCP surface refuses.
api: Renderwolf API
base_url: https://api.ironfang.uk/renderwolf
operations:
  - createScreenshot
  - createPdf
  - createSitePreview
  - renderTemplate
  - submitJob
generated: '2026-09-02'
method: generated
source: >-
  openapi/renderwolf-openapi.yaml (components.schemas.RenderCommon),
  https://ironfang.uk/renderwolf/guides/authenticated-pages,
  https://ironfang.uk/renderwolf/guides/clean-screenshots
---

# Clean and authenticated captures

`RenderCommon` is the shared option block composed into `ScreenshotRequest`, `PdfRequest`,
`SitePreviewRequest` and `RenderTemplateRequest`. Everything below is a field on it, so the same
options work identically across those four operations and inside a `submitJob` `request` body.

## Fields

| Field | Use |
| --- | --- |
| `headers` | Arbitrary request headers, applied **before navigation** so the first request is already signed in. |
| `authorization` | An `Authorization` value sent with the render. |
| `cookies` | `Cookie` objects — `name`, `value`, `domain` (required), `path`. |
| `user_agent` | Override the UA string. |
| `block_ads` | Drop ad and tracker requests at the network layer. |
| `block_cookie_banners` | Hide consent overlays **without clicking accept on anyone's behalf**. |
| `hide_selectors` | Remove any other element by CSS selector. |
| `wait_until` | Navigation completion condition, e.g. `networkidle`. |
| `wait_for_selector` | Wait for a specific element before capturing — the right tool for dashboards that fill in after first paint. |
| `timeout_ms` | Bound the whole render. |
| `no_cache` | Force a fresh capture. Billable. |
| `device_scale_factor` | Retina / DPI output. |

## Steps

1. **Authenticated page.** Send the session the way the site expects it — a `cookies` entry with
   the right `domain`, or `headers` / `authorization` for a token-based app. Because they are
   applied before navigation, the very first request is authenticated; you do not need a login
   flow.

2. **Wait for the real content.** Set `wait_for_selector` to something that only exists once the
   data has loaded. `wait_until: networkidle` alone is not enough for an app that polls.

3. **Clean the page.** `block_ads: true`, `block_cookie_banners: true`, and
   `hide_selectors` for anything left. Note that hiding a consent banner is not the same as
   accepting it — Renderwolf hides rather than clicks, deliberately.

4. **Force freshness only when you need it.** `no_cache: true` for evidence collection,
   archiving or change monitoring. It is billable, is excluded from the cache key (so two fresh
   requests do not hit each other's results), returns `Cache-Control: no-store`, and adds
   `X-Renderwolf-Captured-At` with the UTC capture time. Leave it off and identical requests are
   free cache hits carrying `X-Renderwolf-Cache: hit`.

## Constraints you must respect

- **Private addresses are refused.** A blocked private address returns `422 render_failed`, as
  does an invalid URL or a selector timeout. Renderwolf will not render your internal network.
- **None of this is available to an agent.** The MCP rendering tools take a public URL or
  bounded raw HTML and explicitly refuse cookies, `authorization`, custom request headers, proxy
  settings, scripts to execute and private network targets. If a capture needs a session, it has
  to run through the REST API with a scoped key — not through an assistant.
- **The target-host rate limit is shared.** 60 renders per minute per target host counted across
  all Renderwolf customers, returning `429 target_rate_limited`. Contact Ironfang to raise it for
  a host you own. A rate-limited request spends no credits.
- **Proxy routing and country selection do not exist.** Ironfang's own `/v1/capabilities`
  endpoint lists `proxies` as `not_offered`. Do not design around it.

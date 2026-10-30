# Ironfang

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Ironfang Render is the rendering API from Ironfang Ltd, a UK software company that builds and operates self-service developer APIs. It turns a URL or a block of raw HTML into screenshots, PDFs, templated images, QR codes, captioned video clips and scrolling site previews over plain HTTPS and JSON, with no browser fleet for the customer to run. The v1 REST API is described by a published OpenAPI 3.1 contract covering 33 operations across synchronous rendering, reusable HTML templates, signed render URLs, durable asynchronous jobs, batches of up to 100, and webhook or S3-compatible delivery destinations. A remote MCP server at mcp.ironfang.com exposes the same core to AI assistants over OAuth 2.1 with a per-connection credit budget, and an llms.txt, a TypeScript and Python SDK, a CLI and an n8n node round out the surface. Plans are hard-capped rather than metered into overage, cache hits are free, and failed renders are refunded. Ironfang's own apis.json lists five more product APIs on the same account, portal and key format, each with its own published OpenAPI 3.1 contract under api.ironfang.com, for Audit (website evidence), Finance (e-invoice validation and generation, v1 and v2), Rig (disposable integration test environments), Analytics (session replay) and Security (external security checks).

**Areas:** Developer Tools · Screenshots · website screenshot · HTML to PDF · PDF API · Image API · OG Image API · QR Code API · Website-to-Video · Rendering Infrastructure · MCP · UK-hosted

## Ironfang on APIs.io

Everything profiled for Ironfang is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/ironfang/](https://apis.io/providers/ironfang/)** — or go straight to one of the APIs or properties below.

### APIs (62)

- [Ironfang Account API](https://apis.io/apis/ironfang/ironfang-account-api/) — Usage against quota.
- [Ironfang Batches API](https://apis.io/apis/ironfang/ironfang-batches-api/) — Up to 100 renders submitted, and refused, together.
- [Ironfang Destinations API](https://apis.io/apis/ironfang/ironfang-destinations-api/) — Where a finished job goes - a signed webhook, or your own S3 bucket.
- [Ironfang Jobs API](https://apis.io/apis/ironfang/ironfang-jobs-api/) — The Jobs API from Ironfang — 4 operation(s) for jobs.
- [Ironfang Render API](https://apis.io/apis/ironfang/ironfang-render-api/) — Turn a URL or HTML into an image, PDF or video.
- [Ironfang Signed URLs API](https://apis.io/apis/ironfang/ironfang-signed-urls-api/) — Shareable render URLs that need no API key.
- [Ironfang Templates API](https://apis.io/apis/ironfang/ironfang-templates-api/) — Stored HTML with `{{variable}}` placeholders, rendered on demand.
- [Ironfang Audit Artifacts API](https://apis.io/apis/ironfang/ironfang-audit-artifacts-api/) — Stored screenshots and other captured artifacts.
- [Ironfang Audit Audits API](https://apis.io/apis/ironfang/ironfang-audit-audits-api/) — Audit runs, their pages and evidence.
- [Ironfang Audit Events API](https://apis.io/apis/ironfang/ironfang-audit-events-api/) — The account event stream.
- [Ironfang Audit Export Destinations API](https://apis.io/apis/ironfang/ironfang-audit-exportdestinations-api/) — Where exports are delivered.
- [Ironfang Audit Exports API](https://apis.io/apis/ironfang/ironfang-audit-exports-api/) — Evidence bundle exports.
- [Ironfang Audit Findings API](https://apis.io/apis/ironfang/ironfang-audit-findings-api/) — Findings raised by audits.
- [Ironfang Audit Monitors API](https://apis.io/apis/ironfang/ironfang-audit-monitors-api/) — Scheduled re-audits of a site.
- [Ironfang Audit Notification Preferences API](https://apis.io/apis/ironfang/ironfang-audit-notificationpreferences-api/) — How the organisation is notified.
- [Ironfang Audit Notifications API](https://apis.io/apis/ironfang/ironfang-audit-notifications-api/) — Notifications raised for the organisation.
- [Ironfang Audit Page Observations API](https://apis.io/apis/ironfang/ironfang-audit-pageobservations-api/) — Per-page observations and comparisons.
- [Ironfang Audit Pages API](https://apis.io/apis/ironfang/ironfang-audit-pages-api/) — Pages within an audit.
- [Ironfang Audit Retention API](https://apis.io/apis/ironfang/ironfang-audit-retention-api/) — Quoted, fixed-price extensions of hosted evidence retention.
- [Ironfang Audit Rule Packs API](https://apis.io/apis/ironfang/ironfang-audit-rulepacks-api/) — Installable rule packs.
- [Ironfang Audit Rules API](https://apis.io/apis/ironfang/ironfang-audit-rules-api/) — Rules and their revisions.
- [Ironfang Audit Sites API](https://apis.io/apis/ironfang/ironfang-audit-sites-api/) — Sites under audit.
- [Ironfang Audit Usage API](https://apis.io/apis/ironfang/ironfang-audit-usage-api/) — This month's metered use, capacity and hosted evidence.
- [Ironfang Audit Verify API](https://apis.io/apis/ironfang/ironfang-audit-verify-api/) — Public verification of evidence bundles.
- [Ironfang Audit Webhooks API](https://apis.io/apis/ironfang/ironfang-audit-webhooks-api/) — Webhook endpoints and deliveries.
- [Ironfang Finance E-Invoicing Billing API](https://apis.io/apis/ironfang/ironfang-finance-billing-api/) — Ironfang Finance usage as the organisation's billing account meters it, beside Finance's own content-free record. Payment, limits and invoices belong to the…
- [Ironfang Finance E-Invoicing Deliveries API](https://apis.io/apis/ironfang/ironfang-finance-deliveries-api/) — Destinations subscribe to future terminal validation/generation operations in their organisation.
- [Ironfang Finance E-Invoicing Generation API](https://apis.io/apis/ironfang/ironfang-finance-generation-api/) — Deterministic JSON-to-UBL generation, validated before success.
- [Ironfang Finance E-Invoicing Jobs API](https://apis.io/apis/ironfang/ironfang-finance-jobs-api/) — Authenticated durable validation and generation jobs and ordered batches.
- [Ironfang Finance E-Invoicing Rendering API](https://apis.io/apis/ironfang/ironfang-finance-rendering-api/) — Safe readable PDFs of retained successfully validated generation results.
- [Ironfang Finance E-Invoicing Reports API](https://apis.io/apis/ironfang/ironfang-finance-reports-api/) — Signed validation observations and independent report integrity verification.
- [Ironfang Finance E-Invoicing Results API](https://apis.io/apis/ironfang/ironfang-finance-results-api/) — Authenticated retained validation and generation results.
- [Ironfang Finance E-Invoicing Rulesets API](https://apis.io/apis/ironfang/ironfang-finance-rulesets-api/) — The immutable ruleset registry validation results are pinned to.
- [Ironfang Finance E-Invoicing Validation API](https://apis.io/apis/ironfang/ironfang-finance-validation-api/) — PHIVE validation of UBL Invoice and CreditNote XML with structured findings.
- [Ironfang Finance E-Invoicing V2 Deliveries API](https://apis.io/apis/ironfang/ironfang-finance-v2-deliveries-api/) — Webhook and S3 deliveries of V1 and V2 events together.
- [Ironfang Finance E-Invoicing V2 Jobs API](https://apis.io/apis/ironfang/ironfang-finance-v2-jobs-api/) — Durable validation jobs and batches, V1 and V2 together.
- [Ironfang Finance E-Invoicing V2 Reports API](https://apis.io/apis/ironfang/ironfang-finance-v2-reports-api/) — Signed reports of retained results, and their verification.
- [Ironfang Finance E-Invoicing V2 Results API](https://apis.io/apis/ironfang/ironfang-finance-v2-results-api/) — Retained results, V1 and V2 together.
- [Ironfang Finance E-Invoicing V2 Rulesets API](https://apis.io/apis/ironfang/ironfang-finance-v2-rulesets-api/) — The immutable releases a validation can name.
- [Ironfang Finance E-Invoicing V2 Validation API](https://apis.io/apis/ironfang/ironfang-finance-v2-validation-api/) — Validate one invoice, XML or PDF.
- [Ironfang Rig Connectors API](https://apis.io/apis/ironfang/ironfang-rig-connectors-api/) — Outbound connectors that forward a run's callbacks to fixed local routes.
- [Ironfang Rig Events API](https://apis.io/apis/ironfang/ironfang-rig-events-api/) — The run timeline.
- [Ironfang Rig Evidence API](https://apis.io/apis/ironfang/ironfang-rig-evidence-api/) — Bundles, receipts and the keys they are signed with.
- [Ironfang Rig Faults API](https://apis.io/apis/ironfang/ironfang-rig-faults-api/) — Deterministic interference armed on a run's resources.
- [Ironfang Rig Projects API](https://apis.io/apis/ironfang/ironfang-rig-projects-api/) — Persistent containers for one application or product.
- [Ironfang Rig Resources API](https://apis.io/apis/ironfang/ironfang-rig-resources-api/) — The external identities a run receives.
- [Ironfang Rig Runs API](https://apis.io/apis/ironfang/ironfang-rig-runs-api/) — Disposable executions of a suite version.
- [Ironfang Rig Suites API](https://apis.io/apis/ironfang/ironfang-rig-suites-api/) — Persistent, versioned test definitions.
- [Ironfang Rig Usage API](https://apis.io/apis/ironfang/ironfang-rig-usage-api/) — What the organisation has used, and the deployment's fixed facts.
- [Ironfang Analytics Capabilities API](https://apis.io/apis/ironfang/ironfang-analytics-capabilities-api/) — What this deployment can do and the limits it applies.
- [Ironfang Analytics Heatmaps API](https://apis.io/apis/ironfang/ironfang-analytics-heatmaps-api/) — Totals of where visitors click, how far they scroll, how long each part of a page is on screen and where the pointer goes, across the recorded visits to one…
- [Ironfang Analytics Keys API](https://apis.io/apis/ironfang/ironfang-analytics-keys-api/) — The public collection key a site's install snippet carries.
- [Ironfang Analytics Origins API](https://apis.io/apis/ironfang/ironfang-analytics-origins-api/) — The origins a site's recorder may send from and their DNS verification.
- [Ironfang Analytics Recordings API](https://apis.io/apis/ironfang/ironfang-analytics-recordings-api/) — Recordings of one tab within a session: search, what the visitor's browser reported, the batches to play them back from, live viewing and deletion. Every…
- [Ironfang Analytics Sessions API](https://apis.io/apis/ironfang/ironfang-analytics-sessions-api/) — One browser's visit to one site: every tab, from the first page until thirty minutes pass without the visitor doing anything, or twelve hours from its…
- [Ironfang Analytics Sites API](https://apis.io/apis/ironfang/ironfang-analytics-sites-api/) — Instrumented websites and their capture configuration.
- [Ironfang Analytics Usage API](https://apis.io/apis/ironfang/ironfang-analytics-usage-api/) — This month's recordings as the organisation's billing account counts them, and whether new recordings are being admitted.
- [Ironfang Security Activity API](https://apis.io/apis/ironfang/ironfang-security-activity-api/) — What happened in the organisation's Security account.
- [Ironfang Security Domains API](https://apis.io/apis/ironfang/ironfang-security-domains-api/) — Domains the organisation has added, their ownership verification and authorisation.
- [Ironfang Security Findings API](https://apis.io/apis/ironfang/ironfang-security-findings-api/) — Normalised findings, their evidence, status and rechecks.
- [Ironfang Security Scans API](https://apis.io/apis/ironfang/ironfang-security-scans-api/) — External Security Check runs and their results.
- [Ironfang Security Service API](https://apis.io/apis/ironfang/ironfang-security-service-api/) — Whether Security is available, and the limits that apply.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Ironfang Webhooks](https://apis.io/asyncapis/ironfang/ironfang-webhooks/)

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [Ironfang](https://apis.io/servers/ironfang/ironfang/)
- [mcp](https://apis.io/servers/ironfang/mcp/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Ironfang Agentic Access](https://apis.io/agentic-access/ironfang/ironfang-agentic-access/)

#### JSON Schema (12)

The data models the API reads and writes.

- [ClipRequest](https://apis.io/schemas/ironfang/ironfang-clip-request/)
- [JobDelivery](https://apis.io/schemas/ironfang/ironfang-job-delivery/)
- [PdfRequest](https://apis.io/schemas/ironfang/ironfang-pdf-request/)
- [QrRequest](https://apis.io/schemas/ironfang/ironfang-qr-request/)
- [RenderTemplateRequest](https://apis.io/schemas/ironfang/ironfang-render-template-request/)
- [ScreenshotRequest](https://apis.io/schemas/ironfang/ironfang-screenshot-request/)
- [SignRequest](https://apis.io/schemas/ironfang/ironfang-sign-request/)
- [SignedUrl](https://apis.io/schemas/ironfang/ironfang-signed-url/)
- [SitePreviewRequest](https://apis.io/schemas/ironfang/ironfang-site-preview-request/)
- [Template](https://apis.io/schemas/ironfang/ironfang-template/)
- [TemplateInput](https://apis.io/schemas/ironfang/ironfang-template-input/)
- [Usage](https://apis.io/schemas/ironfang/ironfang-usage/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Ironfang Context](https://apis.io/jsonld/ironfang/ironfang-context/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Ironfang Openapi Overlay](https://apis.io/overlays/ironfang/ironfang-openapi-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Ironfang API Rules](https://apis.io/rules/ironfang/ironfang-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Ironfang Authentication](https://apis.io/security/ironfang/ironfang-authentication/)
- [Ironfang Domain Security](https://apis.io/security/ironfang/ironfang-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Ironfang Scopes](https://apis.io/scopes/ironfang/ironfang-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Ironfang Plans Pricing](https://apis.io/plans/ironfang/ironfang-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Ironfang Rate Limits](https://apis.io/rate-limits/ironfang/ironfang-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.ironfang.com/)
- [Documentation](https://ironfang.com/render/guides)
- [Getting started](https://ironfang.com/render/guides)
- [Pricing](https://ironfang.com/render)
- [Sign up](https://id.ironfang.com/signup)
- [Support](https://ironfang.com/contact)
- [Changelog](https://ironfang.com/changelog)
- [Blog](https://ironfang.com/articles)
- [Terms of service](https://ironfang.com/legal/terms)
- [Privacy policy](https://ironfang.com/legal/privacy)
- [GitHub](https://github.com/ironfang-ltd)
- [Status](https://status.ironfang.com)

## API Evangelist rating

**Kin Score 78.7** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 74.5 |
| Contract governance | 35.6 |
| Operational transparency | 81.6 |
| Developer ergonomics | 85.1 |
| Access clarity | 76.3 |

**Agent readiness 53.5** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | verified |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/ironfang/](https://apis.io/providers/ironfang/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Ironfang: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/ironfang/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

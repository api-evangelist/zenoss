# Zenoss

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

Zenoss is an AIOps and full-stack IT infrastructure monitoring platform, acquired by Virtana in May 2025 and now sold as Virtana Service Observability. It ingests metrics, events and entity models from hybrid estates — VMware, Nutanix, Kubernetes, AWS, Azure, GCP, network and storage — through on-premises Collection Zones, streaming agents and OpenTelemetry/OTLP, then applies dependency mapping, event correlation and anomaly detection to turn raw signal into service impact. The developer surface is a versioned /v1 REST API covering data ingest, event query and management, entity/model context, maintenance windows, the metric dictionary, notification Actions, credentials and user management, plus first-party proto3/gRPC contracts for the data receiver and data registry. API clients authenticate with a long-lived key in the zenoss-api-key header, issued per API Client from the console, and each tenant is assigned one of four regional endpoints.

**Areas:** AIOps · Monitoring · Observability · Infrastructure · Hybrid Cloud · OpenTelemetry · gRPC · Metrics

## Zenoss on APIs.io

Everything profiled for Zenoss is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/zenoss/](https://apis.io/providers/zenoss/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Virtana Service Observability API](https://apis.io/apis/zenoss/zenoss/) — Versioned /v1 REST API for the Zenoss (Virtana Service Observability) platform. Covers the data receiver (metrics, events, entity models), event query and…
- [Zenoss Cloud gRPC Services](https://apis.io/apis/zenoss/zenoss-grpc/) — First-party proto3 service contracts published at github.com/zenoss/zenoss-protobufs and released as a Go module (v1.5.5, 2026-07-27). DataReceiverService…
- [Zenoss API for Collection Zone and Resource Manager](https://apis.io/apis/zenoss/zenoss-router-api/) — The long-standing Zenoss JSON router API, still documented and supported for Zenoss Cloud Collection Zones and on-premises Zenoss Resource Manager / Service…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Zenoss Webhooks](https://apis.io/asyncapis/zenoss/zenoss-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [zenoss-mcp.yml](https://apis.io/servers/zenoss/zenoss-mcp-yml/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Zenoss Authentication](https://apis.io/security/zenoss/zenoss-authentication/)
- [Zenoss Domain Security](https://apis.io/security/zenoss/zenoss-domain-security/)
- [Zenoss Trust Center](https://apis.io/security/zenoss/zenoss-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Zenoss Plans Pricing](https://apis.io/plans/zenoss/zenoss-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Zenoss Rate Limits](https://apis.io/rate-limits/zenoss/zenoss-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Zenoss Finops](https://apis.io/finops/zenoss/zenoss-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.zenoss.com)
- [Documentation](https://docs.zenoss.io/)
- [Getting started](https://docs.zenoss.io/start/get-started.html)
- [API reference](https://docs.zenoss.io/api/zenoss-api.html)
- [Support](https://www.virtana.com/support/)
- [Changelog](https://docs.zenoss.io/admin/updates/cloud-updates.html)
- [Blog](https://www.virtana.com/blog/)
- [Trust centre](https://www.virtana.com/trust/)
- [Terms of service](https://www.virtana.com/legal-notices/)
- [Privacy policy](https://www.virtana.com/privacy/)
- [GitHub](https://github.com/zenoss)
- [Status](https://status.zenoss.io/)

## API Evangelist rating

**Kin Score 50.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 39.0 |
| Contract governance | 31.8 |
| Operational transparency | 50.0 |
| Developer ergonomics | 56.5 |
| Access clarity | 43.4 |

**Agent readiness 26.1** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
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
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/zenoss/](https://apis.io/providers/zenoss/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Zenoss: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/zenoss/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

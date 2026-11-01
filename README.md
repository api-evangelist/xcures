# xCures

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

xCures operates the Clinical Clarity Engine, an AI platform that retrieves, organizes and structures fragmented patient medical records into decision-ready clinical data. Founded in 2018 and headquartered in Oakland, California, the company connects to national health information networks (Carequality and TEFCA) to pull a patient's longitudinal record across every provider and care location, then applies LLM-based named-entity/relation extraction and retrieval-augmented checklist assertion to normalize it into FHIR R4 resources, OHDSI/OMOP-mapped vocabularies (SNOMED, LOINC, RxNorm) and HL7 mCODE oncology elements, with every field anchored to its source document. The xCures Public API exposes that engine over REST at partner.xcures.com — patient (Subject) registration, network Query dispatch and polling, document retrieval and reciprocity publishing, FHIR resource reads and bulk export, fifteen Clinical Concepts domains, AI Checklist evaluation and subject summaries — authenticated with OAuth 2.0 client-credentials bearer tokens scoped by a ProjectId header. Originally an oncology real-world-data platform, it expanded to all therapeutic areas and is sold as SaaS, embedded API connections and de-identified real-world datasets to providers, diagnostics companies, value-based-care organizations and channel partners.

**Areas:** Health · Healthcare · Medical Records · Interoperability · FHIR · Oncology · Real-World Data · Clinical Data · Artificial Intelligence · TEFCA · Carequality · Patient Data

## xCures on APIs.io

Everything profiled for xCures is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/xcures/](https://apis.io/providers/xcures/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [xCures Application API](https://apis.io/apis/xcures/xcures-application-api/) — Account creation (e.g., identity proofing, eConsent) that is required for a patient to progress on the xCures Platform.
- [xCures Checklist API](https://apis.io/apis/xcures/xcures-checklist-api/) — AI-powered feature leveraging xCures’ targeted data extraction/processing to populate validated, customizable question/answer-style items. Responses can be…
- [xCures Clinical Concepts API](https://apis.io/apis/xcures/xcures-clinical-concepts-api/) — Clinical concepts is a proprietary xCures higher-level, flattened, filtered, opinionated view of medical record information, structured around FHIR guidelines.
- [xCures Document API](https://apis.io/apis/xcures/xcures-document-api/) — Patient records retrieved by the xCures platform and/or loaded by platform users.
- [xCures FHIR API](https://apis.io/apis/xcures/xcures-fhir-api/) — **F**ast **H**ealthcare **I**nteroperability **R**esource is an international data model specification developed by HL7 International to enable healthcare…
- [xCures Project API](https://apis.io/apis/xcures/xcures-project-api/) — A configured workspace on the xCures Platform. Use this endpoint to discover the projectId value(s) required by other API calls, without needing to log into…
- [xCures Query API](https://apis.io/apis/xcures/xcures-query-api/) — A specified, approved request for patient records across the network (e.g., via Carequality/TEFCA to support treatment activities, via TEFCA for IAS…
- [xCures Reciprocity Template API](https://apis.io/apis/xcures/xcures-reciprocity-template-api/) — Reciprocity or "Responder" workflows refer to the process of sharing clinical documentation housed within your system with other organizations/providers,…
- [xCures Subject API](https://apis.io/apis/xcures/xcures-subject-api/) — An individual patient created on the xCures Platform.
- [xCures Summary API](https://apis.io/apis/xcures/xcures-summary-api/) — The AI-generated summary of a patient’s overall records and condition(s).
- [xCures O Auth API](https://apis.io/apis/xcures/xcures-oauth-api/) — All API requests to xCures must provide an access token, retrieved via the standard OAuth authorization flow below.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Xcures Application Webhooks](https://apis.io/asyncapis/xcures/xcures-application-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [xCures Docs MCP Server](https://apis.io/servers/xcures/xcures-docs-mcp-server/)

#### Examples (1)

Example requests and responses.

- [Xcures Workflow Playbook.Postman_Collection](https://apis.io/examples/xcures/xcures-workflow-playbook.postman_collection/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Xcures Patient Registry Api Overlay](https://apis.io/overlays/xcures/xcures-patient-registry-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Xcures Authentication](https://apis.io/security/xcures/xcures-authentication/)
- [Xcures Domain Security](https://apis.io/security/xcures/xcures-domain-security/)
- [Xcures Trust Center](https://apis.io/security/xcures/xcures-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Xcures Plans Pricing](https://apis.io/plans/xcures/xcures-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Xcures Rate Limits](https://apis.io/rate-limits/xcures/xcures-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://xcures.com/)
- [Documentation](https://docs.xcures.com/api-introduction)
- [Getting started](https://docs.xcures.com/api-introduction)
- [API reference](https://docs.xcures.com/apis/current)
- [Sign up](https://xcures.com/contact-us/)
- [Support](https://docs.xcures.com/support)
- [Blog](https://xcures.com/blog/)
- [Compliance](https://xcures.com/trust/)
- [Trust centre](https://xcures.com/trust/)
- [Terms of service](https://xcures.com/terms-of-service/)
- [Privacy policy](https://xcures.com/privacy-security-notice/)
- [GitHub](https://github.com/xCures)
- [Status](https://status.xcures.com/)

## API Evangelist rating

**Kin Score 60.8** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 58.2 |
| Contract governance | 18.2 |
| Operational transparency | 71.1 |
| Developer ergonomics | 76.2 |
| Access clarity | 50.0 |

**Agent readiness 59.5** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 30.9** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/xcures/](https://apis.io/providers/xcures/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for xCures: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/xcures/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

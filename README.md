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

xCures operates the Clinical Clarity Engine, an AI platform that retrieves, organizes and structures
fragmented patient medical records into decision-ready clinical data. Founded in 2018, it connects to
national health information networks (Carequality and TEFCA) to assemble a patient's longitudinal record
across every provider and care location, then normalizes it into FHIR R4, OHDSI/OMOP vocabularies and HL7
mCODE oncology elements with every field anchored to its source document.

## What this profile covers

The **xCures Public API** — a 69-operation REST API at `https://partner.xcures.com`, documented at
[docs.xcures.com](https://docs.xcures.com/). OAuth 2.0 client-credentials bearer auth with a required
`ProjectId` header on 67 of 69 operations.

| | |
|---|---|
| Contract | OpenAPI 3.0.0, 63 paths / 69 operations / 64 schemas — [`openapi/`](openapi/) |
| API reference | https://docs.xcures.com/apis/current |
| Getting started | https://docs.xcures.com/api-introduction |
| Base URL | `https://partner.xcures.com` |
| Auth | OAuth 2.0 client credentials → HTTP Bearer (JWT), plus a `ProjectId` header |
| Agent surfaces | Six provider-published Agent Skills, an A2A agent card, and a remote MCP server |
| Pricing | Not published — contact-sales only |

## Notable findings

- **Six provider-published Agent Skills.** xCures serves machine-readable `SKILL.md` workflow guides
  unauthenticated at `/.well-known/agent-skills/`, with a discovery index carrying a sha256 digest per
  skill. Announced in the 2026-08-19 changelog. Captured verbatim in [`skills/`](skills/).
- **A real A2A agent card**, graded *conformant* against the A2A 1.0.0 hard checks — see [`a2a/`](a2a/).
- **A remote MCP server** at `https://docs.xcures.com/mcp`, OAuth-gated, with RFC 8414 and RFC 9728
  discovery documents — see [`mcp/`](mcp/).
- **FHIR R4 is declared in the contract**, not only claimed in marketing: 13 `/fhir/*` operations plus
  `_export`, with twelve responses defined by reference to the HL7 FHIR R4 Bundle definition.
- **HITRUST e1 certified**; HIPAA compliant. The SOC 2 Type 2 and ISO 27001 certifications named on the
  trust page belong to AWS and are inherited, not held by xCures — see
  [`security/xcures-trust-center.yml`](security/xcures-trust-center.yml).
- **No first-party SDK exists in any package registry** despite an "SDKs" link in the docs footer; what
  xCures calls its SDK is a Postman collection and a documentation surface.
- **Idempotency is partial** — client-supplied subject UUIDs give 409-on-duplicate replay protection on
  2 of 12 mutating operations; there is no `Idempotency-Key` header anywhere.
- **One reversible write.** Publishing a document to the exchange network can be unpublished; a
  dispatched network query cannot be recalled.

Source of record: [`apis.yml`](apis.yml).

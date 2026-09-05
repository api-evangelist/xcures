---
name: byod-ingestion
description: >-
  Upload a patient's existing medical records directly to xCures for normalization into
  FHIR R4 and Clinical Concepts, without querying any health information network. Use
  when an organization already holds a copy of a patient's records (payer, lab, or
  health system) and wants xCures to structure that data instead of retrieving it from
  Carequality/TEFCA.
rbac:
  '*': read
tags:
  - byod
  - workflows
---

# Bring Your Own Data (BYOD) Ingestion

## When to use

Use this skill when the application already holds a patient's medical records and
needs xCures to ingest, normalize, and structure them, rather than retrieving records
from a health information network. BYOD does not require Reciprocity, unlike Treatment,
Retrieval Only, and IAS.

## Steps

1. Create the subject with `POST /api/v2/patient-registry/subject`. The body requires
   `id` (a UUID you generate for this subject), `firstName`, and `lastName`. Set
   `options: { initiateEhrQuery: false }` — BYOD subjects should never trigger an
   automatic network query.
2. Register the document with `POST /api/v1/patient-registry/document`. The body
   requires `subjectId`, `fileName`, and `contentType`. The response returns
   `documentId` and a `signedS3Url`.
3. Upload the file bytes with an HTTP `PUT` directly to the `signedS3Url` from step 2.
   This is a pre-signed upload URL, not an xCures API call — do not send an
   `Authorization` header on this request.
4. Poll `GET /api/v1/patient-registry/subject/{id}/status/clinical-concepts` until
   `loaded` is `true`.
5. Once loaded, read the structured output the same way as Treatment subjects:
   `GET /api/v1/patient-registry/clinical-concepts/{type}?subjectId={id}` for any of
   the 15 concept types, plus FHIR Resources, Subject Summary, and Checklists.

## Reference

- xCures API reference: [https://docs.xcures.com/apis/current](https://docs.xcures.com/apis/current)
- Workflow diagram and walkthrough: [https://docs.xcures.com/api-introduction#bring-your-own-data-byod-workflow](https://docs.xcures.com/api-introduction#bring-your-own-data-byod-workflow)

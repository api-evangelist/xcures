---
name: retrieval-only
description: >-
  Query national health information networks (Carequality / TEFCA) for a patient's
  existing medical records and retrieve the raw documents, with no data extraction or
  Clinical Concepts processing performed by xCures. Use when an organization has its own
  processing pipeline and only needs xCures to handle network connectivity and document
  retrieval.
rbac:
  '*': read
tags:
  - retrieval-only
  - workflows
---

# Retrieval Only

## When to use

Use this skill when an application needs raw medical records from connected health
information networks with no downstream processing. xCures returns the retrieved
documents as-is. It does not extract, normalize, or structure them into FHIR R4,
Clinical Concepts, or Checklists, that work happens in your own pipeline. Retrieval
Only customers are also required to contribute documentation back to the network,
covered in the Reciprocity steps below.

## Steps

1. Create the subject with `POST /api/v2/patient-registry/subject`. The body requires
   `id` (a UUID you generate for this subject), `firstName`, and `lastName`. Set
   `options: { initiateEhrQuery: false }` so the explicit query in the next step is the
   only one fired.
2. Dispatch the query with `POST /api/v1/patient-registry/query`, which requires
   `subjectId` in the body (optionally scope it to specific networks with
   `organizationIds`).
3. Poll the query with `GET /api/v1/patient-registry/query/{id}` until its `ccdaStatus`
   reaches a terminal state. This typically takes 20 to 30 minutes.
4. List the retrieved documents with
   `GET /api/v1/patient-registry/document?subjectId={id}`.
5. For each document, get a time-limited download link with
   `GET /api/v1/patient-registry/document/{documentId}/pdf`, which returns `fileName`
   and a `signedUrl` valid for 15 minutes.
6. Reciprocity is mandatory for this product. List available templates with
   `GET /api/v1/patient-registry/reciprocity-template`.
7. Create the document record to publish with `POST /api/v1/patient-registry/document`.
   The body requires `subjectId`, `fileName`, and `contentType`; also set `documentDate`,
   publishing rejects documents without one. The response returns `documentId` and a
   `signedS3Url`.
8. Upload the file bytes with an HTTP `PUT` to the `signedS3Url` from step 7.
9. Publish the document with
   `PUT /api/v1/patient-registry/document/{documentId}/reciprocity` (no request body).
   A `403` here usually means Reciprocity is not yet enabled on the project, contact
   xCures support.

Do not call the Clinical Concepts or Checklist endpoints for Retrieval Only subjects.
xCures does not process these records, so those endpoints will not return meaningful
data for them.

## Reference

- xCures API reference: [https://docs.xcures.com/apis/current](https://docs.xcures.com/apis/current)

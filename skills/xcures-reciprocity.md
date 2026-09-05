---
name: reciprocity
description: >-
  Publish a clinical document back to a health information network (Carequality / TEFCA)
  for a patient whose records your project retrieved. Use when a project is a QHIN network
  participant and must satisfy its reciprocity obligation by sharing documentation with the
  network, separate from any Treatment or Retrieval Only query workflow.
rbac:
  '*': read
tags:
  - reciprocity
  - workflows
---

# Reciprocity

## When to use

Use this skill when a project has retrieved a patient's records from a QHIN-connected
health information network and must publish clinical documentation back to that network
to satisfy its reciprocity obligation. Reciprocity is required for Standard Treatment
Workflow and Retrieval Only projects; it does not apply to Bring Your Own Data (BYOD)
projects, which never query the network. Reciprocity must be enabled on the project, with
Requester Information and Encounter Information configured in the Administration UI,
before publish calls will succeed.

## Steps

1. List available templates with `GET /api/v1/patient-registry/reciprocity-template`
   (requires the `ProjectId` header). Each item in the response array includes an `id`,
   use this as `templateId` in step 4.
2. Create the document record with `POST /api/v1/patient-registry/document`. The body
   requires `subjectId`, `fileName`, and `contentType`; also set `documentDate` (ISO 8601),
   publishing rejects documents without one. The response returns `documentId` and a
   `signedS3Url`.
3. Upload the file bytes with an HTTP `PUT` to the `signedS3Url` from step 2. This is a
   direct upload to signed storage, not an xCures API call.
4. Publish the document with
   `PUT /api/v1/patient-registry/document/{documentId}/reciprocity`. The body requires
   `templateId` from step 1. A `403` here usually means Reciprocity is not yet enabled on
   the project, contact xCures support.

To revoke network availability without deleting the document, call
`DELETE /api/v1/patient-registry/document/{documentId}/reciprocity` (no request body).
The document remains in the project and can be republished at any time by repeating step
4; deleting it permanently requires a separate delete call.

## Reference

- xCures API reference: [https://docs.xcures.com/apis/current](https://docs.xcures.com/apis/current)

---
name: standard-treatment-workflow
description: >-
  Register a patient with xCures and retrieve their structured medical records from
  national health information networks (Carequality / TEFCA). Use when an application
  needs to onboard a new patient and pull their existing clinical history, conditions,
  medications, and documents into FHIR R4 or Clinical Concepts.
rbac:
  '*': read
tags:
  - treatment
  - workflows
---

# Standard Treatment Workflow

## When to use

Use this skill when an application needs to register a new patient in xCures and
retrieve their existing medical records from connected health information networks.
This is the default xCures workflow for organizations with an active Treatment
relationship with the patient, as opposed to BYOD (customer already holds the records)
or IAS (patient-directed, webhook-driven access).

## Steps

1. Create the subject with `POST /api/v2/patient-registry/subject`. The body requires
   `id` (a UUID you generate for this subject), `firstName`, and `lastName`. By default
   this also fires an EHR query automatically. To control query dispatch yourself
   instead, pass `options: { initiateEhrQuery: false }` and do step 2 explicitly.
2. If step 1 auto-fired the query, find it with
   `GET /api/v1/patient-registry/query?subjectId={id}`. Otherwise dispatch one yourself
   with `POST /api/v1/patient-registry/query`, which requires `subjectId` in the body
   (optionally scope it to specific networks with `organizationIds`).
3. Poll the query with `GET /api/v1/patient-registry/query/{id}` until its `ccdaStatus`
   reaches a terminal state. If it reaches `error`, dispatch a fresh query with
   `POST /api/v1/patient-registry/query` and poll again.
4. Once the query completes, list the retrieved documents with
   `GET /api/v1/patient-registry/document?subjectId={id}`.
5. Read structured data instead of raw documents with
   `GET /api/v1/patient-registry/clinical-concepts/{type}?subjectId={id}`, where
   `{type}` is one of the 15 supported concept types (for example `condition`,
   `medication`, `lab`, or `allergy`).
6. To evaluate a checklist against the patient, first look up available checklist
   definitions with `GET /api/v1/patient-registry/checklist`, then run one with
   `POST /api/v1/patient-registry/checklist/{checklistId}/evaluate`, which requires
   `subjectId` in the body.

## Reference

- xCures API reference: [https://docs.xcures.com/apis/current](https://docs.xcures.com/apis/current)
- Workflow diagram and walkthrough: [https://docs.xcures.com/api-introduction#standard-treatment-workflow](https://docs.xcures.com/api-introduction#standard-treatment-workflow)

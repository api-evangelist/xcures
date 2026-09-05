---
name: requery-patient
description: >-
  Check whether a patient already registered in xCures needs a fresh query against
  health information networks, and dispatch one if their records are missing, stale, or
  errored. Use when re-processing an existing roster, or when a patient's prior query
  needs a refresh rather than creating a new patient record.
rbac:
  '*': read
tags:
  - treatment
  - workflows
---

# Existing Patient / Requery

## When to use

Use this skill when a patient already exists in xCures and you need to decide whether
to dispatch a fresh query. Typical cases: a roster onboarded weeks ago that may need
refreshed records, or a patient whose previous query errored or returned thin data. Use
the Standard Treatment Workflow skill instead when the patient is not registered yet.

## Steps

1. Locate the subject. If you already know their `id`, fetch them directly with
   `GET /api/v1/patient-registry/subject/{id}`. Otherwise search with
   `GET /api/v1/patient-registry/subject`, filtering by fields like `lastName`,
   `firstName`, or `externalIdentifiers`.
2. Inspect their query history with `GET /api/v1/patient-registry/query?subjectId={id}`.
   Each result includes `ccdaStatus` and `createdAt`.
3. Decide whether to requery. Skip it if a prior query completed successfully within
   your freshness window, 30 days is a reasonable starting point, tune it to your own
   workflow. Requery if the most recent query errored, returned thin results, or is
   older than your threshold.
4. If requerying, dispatch a new query with `POST /api/v1/patient-registry/query`,
   which requires `subjectId` in the body (optionally scope it with
   `organizationIds`).
5. Poll the new query with `GET /api/v1/patient-registry/query/{id}` until its
   `ccdaStatus` reaches a terminal state, the same as onboarding a new patient.
6. Read the patient's current documents with
   `GET /api/v1/patient-registry/document?subjectId={id}` and structured data with
   `GET /api/v1/patient-registry/clinical-concepts/{type}?subjectId={id}`.

## Reference

- xCures API reference: [https://docs.xcures.com/apis/current](https://docs.xcures.com/apis/current)

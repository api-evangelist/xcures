---
name: bulk-patient-onboarding
description: >-
  Register a large roster of patients in xCures and dispatch queries for all of them,
  safely, without overwhelming the API or double-querying the network. Use when
  onboarding hundreds or thousands of patients at once instead of one at a time.
rbac:
  '*': read
tags:
  - treatment
  - workflows
  - bulk
---

# Bulk Patient Onboarding

## When to use

Use this skill when registering many patients at once, for example a roster import,
instead of the single-patient Standard Treatment Workflow. It covers chunked batch
creation, per-subject failure isolation, and safe concurrency, so a few bad rows or
network hiccups don't stall or corrupt the rest of the run.

## Steps

1. Split your roster into chunks of at most 10 patients. `POST /api/v1/patient-registry/subject`
   accepts up to 10 subjects per request.
2. For each chunk, send a batch body: `{ "subjects": [...], "options": {
   "initiateEhrQueries": false } }`. Each entry in `subjects` requires `id` (a UUID you
   generate), `firstName`, and `lastName`. Setting `initiateEhrQueries: false` prevents
   each creation from firing its own automatic query, since step 4 dispatches one
   explicitly, doing both would double your query volume against the network.
3. The response is an array of results in input order. A result with a `failureReason`
   means that specific subject failed, the other subjects in the chunk are unaffected.
   Record failures for retry; do not treat one failure as a reason to abandon the chunk.
4. For each subject that was created successfully, dispatch a query with
   `POST /api/v1/patient-registry/query`, which requires `subjectId` in the body.
5. Keep no more than 10 to 15 requests in flight at once across steps 2 and 4. Beyond
   that, expect `429` responses; back off rather than increasing concurrency further.
6. Run polling as a separate pass after every chunk in steps 2 through 4 finishes, not
   interleaved with creation. Poll each dispatched query with
   `GET /api/v1/patient-registry/query/{id}` until its `ccdaStatus` reaches a terminal
   state. Store the query IDs from step 4 so this pass can be resumed independently if
   interrupted, a single patient's query can take 20 to 30 minutes.

## Reference

- xCures API reference: [https://docs.xcures.com/apis/current](https://docs.xcures.com/apis/current)

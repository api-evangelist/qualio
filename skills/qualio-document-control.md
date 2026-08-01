---
name: Qualio document control
description: Create, retrieve, update and progress controlled documents (SOPs, policies) through their approval lifecycle in the Qualio QMS.
api: openapi/qualio-openapi.json
operations: [createDocument, queryDocuments, getDocument, updateDocumentContent, changeDocumentStatus, listDocumentVersions]
---

# Qualio document control

Operate on controlled documents in a Qualio tenant. All requests use API-key
authentication (`X-Api-Key` header — see `authentication/qualio-authentication.yml`);
the key must belong to an admin. Base URL `https://api.qualio.com`.

## Steps

1. **Discover templates** — `listDocumentTemplates` (`GET /v1/documents/templates`)
   to pick the controlled-document template to instantiate.
2. **Create the document** — `createDocument` (`POST /v1/documents/document`) with the
   chosen template and metadata.
3. **Set the body** — `updateDocumentContent`
   (`PATCH /v1/documents/document/{documentId}/content`) to write the document content.
4. **Progress the lifecycle** — `changeDocumentStatus`
   (`PUT /v1/documents/document/{documentId}/status`) to move draft → for review →
   for approval → effective, following your quality process.
5. **Verify** — `getDocument` (`GET /v1/documents/document/{documentId}`) and
   `listDocumentVersions` (`GET /v1/documents/document/{documentId}/versions`) to confirm
   state and version history.

## Rules
- Paginate list/query calls with `offset` and `limit`.
- No idempotency-key mechanism exists; do not blindly retry POSTs — re-query first.
- Handle `403` (non-admin / lacks permission), `404` (unknown id/code), `409`
  (conflicting state) and `429` (fair-usage rate limit — back off). See
  `errors/qualio-problem-types.yml`.

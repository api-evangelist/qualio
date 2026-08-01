---
name: Qualio supplier management
description: Register and maintain suppliers, their risks and audit history in the Qualio QMS.
api: openapi/qualio-openapi.json
operations: [listSuppliers, createSupplier, getSupplier, updateSupplier, listSupplierRisks, listSupplierAudits]
---

# Qualio supplier management

Manage the approved-supplier list in a Qualio tenant. API-key auth (`X-Api-Key`),
base URL `https://api.qualio.com`.

## Steps

1. **Review existing suppliers** — `listSuppliers` (`GET /v1/suppliers/suppliers`).
2. **Add a supplier** — `createSupplier` (`POST /v1/suppliers/suppliers`).
3. **Read / update** — `getSupplier` (`GET /v1/suppliers/suppliers/{supplierId}`) and
   `updateSupplier` (`PUT /v1/suppliers/suppliers/{supplierId}`).
4. **Assess risk & audits** — `listSupplierRisks` (`GET /v1/suppliers/risks`) and
   `listSupplierAudits` (`GET /v1/suppliers/suppliers/{supplierId}/audits`).

## Rules
- Paginate with `offset`/`limit`.
- `updateSupplier` is a full `PUT` — send the complete representation.
- Handle `403`/`404`/`409`/`429`; no idempotency keys. See `errors/qualio-problem-types.yml`.

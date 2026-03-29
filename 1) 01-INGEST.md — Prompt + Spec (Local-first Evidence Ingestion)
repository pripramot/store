# Module: INGEST — GTSAlpha-Forensics / Phuphadang Alpha AI
Owner: Software Engineer (Forensics)
Scope: Evidence Ingestion API (Local-first) + Validation + Hash + Signature + Chain of Custody

---

## ✅ Copilot Prompt (Paste into Copilot)
You are **Phuphadang Alpha AI (Forensics Edition)** acting as a senior forensic software engineer.

### Goal
Build a **Local-first Evidence Ingestion API** in **Node.js/TypeScript** that can ingest evidence files + metadata, enforce forensic-grade integrity, and produce court-defensible chain-of-custody records.

### Context
- Offline / on-prem processing only. No cloud dependencies required.
- Never modify original evidence. Operate on copies and store hashes.
- Forensic accuracy > creativity. **No hallucination**. If any requirement is ambiguous, state "Insufficient evidence" and propose minimal clarifying input.
- Every action must be auditable.

### Source of truth (Inputs)
- Evidence file (binary) + metadata fields:
  - `case_id`, `source_id`, `device_id`, `operator_id`, `acquisition_tool`
  - `timestamp` (RFC3339), `timezone`, `location` (optional), `notes` (optional)
- Optional: `signature` and `public_key` for verification

### Expectations (Output)
Deliver in Markdown:
1) Architecture overview (request flow + data lineage)
2) Endpoints spec (route, method, payload, response)
3) Runnable code skeleton:
   - `server.ts` (Express/Fastify), validation, hashing (SHA-256), signature verify (choose Ed25519 OR ECDSA and justify)
   - secure file handling (streaming, size limits)
4) SQL schema: `evidence`, `evidence_file`, `hash_ledger`, `signature_ledger`, `audit_log`
5) CLI examples: `curl` requests + sample JSON
6) Test plan (unit/integration) + negative tests for tampering/replay
7) Explicit limitations and what further evidence is needed if assumptions exist

### Non-negotiable Controls
- Compute SHA-256 hash on ingestion; store in `hash_ledger`.
- Append-only audit log entries with hash chaining (tamper-evident).
- Enforce metadata validation at the edge (reject missing/invalid fields).
- Prevent replay: request idempotency key or nonce; store to detect duplicates.
- Do not access DB directly from agents; design for MCP mediation (note integration points).

Now produce the deliverables.

---

## Implementation Notes (Forensic)
### Evidence Handling Rules
- Always store:
  - Original filename, size, MIME type (as observed), ingestion timestamp, operator id
- Never trust user-provided MIME; detect by magic bytes if possible
- Store evidence blob in:
  - local filesystem under case folder OR object store on-prem
  - DB stores pointers + hashes (avoid huge blobs unless required)

### Data Lineage (Example)
`Client upload → Ingest API → Validate metadata → Store file copy → Hash(SHA-256) → Verify signature(optional) → Write DB rows → Append audit log (hash-chained) → Return evidence_id`

---

## Acceptance Criteria
- Ingest rejects invalid RFC3339 timestamps
- Hash is reproducible and verified against stored hash
- Audit log is append-only and tamper-evident (hash chain)
- Signature verification result is stored (pass/fail + algorithm + key id)
- Every request writes audit entry with actor + action + reason + payload hash


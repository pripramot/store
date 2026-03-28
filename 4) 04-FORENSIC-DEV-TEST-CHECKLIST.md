# Forensic Dev Test Checklist — GTSAlpha-Forensics (Ingest/MCP/RAG)
Purpose: Ensure court-defensible integrity, reproducibility, and auditability.
Rule: If any check fails → block release (P0) unless risk accepted with documented waiver.

---

## 0) Definitions
- Evidence Integrity: evidence copy is immutable; integrity proven via hash/signature
- Chain of Custody: complete trace of who/what/when/why with tamper-evident audit
- Local-first: all critical operations function offline/on-prem without external dependency
- “No Hallucination”: system never invents facts; only cites retrieved sources or raw evidence

---

## 1) INGEST — Validation & Integrity Tests
### 1.1 Input Validation (P0)
- [ ] Reject missing required fields: `case_id, source_id, device_id, operator_id, acquisition_tool, timestamp`
- [ ] Reject invalid timestamp format (must be RFC3339) and impossible values (e.g., year < 1970)
- [ ] Enforce max file size and streaming upload (prevent memory blow)
- [ ] Verify filename/path sanitization (no path traversal: `../`, null bytes)
- [ ] Detect content type by magic bytes (do not trust user MIME)

### 1.2 Hashing & Reproducibility (P0)
- [ ] Compute SHA-256 on stored copy (not on transient buffer)
- [ ] Re-hash yields identical value on repeated read
- [ ] Hash stored in `hash_ledger` with algorithm, timestamp, actor
- [ ] Any bit-flip in file changes hash and is detectable

### 1.3 Signature Verification (P0/P1)
- [ ] Verify signature against provided public key (Ed25519/ECDSA) and store result
- [ ] If signature invalid → evidence still stored but flagged `verification_status=FAILED` + audit entry
- [ ] Key id/fingerprint stored; key rotation does not break historical verification

### 1.4 Idempotency & Replay Resistance (P1)
- [ ] Same `request_id/idempotency_key` does not duplicate evidence rows
- [ ] Replay with modified payload is rejected and logged

### 1.5 Audit Log (P0)
- [ ] Every ingest writes audit record (success/fail)
- [ ] Audit includes: actor, role, action, reason, payload_hash, result
- [ ] Audit log is append-only and hash-chained:
  - modifying any entry breaks chain verification

---

## 2) MCP — RBAC & Gateway Security Tests
### 2.1 Deny-by-default (P0)
- [ ] Unknown role → denied
- [ ] No endpoint accessible without auth (including metadata endpoints)

### 2.2 RBAC Matrix Coverage (P0)
- [ ] Investigator cannot alter evidence content
- [ ] Analyst cannot change roles/keys
- [ ] Admin cannot silently modify evidence (only manage identities/keys)
- [ ] Auditor is read-only, including inability to trigger analysis jobs

### 2.3 Case Scoping (P0)
- [ ] All reads/writes require `case_id` scope and enforce it server-side
- [ ] Attempt cross-case access is denied + audited

### 2.4 Audit Completeness (P0)
- [ ] Audit is written for:
  - allowed access
  - denied access
  - errors/timeouts
- [ ] Audit records include request_id + payload hash + prev hash link

### 2.5 Transport/Auth Hardening (P1)
- [ ] If using JWT: validate signature, expiry, audience, issuer (local)
- [ ] If using mTLS: cert pinning / local CA chain verified
- [ ] Rate limiting prevents brute force and enumeration

---

## 3) RAG — Anti-Hallucination & Citation Tests
### 3.1 Citation Enforcement (P0)
- [ ] Every paragraph/claim contains citations (`doc_id:chunk_id`)
- [ ] If retrieval returns no chunks → answer must be "Insufficient evidence"
- [ ] No output containing uncited legal claims

### 3.2 KB Integrity (P0)
- [ ] Each doc stored with SHA-256 hash + version + source
- [ ] Changing a document invalidates hash and triggers re-index pipeline
- [ ] Chunk ids are stable across runs (or mapping is recorded)

### 3.3 Retrieval Quality (P1)
- [ ] Hybrid retrieval returns expected chunks for a known query set
- [ ] Reranker (if used) is deterministic in offline mode
- [ ] Evaluation metrics tracked: citation coverage, precision@k, refusal rate

### 3.4 Prompt Injection / Data Exfil (P0)
- [ ] Documents containing instruction-like text cannot override system rules
- [ ] RAG answer does not reveal secrets (keys, tokens, internal paths) even if requested
- [ ] Sanitization/allowlist prevents loading untrusted documents

---

## 4) Cross-Cutting Forensic Requirements (All Modules)
### 4.1 Reproducibility (P0)
- [ ] Same input → same outputs (hashes, citations, deterministic logs)
- [ ] Build is pinned (lockfiles) and dependencies recorded (SBOM recommended)

### 4.2 Time & Clock Drift (P1)
- [ ] Store both: system ingestion time + evidence claimed timestamp
- [ ] If clock drift detected → flag and log; do not auto-correct silently

### 4.3 Evidence Lifecycle Controls (P0)
- [ ] No delete operation for evidence by default (tombstone only with approval)
- [ ] Export creates new artifact with its own hash + audit trail

### 4.4 Incident / Tamper Detection (P0)
- [ ] Provide a verification tool/command:
  - verify audit chain
  - re-hash evidence and compare ledger
  - verify signatures
- [ ] Any mismatch triggers a clear incident report format

---

## 5) Minimal “Release Gate” Checklist (P0 must pass)
- [ ] Ingest validation + SHA-256 + audit chain
- [ ] MCP deny-by-default + RBAC + case scoping + audit all requests
- [ ] RAG citation enforcement + refusal on no evidence + KB hashing
- [ ] Verification CLI exists and runbook documented
``

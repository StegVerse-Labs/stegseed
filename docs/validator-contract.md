# Validator Contract (StegSeed)

This document defines the minimum required behavior of a StegSeed validator.

A “validator” is any tool, service, CI job, or agent that asserts whether a given instance is StegSeed-compliant.

## 1. Inputs

A validator MUST be able to consume:

- A Seed Definition (Potential)
- A Seed Instance (Actual)
- A Witness Bundle (Proof)
- Referenced artifacts (as needed) or their hashes/manifests

Validators MAY operate offline if all required materials are present.

### 1.1 Optional Ecosystem Inputs

A validator MAY additionally consume:

- An **Acceptance Policy** (local rules for accepting imported reality)
- A **History / Ledger View** (events needed for budgets, one-shot constraints, and count-based rules)

If these are not provided, validators MUST NOT guess. They SHOULD return NEEDS_REVIEW for evaluations that require missing inputs (when operating in policy mode).

## 2. Required Validation Steps

### 2.1 Resolve Definition
The validator MUST:
- Load the referenced seed definition by `seed_id` and `seed_version`
- Confirm `entity_type` matches between definition and instance

### 2.2 Verify Definition Integrity
The validator MUST:
- Verify the definition signature (if present)
- Verify that `definition_hash` matches the supplied definition payload (if provided)

### 2.3 Verify Witness Bundle Integrity
The validator MUST:
- Fetch or load the witness bundle referenced by `witness_bundle_ref`
- Verify witness bundle hashes using `hash_manifest`
- Verify that required evidence items are included and hash-valid
- Verify witness signatures against the canonicalized witness manifest (see canonicalization rules)

### 2.4 Evaluate Admissibility
The validator MUST:
- Evaluate the definition’s admissibility `conditions` at the instance `substantiated_at` time
- Evaluate against world-state snapshots referenced in:
  - `admissibility_snapshot.world_state_refs` (instance)
  - `context.world_state_refs` (witness, if present)
- Confirm the evaluation yields admissible at substantiation time

The validator MUST NOT accept an instance that claims admissible if the evaluator yields blocked.

### 2.5 Enforce Evidence Obligations
The validator MUST:
- Load `evidence_obligations` from the seed definition
- Ensure the witness bundle contains required evidence types/scopes and minimum counts
- Ensure evidence entries are hash-addressed and integrity-checked

### 2.6 Authority Checks (Recommended)
When `authority_grant_ref` is present, validators SHOULD:
- Resolve the referenced authority grant
- Confirm the grant is **active** at `substantiated_at`
- Confirm the grant role/capability covers the asserted role(s)
- Confirm the grant itself has a valid witness bundle (integrity + signature)

### 2.7 Append-Only Consistency
Where history is available, validators SHOULD:
- Confirm no destructive operations are implied
- Confirm status transitions (supersede/revoke/retire) occur via new admissible instances

## 3. Policy Mode (Acceptance Policy)

When an Acceptance Policy is provided, the validator MAY run in **policy mode** for imported instances.

In policy mode, the validator MUST:
1. Perform full StegSeed validation (Sections 2.1–2.5)
2. Identify the source realm (from instance metadata or witness context if provided)
3. Apply assurance translation (if a translation rule matches source realm)
4. Apply minimum assurance thresholds for the requested **context**:
   - view / simulation / operational
5. Enforce required signers and extra evidence (if specified by policy)
6. Enforce risk budgets when a ledger/history view is available

If the Acceptance Policy requires budgets/history and those inputs are missing, the validator SHOULD return **NEEDS_REVIEW** rather than accept.

## 4. Output

A validator MUST produce a deterministic result for core validation:
- PASS (StegSeed-compliant)
- FAIL (non-compliant)

In policy mode, a validator SHOULD additionally support:
- ACCEPT
- REJECT
- QUARANTINE
- NEEDS_REVIEW

A validator SHOULD emit a structured report:
- failing rule(s)
- missing evidence
- signature failures
- condition evaluation results
- policy rule matched (if any)
- budget counters used (if any)

## 5. Security Requirements

Validators MUST:
- Treat missing required evidence as failure
- Treat invalid signatures as failure when signatures are required by obligations
- Treat mismatched hashes as failure
- Treat time-window violations as failure
- Prefer local verification and avoid reliance on centralized trust

## 6. Notes

StegSeed validation is about admissible existence, not business optimization.

If it affects the world, it must be provable.

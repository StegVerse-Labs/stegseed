# Canonicalization & Signing (StegSeed)

To make hashes and signatures interoperable, StegSeed requires deterministic canonicalization of JSON structures before hashing/signing.

## 1. Canonical JSON

StegSeed RECOMMENDS using the JSON Canonicalization Scheme (JCS), RFC 8785.

Key properties:
- UTF-8 encoding
- deterministic key ordering
- normalized number and string representations
- no insignificant whitespace

If JCS is not used, an alternative scheme MUST be documented and consistently applied across:
- definition hashes
- witness manifests
- signature payloads

## 2. What Must Be Canonicalized

### 2.1 Seed Definition
If `signature` is provided, it SHOULD be computed over a canonicalized form of:
- the seed definition object excluding the `signature` field itself

### 2.2 Witness Bundle
Witness signatures SHOULD be computed over:
- `hash_manifest` in canonical form
OR
- the entire witness bundle canonicalized, excluding signature fields

StegSeed v0.1 prefers signing the `hash_manifest` to avoid accidental signature invalidation due to metadata additions.

## 3. Hash Prefix Convention

StegSeed RECOMMENDS prefixing hashes with algorithm identifiers, e.g.:
- `sha256:<hex>`
- `sha512:<hex>`

Where tools store raw hashes, the `hash_alg` field MUST remain authoritative.

## 4. Evidence Artifact Hashing

Evidence artifacts referenced by URI MUST be integrity protected by:
- hashing the artifact bytes with the declared algorithm
- storing the resulting hash in the witness bundle

Artifacts SHOULD be immutable once referenced.

## 5. Time Anchoring

If a trusted time source is used (e.g., TSA, signed timestamping, secure NTP receipts), it MAY be included as evidence:
- `type: timestamp_receipt`
- `scope: system_state`

Time anchoring strengthens non-replayability but is not required for v0.1.

## 6. Goal

Canonicalization prevents “same meaning, different bytes” failures.

Signatures protect legitimacy.

Together they make StegSeed verifiable anywhere.

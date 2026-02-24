# StegSeed DNA

StegSeed DNA defines the structural invariants that all StegVerse-compliant systems MUST inherit.

These are not policies or preferences.  
They are architectural constraints that ensure all consequential operations obey the **Admissible Existence Axiom**.

Each strand describes:
- What MUST be true  
- Why it exists  
- Where it is enforced  

---

## Strand 0 — Validator Supremacy

**Invariant**  
No component may treat an entity as operationally real unless a conforming StegSeed validator attests validity.

**Purpose**  
Prevents soft bypass, implicit trust, or assumption-based activation.

**Enforced By**
- Official reference validator implementation
- Mandatory `seed_instance_hash` binding in downstream schemas
- Runtime rejection of unvalidated entities
- CI validation requirements for compliant systems

---

## Strand 1 — Admissible Existence

**Invariant**  
Nothing becomes operationally real unless it passes admissibility at ⟨time, conditions⟩ and leaves verifiable evidence.

**Purpose**  
Prevents ungoverned state transitions.

**Enforced By**
- `seed-definition.schema.json` (requires admissibility model)
- `seed-instance.schema.json` (requires substantiation metadata)
- Validators MUST evaluate admissibility predicates deterministically

---

## Strand 2 — Evidence Before Authority

**Invariant**  
Authority MUST be demonstrated through time-valid evidence, not assumed from identity or role alone.

**Purpose**  
Prevents silent, inherited, or retroactive privilege.

**Enforced By**
- Witness bundle signature requirements
- Time-scoped authority fields in instances
- Validators MUST verify role validity at substantiation time

---

## Strand 3 — Potential ≠ Instance

**Invariant**  
Definitions describe what may exist. Instances record what did exist.

**Purpose**  
Maintains separation between intent and consequence.

**Enforced By**
- Separate schemas for definitions and instances
- Instance schema MUST reference definition ID + version hash
- Immutable definition records

---

## Strand 4 — Witnessed Transition

**Invariant**  
Every consequential transition MUST produce a valid witness bundle.

**Purpose**  
Ensures transitions are inspectable and accountable.

**Enforced By**
- `witness-bundle.schema.json`
- Mandatory witness reference in every instance
- Validators MUST reject instances lacking a valid witness bundle

---

## Strand 5 — Local Verifiability

**Invariant**  
The validity of an entity’s existence MUST be independently verifiable without centralized services.

**Purpose**  
Ensures resilience, portability, and trust in disconnected environments.

**Enforced By**
- Content-addressed evidence references
- Deterministic validation rules
- Export packet formats containing complete proof sets
- No validator dependency on external network services

---

## Strand 6 — Append-Only History

**Invariant**  
Instantiated entities MUST NOT be erased. They may only be superseded, revoked, or retired through new admissible transitions.

**Purpose**  
Preserves causality and accountability.

**Enforced By**
- No destructive update operations in schemas
- Supersession and revocation modeled as new instances
- Ledger/audit trail requirements
- Validators rejecting mutation of historical records

---

## Strand 7 — Legitimacy Over Convenience

**Invariant**  
If admissibility or evidence is incomplete, the transition MUST fail.

**Purpose**  
Prioritizes safety and accountability over speed.

**Enforced By**
- Strict validator failure on missing or invalid requirements
- No “warning-only” existence transitions
- Required evidence obligations tied to definitions

---

## Strand 8 — Uniform Grammar Across Domains

**Invariant**  
The same admissibility and substantiation structure MUST apply to physical, digital, human, AI, and temporal entities.

**Purpose**  
Prevents governance fragmentation.

**Enforced By**
- Shared core schemas
- Shared Conditions DSL
- Shared witness bundle structure across all instance types
- Cross-domain validation consistency checks

---

## Strand 9 — Policy-Time Binding

**Invariant**  
An instance MUST bind to the exact definition version and admissibility rules in force at time t.

**Purpose**  
Prevents retroactive reinterpretation of history.

**Enforced By**
- Definition version hash embedded in instance
- Conditions DSL version field
- Validator refusal to re-evaluate prior instances under newer rule sets
- Immutable policy-version references within instances

---

# Relationship to the Axiom

The **Admissible Existence Axiom** defines the core rule.

StegSeed DNA encodes the mechanisms that make that rule unavoidable.

```
Axiom -> Law
DNA -> Enforcement Pattern
Principle -> Structural Invariant
Meaning -> Implementation Constraint
```

---

# Compliance Implication

A system claiming StegVerse alignment MUST demonstrate that its operations inherit and enforce all StegSeed DNA strands.

If a system allows:
- Unverified authority  
- Silent state creation  
- Non-witnessed transitions  
- Retroactive reinterpretation  
- Deletable history  

…it is NOT StegSeed-compliant.

---

# Summary

StegSeed DNA ensures every part of the ecosystem grows from the same genetic rules:

**Existence requires admissibility.**  
**Admissibility requires evidence.**  
**Evidence preserves history.**  
**History cannot be rewritten.**

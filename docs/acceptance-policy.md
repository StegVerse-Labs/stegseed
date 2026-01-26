# Acceptance Policy (StegSeed)

An Acceptance Policy defines how a realm/system decides whether to accept externally produced StegSeed instances and their witness bundles.

This is the ecosystem handshake layer: it governs *imported reality*.

## 1. Why Acceptance Policies Exist

Even if an instance is valid in its source realm, a receiving realm may require:
- stronger assurance tiers for operational use
- additional evidence for local regulations
- specific signers (inspector/regulator)
- bounded risk budgets for degraded operations
- quarantine rules for unknown origins

Acceptance is not “trust them.”  
Acceptance is “verify proof + apply local constraints.”

## 2. Core Concepts

### 2.1 Context
Acceptance requirements differ by how the imported reality will be used:

- **view**: awareness dashboards and monitoring
- **simulation**: modeling, testbeds, planning
- **operational**: production control and real-world actuation

### 2.2 Minimum Assurance by Context
A realm can set:
- view: allow C
- simulation: require B
- operational: require A

### 2.3 Assurance Translation
Different realms may define assurance tiers differently.
Translation maps foreign A/B/C into local A/B/C (or reject).

Example:
- foreign B → local C
- foreign C → reject

### 2.4 Actions
When an import is evaluated:
- **accept**: allow under context constraints
- **accept_read_only**: allow only for view/simulation
- **accept_and_upgrade**: accept then re-substantiate locally with additional evidence to reach a higher tier
- **queue_for_human_review**: cannot decide automatically
- **quarantine**: hold artifacts for investigation

### 2.5 Risk Budgets
Risk budgets allow controlled acceptance of lower-tier imports.

Example:
- “At most 3 Tier B operational imports per month for asset group X.”

Budgets must be auditable and enforced by validators.

### 2.6 Required Signers & Extra Evidence
Policies can require:
- specific signer kinds (e.g., inspector, regulator)
- specific signer identities
- extra evidence beyond the seed definition (local compliance)

## 3. Recommended Defaults

Most realms start with:

- Operational: require A
- Simulation: allow B
- View: allow C

And:
- Unknown realms → quarantine
- Missing history for budgets → queue for review

## 4. How Validators Use This

A receiving validator:
1. Verifies the incoming instance + witness bundle normally
2. Applies translation (if any) for the source realm
3. Applies minimum assurance requirements for the requested context
4. Enforces required signers / extra evidence
5. Enforces risk budgets (if history is available)
6. Returns accept / reject / quarantine / needs_review

## 5. Design Principle

Acceptance policies make legitimacy interoperable without centralization.

They enable:
- federated trust
- negotiated assurance
- bounded risk
- upgradeable proof chains

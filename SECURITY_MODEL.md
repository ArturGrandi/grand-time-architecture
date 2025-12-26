# Security Model (Research-Only)

## Status
This security model operates strictly within the boundaries
defined by ARCHITECTURE_1_0.md and FORMULAS.md.

Security mechanisms must preserve economic invariants
and must never redefine valuation logic or system meaning.
Active — Architecture & Specification Phase (research-only, non-production)

## Purpose
This document defines the security assumptions and safety constraints for the Grand Time architecture and GT 1.0 implementation artifacts.

It is **architecture-binding**: implementations MUST preserve these constraints.
This document does not introduce tokenomics, investment properties, or any production promises.

---

## 1. System Safety Priorities
Grand Time security is defined around the following priorities:

1. **No reflexive failure cascades**
   - failures must not create automatic sell-offs, liquidations, or price spirals.

2. **Invariant preservation over availability**
   - when uncertain, the system prefers pausing issuance over continuing with degraded assumptions.

3. **Stable semantics across assets**
   - asset suspension or oracle instability must not change protocol meaning or price behavior.

---

## 2. Threat Model (High-Level)
The model assumes the following classes of risk:

- oracle malfunction, manipulation, or downtime,
- stablecoin-specific failures (depeg, freeze, blacklist, bridge risk),
- multisig compromise or signer collusion,
- implementation bugs and integration errors,
- governance misinterpretation (attempts to redefine economic meaning via interfaces).

This repository is research-only, but safety constraints are written as if enforced by an implementation.

---

## 3. Emergency Asset Segregation (Level 1 + Level 2)
Grand Time assumes a multi-asset stablecoin environment.

### Level 1 — Asset Suspension
Any supported asset (USDT/USDC/DAI; extendable) may be suspended if:
- depeg risk increases materially,
- transfer/withdraw is blocked (freeze/blacklist),
- oracle feed becomes unreliable,
- issuer or bridge introduces unacceptable counterparty risk.

Suspension MUST:
- prevent new deposits of the suspended asset,
- keep accounting isolated for the asset’s balances,
- preserve protocol meaning and price semantics.

### Level 2 — Segregated Accounting
Suspended assets MUST be isolated into a segregated ledger domain so that:
- valuation logic does not incorporate unreliable balances,
- coverage calculations are computed from eligible assets only,
- no forced conversions are triggered.

Asset segregation MUST NOT:
- reduce protocol reference price,
- trigger liquidation logic,
- force exit conversions into other assets.

---

## 4. Mint Gating and Safety Pauses (Security Semantics)
When safety conditions are violated, GT 1.0 relies on a non-reflexive pause mechanism.

### Mandatory Safety Action
In any state where required safety assumptions are not met:
- **valuation issuance is paused**, and
- **daily mint is redirected to Time Capital**, and
- **protocol reference price remains unchanged**.

This safety action applies in particular to:
- oracle failure or inconsistency,
- coverage failure (insufficient eligible Stability Fund coverage),
- asset suspension events affecting eligibility,
- any verified inconsistency that would otherwise induce reflexive behavior.

This pause mechanism is a safety boundary: it prevents price drops driven by uncertainty.

---

## 5. Oracle Security Model

### Oracle Role
Oracles provide **reference valuation only**.

They do not:
- define economic meaning,
- trigger automatic sell-offs,
- enforce liquidation logic,
- alter protocol invariants.

### Oracle Failure Handling (Binding)
An oracle failure is any condition where the oracle feed is:
- unavailable,
- stale beyond acceptable bounds,
- inconsistent across sources,
- deviating beyond safety thresholds,
- provably manipulable under current market conditions.

**In case of oracle failure or inconsistency:**
- valuation issuance is **paused**,
- daily mint is **redirected to Time Capital**,
- protocol reference price **remains unchanged**.

No oracle failure may trigger:
- forced asset conversion,
- price collapse,
- reflexive mint adjustments.

Oracle restoration resumes normal operation only after consistency is re-established under protocol-defined rules.

---

## 6. Multisig Security Model (DAO Grand Time Fund)
Operational execution is expected to be controlled by a multisignature model (10 signers).

Security assumptions:
- signers are independent,
- no on-chain voting is used,
- no token-based governance exists.

The multisig MUST NOT be used to:
- redefine protocol meaning,
- introduce investment mechanics,
- change economic invariants without an explicit architecture update by the project owner.

---

## 7. Non-Goals (Explicit)
This security model explicitly does NOT:
- promise financial return or stability of value,
- define tokenomics or market behavior,
- describe production deployment controls,
- replace legal compliance requirements,
- introduce liquidation or leverage mechanisms.

---

## 8. Relationship to Other Documents
- ARCHITECTURE_1_0.md — canonical meaning, boundaries, invariants, and non-goals
- FORMULAS.md — formal representation of the model and invariant assumptions
- CONTRACT_MAP_V1.md — mandatory contract roles and enforcement points
- DAO_GRAND_TIME_FUND.md — execution and coordination layer constraints
- CONTRIBUTION_GUIDELINES.md — contribution scope enforcement

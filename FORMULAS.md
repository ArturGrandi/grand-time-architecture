# Grand Time — Formal Model (GT 1.0)

## Status
Active (Specification Reference)

## Scope
This document defines the formal mathematical and logical model
of the Grand Time system.

It specifies invariants, parameters, and valuation rules.
No production deployment is implied.

---

## Core Quantities

### Population Baseline (N0)
N0 denotes the official global human population
at the moment of system launch.

N0 is a runtime deployment parameter and MUST NOT be hardcoded.

Population verification after launch does not violate N0.
Verified humans exceeding N0 are treated as newly verified population
and accrue value with coefficient **1 : 1.5** from the moment of verification.

---

## Time Capital (TC)
Time Capital represents accumulated human time value
that is not released into valuation circulation.

TC is used as a stabilization buffer
and as a sink during valuation pauses.

---

## Daily Mint

### Total Daily Mint
Total daily mint is fixed:

M = 10,000,000 GUCT / day

This value is invariant under GT 1.0.

---

### DAO Fund Allocation
Daily allocation to DAO Grand Time Fund is fixed:

M_DAO = 111,111 GUC / day


This allocation is operational
and does not imply investment or profit mechanics.

---

### Valuation Allocation
Remaining daily mint is allocated according to
human time valuation logic and mint gate conditions:

M_VAL = M − M_DAO


Valuation minting is subject to coverage, stability,
and oracle safety constraints.

---

## Mint Coverage Gate

Valuation issuance is allowed only if coverage condition holds:

F_stab ≥ P × M_VAL

Where:
- F_stab — Stability Fund (eligible assets, USD-equivalent)
- P — protocol reference price
- M_VAL — valuation mint amount

---

### Gate Behavior
If coverage condition is violated:
- valuation issuance is paused,
- M_VAL is redirected to Time Capital,
- protocol reference price remains unchanged.

No reflexive price decrease is allowed.

---

## Stability Constraint
GT 1.0 enforces a **333-day stability standard**.

The stability constraint limits valuation behavior
but does not imply fixed price guarantees.

---

## Bonding Premium Constraint
Bonding premium is capped:

Premium ≤ 44%

This cap applies globally and invariantly.

---

## Oracle Role
Oracles provide reference valuation inputs only.

They do not:
- define economic meaning,
- trigger liquidation,
- enforce reflexive mint behavior.

Oracle failure triggers valuation pause,
not price or supply reconfiguration.

---

## Invariants Summary
- No forced fiat convertibility
- No profit guarantees
- No liquidation cascades
- No reflexive price mechanics
- Architecture defines meaning, not interfaces

---

## Relationship to Other Documents
- ARCHITECTURE_1_0.md — canonical system meaning
- SECURITY_MODEL.md — failure and attack handling
- DAO_GRAND_TIME_FUND.md — execution coordination
---

## Authority and Scope

This document specifies formal parameters and invariants only.

It does not define:
- economic meaning,
- governance intent,
- commercial or investment properties.

All semantic interpretation is defined
exclusively in ARCHITECTURE_1_0.md.

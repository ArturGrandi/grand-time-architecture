# Contract Map v1 — GT 1.0

## Purpose

This document defines the mandatory contract roles required to implement
the GT 1.0 protocol invariants.

It is a **binding architectural map**, not executable code and not an
economic discussion.

Architecture defines meaning.
Formulas define constraints.
Contracts enforce invariants.

Interfaces do not define economic meaning.

---

## Binding Mapping Principles

- Architectural documents define **economic meaning** (what GUCT is and is not).
- FORMULAS.md defines **formal constraints and invariants**.
- Smart contracts exist solely to **enforce those invariants**.
- Token standards (e.g. ERC-20) are optional technical interfaces only.

No contract may redefine protocol meaning.

---

## Mandatory Contract Roles

### 1. Protocol Config / Constants

**Responsibility:**  
Stores protocol-level constants and invariant parameters.

**Must enforce:**
- 333-day stability standard
- Bonding premium cap: **44%**
- Protocol fees: **0%** on stablecoin in/out (network gas excluded)
- Mint coverage gate thresholds and limits

---

### 2. Asset Registry

**Responsibility:**  
Single source of truth for supported assets and their operational status.

**Must enforce:**
- Stablecoin-agnostic design (USDT / USDC / DAI, extendable)
- Emergency asset suspension without affecting pricing or mint logic
- Definition of *eligible assets* for Stability Fund calculations

---

### 3. Oracle Adapter

**Responsibility:**  
Normalize asset prices into USD-equivalent reference values.

**Must enforce:**
- Oracle failure does **not** trigger reflexive price behavior
- Fail-closed or safe-fallback behavior aligned with protocol invariants
- No price decrease caused by oracle degradation

---

### 4. Funds Controller / Ledgers

**Roles:**
- Stability Fund Ledger (`F_stab`)
- Time Capital Ledger (`TC`)

**Must enforce:**
- `F_stab` includes only eligible assets from Asset Registry
- Time Capital is a separate accounting destination
- No implicit or hidden fiat convertibility

---

### 5. Mint Controller

**Responsibility:**  
Controls daily mint issuance and routing.

**Must enforce (binding):**
- Mint coverage gate:
  - If `F_stab < P × M`:
    - valuation issuance pauses
    - daily mint is redirected to Time Capital
    - protocol reference price does **not** decrease
- Issuance resumes only after coverage restoration

---

### 6. Pricing / Bonding Module

**Responsibility:**  
Reference price and bonding premium calculation.

**Must enforce:**
- Bonding premium cap: **44%**
- Small purchase rule:
  - purchases ≤ 111 daily shares priced at `P_next_min`
- Explicit prohibition of reflexive pricing mechanics

---

### 7. Emergency Segregation Layer (Level 1 + Level 2)

**Responsibility:**  
Operational isolation of failing or suspended assets.

**Must enforce:**
- Asset suspension does not alter pricing or mint invariants
- Segregation affects asset handling only, not economic meaning

---

## Explicit Non-Goals

- Not a whitepaper
- Not tokenomics
- Not an investment or fundraising document
- Not a production deployment plan

---

## Document Relationships

- ARCHITECTURE_1_0.md — economic meaning and boundaries
- FORMULAS.md — formal mathematical constraints
- gt1-formular-standard — non-production, spec-first reference

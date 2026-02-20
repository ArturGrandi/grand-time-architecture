# FORMAL_EVENT_PRECONDITIONS — Hoare-style Event Semantics (GT 1.0)

**Status:** Canonical · Frozen · GT 1.0 Event Semantics  
**Purpose:** To define formal preconditions and postconditions for each admissible event using Hoare-style notation.

For each event E:

{ P_E ∧ S ∈ D }  
δ(S, E)  
{ S' ∈ D ∧ Invariants Preserved }

Where invariants I1–I10 are defined in PROOF_OF_INVARIANT_PRESERVATION.md.

All operations defined only inside declared domain D.

---

## 1. OracleUpdate(price_vector)

Precondition:

- price_vector finite
- price_vector within declared tolerance
- No undeclared state referenced

Postcondition:

- Oracle state updated
- F_stab, F_liq, F_sys recalculated
- F_stab ≥ 0, F_liq ≥ 0, F_sys ≥ 0
- No direct mutation of Supply
- Invariants preserved

---

## 2. Deposit(asset, amount)

Precondition:

- amount ≥ 0
- asset in declared registry
- amount_USD finite
- amount_USD ≥ 0

Postcondition:

- F_liq := F_liq + amount_USD
- Supply unchanged
- All state variables finite
- Invariants preserved

---

## 3. Redeem(asset, amount)

Precondition:

- amount ≥ 0
- asset in declared registry
- amount_USD ≤ F_liq
- System not in containment pause for redeem path

Postcondition:

- F_liq := F_liq − amount_USD
- F_liq ≥ 0
- Supply unchanged
- Invariants preserved

---

## 4. MintTrigger

Precondition:

- Mint path enabled
- Coverage gate satisfied:
  F_stab ≥ P × M_VAL

Postcondition:

- mint_amount := min(daily_cap, declared bound)
- Supply := Supply + mint_amount
- No direct mutation of P
- No mutation of TimeCapital
- Invariants preserved

If coverage gate fails:

- mint_amount := 0
- Supply unchanged
- Invariants preserved

---

## 5. ActivationRequest(amount)

Precondition:

- amount ≥ 0
- amount ≤ latent TimeCapital
- Premium bounded by declared cap
- Activation path enabled

Postcondition:

- Activated_TimeCapital := Activated_TimeCapital + amount
- Activated_TimeCapital ≤ Total_TimeCapital
- Supply unchanged
- P unchanged
- Invariants preserved

---

## 6. EmergencyTrigger

Precondition:

- Declared trigger condition satisfied

Postcondition:

- Assets reassigned to segregated vault
- Mint and activation paths disabled
- Supply unchanged
- P unchanged
- Invariants preserved

---

## 7. EpochAdvance

Precondition:

- Time boundary reached

Postcondition:

- epoch := epoch + 1
- Rolling window updated
- No direct mutation of Supply, P, TimeCapital
- Invariants preserved

---

## Global Guarantee

For every admissible E and S ∈ D:

{ P_E ∧ S ∈ D }  
δ(S, E)  
{ S' ∈ D ∧ invariants preserved }

δ is:

- Deterministic
- Total over D
- Invariant-preserving

Outside D → fail-closed containment (FORMAL_BOUNDARIES.md).

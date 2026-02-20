# FORMAL BOUNDARIES — Declared Mathematical Domain (GT 1.0)

**Status:** Canonical · Frozen · GT 1.0 Declared Mathematical Domain  
**Purpose:** To formally define the declared mathematical domain D over which the GT 1.0 transition function δ is total.  
This document does not introduce formulas. It defines admissible input ranges and structural constraints.

---

## 1. Declared Domain D

The transition function δ : (S, E) → S' is total over declared domain D.

D consists of all state-event tuples (S, E) satisfying:

- All state variables are finite elements of the declared numeric domain.
- No state variable is NaN, undefined, or non-finite.
- All accounting quantities are ≥ 0.
- Epoch index ∈ ℕ.
- Oracle inputs ∈ declared tolerance bands.
- Zone definitions preserve declared monotonic structure.
- (S, E) conforms to declared transition and state formation rules.

D is the set of all well-formed states and events under the frozen GT 1.0 specification.

---

## 2. State Variable Constraints

For all S ∈ D:

- Supply ≥ 0
- TimeCapital ≥ 0
- TimeSafe ≥ 0
- F_stab ≥ 0
- F_liq ≥ 0
- F_sys ≥ 0
- P > 0
- M_VAL ≥ 0
- N_stat ≥ 0
- N_verified ≥ 0

Derived:
- N_eff = max(N_stat, N_verified)

If activation accounting is partitioned:
- Activated_TimeCapital ≤ Total_TimeCapital

Oracle constraint (within D):
- |price − peg| ≤ declared_tolerance

---

## 3. Event Constraints

For all E ∈ D:

- Events reference declared state variables only.
- Event payload is explicit and finite.
- No event introduces new state dimensions.
- Event ordering follows declared deterministic sequencing rule.
- No duplicate event identifiers under declared uniqueness rule.

---

## 4. Totality of δ

For all (S, E) ∈ D:

- δ(S, E) is defined.
- δ(S, E) produces S' ∈ D.
- δ never produces negative accounting state.
- δ never produces non-finite values.
- δ preserves declared structural invariants.

δ is total over D.

---

## 5. Domain Exit Handling (Fail-Closed Semantics)

If (S, E) ∉ D:

The system does not collapse.

Instead, containment behavior applies:

- Activation paths are disabled.
- Liquidity release is halted.
- Pause or segregation mechanism may be triggered.
- No unauthorized supply mutation occurs.

Domain exit results in containment,
not architectural failure.

Examples (outside D):

- Oracle price negative or non-finite.
- Accounting variable becomes undefined.
- Event malformed or structurally inconsistent.

---

## 6. Stability Domain

Declared stability invariants operate strictly within D.

Violation of domain constraints is not a stability breach.
It is domain exit and must trigger containment behavior.

---

## 7. Structural Interpretation

GT 1.0 is defined as:

- A total deterministic transition system
- Over explicitly declared domain D
- With fail-closed containment outside D

Undefined mathematical behavior is not permitted.
Collapse semantics are not defined within GT 1.0.

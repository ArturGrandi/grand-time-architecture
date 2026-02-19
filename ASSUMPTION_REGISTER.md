ASSUMPTION REGISTER — Structural Trust Surface (GT 1.0)

Status: Canonical · Spec-level assumption inventory

Purpose:
To explicitly enumerate structural assumptions upon which GT 1.0 depends.
This document does not introduce logic.
It makes implicit dependencies explicit.

An assumption is a required condition for structural validity.
It is not a guarantee.
Violation of an assumption alters the trust surface
but does not automatically constitute falsification.


---------------------------------------------------------------------

1. Oracle Assumptions

AR1 — Bounded Deviation
Oracle values are assumed to remain within declared tolerance bands.
Deviation beyond bounds places the system outside declared domain.

AR2 — Bounded Delay
Oracle updates are assumed to occur within declared maximum timing windows.

AR3 — No Coordinated Multi-Oracle Manipulation Within Bounds
Oracle feeds are assumed not to drift adversarially
while remaining simultaneously inside declared tolerance limits.

AR4 — Deterministic Read
Oracle adapter produces identical output for identical input
without hidden state.


---------------------------------------------------------------------

2. Temporal Assumptions

AT1 — Epoch Discreteness
Time is discretized into declared epoch boundaries.

AT2 — No Retroactive Mutation
Past epoch state cannot be mutated once committed.

AT3 — Deterministic Event Ordering
Event ordering follows declared deterministic rules.
No undeclared ordering mechanism exists.


---------------------------------------------------------------------

3. Structural Assumptions

AS1 — Transition Completeness
All state transitions occur exclusively via declared δ function.
δ is defined over declared domain or explicitly partial.

AS2 — No Hidden State
All state variables are declared in canonical specification.

AS3 — Activation Path Uniqueness
Time Capital can only enter circulating domain via declared Mint Gate.

AS4 — Zone Monotonicity Integrity
Bonding zones preserve declared monotonic pricing relationships.


---------------------------------------------------------------------

4. Accounting Assumptions

AA1 — Supply Traceability
All circulating supply changes are traceable via declared transitions.

AA2 — Latent-Circulating Separation
Time Capital and circulating supply remain structurally separated domains.

AA3 — Stability Invariant Coherence
Declared stability invariants are internally coherent under valid inputs.


---------------------------------------------------------------------

5. Determinism Assumptions

AD1 — Pure Transition Function
δ(S, E) contains no hidden randomness.

AD2 — State Isolation
Transition evaluation does not depend on external mutable state.

AD3 — No Implicit Scheduler
No undeclared concurrency or scheduling layer modifies ordering.


---------------------------------------------------------------------

6. Boundary Assumptions

AB1 — Frozen Scope
GT 1.0 scope remains frozen during evaluation.

AB2 — No Governance Override
No voting-based state mutation layer exists.

AB3 — No Fiat Convertibility Path
No implicit external redemption or convertibility channel exists.

AB4 — No Administrative Key Path
No privileged override exists outside declared transitions.


---------------------------------------------------------------------

7. Relationship to Threat Model

If a threat exploits violation of an assumption,
classification must reference this register.

If an assumption is invalidated,
architectural impact must be evaluated separately
from invariant violation.


---------------------------------------------------------------------

8. Interpretation Rule

If a structural dependency is discovered that is not listed here,
it must be added explicitly.

Unlisted implicit dependencies are treated as structural risk.

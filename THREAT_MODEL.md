THREAT MODEL — Structural Attack Surface (GT 1.0)

Status: Canonical · Spec-level risk analysis layer

Purpose:
To enumerate structural attack surfaces within declared GT 1.0 scope.
This document does not introduce new logic.
It identifies adversarial vectors operating within declared rules.


---------------------------------------------------------------------

1. Trust Assumptions

GT 1.0 operates under the following declared assumptions:

A1 — Oracle Boundedness
Oracle inputs are assumed to remain within declared tolerance
and timing constraints.
If boundedness is violated, the system is outside declared scope.

A2 — Deterministic Transition Integrity
δ(S, E) remains deterministic for identical ordered inputs.

A3 — No Hidden Administrative Override
No undisclosed privileged state mutation path exists.

A4 — Frozen Specification
GT 1.0 formulas and invariants are not modified during evaluation.


---------------------------------------------------------------------

2. Threat Categories

T1 — Oracle Timing Manipulation

Attack Surface:
Delayed oracle updates affecting stabilization thresholds.

Risk:
Temporary misalignment between F_stab and pricing logic.

Invariant Impact:
SR (containment), potentially CR if misapplied.


T2 — Oracle Value Boundary Exploit

Attack Surface:
Oracle values near tolerance boundary triggering activation paths.

Risk:
Edge-case activation without intended economic signal.

Invariant Impact:
CR (activation gate), declared stability consistency.


T3 — Liquidity Exhaustion

Attack Surface:
Rapid multi-asset withdrawal attempts.

Risk:
Stress on F_liq prior to containment trigger.

Invariant Impact:
SR (liquidity isolation), pause integrity.


T4 — Activation Asymmetry

Attack Surface:
Partial Time Capital activation under stress.

Risk:
Accounting imbalance between latent and circulating domains.

Invariant Impact:
CR (accounting symmetry), monotonic zone enforcement.


T5 — Multi-Asset Correlation Shock

Attack Surface:
Simultaneous external asset value drop affecting reserve assumptions.

Risk:
Compound stress on stabilization component.

Invariant Impact:
SR (reserve integrity), declared stability invariants.


T6 — Pause Abuse

Attack Surface:
Repeated triggering of pause condition via adversarial sequence.

Risk:
Operational denial effect without invariant breach.

Invariant Impact:
SR (containment integrity).


T7 — Verification Path Abuse

Attack Surface:
High-frequency verification attempts near nullifier boundaries.

Risk:
Replay or ordering asymmetry.

Invariant Impact:
CR (no double-claim), deterministic enforcement.


T8 — Deterministic Ordering Exploit

Attack Surface:
Adversarial ordering of valid events within same epoch.

Risk:
Non-commutative transition sequence leading to asymmetry.

Invariant Impact:
Deterministic transition integrity, CR layer.


---------------------------------------------------------------------

3. Non-Threat Domain (Out of Scope)

The following are explicitly excluded:

N1 — Nation-state oracle takeover.
N2 — Full validator collusion.
N3 — Fiat regulatory override.
N4 — Redesign proposals altering declared formulas.
N5 — Market equilibrium or incentive stability analysis.


---------------------------------------------------------------------

4. Threat Evaluation Criteria

A threat is structurally material if:

- It operates within declared domain D (state, transition, oracle bounds).
- It respects declared specification constraints.
- It results in one or more of:
    CR violation,
    SR violation,
    deterministic inconsistency,
    unauthorized supply expansion,
    declared stability invariant breach.


---------------------------------------------------------------------

5. Containment Philosophy

GT 1.0 prioritizes:

- Deterministic containment over reactive governance.
- Structural invariants over economic tuning.
- Fail-closed behavior over discretionary adjustment.

All containment transitions must be explicit in δ.
No discretionary override paths are assumed.

If a threat results in Structural Failure,
it must be recorded in FALSIFICATION_REGISTRY.md.


---------------------------------------------------------------------

6. Relationship to Other Layers

PROOF_SURFACE.md
Defines deterministic and invariant logic.

FALSIFICATION_SURFACE.md
Defines admissible adversarial attempts.

FALSIFICATION_REGISTRY.md
Records outcomes.

This document enumerates potential attack vectors
prior to adversarial execution.

GLOSSARY — Canonical Structural Terms (GT 1.0)

Status: Canonical · Spec-level semantic layer

Purpose:
To define minimal structural terminology used across GT repositories.
This document ensures semantic consistency.
It does not redefine formulas, parameters, or invariants.


---------------------------------------------------------------------

1. Core Units

GUCT
Grand Unit of Coordinated Time.
Primary accounting unit defined by GT 1.0 formulas.

Time Capital
Latent accounting stock representing accumulated but non-circulating time.
May enter circulating accounting domain only via declared Mint Gate rules.

TimeSafe
Accumulation buffer for deferred distribution.
Does not directly increase circulating accounting supply.

Supply
Circulating accounting quantity of GUCT currently active in protocol state.


---------------------------------------------------------------------

2. Stability & Funds

333-day stability
Canonical declared stability invariant of GT 1.0.
Constrains system behavior across defined temporal accounting boundaries.

F_stab
Stabilization reserve component used in declared stability logic.

F_liq
Liquidity reserve component used in declared liquidity logic.

F_sys
System reserve component used for structural accounting separation.

M_VAL
Declared valuation reference variable used in pricing logic.

P
Protocol price reference defined by bonding logic.


---------------------------------------------------------------------

3. Structural Mechanisms

Mint Gate
Declared rule path governing authorized supply activation.

Activation
State transition event (via δ) enabling release of Time Capital
into circulating accounting domain under declared conditions.

Zone Z0 / Z1
Bonding curve regions defined in pricing module.
Z1 must not produce a lower effective price than Z0.

Oracle Adapter
Declared bounded input layer providing external data
under defined trust assumptions.


---------------------------------------------------------------------

4. Invariant Layers

CR (Correctness Requirements)
Structural invariants governing accounting validity.

SR (Safety Requirements)
Structural invariants governing containment and system integrity.

Deterministic Transition
δ(S, E) → S' produces identical output
for identical ordered inputs.


---------------------------------------------------------------------

5. Structural Failure

Structural Failure
Invariant violation under valid declared inputs
without modification of specification.
Indicates architectural inconsistency.


---------------------------------------------------------------------

Rule of Interpretation

If ambiguity arises between repositories,
definitions in this document take semantic precedence
within the frozen GT 1.0 scope.

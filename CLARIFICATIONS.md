# CLARIFICATIONS — Canonical Behavioral Clarifications (GT 1.0)

**Status:** Canonical · Clarification Layer (no redesign)  
**Scope:** No change to invariants, formulas, genesis parameters, or declared transition structure.  
**Purpose:** To formalize operational semantics that were previously implicit but not explicitly ordered in the frozen specification.

## Clarification 1 — Daily Mint Behavior During Pause

**Date added:** 20 February 2026  
**Scope Reference:** FORMULAS.md (mint gate), SECURITY_MODEL.md (pause/redirection), gt1-formular-standard/spec (MintController)

**Background**  
The frozen GT 1.0 specification defines:  
- Daily mint = 10M GUCT.  
- Coverage gate: F_stab ≥ P × M_VAL.  
- Pause state triggered by oracle failure or security containment.  
- Redirection to Time Capital in containment scenarios.

However, the specification did not explicitly define the priority ordering of daily mint allocation while paused = true.

**Canonical Rule**  
Pause does not imply automatic full redirection of daily mint to Time Capital.  

Operational ordering is defined as follows:

1. Coverage gate (F_stab ≥ P × M_VAL) is always evaluated first.  
2. If coverage gate fails:  
   - Mint amount = 0.  
   - No supply expansion occurs.  
3. If coverage gate holds:  
   - While paused = true:  
     - The daily mint is first covered from available F_stab.  
     - If F_stab is sufficient to fully support the daily mint: mint proceeds normally.  
     - If F_stab is insufficient to fully support the daily mint:  
       - The covered portion mints normally.  
       - The uncovered portion is redirected to Time Capital.

No mint may violate the coverage gate.

**Structural Rationale**  
The system prioritizes active living participation over historical latent accumulation. Immediate full redirection during pause would unnecessarily penalize current participants when stabilization reserves remain available.

This clarification defines priority ordering only. It does not introduce new logic.

**Architectural Integrity**  
This clarification:  
- Preserves coverage gate enforcement.  
- Preserves the 333-day stability invariant.  
- Preserves non-negative accounting.  
- Preserves fail-closed containment outside declared domain D.  
- Introduces no new state variables.  
- Modifies no formulas.  
- Does not alter δ structure.

**Formal Impact**  
No modification required to:  
- FORMAL_BOUNDARIES.md  
- PROOF_OF_TOTALITY.md  
- PROOF_OF_INVARIANT_PRESERVATION.md  
- PROOF_OF_STABILITY_WINDOW.md

This clarification resolves an unspecified semantic ordering within the already frozen architecture.

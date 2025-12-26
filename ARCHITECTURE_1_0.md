# Grand Time Architecture 1.0

## Status
Architecture 1.0 — Active (Research-only)

## Purpose
This document defines the canonical architecture of the Grand Time system.
It establishes meaning, boundaries, invariants, and explicit non-goals.

## Core Principle
Human time is treated as an independent unit of economic meaning,
parallel to money but not reducible to or convertible into it.

## System Layers
- Conceptual layer (meaning, time, contribution)
- Formal layer (formulas and invariants)
- Implementation layer (interfaces only, optional)

## Population Baseline (N0)
N0 represents the official global human population
at the moment of system launch.

N0 is a runtime deployment parameter and MUST NOT be hardcoded.

Any verified human accounts exceeding N0 after system launch
are treated as newly verified population and accrue value
with coefficient **1 : 1.5** from the moment of verification.

Population growth handling does not modify economic invariants
and does not imply capped supply or demographic constraints.

## GUCT Definition
GUCT represents capital of human time.

It is not a currency, not a security,
and not an investment instrument by nature.

Any token standard (e.g. ERC-20) is an implementation interface only
and does not define economic meaning.

## Invariants
- No forced convertibility to fiat
- No profit guarantees
- No reflexive price mechanics
- Architecture defines meaning, not interfaces

## Non-Goals
- No investment offering
- No tokenomics
- No yield, dividends, or speculation layer
- No production deployment implied

## Relationship to Other Documents
- FORMULAS.md — formal mathematical representation
- DAO_GRAND_TIME_FUND.md — execution and coordination layer
- COLLABORATION_AND_IMPLEMENTATION.md — research and engineering entry point

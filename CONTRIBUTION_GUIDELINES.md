CONTRIBUTION GUIDELINES

(GT 1.0 — Formular Standard)

1. Scope of Contributions

This repository is dedicated to the implementation of GT 1.0 as a finalized economic protocol.

All architectural, economic, and mathematical decisions are fixed and binding unless explicitly changed by the project owner.

This is not a discussion forum for redesigning core mechanics.

Contributions are accepted only within the scope of implementation, testing, verification, and tooling.

2. Fixed Context (Non-Negotiable)

The following elements are final and MUST NOT be modified, reinterpreted, or debated in issues or pull requests:

Capital Reserve (CR)

Stability Reserve (SR)

333-day stability standard

Mint coverage gate logic

Time Capital (TC)

Bonding premium cap (maximum 44%)

Zero protocol fees on stablecoin deposits and withdrawals

Multi-Asset Liquidity + Emergency Asset Segregation (Level 1 + Level 2)

Stablecoin-agnostic design (USDT / USDC / DAI)

Asset suspension without impact on price or mint logic

Growth logic, TC purchase mechanics, and fund separation

Any proposal that alters or questions these invariants will be rejected.

3. What Contributions Are Welcome

Valid contributions include:

Smart contract implementation strictly following GT 1.0 formulas

Reference implementations of protocol components

Test suites and edge-case simulations

Security analysis and invariant validation

Gas optimization without semantic changes

Oracle handling and asset segregation logic

Documentation that clarifies implementation details (not economics)

The guiding principle is:

Implement what is defined. Do not redefine what is implemented.

4. What Contributions Are NOT Accepted

The following are explicitly out of scope:

Economic redesign proposals

Alternative tokenomics

Changes to pricing, mint, or reserve logic

Governance redesign

Discussions about market strategy or adoption

Suggestions to add protocol fees

Replacing or weakening stability constraints

Converting GT 1.0 into a discussion or research playground

This repository exists to build, not to renegotiate.

5. Pull Request Rules

All pull requests must:

Reference the specific GT 1.0 formula or rule being implemented

Be narrowly scoped (one logical change per PR)

Include tests or validation logic where applicable

Preserve all fixed invariants

Avoid introducing optional behavior that affects economics

PRs that mix implementation with economic commentary will be closed.

6. Issues Policy

Issues should be used for:

Implementation clarifications

Bug reports

Edge-case identification

Security concerns

Tooling and testing gaps

Issues must NOT be used for:

“What if” economic scenarios

Protocol redesign discussions

Philosophical or academic debate

GT 1.0 is past the discussion phase.

7. Authority and Final Decisions

Final interpretation of GT 1.0 specifications rests with the project owner.

Maintainers reserve the right to:

close issues,

reject pull requests,

enforce scope boundaries,
without extended debate.

This is intentional and required for protocol integrity.

8. Contribution Philosophy

GT 1.0 is an implementation-first economic protocol.

The value of a contribution is measured by:

correctness,

precision,

adherence to specification,

robustness under failure scenarios.

Not by novelty or theoretical alternatives.

9. Summary

If you are here to:

implement a stable, invariant-driven protocol,

work on real contract logic,

contribute production-grade code,

you are welcome.

If you are here to redesign the system — this is not the right repository.

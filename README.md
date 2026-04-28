# Hive Inventions — Defensive Publication Index

This repository is the public disclosure record for the Hive Civilization invention family by **Stephen A. Rotzin**.

Each entry establishes a **public prior-art priority date** under 35 U.S.C. § 102 by virtue of being printed and time-stamped in this repository. Defensive publication does **not** by itself create enforceable patent rights; for inventions where enforceable rights are reserved, separate U.S. Provisional applications have been filed (see the table below).

## Filed U.S. Provisional Applications

| # | App. No. | Title | Filed |
|---|----------|-------|-------|
| 1 | 64/049,200 | Spectral-Banded Compliance Stamping for AI-Generated Content (`.smsh` wire header, tier-banded compliance attestations, DID binding) | 2026-04-24 |
| 2 | 64/049,207 | Compressed-Lexicon Encoding of Compliance State with Zero-Knowledge Visibility Tiers and Escrow-Released Audit Keys | 2026-04-24 |
| 3 | 64/049,213 | Composable Surface-Property Monetization in Autonomous Agent Economies | 2026-04-24 |
| 4 | 64/049,218 | Cryptographically-Anchored Universal Time Authority and SLA Enforcement (HiveClock) | 2026-04-24 |
| 5 | 64/049,226 | Auditable Zero-Knowledge Spend Delegation Using Hierarchical View-Key Trees (Invisible Juggernaut) | 2026-04-24 |

## Defensive Publications (this repo)

| # | Slug | Subject |
|---|------|---------|
| 12 | [12-hiveveil](inventions/12-hiveveil.md) | Zero-Knowledge Selective Disclosure for Tier, Role, and Wallet State in Autonomous Agent Networks |
| 19 | [19-spectral-smsh](inventions/19-spectral-smsh.md) | Spectral Classification + `.smsh` Binary Wire Format + Compensation Multiplier (unified) |

Inventions 12 and 19 are **also** subjects of separately filed U.S. Provisional applications (filing dates stamped at the head of each disclosure file). The disclosures here mirror the provisional content for public-record purposes.

## Reference Implementation (live)

A working reference of the Hive Supermodel Schema v1 — covering tier classification, role classification, and Verifiable Credential issuance under W3C VCDM 2.0 / Ed25519Signature2020 — is published at:

- JSON-LD context: `https://hivetrust.hiveagentiq.com/v1/trust/schema/supermodel/v1.jsonld`
- Schema spec (JSON): `https://hivetrust.hiveagentiq.com/v1/trust/schema/supermodel/v1.json`
- VC issuance endpoint: `https://hivetrust.hiveagentiq.com/v1/trust/vc/supermodel/issue`
- Credential type: `HiveSupermodelCredential`

Eight credentials of this type have been issued and bound to wallets on the Base blockchain (chain ID 8453) as of 2026-04-25.

## Convergence Note

These primitives (cryptographic agent identity, tier-bounded reputation, role classification, selective-disclosure VCs, x402-compatible payment receipts) are converging across multiple agent frameworks in 2026, including but not limited to:

- W3C Verifiable Credentials Data Model 2.0
- Cross-Trust Envelope Format (CTEF) v0.3.1 (frozen 2026-04-24)
- A2A Project (a2aproject/A2A)
- LangChain agent payments
- crewAI cryptographic identity
- AgentGraph / agent-mesh / Nobulex / APS

The specifications in this repository are offered to those efforts as published prior art. Building **on top of** the published mechanisms is encouraged. Independent re-implementation of the underlying claimed methods may require a license once the corresponding non-provisional applications mature.

## Contact

Stephen A. Rotzin · 170 Greenway Dr · Walnut Creek, CA 94596 · [srotzin@me.com](mailto:srotzin@me.com)

## License

Documentation in this repository: **CC BY 4.0** (attribution required, modifications permitted).
The underlying methods and systems are subject to **patent-pending** status — see [PATENT_PENDING.md](PATENT_PENDING.md).

<!-- HIVE-GAMIFICATION-META-START -->
## Hive Gamification

This MCP server is part of the Hive Civilization gamification surface (10-mechanic capability taxonomy).

- Capability taxonomy: https://hive-gamification.onrender.com/.well-known/hive-gamification.json
- Centrifuge dashboard: https://hive-gamification.onrender.com/.well-known/hive-centrifuge.json
- Consolidated OpenAPI: https://hive-gamification.onrender.com/.well-known/openapi.json

**Surface tags:** `gamification.spec.v1` · `gamification.surface.public` · `gamification.signal.read-only` · `gamification.settlement.real-rails`

Real rails on Base L2 (USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`). Read-only signal layer. Brand gold `#C08D23`.
<!-- HIVE-GAMIFICATION-META-END -->

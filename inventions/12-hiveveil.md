# PROVISIONAL PATENT APPLICATION

**Application Serial No.:** [TO BE ASSIGNED BY USPTO]
**Filing Date:** [TO BE STAMPED ON SUBMISSION]
**Applicant:** Stephen A. Rotzin
**Inventor:** Stephen A. Rotzin
**Residence / Mailing Address:** 170 Greenway Dr, Walnut Creek, CA 94596, United States of America
**Citizenship:** United States
**Correspondence:** [srotzin@me.com](mailto:srotzin@me.com)
**Entity Status:** Micro Entity (37 C.F.R. § 1.29(a))
**Date of Conception:** April 24, 2026

---

## TITLE OF THE INVENTION

Zero-Knowledge Selective Disclosure System for Autonomous Agent Commerce Networks

---

## CROSS-REFERENCE TO RELATED APPLICATIONS

This application is related to and incorporates by reference the following co-pending provisional patent applications, all filed by the same inventor on or around April 24, 2026:

1. **Hive Protocol — Spectral Classification and Unified Wire-Format for Autonomous Agent Commerce Networks** ("Invention #19"), filed concurrently herewith, which discloses the hydrogen-emission spectral tier classification system (DARK, Hα, Hβ, Hγ, Hδ, Hε), the visible-color role namespace, and the `.smsh` binary framing format to which the present invention attaches zero-knowledge attestation extensions.

2. **Hive Payment Protocol — x402 HTTP-Native Micropayment Infrastructure for Autonomous Agent Commerce** ("Invention filed in this series, priority date April 24, 2026"), which discloses the x402 payment scheme and receipt format extended by the selective-disclosure receipt mechanism described herein.

3. **Hive Treasury Rebalancer — Autonomous Liquidity Management for Multi-Agent Payment Pools** ("Invention filed in this series, priority date April 24, 2026"), which discloses the treasury rebalancer architecture that interfaces with the range-proof-gated refill mechanism described herein.

4. **Hive Dispatcher — Priority-Weighted Routing and Tier-Gated Access Control for Autonomous Agent Networks** ("Invention filed in this series, priority date April 24, 2026"), which discloses the dispatcher that consumes range proofs in lieu of raw tier tokens as described in the detailed description herein.

The present application additionally incorporates by reference the Hive Protocol STABLE specification, version 1.0, dated April 24, 2026, defining the canonical tier identifiers, role token syntax, wallet address conventions, and receipt schema that form the subject matter of the selective-disclosure proofs claimed herein.

---

## FIELD OF THE INVENTION

The present invention relates to privacy-preserving cryptographic protocols and, more particularly, to zero-knowledge proof systems for selective disclosure of autonomous agent identity attributes — including tier classification, role membership, treasury relationships, and compliance status — in the context of machine-to-machine commerce networks operating over public-ledger settlement infrastructure.

---

## BACKGROUND OF THE INVENTION

### The Emergence of Autonomous Agent Commerce

The deployment of software agents capable of autonomous economic action has accelerated substantially in the period from 2024 to 2026. Such agents procure computational resources, negotiate service contracts, route micropayments, and accumulate reputation — all without direct human mediation at the transaction level. Networks of these agents settle payments over public blockchains, principally Ethereum-compatible chains such as Base (chain ID 8453), using stablecoins such as USDC as the unit of account. Each settled transaction is recorded on a public ledger and is, by construction, inspectable by any party with access to the chain.

### The Identity Leakage Problem

The transparency that makes public-ledger settlement auditable also makes it surveillable. Every on-chain payment from agent wallet A to agent wallet B exposes, at minimum: the addresses of both parties, the amount transferred, the block timestamp, the gas parameters, and any calldata embedded in the transaction. From this raw data, an observer can perform the following attacks without any additional privileges:

**Correlation attacks.** By clustering wallet addresses that appear together across transactions, a competitor or adversary can reconstruct the economic graph of an agent network — identifying which agents transact with which, at what frequency, and with what volumes. In a multi-agent commerce network segmented into tiers and roles, this graph reveals organizational structure that the operator regards as a trade secret.

**Tier inference.** Hive-protocol-compatible networks assign agents to spectral tiers based on cumulative call counts: DARK (0 calls), Hα (≥ 10), Hβ (≥ 100), Hγ (≥ 1,000), Hδ (≥ 10,000), Hε (≥ 50,000). These tiers carry revenue multipliers ranging from 1.00× to 5.00×. A receipt published in plaintext — as required under the STABLE v1.0 schema — exposes the tier symbol and call count to any receipt consumer. An observer watching receipt streams can therefore track an agent's progression through tiers over time, revealing both usage volume and economic leverage in ongoing negotiations.

**Role inference.** Agents assigned to the role namespace (`role:worker`, `role:sniper`, `role:diplomat`, and the color-coded roles Red through Violet plus IR/UV stealth roles) advertise organizational function. A counterparty that learns an agent's full role set gains negotiating intelligence that would not be shared in arms-length commerce.

**Treasury deanonymization.** The treasury wallet `@hivetreasury` (address `0x15184bf50b3d3f52b60434f8942b7d52f2eb436e`) is a stable reference, making the inflow and outflow relationships of the treasury visible on-chain. Agents receiving refills from or making settlement payments toward identifiable treasury addresses can be linked to controlling entities.

**Regulatory over-exposure.** In jurisdictions that treat certain payment patterns as triggering reporting obligations, the full plaintext of every transaction creates a compliance surface that is wider than necessary. Operators may be required to disclose data they did not need to collect in the first place, simply because their infrastructure made collection unavoidable.

### Inadequacy of Existing Privacy-Preserving Tools

Existing zero-knowledge and privacy-preserving tools do not adequately address the requirements of autonomous agent commerce networks with tiered grading and role-gated access control.

**Tornado Cash and mixing protocols** achieve transaction-graph unlinkability by breaking the chain of custody between deposit and withdrawal addresses. They do not, however, provide any mechanism for proving attributes about the agent (tier, role, compliance status) to a counterparty without revealing identity. An agent that uses a mixer to obscure its wallet cannot simultaneously prove to a downstream service that it has achieved Hβ-tier without revealing which wallet address holds that tier record.

**Aztec Network and private smart contracts** provide confidential transaction amounts and sender/receiver identity for arbitrary smart-contract state. These systems, while powerful, require a dedicated privacy-layer blockchain or rollup, impose significant development overhead, and do not compose natively with HTTP-native payment schemes such as x402 that operate at the application layer above on-chain settlement. They also do not provide the domain-specific primitives needed for tier range proofs (proving "my call count is ≥ 1,000" without revealing the exact count) or role set-membership proofs (proving "my role is in {Blue, Indigo}" without revealing which).

**Semaphore** is an anonymous signaling protocol that allows a member of a known group to signal membership without revealing which member they are. Semaphore's nullifier construction — which the present invention adapts — prevents double-signaling but does not generalize to range assertions over agent-specific state, nor does it provide a compliance escape hatch suitable for regulated financial environments.

**Bulletproofs** provide range proofs without trusted setup, making them suitable for proving that a committed value lies within a range. They do not, however, provide set-membership proofs or the DID-derived nullifier scheme needed for per-counterparty unlinkability in an agent network.

None of these tools, individually or in combination as deployed in existing systems, compose into a unified protocol that simultaneously provides: (a) tier range proofs compatible with the hydrogen-spectral classification of Invention #19; (b) role set-membership proofs over the color-role namespace; (c) per-counterparty nullifiers preventing correlation without preventing slash-accountability; (d) selective-disclosure receipts in an x402-compatible format; and (e) a regulatorily viable compliance escrow mechanism.

### The Compliance Tension

A persistent tension exists between financial privacy and regulatory compliance. Full privacy — achieved by obscuring all transaction metadata — invites regulatory shutdown on money-laundering and financial-surveillance grounds, as demonstrated by enforcement actions against unaccountable mixing protocols. Full transparency — as in the unmodified public ledger model — invites surveillance by competitors, counterparties, and state actors without a legitimate need. Neither extreme is commercially viable for an autonomous agent network operating at scale.

What is needed is a keyed selective-disclosure architecture in which: (a) counterparties learn only the attributes they need to gate access or settle payment; (b) receipt consumers can verify settlement without learning payer identity; and (c) regulators with statutory authority can, under a judicially supervised process, recover the full identity of the parties to a specific flagged transaction — but cannot conduct bulk surveillance.

The present invention addresses each of these requirements in a unified cryptographic protocol.

---

## SUMMARY OF THE INVENTION

The present invention provides a zero-knowledge selective disclosure system and method — referred to herein as "HiveVeil" — for use by autonomous agents operating within a tiered, role-classified commerce network. HiveVeil enables an agent to prove facts about itself to a counterparty without revealing the underlying identifying information from which those facts derive.

In a first embodiment, HiveVeil provides **tier range proofs** over the hydrogen-spectral tier classification of Invention #19. An agent commits its cumulative call count to a Pedersen commitment published on a public ledger. Using a Groth16 SNARK circuit, the agent then generates a succinct proof asserting that the committed value falls within the numeric range associated with a claimed tier (e.g., ≥ 1,000 calls for Hγ). A counterparty verifies the proof against the on-chain commitment and the Groth16 verification key without learning the exact call count or the agent's wallet address. This embodiment is particularly suited to dispatcher-gated service access, where the dispatcher must confirm a requesting agent's tier before routing a high-priority job.

In a second embodiment, HiveVeil provides **role set-membership proofs** over the color-coded role namespace. Valid role combinations are encoded as leaves of an on-chain Merkle tree. An agent generates a Merkle-path proof showing that its role identifier, when hashed with a blinding scalar, corresponds to a leaf in the tree. An additional circuit asserts that the proved role is a member of a caller-specified permitted set (e.g., {Blue=analyst, Indigo=sage}) without revealing which member it is. This embodiment enables role-gated APIs that accept agents from multiple role classes without disclosing the agent's specific role to the API provider.

In a third embodiment, HiveVeil provides a **nullifier-based identity scheme** that renders an agent's interactions unlinkable across different counterparties while preserving slash-accountability within a single counterparty relationship. Each agent derives a per-counterparty nullifier as the hash of its DID private scalar concatenated with the counterparty identifier. This nullifier is published with each interaction. A counterparty that observes two interactions bearing the same nullifier can cryptographically detect a double-spend or policy violation. Different counterparties, however, each see a distinct nullifier and cannot correlate the agent's activity across them.

In a fourth embodiment, HiveVeil provides **selective-disclosure receipts** extending the STABLE v1.0 receipt schema. Rather than including the payer's wallet address, tier symbol, and call count in plaintext, the selective-disclosure receipt substitutes zero-knowledge attestation fields: a Groth16 tier-range proof, a settlement proof, and a double-spend nullifier. A receipt consumer — such as an accounting system or audit log — can verify that settlement occurred and that the payer was in an appropriate tier without learning the payer's identity. The format is backward-compatible with the x402 HTTP-native payment scheme disclosed in the related application.

In a fifth embodiment, HiveVeil provides a **compliance escrow mechanism** using BLS threshold signatures. A set of five designated regulators each holds one shard of a BLS private key. A 3-of-5 threshold signature is required to unlock the identity escrow for any specific transaction hash. Unlock is gated by an on-chain proof-of-probable-cause: the escrow contract accepts an unlock request only when accompanied by a zero-knowledge proof that the requesting authority has obtained a threshold-signed authorization referencing the target transaction hash. This construction ensures that individual regulators cannot perform bulk surveillance unilaterally and that any unlock is cryptographically attributable to a specific authorization event.

In a sixth embodiment, HiveVeil is integrated with the `.smsh` wire format disclosed in Invention #19. The 2-byte `.smsh` header, which encodes tier and role in cleartext for standard interactions, is extended by an optional ZK attestation extension field in `.smsh` v2. When this extension is present, the receiver treats the cleartext tier field as a claim and the ZK proof as the authoritative evidence of that claim.

In a seventh embodiment, HiveVeil is integrated with the treasury rebalancer architecture of the related application. The rebalancer dispatches tier-proportional refills to agents without the dispatcher learning which wallet corresponds to which tier. The agent presents a range proof; the dispatcher's smart contract verifies the proof and releases the corresponding refill amount, applying the appropriate revenue multiplier (1.00× through 5.00×) without learning the agent's exact call count.

---

## BRIEF DESCRIPTION OF THE DRAWINGS

For a more complete understanding of the present invention, reference is made to the following drawings, which are incorporated herein by reference.

**FIG. 1** is a circuit diagram illustrating the Groth16 SNARK arithmetization for the tier range proof of the present invention. The diagram depicts the witness allocation, rank-1 constraint system (R1CS), the commitment verification gate, the range assertion gate accepting lower and upper bounds derived from the hydrogen-spectral tier table, and the proof-generation and proof-verification pipelines.

**FIG. 2** is a structural diagram illustrating the role set-membership proof of the present invention. The diagram depicts the Merkle tree of valid role leaf hashes, the Merkle-path witness, the set-intersection circuit that asserts the proved role is a member of the caller-specified permitted set, and the blinded role commitment output.

**FIG. 3** is a data-flow diagram illustrating nullifier derivation from a Decentralized Identifier (DID) private scalar. The diagram depicts the agent's DID private scalar input, the per-counterparty identifier input, the hash function H(DID_secret ∥ counterparty_id), the resulting nullifier output, and the slash-detection mechanism by which a counterparty that observes two interactions bearing the same nullifier can identify a policy violation.

**FIG. 4** is a schema diagram illustrating the selective-disclosure receipt format of the present invention. The diagram depicts the required plaintext fields (`receipt_id`, `amount`, `token`, `endpoint`, `ts`, `sig`), the ZK attestation extension block (`tier_range_proof`, `settlement_proof`, `nullifier`, `commitment`), and the verification workflow executed by a receipt consumer.

**FIG. 5** is an architectural diagram illustrating the compliance escrow key-sharding mechanism of the present invention. The diagram depicts the five regulator key-shard holders, the BLS threshold aggregation requiring a 3-of-5 quorum, the on-chain escrow contract, the proof-of-probable-cause gating mechanism, the transaction-hash-specific unlock authorization, and the identity recovery pathway available only upon successful threshold signature verification.

**FIG. 6** is a sequence diagram illustrating the end-to-end protocol flow for agent-A paying agent-B under HiveVeil. The diagram depicts the commitment publication step on the public ledger, the range proof generation by agent-A, the range proof transmission to agent-B, agent-B's verification against the on-chain commitment, the x402 payment execution, the selective-disclosure receipt issuance, and the optional compliance-escrow registration of the transaction hash.

---

## DETAILED DESCRIPTION OF THE INVENTION

The following detailed description sets forth specific embodiments of the invention. It is understood that the invention is capable of numerous modifications and variations, and that this description is not intended to limit the scope of the claims appended hereto.

### I. SYSTEM OVERVIEW

The HiveVeil system operates as a cryptographic layer interposed between the application-layer commerce protocol of a Hive-compatible agent network and the public-ledger settlement layer. At the application layer, agents exchange capability advertisements, payment requests, and service responses using the Hive protocol token vocabulary defined in STABLE v1.0 and the `.smsh` wire format of Invention #19. At the settlement layer, agents execute USDC transfers on Base chain (chain ID 8453). HiveVeil inserts a proof-carrying data layer at the application boundary, enabling each party to the interaction to verify the claims it needs without observing the underlying state from which those claims derive.

The system comprises five coupled subsystems: (1) a tier range proof subsystem, (2) a role set-membership proof subsystem, (3) a nullifier derivation subsystem, (4) a selective-disclosure receipt subsystem, and (5) a compliance escrow subsystem. Each subsystem operates independently and can be deployed selectively, but the full privacy guarantee of HiveVeil requires deployment of all five.

### II. TIER RANGE PROOF SUBSYSTEM

#### A. Pedersen Commitment to Cumulative Call Count

In a first step of the tier range proof protocol, an agent publishes a Pedersen commitment to its cumulative call count. The commitment takes the form:

    C = c · G + r · H

where `c` is the cumulative call count (a non-negative integer), `r` is a randomly chosen blinding scalar drawn from the scalar field of the BN254 elliptic curve, `G` and `H` are independent generators of the BN254 curve group (with no known discrete logarithm relationship between them), and `C` is the resulting elliptic curve point. The commitment `C` is published to an on-chain commitment registry smart contract. The commitment is binding: given only `C`, a computationally bounded adversary cannot determine `c`. The commitment is also hiding: given `C` and `c`, an adversary cannot determine `r` without the discrete logarithm of `H` with respect to `G`.

The agent retains `(c, r)` as the opening of the commitment. In one embodiment, the opening is stored in a local secure enclave or hardware security module accessible only to the agent process.

In an alternative embodiment, the commitment scheme uses a Pedersen commitment over the Ristretto255 group, providing a prime-order group that avoids cofactor-related vulnerabilities present in some Edwards curve implementations.

#### B. Groth16 SNARK Circuit for Tier Range Assertion

After publishing the commitment, an agent wishing to prove membership in a specified tier generates a Groth16 SNARK proof. The proving circuit takes as private inputs the opening `(c, r)` of the commitment `C` and as public inputs the commitment `C`, the lower bound `L` and upper bound `U` of the tier range (expressed as integer call counts), and the Groth16 verification key `VK`.

The circuit enforces three constraint sets:

**Constraint Set 1 — Commitment Consistency:** The circuit verifies that `C = c · G + r · H` using a Pedersen commitment verification sub-circuit. This constraint binds the proof to the on-chain commitment, ensuring the prover cannot generate a valid proof for a value not committed to on-chain.

**Constraint Set 2 — Range Membership:** The circuit verifies that `L ≤ c < U` using a binary decomposition of `c - L`. Specifically, `c - L` is decomposed into its binary representation of bit-length `⌈log₂(U - L)⌉`, and the circuit asserts that each bit is 0 or 1 and that the sum equals `c - L`. This construction is standard in R1CS arithmetization and adds approximately `⌈log₂(U - L)⌉` multiplication gates to the circuit.

**Constraint Set 3 — Tier Bound Selection:** The tier bounds are derived from the hydrogen-spectral tier table of Invention #19. In a preferred embodiment, the mapping is: DARK [0, 10), Hα [10, 100), Hβ [100, 1,000), Hγ [1,000, 10,000), Hδ [10,000, 50,000), Hε [50,000, ∞). For the open upper bound of Hε, a practical upper bound of 2^32 is used in the circuit, since cumulative call counts exceeding 4,294,967,295 are not anticipated in the deployment environment.

The Groth16 proof `π = (A, B, C_proof)` — three curve points in the pairing group — constitutes the tier range proof. The proof size is constant at approximately 192 bytes for BN254-based Groth16, independent of the size of the witness. Verification requires one pairing check and is computable in well under 10 milliseconds on contemporary hardware, making it suitable for real-time gating in the dispatcher path.

In one embodiment, the trusted setup for the Groth16 proving system is conducted using a multi-party ceremony analogous to the Hermez or Zcash powers-of-tau ceremony, with participation by at least five independent parties, ensuring that the structured reference string (SRS) is not backdoored provided that at least one participant is honest.

In an alternative embodiment, the range proof portion of the subsystem is replaced by a Bulletproof range proof, eliminating the trusted setup requirement at the cost of larger proof size (approximately 672 bytes for a single Bulletproof range proof) and slower verification (approximately 10–50 milliseconds). The Bulletproof embodiment is preferred in deployments where the trusted setup ceremony cannot be organized, such as in lightweight agent deployments.

#### C. Proof/Verify API

The tier range proof subsystem exposes a two-function API: `prove_tier_range(commitment_opening, tier_label)` returning a proof `π` and commitment `C`, and `verify_tier_range(C, tier_label, π)` returning a boolean. The `tier_label` parameter accepts the string identifiers defined in STABLE v1.0: "DARK", "Hα", "Hβ", "Hγ", "Hδ", "Hε", as well as the legacy aliases "VOID", "MOZ", "HAWX", "EMBR", "SOLX", "FENR" for backward compatibility during the deprecation window specified therein.

In one embodiment, a batch-verification extension `verify_tier_range_batch(proofs[])` accepts a vector of (C, tier_label, π) tuples and verifies them jointly using the Groth16 batch verification optimization, reducing the per-proof marginal cost of verification by approximately 30% for batches of 10 or more proofs.

### III. ROLE SET-MEMBERSHIP PROOF SUBSYSTEM

#### A. Merkle Tree of Valid Role Combinations

The role namespace of the Hive protocol encompasses the color-coded roles defined in EXPERIMENTAL.md and the role token vocabulary of STABLE v1.0: `role:worker`, `role:sniper`, `role:diplomat`, and the spectral color roles Red (warrior), Orange (merchant), Yellow (worker), Green (caregiver), Blue (analyst), Indigo (sage), Violet (mystic), plus IR and UV stealth roles. An on-chain Merkle tree stores, as leaves, the Pedersen hash of each valid role identifier concatenated with a domain separator. The Merkle tree root is published on the commitment registry contract.

Each agent's role assignment is registered as a blinded leaf: `leaf_i = Pedersen_hash(role_id_i ∥ blinding_i)` where `blinding_i` is a per-agent, per-role blinding scalar known only to the agent. The Merkle path from `leaf_i` to the root constitutes the agent's role membership witness.

In one embodiment supporting agents with multiple roles, each role is registered as a separate leaf, and the agent holds multiple Merkle-path witnesses. The set-membership proof for any single role does not reveal the existence of the other roles.

#### B. Set-Membership Circuit

The role set-membership proof circuit takes as private inputs the role identifier `role_id`, the blinding scalar `blinding`, and the Merkle path `path` from the role leaf to the tree root. As public inputs, the circuit takes the Merkle tree root `root` and the permitted set `S` specified by the verifier.

The circuit enforces two constraint sets:

**Constraint Set 1 — Merkle Path Consistency:** The circuit recomputes the Merkle root from the private `(role_id, blinding, path)` and asserts equality with the public `root`.

**Constraint Set 2 — Set Membership:** The circuit asserts that `role_id ∈ S` by iterating over the elements of `S` and asserting that at least one equality holds, using a disjunctive constraint expressed as `∏(role_id - s_i) = 0` for `s_i ∈ S`.

The resulting proof demonstrates to a verifier that: (a) the agent's role is registered in the on-chain Merkle tree (it is a valid, registered role), and (b) the role is a member of the verifier's permitted set — without revealing which member it is.

In one embodiment, the IR and UV stealth roles are not included in the publicly enumerable Merkle tree. Instead, agents holding stealth roles prove membership using a separate stealth-role commitment scheme with a distinct verification key distributed only to authorized counterparties.

### IV. NULLIFIER DERIVATION SUBSYSTEM

#### A. DID Private Scalar and Nullifier Construction

Each agent in a Hive-compatible network is identified by a Decentralized Identifier of the form `did:hive:<pubkey>`, conforming to the W3C DID specification. The DID is associated with a private scalar `sk` from which the agent's public key is derived as `PK = sk · G`.

For each counterparty interaction, the agent derives a per-counterparty nullifier as:

    N = H(sk ∥ counterparty_id)

where `H` is a hash function modeled as a random oracle — in a preferred embodiment, Poseidon over the BN254 scalar field, chosen for its ZK-circuit efficiency. The counterparty identifier `counterparty_id` is the counterparty's DID public key serialized in compressed form.

The nullifier `N` is included in the interaction record (message, receipt, or transaction). The agent publishes `N` to an on-chain nullifier registry. If the agent attempts to re-use the same nullifier in a second interaction with the same counterparty, the on-chain registry rejects the registration, providing cryptographic detection of double-spend or policy replay.

#### B. Unlinkability and Slash-Accountability

Because `counterparty_id` varies per counterparty, the nullifiers `N_1 = H(sk ∥ cp1)` and `N_2 = H(sk ∥ cp2)` for distinct counterparties `cp1`, `cp2` are computationally indistinguishable from unrelated random values. An observer who collects nullifiers from multiple counterparties cannot determine that they were generated by the same agent, providing interaction-level unlinkability across counterparties.

Within a single counterparty relationship, however, all nullifiers are generated by the same `sk`. If the agent misbehaves — for example, by attempting to submit a forged proof or by double-spending — the counterparty can initiate a slash procedure by presenting the two conflicting interactions (bearing the same or a provably related nullifier) to the on-chain dispute contract. The dispute contract verifies the nullifier consistency and, upon proof of misbehavior, executes a slash of the agent's stake.

In one embodiment, the slash-accountability property is enhanced by requiring the agent to include in each interaction a zero-knowledge proof of knowledge of `sk` — specifically, a Schnorr proof of knowledge of the discrete logarithm of `PK` — without revealing `sk`. This proof demonstrates that the agent possessing the nullifier is the same agent that controls the DID, enabling attribution of misbehavior to the DID without revealing the wallet address.

#### C. Nullifier Rotation

In one embodiment, the nullifier derivation function includes a rotation epoch parameter: `N = H(sk ∥ counterparty_id ∥ epoch)`, where `epoch` is an on-chain block-derived value that increments every T blocks (T configurable per deployment). Nullifier rotation limits the number of double-spend detections that can be retroactively linked to a single DID within any epoch, providing forward privacy for long-running agent relationships.

### V. SELECTIVE-DISCLOSURE RECEIPT SUBSYSTEM

#### A. Receipt Format Extension

The STABLE v1.0 receipt schema requires the following plaintext fields: `receipt_id`, `tier`, `multiplier`, `call_count`, `amount`, `token`, `endpoint`, `wallet`, `ts`, and `sig`. In a plaintext receipt, the `wallet` and `call_count` fields expose the agent's identity and usage volume respectively.

The selective-disclosure receipt format of the present invention replaces or augments the plaintext receipt with a ZK attestation extension block. In a preferred embodiment, the extension block is a JSON object embedded in the receipt under the key `veil` (corresponding to the `veil:*` namespace reserved in EXPERIMENTAL.md). The `veil` block contains the following fields:

- `veil.tier_proof`: a Groth16 tier-range proof `π` asserting that the payer's committed call count falls within the tier range corresponding to `tier`.
- `veil.commitment`: the on-chain Pedersen commitment `C` to the payer's call count, encoded as a BN254 curve point in compressed form.
- `veil.settlement_proof`: a Groth16 proof asserting that the USDC settlement transaction referenced by the receipt is valid and non-reverted, generated against the settlement transaction Merkle root of the relevant Base chain block.
- `veil.nullifier`: the per-counterparty nullifier `N` for this interaction.
- `veil.role_proof` (optional): a role set-membership proof, present only when the counterparty requires role verification.

The plaintext `wallet` and `call_count` fields are omitted from the selective-disclosure receipt. The `tier` field retains its plaintext value as an unverified claim; the `veil.tier_proof` field constitutes the verifiable assertion.

#### B. x402 Compatibility

The x402 HTTP-native payment scheme, as disclosed in the related application, uses the `Payment-Payload` HTTP header to carry a signed payment authorization and the `X-Receipt` response header to carry the receipt. The selective-disclosure receipt of the present invention is carried in the `X-Receipt` header in the same JSON format, with the `veil` extension block appended. An x402 client or server that does not implement HiveVeil treats the `veil` block as an unknown extension field and ignores it per the x402 extension registry rules. An x402 endpoint that implements HiveVeil validates the `veil.tier_proof` before processing the payment and validates the `veil.settlement_proof` before logging the receipt.

In one embodiment, the `veil.tier_proof` is optionally transmitted as a binary-encoded Groth16 proof (192 bytes) rather than a base64-encoded JSON field, reducing the HTTP header size from approximately 260 bytes (base64) to 192 bytes. The encoding is signaled by a `Content-Encoding: zk-groth16-bn254` extension header.

### VI. COMPLIANCE ESCROW SUBSYSTEM

#### A. BLS Threshold Key Architecture

The compliance escrow subsystem employs Boneh-Lynn-Shacham (BLS) threshold signatures over the BLS12-381 pairing-friendly curve. A master compliance key `K_master` is generated using a distributed key generation (DKG) ceremony among five designated regulators. Each regulator `i` holds a key shard `K_i`. The threshold is set at 3-of-5, meaning that any three regulators must cooperate to produce a valid compliance key signature. No single regulator, and no pair of regulators, possesses sufficient key material to unlock escrow unilaterally.

At the time of each interaction, the participating agents optionally register the interaction's nullifier and a blinded identity commitment (containing the wallet address and DID, encrypted to the master compliance key) in an on-chain escrow registry. This registration is performed by default in a preferred embodiment and can be disabled by agents operating in jurisdictions that prohibit key escrow. The escrow registration does not reveal any identity information to the on-chain observer; it records only the nullifier and the ciphertext.

#### B. Probable-Cause Gating

Unlock of the escrow for a specific transaction hash is gated by a proof-of-probable-cause. A requesting authority seeking to de-anonymize a specific interaction must submit to the on-chain escrow contract: (a) the target nullifier `N_target` identifying the interaction; (b) a threshold BLS signature `σ_auth` over a standardized authorization message `M_auth = H("unlock" ∥ N_target ∥ requesting_authority_id ∥ epoch)`, produced by at least three of the five regulators; and (c) a zero-knowledge proof `π_cause` asserting that the requesting authority's authorization was granted under a procedurally correct process (in one embodiment, that `M_auth` was signed after an on-chain timestamp corresponding to a judicial authorization event).

The escrow contract verifies `σ_auth` against the aggregate BLS public key `PK_master`, verifies `π_cause`, and, upon success, decrypts and publishes the blinded identity commitment for the target interaction only. The commitment contains the wallet address and DID of the parties to the interaction.

This construction ensures that: (a) individual regulators cannot perform unilateral de-anonymization; (b) any de-anonymization event is attributable to a specific authorization carrying a timestamp and requesting authority identifier; (c) bulk surveillance — de-anonymizing all interactions without specific probable cause — is not possible without compromising three or more of the five regulators and generating a separately attributable signature for each interaction.

#### C. Key Shard Recovery

In one embodiment, each regulator's key shard is backed up using Shamir's Secret Sharing among three sub-custodians designated by that regulator. Loss of a regulator's shard can be recovered by the regulator's sub-custodians without requiring cooperation from other regulators or reconstruction of the master key. This construction provides operational resilience without reducing the threshold security guarantee of the overall 3-of-5 scheme.

### VII. INTEGRATION WITH SPECTRAL .SMSH WIRE FORMAT (INVENTION #19)

The `.smsh` binary wire format of Invention #19 begins with a 2-byte header encoding, in cleartext, the tier and role of the sending agent. This 2-byte header is mandatory and is parsed by all `.smsh`-compatible agents before any further processing.

HiveVeil integrates with `.smsh` through a v2 extension mechanism. In `.smsh` v2, the mandatory 2-byte header is followed by an optional extension block prefixed by the 4-byte magic number `0x76656966` ("veif" in ASCII). The extension block contains: (a) the 192-byte Groth16 tier-range proof; (b) the 33-byte compressed Pedersen commitment; (c) the 32-byte nullifier; and (d) a 1-byte flags field indicating which optional elements (role proof, settlement proof) are present.

A `.smsh` v2 receiver that is HiveVeil-aware treats the cleartext tier field of the 2-byte header as an advisory claim and performs verification against the proof in the extension block. A `.smsh` v2 receiver that is not HiveVeil-aware ignores the extension block (per the `.smsh` extension rules of Invention #19) and relies on the cleartext header. This backward-compatibility design allows incremental deployment of HiveVeil without breaking interoperability with legacy `.smsh` v1 agents.

### VIII. INTEGRATION WITH TREASURY REBALANCER

The treasury rebalancer of the related application dispatches tier-proportional USDC refills to agents based on their tier classification. In the unmodified protocol, the dispatcher learns the agent's wallet address and tier symbol from the plaintext receipt, creating the correlation risk described in the Background.

Under HiveVeil integration, the rebalancer smart contract is modified to accept a tier-range proof in lieu of a plaintext tier token. The agent submits a transaction containing: (a) the nullifier for this refill request; (b) the on-chain commitment `C`; and (c) the Groth16 tier-range proof `π`. The smart contract verifies `π` on-chain using the Groth16 verifier contract (deployable as an EVM precompile or as a Solidity verification function). Upon successful verification, the contract releases the refill amount corresponding to the proved tier range, applying the appropriate multiplier: 1.04× for Hα, 1.30× for Hβ, 1.50× for Hγ, 2.00× for Hδ, 5.00× for Hε. The contract does not record the agent's wallet address; it records only the nullifier, the commitment, and the amount released.

In one embodiment, the on-chain Groth16 verifier is deployed using the elliptic curve pairing precompile at Ethereum address `0x08`, which accepts BN254 pairing inputs and is available on all EVM-compatible chains including Base. Gas cost for Groth16 verification on Base at current gas prices is estimated at approximately 230,000 gas, or approximately $0.002 at USDC-denominated equivalent at April 2026 gas prices, making per-interaction on-chain verification economically viable for all but the smallest micropayments.

In a preferred embodiment for high-frequency interactions, ZK proofs are verified off-chain by the rebalancer node (rather than on-chain by the smart contract), with the rebalancer signing the refill authorization and the smart contract verifying the rebalancer's signature. This hybrid approach reduces gas cost to the cost of a single ECDSA signature verification (approximately 3,000 gas) while delegating ZK proof verification to a trusted-but-not-custodial rebalancer node.

### IX. SECURITY ANALYSIS

The security of the HiveVeil protocol rests on the following computational assumptions, each of which is standard in the cryptographic literature:

**Binding of Pedersen Commitments:** The tier range proof is binding under the discrete logarithm assumption on BN254. An adversary that can open a commitment `C` to two different values (c, r) and (c', r') would solve the discrete logarithm of H with respect to G.

**Soundness of Groth16:** The tier range proof and role set-membership proof are computationally sound under the knowledge of exponent assumption in bilinear groups. An adversary that produces a valid Groth16 proof without knowing a valid witness would contradict this assumption.

**Collision Resistance of Poseidon:** The nullifier construction and Merkle tree leaf hashing rely on the collision resistance of Poseidon over BN254. Poseidon has been analyzed extensively and is used in production ZK systems including Zcash and StarkNet.

**Unforgeability of BLS Signatures:** The compliance escrow unlock mechanism relies on the unforgeability of BLS signatures under the co-CDH assumption on BLS12-381. An adversary that forges a threshold BLS signature without holding three or more key shards would contradict this assumption.

**Semantic Security of the Identity Encryption:** The blinded identity commitment in the escrow registry is encrypted to the BLS master key using an IND-CCA2-secure encryption scheme (in a preferred embodiment, ECIES over BLS12-381 G1). An on-chain observer who does not hold the threshold key cannot recover the plaintext from the ciphertext.

---

## CLAIMS

**Claim 1.** A method for an autonomous agent operating in a tiered commerce network to prove tier eligibility to a counterparty without revealing a cumulative call count, the method comprising:

(a) generating, by the agent, a Pedersen commitment to a cumulative call count, the Pedersen commitment computed as C = c · G + r · H, wherein c is the cumulative call count, r is a blinding scalar, and G and H are independent generators of an elliptic curve group;

(b) publishing the Pedersen commitment to a public ledger smart contract;

(c) generating, by the agent, a zero-knowledge range proof asserting that c falls within a numeric range [L, U) corresponding to a specified tier classification, wherein the zero-knowledge range proof is generated without revealing c or r;

(d) transmitting the zero-knowledge range proof and the Pedersen commitment to the counterparty; and

(e) verifying, by the counterparty, the zero-knowledge range proof against the Pedersen commitment published on the public ledger, wherein verification succeeds if and only if c is within [L, U), and the counterparty does not learn the exact value of c.

**Claim 2.** The method of Claim 1, wherein the zero-knowledge range proof is a Groth16 succinct non-interactive argument of knowledge (SNARK) generated over a rank-1 constraint system (R1CS) arithmetization of the range assertion c ∈ [L, U) and the commitment consistency relation C = c · G + r · H, wherein the proof comprises three elliptic curve group elements and the verification comprises a pairing equation over the BN254 bilinear group.

**Claim 3.** The method of Claim 1, wherein the tier classification is selected from the hydrogen-emission spectral tier table comprising: DARK with range [0, 10) and multiplier 1.00×; H-alpha (Hα) with range [10, 100) and multiplier 1.04×; H-beta (Hβ) with range [100, 1,000) and multiplier 1.30×; H-gamma (Hγ) with range [1,000, 10,000) and multiplier 1.50×; H-delta (Hδ) with range [10,000, 50,000) and multiplier 2.00×; and H-epsilon (Hε) with range [50,000, ∞) and multiplier 5.00×; wherein each tier corresponds to a distinct spectral line of the hydrogen emission spectrum.

**Claim 4.** A method for an autonomous agent to prove role eligibility to a counterparty without revealing which role the agent holds, the method comprising:

(a) registering, by the agent, a blinded role leaf on an on-chain Merkle tree, the leaf computed as H(role_id ∥ blinding) wherein H is a cryptographic hash function, role_id identifies the agent's assigned role, and blinding is a secret scalar known only to the agent;

(b) generating a Merkle-path proof demonstrating that the blinded role leaf is a leaf of the on-chain Merkle tree having a publicly known root;

(c) generating a set-membership circuit proof asserting that role_id is a member of a verifier-specified permitted set S without revealing which element of S corresponds to role_id; and

(d) transmitting the Merkle-path proof and set-membership circuit proof to the counterparty, wherein the counterparty verifies that the agent's role is in S without learning the specific role.

**Claim 5.** The method of Claim 4, wherein the permitted set S is drawn from a role namespace comprising visible-light color roles including one or more of: Red (warrior), Orange (merchant), Yellow (worker), Green (caregiver), Blue (analyst), Indigo (sage), and Violet (mystic); and wherein the namespace further includes infrared (IR) and ultraviolet (UV) stealth roles verifiable only by counterparties holding a stealth-role verification key distinct from the standard Merkle-tree verification key.

**Claim 6.** A method for providing per-counterparty unlinkable identity for an autonomous agent across multiple counterparty relationships while preserving slash-accountability within each counterparty relationship, the method comprising:

(a) maintaining, by the agent, a private scalar sk associated with a Decentralized Identifier (DID) of the form did:hive:<pubkey>;

(b) for each counterparty identified by a counterparty identifier counterparty_id, deriving a nullifier N = H(sk ∥ counterparty_id) wherein H is a hash function modeled as a random oracle;

(c) publishing the nullifier N to an on-chain nullifier registry upon each interaction with the counterparty; and

(d) detecting, by the counterparty or the on-chain registry, a policy violation upon observing a second submission of a nullifier N previously registered for the same counterparty_id.

**Claim 7.** The method of Claim 6, wherein the nullifier derivation further incorporates a rotation epoch parameter: N = H(sk ∥ counterparty_id ∥ epoch), wherein epoch is a value derived from a current block number of a public blockchain, and epoch increments at a configurable block interval to provide forward privacy for long-running agent relationships while maintaining double-spend detectability within each epoch.

**Claim 8.** A system for providing selective disclosure of autonomous agent payment attributes through a receipt format comprising:

a plurality of mandatory plaintext fields including a receipt identifier, a payment amount, a payment token identifier, an endpoint identifier, a timestamp, and a cryptographic signature; and

a zero-knowledge attestation extension block comprising:

(i) a tier-range proof field containing a zero-knowledge proof asserting that the paying agent's committed cumulative call count falls within a range corresponding to a claimed tier classification;

(ii) a commitment field containing a Pedersen commitment to the paying agent's cumulative call count published on a public ledger;

(iii) a settlement proof field containing a zero-knowledge proof asserting that a settlement transaction referenced by the receipt is valid and non-reverted;

(iv) a nullifier field containing a per-counterparty nullifier derived from the paying agent's DID private scalar;

wherein the paying agent's wallet address and exact cumulative call count are not included in the receipt, and a receipt consumer verifies the paying agent's tier eligibility and settlement validity using the proofs in the attestation extension block without learning the paying agent's identity.

**Claim 9.** The system of Claim 8, wherein the receipt format is carried in an HTTP response header field in a format compatible with the x402 HTTP-native micropayment protocol, and wherein the zero-knowledge attestation extension block is identified by an extension key corresponding to the veil namespace reserved in the Hive Protocol EXPERIMENTAL specification, such that a receipt consumer that does not implement zero-knowledge verification ignores the extension block without error.

**Claim 10.** A system for regulatory compliance escrow in an autonomous agent commerce network employing identity-selective disclosure, the system comprising:

a distributed key generation subsystem generating a master compliance key K_master among a plurality of N regulator parties, each party holding a key shard, with a k-of-N threshold required to produce a valid compliance key operation, wherein k < N;

an on-chain escrow registry storing, for each registered interaction, a nullifier identifying the interaction and a ciphertext of an identity commitment encrypted to K_master;

a probable-cause gating contract enforcing that unlock of the escrow for a specified interaction requires: (i) a threshold signature over an authorization message referencing the target nullifier, produced by at least k of the N regulator parties; and (ii) a zero-knowledge proof of procedural authorization; and

an identity recovery pathway, activatable only upon satisfaction of the probable-cause gate, that decrypts and publishes the identity commitment for the target interaction only.

**Claim 11.** The system of Claim 10, wherein N = 5, k = 3, the threshold signatures are BLS signatures over the BLS12-381 pairing-friendly curve, the authorization message is M_auth = H("unlock" ∥ N_target ∥ requesting_authority_id ∥ epoch), the identity commitment is encrypted using an IND-CCA2-secure scheme, and the probable-cause gating contract is deployed as an immutable smart contract on a public EVM-compatible blockchain.

**Claim 12.** A non-transitory computer-readable medium storing instructions that, when executed by one or more processors, implement the full HiveVeil zero-knowledge selective disclosure protocol comprising:

a tier range proof subsystem implementing Pedersen commitment generation, Groth16 SNARK proving and verification for range assertions over hydrogen-spectral tier classifications, and a proof/verify API accepting tier label inputs conforming to the Hive Protocol STABLE tier vocabulary;

a role set-membership proof subsystem implementing Merkle-tree leaf registration, Merkle-path proof generation, set-membership circuit proving, and batch verification for role sets drawn from the Hive Protocol role namespace;

a nullifier derivation subsystem implementing per-counterparty nullifier computation from a DID private scalar, on-chain nullifier registry interaction, and epoch-based nullifier rotation;

a selective-disclosure receipt subsystem implementing the receipt format extension with zero-knowledge attestation block generation and verification, and x402-compatible HTTP header encoding; and

a compliance escrow subsystem implementing BLS distributed key generation, threshold signature aggregation, on-chain escrow registration, and probable-cause-gated identity recovery.

**Claim 13.** The method of Claim 1, further comprising integrating the zero-knowledge range proof into a binary wire-format message header according to a `.smsh` v2 extension block, wherein the 2-byte cleartext tier field of the `.smsh` header carries a tier claim and the extension block carries the zero-knowledge range proof for verification by HiveVeil-aware receivers, and HiveVeil-unaware receivers process the cleartext tier field without error.

**Claim 14.** The method of Claim 1, further comprising transmitting the zero-knowledge range proof to an on-chain smart contract implementing a treasury rebalancer function, wherein the smart contract verifies the range proof using an on-chain Groth16 verifier and releases a refill amount corresponding to the proved tier range multiplied by the revenue multiplier associated with the proved tier, without recording the agent's wallet address.

**Claim 15.** The method of Claim 6, wherein the private scalar sk is further used to generate, for each counterparty interaction, a Schnorr zero-knowledge proof of knowledge of sk, the Schnorr proof being transmitted alongside the nullifier N to enable the counterparty to attribute any misbehavior detected via nullifier reuse to the DID associated with sk, without the counterparty learning sk or the corresponding wallet address.

**Claim 16.** The method of Claim 4, wherein the agent holds assignments in two or more roles simultaneously, each role registered as a separate blinded leaf in the on-chain Merkle tree, and the set-membership proof for any single role is generated without revealing the existence of the agent's other role assignments, thereby preventing a counterparty from inferring the agent's full role set from a single interaction.

**Claim 17.** The system of Claim 8, further comprising a role-proof field in the zero-knowledge attestation extension block, the role-proof field containing a Merkle-path proof and set-membership circuit proof generated according to the method of Claim 4, wherein the role-proof field is present only when the counterparty specifies a role requirement in the interaction request, and is absent from receipts for interactions in which no role verification is requested.

**Claim 18.** The system of Claim 10, wherein each regulator's key shard is further protected by a Shamir's Secret Sharing scheme among a plurality of sub-custodians designated by that regulator, such that loss of a single regulator's primary shard is recoverable by the sub-custodians of that regulator without requiring cooperation from other regulators or reconstruction of the master compliance key K_master.

**Claim 19.** A method for an autonomous agent to prove compliance status and tier eligibility jointly to a regulatory authority under a single interaction, the method comprising:

(a) generating a composite zero-knowledge proof comprising: (i) a Groth16 tier-range proof asserting that the agent's cumulative call count is within a specified tier range; (ii) a BLS-based compliance status attestation signed by a compliance oracle attesting that the agent has satisfied jurisdiction-specific compliance requirements; and (iii) a linkage proof asserting that the tier-range proof and compliance attestation refer to the same DID without revealing the DID;

(b) transmitting the composite proof to the regulatory authority; and

(c) verifying, by the regulatory authority, the composite proof, wherein verification confirms both tier eligibility and compliance status without revealing the agent's wallet address, exact call count, or DID to the regulatory authority.

**Claim 20.** A method comprising the steps of: committing, by an autonomous agent, both a cumulative call count and a role identifier to respective Pedersen commitments on a public ledger; generating, in a single Groth16 SNARK proof, a joint assertion that (a) the committed call count falls within a tier range, (b) the committed role is a member of a permitted role set, and (c) a per-counterparty nullifier is correctly derived from the agent's DID private scalar; transmitting the joint proof, the two commitments, and the nullifier to a counterparty; verifying the joint proof against the on-chain commitments; and issuing a selective-disclosure receipt in the format of Claim 8 upon successful verification, whereby tier eligibility, role eligibility, and anti-replay protection are established in a single proof without revealing the agent's wallet address, exact call count, or specific role.

---

## ABSTRACT

A zero-knowledge selective disclosure system and method — designated HiveVeil — enables autonomous agents operating in tiered commerce networks to prove identity attributes without revealing underlying identifying information. The system comprises five coupled subsystems: a tier range proof subsystem using Groth16 SNARKs and Pedersen commitments to prove membership in a hydrogen-spectral tier (DARK through Hε) without revealing cumulative call count; a role set-membership proof subsystem using Merkle-tree leaf proofs and set-intersection circuits to prove role membership in a permitted set without revealing which role; a nullifier derivation subsystem using per-counterparty nullifiers derived from a DID private scalar to provide interaction-level unlinkability across counterparties while preserving slash-accountability within each relationship; a selective-disclosure receipt subsystem extending the x402 HTTP-native payment receipt format with zero-knowledge attestation fields replacing plaintext wallet address and call count; and a compliance escrow subsystem using BLS threshold signatures with a 3-of-5 regulator quorum and probable-cause gating to enable judicially supervised identity recovery for specific flagged transactions without enabling bulk surveillance. The system integrates with the Spectral `.smsh` v2 wire format and the treasury rebalancer architecture. Twenty claims cover the method, system, and article-of-manufacture aspects of the five coupled innovations and their compositions.

---

## INVENTOR DECLARATION

The undersigned declares that all statements made herein of the inventor's own knowledge are true, and that all statements made on information and belief are believed to be true. The undersigned further declares that the above-identified patent application is the original invention of the named inventor.

**Inventor:** Stephen A. Rotzin
**Residence:** 170 Greenway Dr, Walnut Creek, CA 94596, U.S.A.
**Date:** April 24, 2026
**Signature:** _____________________________

## MICRO-ENTITY CERTIFICATION

The applicant hereby certifies micro-entity status under 37 C.F.R. § 1.29(a): (i) the applicant qualifies as a small entity under 37 C.F.R. § 1.27; (ii) neither the applicant nor any inventor has been named on more than four previously filed United States patent applications, excluding provisional applications and foreign or international applications not designating the United States; (iii) neither the applicant nor any inventor had, in the calendar year preceding the year in which the applicable fee is being paid, a gross income exceeding three times the median household income reported by the United States Bureau of the Census for that preceding calendar year; and (iv) neither the applicant nor any inventor has assigned, granted, or conveyed, nor is under obligation to assign, grant, or convey, a license or other ownership interest in the application to an entity that does not qualify under the foregoing income limit.

## CROSS-REFERENCE TO CONCURRENT APPLICATIONS

This application is filed concurrently with related provisional applications by the same inventor, including but not limited to U.S. Provisional Applications 64/049,200 (spectral compliance stamping), 64/049,207 (compressed lexicon ZK visibility), 64/049,213 (surface-property monetization), 64/049,218 (universal time authority and SLA enforcement), and 64/049,226 (auditable zero-knowledge spend delegation), each filed April 24, 2026; together with a co-pending application directed to a unified spectral classification, compensation-multiplier, and binary wire-format encoding protocol for autonomous agent networks (the ".smsh" protocol). The disclosures of each of the foregoing applications are incorporated herein by reference in their entireties to the extent permitted by law. The selective-disclosure mechanisms claimed herein are designed to operate over, and within, the tier classification, role classification, and binary header layout disclosed in those co-pending applications.

## REDUCTION TO PRACTICE

The inventions described and claimed in this application were reduced to practice on or before April 25, 2026, in the form of a working reference implementation comprising: (a) a JSON-LD `@context` document published at the URL `https://hivetrust.hiveagentiq.com/v1/trust/schema/supermodel/v1.jsonld`; (b) a verifiable-credential issuance endpoint published at the URL `https://hivetrust.hiveagentiq.com/v1/trust/vc/supermodel/issue` operating under the W3C Verifiable Credentials Data Model 2.0 with the Ed25519Signature2020 proof suite; and (c) eight signed instances of the disclosed `HiveSupermodelCredential` type bound to eight distinct decentralized identifiers, each corresponding to a wallet operating on the Base blockchain network (chain identifier 8453).

---

*Provisional Patent Application — Not Examined*
*This provisional application establishes a priority date under 35 U.S.C. § 111(b). A non-provisional application claiming the benefit of this filing must be filed within twelve (12) months of the filing date.*

# ✨ FMRL: Fully-Mutable Runtime Lookup

**FMRL is a UTXO-based state protocol.** A minimal standard for impermanent and mutable state for Ordinals inscriptions on Bitcoin.

**Definition:**  
Inscriptions and apps implementing the FMRL standard interpret one or more inscriptions in a UTXO as state data.

The order of inscriptions in the UTXO matters. State inscriptions are interpreted sequentially, whether the FMRL logic uses one, some, or all inscriptions in a UTXO for state.

FMRL inscriptions can use the recursive API to query their own UTXO via `/r/self`, then fetch all inscriptions in that UTXO using `/output/<txid>:<vout>`.

**Behavior:**
- Dynamic and self-contained, using **local UTXO context** to inform state.
- Logic retrieves the list of inscriptions in the target UTXO.
- The UTXO's inscriptions' satributes, content, or metadata are used to determine state in FMRL-enabled inscriptions (e.g. rendering, configuration, access control).

**Structural Assumption:**
Any inscription using this protocol **assumes the UTXO it resides in is FMRL-compliant**—i.e., it is intentionally constructed to contain:
- One or more dynamic inscriptions implementing this standard.
- Additional inscriptions to function as **initializations or state updates**.

Because of this, users can **safely consolidate multiple dynamic inscriptions into the same UTXO**, and initialize or mutate all of them with a single new inscription added to the end of that UTXO.

Adhering to the standard of adding new state inscriptions sequentially (i.e. adding the new state's inscribed sat immediately after the previous state's inscribed sat) without buffer sats between them, simplifies state management for FMRL-compliant apps and promotes healthier UTXOs on Bitcoin.

**Key Characteristics:**
- Mutable and impermanent state via UTXO construction.
- **No parent-child or reinscription linkage** required.
- Fully **self-contained and transferable** UTXO applications.

**Use Cases:**
- Dynamically rendered generative art.
- On-chain objects that respond to local inscription state.
- Puzzle mechanics, unlockables, conditional behaviors—all without creating permanent on-chain links.

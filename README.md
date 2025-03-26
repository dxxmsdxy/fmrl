# FMRL: Fully-Mutable Runtime Lookup

**FMRL is a UTXO-based state protocol.**
*A minimal standard for dynamic, recursive state in Ordinals inscriptions.*

**Definition:**  
Inscriptions using the FMRL standard store their state as inscriptions in their UTXO.

Changes to state should be interpreted sequentially, whether the FMRL inscription uses one, some, or all inscriptions in its UTXO for state.

FMRL inscriptions can use the recursive API to query their own UTXO via `/r/self`, then fetch all inscriptions in that UTXO using `/output/<txid>:<vout>`.

**Behavior:**  
- The inscription **does not depend on parent-child or reinscription links**.
- It is stateless and self-contained, relying solely on its **local UTXO context**.
- The inscription uses retrieves the list of inscriptions in its UTXO.
- The inscription's satributes, content, or metadata are used to update or influence logic dynamically (e.g. rendering, configuration, access control).

**Structural Assumption:**  
Any inscription using this protocol **assumes the UTXO it resides in is FMRL-compliant**—i.e., it is intentionally constructed to contain:
- One or more dynamic inscriptions implementing this standard.
- Additional inscriptions to function as **initializations or state updates**.

Because of this, users can **safely consolidate multiple dynamic inscriptions into the same UTXO**, and initialize or mutate all of them with a single new inscription added to the end of that UTXO.

**Key Characteristics:**
- Unlocks mutable and impermanent state via UTXO construction
- **No parent-child or reinscription linkage** required.
- **Soft state** determined by UTXO-local inscription order.
- Fully **self-contained and transferable** UTXO applications.

**Use Cases:**
- Dynamically rendered generative art.
- On-chain objects that respond to local inscription state.
- Puzzle mechanics, unlockables, conditional behaviors—all without creating permanent on-chain links.

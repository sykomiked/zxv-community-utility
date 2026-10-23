# ZXV — Architecture Overview

**The engineering behind the paraconsistent settlement layer, presented as a community utility.**

---

## 1. The layered design

```
DISCOVERY    → the registry (136 capabilities)
SETTLEMENT   → the gate (only TRUE settles)
MONEY        → the treasury (the 50/25/15/10 work-based economy)
IDENTITY     → the rails (Dragon/Phoenix/Thunderbird cards)
AUDIT        → the receipts (the hash-chained journal)
EXECUTION    → the Venice Gas Station (2x matches on TRUE)
INCENTIVES   → rewards (tiers/streaks/bounties) + player (quests/badges)
OPERATIONS   → ops (bounds/rate-limits/timelocks/circuit-breakers)
ACCESS       → the universal interface (ux_manifest)
INTEROP      → the bridge (any relayer implements the standard)
INTELLIGENCE → the AI layer (chiglet DNA + aipi escrow)
```

## 2. The kernel core (lpres)

The kernel's `lpres` module defines the four states as bit patterns in
a single byte. The conjoin and disjoin operations are pure integer
comparisons over a rank table — zero allocation, a handful of
instructions, real-time friendly.

## 3. The chain-meet algebra

The total order is FALSE < NEITHER < BOTH < TRUE. The meet returns the
smaller rank; the join the larger. Because TRUE is the top, the
invariant is structural.

## 4. State-compatible upgrades

The serialized top-level struct never changes; new features live in
reserved namespaces of the store map. This Borsh forward compatibility
let 110 kits accumulate without breaking deployed state.

## 5. The audit chain

Every settlement links into a hash chain (the receipts).
`verify_chain` confirms the full chain's integrity — the
event-sourcing pattern on-chain, an immutable audit trail from
contradiction to resolution.

## 6. The gas economics

A TRUE settlement receives a 2x protocol gas match (the Venice Gas
Station); a BOTH forfeits the match (the drain shield). Reads are
entirely gas-free.

## 7. The quality record

| Check | Result |
|---|---|
| QC harness (vs the kernel C source) | 55/55, zero bugs |
| On-chain audit (all layers) | 24/24 |
| Durability stress | 70/70 |
| Registration audit | 136/136 |
| Gas-wall test (reads / writes) | 125/125 / 10/10 |

---

*Copyright (c) 2024-2026 Michael Laurence Curzi and 36N9 Genetics, LLC · SPDX-License-Identifier: Apache-2.0*
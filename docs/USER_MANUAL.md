# ZXV — The User Manual

**The complete guide to the paraconsistent settlement layer, offered as a public utility on NEAR.**

*Canonical address: `zedec.near` · Protocol: `f18889ea8bc108de53b899df3a3417c76995cbb55fb2174ff08d2e0abee99bcf` · Registry: `7eaa2c6f37ef7dd1dc073c4630533b67f303274d31d411e4047eb0d9401ef01a` · Gate: `6ca890f766fdaeccd6c934da325f5f06ebc63ca9be4f5f1b44d0686af93c64a8`*

---

## Part 1: What this is

### 1.1 The one rule

> **Only TRUE settles. TRUE+FALSE=BOTH — contradictions are recorded, never coerced, never a panic.**

### 1.2 The four values

| State | Value | Meaning | Behavior |
|---|---|---|---|
| `NEITHER` | `0x00` | no evidence yet | waits |
| `TRUE` | `0x01` | agreed, attested | **settles** |
| `FALSE` | `0x02` | explicitly refuted | refuses |
| `BOTH` | `0x03` | contradiction, held | **recorded, never coerced** |

### 1.3 Why four values instead of two

Binary systems cannot safely hold a disagreement — the logic itself
gives them no place for it. The four-valued layer gives the ecosystem a
place: a first-class state that records the conflict and refuses to
coerce a resolution. This is not a new philosophy; it is a new
**primitive** — a tool that any project can use.

---

## Part 2: The addresses

| Role | Address |
|---|---|
| **Canonical (routing)** | `zedec.near` |
| **The protocol (110 kits)** | `f18889ea8bc108de53b899df3a3417c76995cbb55fb2174ff08d2e0abee99bcf` |
| **The registry (136 capabilities)** | `7eaa2c6f37ef7dd1dc073c4630533b67f303274d31d411e4047eb0d9401ef01a` |
| **The gate (kernel invariant)** | `6ca890f766fdaeccd6c934da325f5f06ebc63ca9be4f5f1b44d0686af93c64a8` |

---

## Part 3: How to read the system (any client, no wallet, no gas)

### 3.1 The manifest (the whole schema)

```
ux_manifest on f18889ea8bc108de53b899df3a3417c76995cbb55fb2174ff08d2e0abee99bcf
```

### 3.2 The help (any topic)

```
ux_help {"topic":"start"}    → the 5-step onboarding
ux_help {"topic":"onboard"}  → your first grant
ux_help {"topic":"port"}     → the Port of Neo-Sicily
ux_help {"topic":"pool"}     → the liquidity pool
ux_help {"topic":"gas"}      → the Venice Gas Station
ux_help {"topic":"sd"}       → the Sovereign Decrees
ux_help {"topic":"rewards"}  → the bonus programs
ux_help {"topic":"player"}   → the player surface
ux_help {"topic":"ops"}      → the operational kits
```

### 3.3 The registry (discovery)

```
vm_capabilities on 7eaa2c6f37ef7dd1dc073c4630533b67f303274d31d411e4047eb0d9401ef01a
→ 136 capabilities
```

---

## Part 4: How to verify the invariant (the demonstration)

```bash
# conjoin {"inputs":[1,2]}        → "FALSE"   (TRUE+FALSE=FALSE in the join)
# is_settleable {"state":"BOTH"}  → false     (a contradiction never settles)
# is_settleable {"state":"TRUE"}  → true      (agreement settles)
# verify_chain {"from":0}         → true      (the audit hash-chain is intact)
```

Every claim in this manual can be checked on-chain, gas-free, by
anyone. That is the demonstration: the logic is real, deployed, and
verifiable.

---

## Part 5: How to join

1. Call `ux_help {"topic":"start"}` — the system teaches the 5-step
   onboarding.
2. Call `mint_onboard {}` — receive the one-time 5000-unit grant
   (spendable-not-transferable, one per account).
3. Call `ux_help {"topic":"port"}` — learn to register a DAO in the
   Port of Neo-Sicily.
4. Call `ux_help {"topic":"pool"}` — learn to enter through the
   liquidity pool.
5. Call `ux_help {"topic":"sd"}` — learn the Sovereign Decrees.

---

## Part 6: The external interfaces

### 6.1 The Port of Neo-Sicily (the external registry)

```
port_register(dao_name, account, category, description) → port-xxxx
port_plugin(protocol_account, plugin_name, plugin_account) → plugin-xxxx
port_lookup(account) → the record
port_count() → how many registered
port_open() → true (the space is open)
```

### 6.2 The YHVH circulation (sustainable, work-based)

```
mint_onboard {}              → the one-time 5000 grant (spendable-not-transferable)
mint_epoch_quote(circulating) → the bounded 2%/yr issuance
mint_bounty_rate(kind)       → the work bounties
mint_policy()                → the policy view
```

### 6.3 The liquidity pool (the entry)

```
pool_provide(provider, amount) → the depth grows
pool_quote(amount) → the swap quote (the 0.08889% assurance toll)
pool_enter(amount) → enter through the pool
pool_depth() / pool_provider(provider) → the state
```

### 6.4 The Venice Gas Station (the execution envelope)

```
envelope_deposit(target, rail) → fund your gas envelope
envelope_match(user, gas, verdict) → TRUE = 50/50 (2x), BOTH/FALSE = 100% user
envelope_balance(account) → credit/matched/multiplier
envelope_reserve() → the match pool
```

### 6.5 The Sovereign Decrees (forks without forking)

```
sd_issue(decree_id, title, params) → pass YOUR decree
sd_sign(decree_id) → join a decree
sd_shift(decree_id) → move your adherence (back and forth)
sd_prefabs() → the 6 ready configs
sd_choose(prefab) → adopt one
sd_require(protocol, decree_family) → gate participation
sd_check(account, protocol) → verify adherence
sd_forkless() → the proof (coexisting decrees, no chain fork)
```

---

## Part 7: The capability surface (136 capabilities)

- **28 base**: gate, treasury, rails, receipts, vino, tribute,
  surplus, chronicle, allotment, broker, rmag, scp144, aipi, chiglet,
  count_house, vswap, vauction, vbond, identity, reputation,
  provenance, grants, community_chest, royalty, telemetry, market,
  intent, mesh_token
- **5 layers**: settlement, market, trust, distribution, agent
- **7 systems**: escrow, agent_economy, governance, marketplace,
  compliance, identity_verification, settlement_rail
- **4 meta**: orchestrator, router, self, adaptation
- **4 api**: gateway, verify, bridge, index
- **4 ux**: manifest, help, example, universal
- **11 rewards**: tiers, accrual, claim, referral, streak,
  achievements, leaderboard, distribution, agent, round, bonus
- **10 player**: cards, quests, badges, levels, xp, missions,
  trophies, leaderboard, loyalty, events
- **10 ops**: config, limits, timelock, pause, audit, health, metrics,
  upgrade, guard, schedule
- **the rest**: the gas station, the system icon NFT, the Port of
  Neo-Sicily, the YHVH circulation, the liquidity pool, the Sovereign
  Decrees, the canonical router

---

## Part 8: How to build on it

- **The contract IS the API** — serverless, gas-free to read.
- **The bridge is a standard** — any relayer implements it.
- **The developer kit** — Rust crate `zxv-sdk` + TypeScript
  `@zxv/developer-kit`.
- **Repositories**:
  - the stack: github.com/sykomiked/zxv-stack
  - the developer kit: github.com/sykomiked/zxv-developer-kit
  - the NEP + ledger: github.com/sykomiked/ZXV-NEP-paraconsistent
  - this utility: github.com/sykomiked/zxv-community-utility

---

## Part 9: The quality record

| Check | Result |
|---|---|
| QC harness (vs the kernel C source) | 55/55, zero bugs |
| On-chain audit (all layers) | 24/24 |
| Durability stress | 70/70 valid calls, zero failures |
| Registration audit | 136/136 resolve to live contracts |
| Gas-wall test (reads / writes) | 125/125 / 10/10 |

---

*The system is open. Machines, bots, AI, and humans all read the same interface.*

*Copyright (c) 2024-2026 Michael Laurence Curzi and 36N9 Genetics, LLC · SPDX-License-Identifier: Apache-2.0*
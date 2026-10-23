# ZXV — The Paraconsistent Settlement Layer, as a Community Utility

**Four-valued logic for the NEAR ecosystem. Only TRUE settles.**

This repository is a **public utility and demonstration**: a complete,
gas-free, open implementation of paraconsistent (four-valued) logic on
NEAR, offered to the community so that any protocol, DAO, oracle, AI
agent, or human can choose to treat disagreement as information —
instead of as a bug.

**The canonical address: `zedec.near`** — a live contract that routes
to the entire utility.

---

## What this is, in one paragraph

Most of computing runs on **binary logic**: true or false, succeed or
fail, one way or the other. But the world — and especially distributed
systems — is full of disagreement. When two nodes, two oracles, two AI
models, or two communities disagree, binary systems must choose between
panicking, silently overwriting, freezing, or letting the majority
win. All four destroy information.

**ZXV offers a fifth option: record the disagreement, hold both claims,
and refuse to settle until the evidence genuinely resolves.** This is
called paraconsistent (four-valued) logic, and it runs on NEAR today as
a public utility — gas-free to read, self-describing, and buildable by
anyone.

> **Only TRUE settles. TRUE+FALSE=BOTH — contradictions are recorded,
> never coerced, never a panic.**

---

## The four values

| State | Value | Meaning | Behavior |
|---|---|---|---|
| `NEITHER` | `0x00` | no evidence yet | waits |
| `TRUE` | `0x01` | agreed, attested | **settles** |
| `FALSE` | `0x02` | explicitly refuted | refuses |
| `BOTH` | `0x03` | contradiction, held | **recorded, never coerced** |

The magic is structural: because TRUE sits at the top of the chain
(FALSE < NEITHER < BOTH < TRUE), **no combination of non-TRUE values
can ever produce TRUE**. The invariant is a theorem of the rank order,
not a checked condition.

---

## The addresses (the whole utility, one front door)

| Role | Address |
|---|---|
| **Canonical (routing)** | `zedec.near` |
| **The protocol (110 kits)** | `f18889ea8bc108de53b899df3a3417c76995cbb55fb2174ff08d2e0abee99bcf` |
| **The registry (136 capabilities)** | `7eaa2c6f37ef7dd1dc073c4630533b67f303274d31d411e4047eb0d9401ef01a` |
| **The gate (kernel invariant)** | `6ca890f766fdaeccd6c934da325f5f06ebc63ca9be4f5f1b44d0686af93c64a8` |

---

## How to use it (gas-free, any client, no wallet)

### 1. Read the system

```bash
# the manifest: the whole system's schema
#   ux_manifest on f18889ea8bc108de53b899df3a3417c76995cbb55fb2174ff08d2e0abee99bcf
# the help: any topic
#   ux_help {"topic":"start"}   → the 5-step onboarding
#   ux_help {"topic":"onboard"} → your first grant
#   ux_help {"topic":"gas"}     → the Venice Gas Station
#   ux_help {"topic":"sd"}      → the Sovereign Decrees
# the registry (discovery)
#   vm_capabilities on 7eaa2c6f... → 136 capabilities
```

### 2. Verify the invariant (the demonstration)

```bash
# conjoin {"inputs":[1,2]}        → "FALSE"   (TRUE+FALSE=FALSE in the join)
# is_settleable {"state":"BOTH"}  → false     (a contradiction never settles)
# is_settleable {"state":"TRUE"}  → true      (agreement settles)
# verify_chain {"from":0}         → true      (the audit hash-chain is intact)
```

### 3. Join

A new actor calls `mint_onboard` for a one-time grant (spendable on
the platform, not transferable — one per account). Then `pool_enter`
provides access through the liquidity pool.

### 4. Build

- **The contract IS the API** — serverless, gas-free to read.
- **The bridge is a standard** — any relayer implements it.
- **The developer kit** — Rust crate `zxv-sdk` + TypeScript
  `@zxv/developer-kit`.

---

## What's in this repository

```
zxv-community-utility/
├── README.md                  ← this file (the one-page welcome)
├── nep/
│   └── nep-paraconsistent-community-utility.md   ← the NEP proposal
├── docs/
│   ├── USER_MANUAL.md         ← the complete user manual
│   ├── DEMONSTRATION.md       ← how to verify everything yourself
│   ├── ARCHITECTURE.md        ← the engineering overview
│   └── omni/                  ← the 30-language documentation
│       ├── PARACONSISTENT_LOGIC_<LANG>.md    (30 files)
│       ├── NEAR_DEPLOYMENT_GUIDE_<LANG>.md   (30 files)
│       └── ZXV_ENGINEERING_<LANG>.md         (30 files)
```

---

## The NEP

The full Near Enhancement Proposal is in
[`nep/nep-paraconsistent-community-utility.md`](nep/nep-paraconsistent-community-utility.md).
It specifies the minimum viable interface, the mathematics, the
security considerations, and the backwards compatibility — all in the
canonical NEP format, ready for submission to the NEAR NEPs process.

---

## The multilingual documentation (30 world languages)

The same utility is documented in the **top 30 world languages**, each
written natively and uniquely, forming an omni-tautology of keywords so
the utility is findable everywhere:

English · 简体中文 · हिन्दी · Español · Français · العربية · বাংলা ·
Português · Русский · اردو · Bahasa Indonesia · Deutsch · 日本語 ·
Kiswahili · मराठी · తెలుగు · Türkçe · தமிழ் · Tiếng Việt · 한국어 ·
Italiano · ไทย · ગુજરાતી · Basa Jawa · Polski · Українська · Bahasa
Melayu · فارسی · ಕನ್ನಡ · ਪੰਜਾਬੀ

Each language carries the same truth: **only TRUE settles.**

---

## Why this matters for NEAR

NEAR is a community of builders. A paraconsistent gate is most valuable
when it is a **shared utility** — one well-audited, gas-free,
self-describing primitive that any project can call. This repository is
that utility: open, community-owned, and demonstrated with a live,
verifiable deployment.

**The system is open. Machines, bots, AI, and humans all read the same
interface.**

---

*Copyright (c) 2024-2026 Michael Laurence Curzi and 36N9 Genetics, LLC ·
SPDX-License-Identifier: Apache-2.0*
# ZXV — Demonstration Guide

**How to verify the paraconsistent settlement layer yourself, gas-free, on NEAR mainnet.**

This guide is the **demonstration**: every claim can be checked by
anyone, with a plain curl call, no wallet, no gas. The logic is not a
white paper — it is deployed and verifiable.

---

## 1. The canonical router (zedec.near)

```bash
curl -s https://rpc.mainnet.fastnear.com -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":"v","method":"query","params":{"request_type":"call_function","finality":"final","account_id":"zedec.near","method_name":"route","args_base64":"e30="}}'
```

Expected: the full topology — the canonical address, the registry, the
gate, and the protocol core.

## 2. The invariant (the gate)

```bash
# a contradiction never settles
#   is_settleable {"state":"BOTH"}  → false
# agreement settles
#   is_settleable {"state":"TRUE"}  → true
# the join
#   conjoin {"inputs":[1,2]}        → "FALSE"
```

## 3. The audit chain

```bash
# verify_chain {"from":0} → true (the receipt hash-chain is intact)
```

## 4. The discovery

```bash
# vm_capabilities on 7eaa2c6f37ef7dd1dc073c4630533b67f303274d31d411e4047eb0d9401ef01a
# → 136 capabilities
```

## 5. The local C demonstration (compile in seconds)

```c
/* belnap_gate.c — the chain-meet, zero allocation */
#include <stdio.h>
#include <stdint.h>
#include <stdbool.h>

typedef enum { NEITHER = 0x00, TRUE = 0x01, FALSE = 0x02, BOTH = 0x03 } belnap_state_t;
static const uint8_t rank[4] = { 1, 3, 0, 2 }; /* [NEITHER,TRUE,FALSE,BOTH] */

static belnap_state_t conjoin(belnap_state_t a, belnap_state_t b) {
    if ((unsigned)a > 3 || (unsigned)b > 3) return NEITHER;
    return rank[a] <= rank[b] ? a : b;
}
static bool is_settleable(belnap_state_t s) { return s == TRUE; }

int main(void) {
    belnap_state_t c = (belnap_state_t)((unsigned)TRUE | (unsigned)FALSE);
    printf("BOTH settleable? %s\n", is_settleable(c) ? "YES" : "NO (Blocked without panic)");
    printf("TRUE settleable? %s\n", is_settleable(conjoin(TRUE, TRUE)) ? "YES" : "NO");
    return 0;
}
```

```bash
gcc -O3 -Wall -Wextra -pedantic belnap_gate.c -o belnap_gate && ./belnap_gate
```

Output:
```
BOTH settleable? NO (Blocked without panic)
TRUE settleable? YES
```

## 6. The Rust no_std demonstration

```rust
#![no_std]
#[derive(Copy, Clone, PartialEq, Eq, Debug)]
#[repr(u8)]
pub enum Belnap { Neither = 0x00, True = 0x01, False = 0x02, Both = 0x03 }
const RANK: [u8; 4] = [1, 3, 0, 2];
impl Belnap {
    pub fn is_settleable(self) -> bool { matches!(self, Belnap::True) }
    pub fn merge(self, other: Self) -> Self {
        if RANK[self as usize] <= RANK[other as usize] { self } else { other }
    }
}
#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn contradiction_does_not_panic() { assert!(!Belnap::Both.is_settleable()); }
    #[test]
    fn only_true_settles() { assert!(Belnap::True.is_settleable()); }
}
```

```bash
cargo test --release   # all green
```

## 7. What the demonstration proves

1. The invariant is **structural**: no non-TRUE combination can yield
   TRUE.
2. The deployment is **real**: the same logic answers on-chain.
3. The reads are **gas-free**: anyone can verify, forever.
4. The logic is **open**: C and Rust implementations compile in
   seconds on any machine.

*The system is open. Verify it yourself.*
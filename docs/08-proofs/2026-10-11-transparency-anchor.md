# Proof · methodology and calculation code anchored on Solana mainnet

Status: **CONFIRMED** (reported by the site after signing; re-check with "Verify" on [/transparencia](https://upay3food.com/transparencia) or on Solscan)

On 2026-10-11, the founder signed one SPL Memo transaction from Phantom on
[/transparencia](https://upay3food.com/transparencia). The memo carries the
SHA-256 of the public methodology and of the code that computes every number
UPAY3FOOD shows. It moves no funds; it costs only the network fee.

## Receipt

| Field | Value |
| --- | --- |
| Network | Solana `mainnet-beta` |
| Program | SPL Memo `MemoSq4gqABAXKb96qnH8TysNcWxMyWCqXgDLGmfcHr` |
| Signature | `3NcV2SHoB2cvcg15goPEVxk3crjrAjbntXhC5bhc8SAr8uiaQm5f1axFxRzyNLfQr8Vh7BzUGVaPJQaB1u5QaRaK` |
| Slot | `455501588` |
| Wallet | Phantom |
| Provider | RPC Fast through the same-origin server proxy |

Explorer: https://solscan.io/tx/3NcV2SHoB2cvcg15goPEVxk3crjrAjbntXhC5bhc8SAr8uiaQm5f1axFxRzyNLfQr8Vh7BzUGVaPJQaB1u5QaRaK

## Memo

```
UPAY3FOOD transparency v1 | methodology sha256:8fde83dd3d912d2c18d4da2af1fbe814d1be43a08c5349f9d0a1c3cb0acacc66 | engine sha256:0b0a87495a679debf0c01017039a6f01b92b172a4015229d5193e751b0b341fa | commit 3d2843c
```

## Check it yourself

From a clone of the repository, at commit `3d2843c` or any later commit that
has not changed these files:

```bash
sha256sum docs/05-architecture/price-calculations.md
# 8fde83dd3d912d2c18d4da2af1fbe814d1be43a08c5349f9d0a1c3cb0acacc66
cat packages/domain/src/insights.ts packages/domain/src/liquids.ts packages/domain/src/burger.ts \
    packages/domain/src/volume.ts packages/domain/src/text-readers.ts packages/agent/src/menu-advisor.ts | sha256sum
# 0b0a87495a679debf0c01017039a6f01b92b172a4015229d5193e751b0b341fa
```

If a later version changes the methodology or the engine, its hashes change
and a new anchor is needed; the site shows which version each anchor matches.

## What this proves, and what it does not

- It proves these exact rules existed, unchanged, at slot 455501588.
- It does not prove that every number on the site is right; it makes any later
  change to the rules visible.
- No price, user data, address or personal data is on-chain: only hashes and
  a commit id.

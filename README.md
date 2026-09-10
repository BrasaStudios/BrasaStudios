# Brasa Studios

Independent game studio building tactical RPGs — and building them on the DigiByte blockchain.

**Site:** [brasastudios.games](https://brasastudios.games) · **X:** [@Brasa_Games](https://x.com/Brasa_Games)

## What we're building

- **Elements of War** — a tactical RPG, now in production. Limited-edition collectibles ship as
  DigiAssets: on-chain, verifiable, tradeable.
- **A direct storefront** at brasastudios.games accepting USD, DigiByte (DGB), and DigiDollar (DD),
  running against our own full node — no third-party payment processors on the crypto rails.

We build on this stack daily, so we test it hard and report what we find. Everything below is
public and independently verifiable — check the links, not our word.

## Contributions to the DigiByte ecosystem

The fixes below shipped in **DigiAsset Core** (the asset layer for DigiByte) and in the
**DigiByte Android Wallet** ([JohnnyLawDGB/digibytewallet-android](https://github.com/JohnnyLawDGB/digibytewallet-android))
as a direct result of our testing and bug reports on
[PR #26](https://github.com/DigiAsset-Core/DigiAsset_Core/pull/26),
[issue #29](https://github.com/DigiAsset-Core/DigiAsset_Core/issues/29), and a private report under
the wallet's [bug-bounty program](https://github.com/JohnnyLawDGB/digibytewallet-android/blob/develop/BUG-BOUNTY.md).
Each row links to the commit; the credit line is quoted verbatim from the commit message.

### Named in the commit message

| Date | Commit | Fix shipped | Credit, verbatim |
|---|---|---|---|
| 2026-08-25 | [`425cccdc`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/425cccdc72e2bb3b45b0be45ba04dc16f72c4416) | Stop locking every fee coin when storenonassetutxo=0 | Reported by BrasaStudios on PR #26. |
| 2026-08-25 | [`554a2930`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/554a2930007420591a9ba5d2f10522d37faae9e4) | Refuse to start on config keys still holding the # placeholder | It cost BrasaStudios a failed launch to work out on PR #26. |
| 2026-08-25 | [`6e2de2e6`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/6e2de2e64358d481b26ec143631ea5621e98251c) | Return asset data on pruning nodes instead of a pruned error | Reported by BrasaStudios on PR #26. |
| 2026-08-25 | [`7b15f61a`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/7b15f61ade00f07c0b7329395f958bdc07ebd18e) | Add rpcwallet so multi wallet nodes work | Reported by BrasaStudios on PR #26, who had to unload their treasury wallet around every operation. |
| 2026-08-25 | [`949af460`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/949af46037b0d2138a6b6c0622750799e300e746) | Merge PR 26 review fixes from asset_features | Brings in the fixes for BrasaStudios' 2026-08-25 report: fee coins all being locked under storenonassetutxo=0, getassetdata failing on pruning nodes, DigiByte Core errors reported as "Core Offline", rpcwallet for multi wallet nodes, the psp# placeholder config check, and the chain analyzer retry spin. |
| 2026-08-25 | [`e3abf7f3`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/e3abf7f35caffb3273c1ff54f81a7692c50dcda6) | Stop reporting every DigiByte Core error as "Core Offline" | BrasaStudios hit this on PR #26 chasing a multi wallet error that came back as "DigiByte Core Exception: Core Offline". |
| 2026-09-06 | [`62420c4c`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/62420c4ce6a63ad59b4fbc03857277f18a7b17f0) | Refuse transfers of assets whose rules a wallet cannot satisfy (issue 29) | Reported with mainnet reproduction and evidence by Ray / Brasa Studios; the wallet-side approach was proposed by chopperbriano. |
| 2026-09-09 | [`90a0592c`](https://github.com/JohnnyLawDGB/digibytewallet-android/commit/90a0592ced50a950ca8cc293cd65a4c4e0085b94) | docs(security): ruled-asset transfer gate — report, verification, and approved design | Reported 2026-09-06 by Brasa Studios, verified from source at both ends. |

### Not named, but provably ours

The commit repeats a figure that appears only in our public report.

| Date | Commit | Fix shipped | What it quotes back | Where that figure is public |
|---|---|---|---|---|
| 2026-08-25 | [`90f0ea60`](https://github.com/DigiAsset-Core/DigiAsset_Core/commit/90f0ea6090b104af29b481fda189cecabe95db5f) | Say what the chain analyzer failed on and stop spinning on it | One report had 3,851,461 "Rewinding Phase Started" lines and not one saying what had gone wrong, filling the disk instead of pointing at the problem. | 3,851,461 -> PR #26 comment 2026-08-17 and 2026-08-25 - our 'Rewinding Phase Started' count |

## Field reports

- **First known test of DigiAsset Core v1.0.0 (PR #26) against DigiByte Core v9.26.4, on Linux.**
  Built and ran on Ubuntu 22.04 and 26.04 (maintainer testing had covered macOS + 8.22.2 only).
  Nine findings with root causes and verified workarounds, posted on the PR.
- **Diagnosed a mainnet chain-sync livelock down to the line.** Sync died at 99% and retried
  3.85 million times; we isolated the failing constraint and the dead recovery path, then re-synced
  through the death height to confirm the maintainer's fix empirically.
- **Issued DigiAsset #5381 — "Brasa Studios - Test Issue 001".** 100 units, locked supply, metadata
  self-hosted on IPFS. assetId `La9q3eDK2deYHQnu7DFqAF3Tn9vqekPbz7V88j`, issuance tx
  `dd86362f6d765181e5bd90503b85166ead6e39e50971b3c66ed10f6cffe64cc8` (height 24,081,128). The dry
  run for Elements of War's on-chain collectibles.
- **Ran a full DigiDollar mint-and-redeem cycle in DD's first month on mainnet** (2026-07-27).
  $100 DD minted against locked DGB collateral, held, redeemed, 100% of collateral recovered —
  total round-trip cost about one tenth of a cent in fees.
- **Found and reproduced a silent asset-destroying bug, then tested the fix on mainnet**
  ([issue #29](https://github.com/DigiAsset-Core/DigiAsset_Core/issues/29)). Sending 1 unit of a
  royalty-ruled DigiAsset destroyed the sender's entire holding of 5, with no log line — proven
  deliberately on a throwaway asset (tx `f385d004…`, block 24,106,276). Reported with the mechanism
  and on-chain evidence; the maintainer shipped a wallet-side guard the same day (`62420c4c`), and
  we confirmed it on mainnet against a second throwaway asset: refused, no txid, supply unchanged.
- **Found the same door in the DigiByte Android Wallet, reported it privately under the wallet's
  bug-bounty program, and supplied the live case** (2026-09-06 to 09-09). The wallet built a plain
  transfer for a royalty-ruled asset, so one send destroyed the whole holding while the app reported
  success. We found it by reading the source; the maintainer confirmed it from source the same day,
  and we issued throwaway ruled assets straight to his test phone so the burn could be captured on
  the shipped release and the refusal proven on the fix. Rated High and shipped as
  [v4.0.80](https://github.com/JohnnyLawDGB/digibytewallet-android/releases/tag/v4.0.80) on
  2026-09-09, with Brasa Studios credited as reporter in the release's
  [audit log](https://github.com/JohnnyLawDGB/digibytewallet-android/blob/v4.0.80/security/AUDIT-LOG.md)
  and [bounty report](https://github.com/JohnnyLawDGB/digibytewallet-android/blob/v4.0.80/security/reports/bounty/2026-09-06-ruled-asset-send-burns-holding.md).

## How this page stays honest

This ledger is regenerated by script from the upstream repositories — never hand-maintained — and
every claim links to a commit, a pull request, or an on-chain transaction that anyone can check.
Fixes listed are to DigiAsset Core and the DigiByte Android Wallet, not to DigiByte Core itself.
*Last verified: 2026-09-09.*

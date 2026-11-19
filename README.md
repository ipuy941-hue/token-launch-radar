# token-launch-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/ipuy941-hue/token-launch-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/ipuy941-hue/token-launch-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Launch Radar: every rankable pre-token protocol in a sealed DefiLlama snapshot, ranked by an implied value computed from its own figures, with a concrete farm plan for each one.

## What it does

`main.ts` reads the sealed snapshot (`/input/snapshot.json`), scores every protocol that records no token, and writes the ranked board to `/output/board.json` plus a static dashboard to `/output/dashboard/` and a dossier to `/output/dossier.json`.

- **198 rows, not a capped top list.** The watchlist (40 protocols at or above $50M TVL with no token) is the floor; the early radar adds every other rankable pre-token protocol below the floor (158 more). Wrapped, staked and bridged products of tokens that already trade are excluded, as are centralised exchanges and versioned pools, and live-token protocols are set aside with their market caps shown.
- **Model radar-2, one function for every row:** `implied = round(TVL x 0.25 x (1 + clamp(change_7d, -60, 120) / 100 x 0.5) x (0.55 + min(age_days, 1460) / 1460 x 0.60) x (1 + min(chains - 1, 5) x 0.02))`. TVL is the size of the prize, seven-day growth is momentum, age is how long the protocol has run with no token, and chain breadth (up to +10%) is durability. No protocol name is special-cased.
- **Farm plans with cost and time.** Seven steps per protocol, derived from its category, chains, TVL and age: a fresh wallet, the category action with a concrete capital amount, a weekly qualifying action, a hold of 30–60 days, a monthly points check, the safety rule (claim only from a link the protocol itself publishes, never pay to claim), and a farm log.
- **Dashboard you can use.** Sortable board, search, category and chain filters, a watchlist-only toggle, a live-token view, a detail view for each protocol with the model's full breakdown, and a model sandbox: move the base-multiple and growth-weight sliders to recompute the board and see how the ranking responds. The sandbox changes only what the page shows; `board.json` keeps the radar-2 defaults.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

Node 22 or later, standard library only, no network. The program runs twice and writes the same bytes both times.

## The model, in one paragraph

A token launch is worth what the protocol behind it is worth. This radar does not predict whether or when a token is issued; it prices the launch as if the protocol's record stayed as it is. Bigger TVL means a bigger launch, faster seven-day growth means a protocol still compounding, a longer run with no token means a launch is readier and the airdrop record is longer, and more chains means more places to issue from. The dashboard states the formula and recomputes every row in the page, so the screenshots, the code and `board.json` are the same arithmetic.

---

Entered on [make.fun](https://make.fun/?ref=895mnnwc&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards

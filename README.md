[![make.fun](https://make.fun/badge/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1.svg)](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1)
[![rank](https://make.fun/badge/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/Ritwan007/tiny-bot-mr-01/rank.svg)](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1)
[![reward](https://make.fun/badge/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1/Ritwan007/tiny-bot-mr-01/reward.svg)](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1)

# Tiny Bot — 24h dip mean-reversion + EMA trend

Entry for [Tiny Bot, Easy $2: Beat Buy-and-Hold on Solana](https://make.fun/bounty/u-gorun-gadget-tiny-bot-easy-2-beat-a48f3ce1) on [make.fun](https://make.fun).

A tiny paper-trading bot for hourly Solana prices. It runs `main.ts` on Node 22 under the `agent-fun/bars-replay/v1` harness: each hourly bar, it decides which symbols to hold and which to leave in USDC.

## Strategy

Two engines, each position tagged with the engine that opened it:

1. **24h dip mean-reversion** — buy a symbol whose 24-hour return is at or below −5%; sell when its 24h return reaches +3%.
2. **EMA trend** — buy when EMA(8) is above EMA(21); sell when it turns below.

Each position exits on its own engine's signal, which keeps the trade count well above the 8-trade guardrail while holding drawdown low. Positions are capped at 25% of equity each. No clock, no randomness, no network — every order is a pure function of the bars seen so far.

## Dev-window result (kit `grade-local`)

- **Net PnL +$400.39** on $10,000 capital (+4.00%), 30 trades, 4.4% max drawdown, 90% interval $86.36–$703.19
- Buy-and-hold on the same window: **−$869.34**; best house baseline (hold-cash): $0.00

## Run it

```sh
node cli/makefun.mjs grade-local --kit <kit-dir> --bot . --driver docker
```

## License

MIT — see [LICENSE](LICENSE).

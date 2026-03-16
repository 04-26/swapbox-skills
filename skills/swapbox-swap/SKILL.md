---
name: swapbox-swap
description: "Execute on-chain token swaps via the SwapBox DEX aggregator. Swap any token pair on the same blockchain with optimal routing. — Status: Coming Soon"
license: Apache-2.0
metadata:
  author: swapbox
  version: "1.0.0"
  homepage: "https://swapbox.io"
  status: coming-soon
---

# SwapBox On-Chain Swap Skill

> **Status: Coming Soon** — This skill is currently under development and not yet available for use.

Execute token swaps on the same blockchain using SwapBox's DEX aggregator, which finds the optimal route across multiple DEXes.

## Planned Features

- Swap any token pair on the same chain (e.g., ETH → USDT on Ethereum)
- Multi-DEX route optimization (OKX, 1inch, Uniswap, etc.)
- Slippage protection with configurable tolerance
- Anti-MEV protection option
- Token approval management
- Transaction simulation before execution

## Skill Routing

**Will be used when the user:**

- Wants to swap/trade/buy/sell tokens on the same chain
- Asks "swap 10 USDC for ETH", "兑换 BNB 为 USDT"
- Wants a swap quote before executing

**Do NOT use this skill:**

- For price queries only → use `swapbox-price`
- For cross-chain transfers → use `swapbox-bridge`

## API Endpoint (Preview)

This skill will use the same `/api/swap/route` endpoint as the price skill, but with additional execution steps:

1. Get route quote via `POST /api/swap/route`
2. Approve token spending (if needed)
3. Execute the swap transaction
4. Track transaction status

## Coming Soon

This feature is under active development. Stay tuned for updates.

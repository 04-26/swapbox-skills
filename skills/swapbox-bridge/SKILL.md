---
name: swapbox-bridge
description: "Bridge tokens across different blockchains via SwapBox's cross-chain aggregator. Transfer assets between 30+ chains with optimal routing. — Status: Coming Soon"
license: Apache-2.0
metadata:
  author: swapbox
  version: "1.0.0"
  homepage: "https://swapbox.io"
  status: coming-soon
---

# SwapBox Cross-Chain Bridge Skill

> **Status: Coming Soon** — This skill is currently under development and not yet available for use.

Bridge tokens across different blockchains using SwapBox's cross-chain aggregator, supporting 30+ chains with optimal routing.

## Planned Features

- Cross-chain token transfers (e.g., ETH on Ethereum → ETH on Arbitrum)
- Cross-chain swaps (e.g., ETH on Ethereum → USDT on BSC)
- Multi-bridge route optimization
- Cross-chain fee estimation
- Transaction tracking across chains

## Skill Routing

**Will be used when the user:**

- Wants to transfer tokens between different chains
- Asks "bridge ETH from Ethereum to Arbitrum", "跨链转 USDT 到 BSC"
- Wants to swap tokens across chains

**Do NOT use this skill:**

- For price queries only → use `swapbox-price`
- For same-chain swaps → use `swapbox-swap`

## API Endpoint (Preview)

This skill will use `/api/swap/route` with `fromChain` different from `toChain`:

1. Get cross-chain route via `POST /api/swap/route`
2. Approve token spending (if needed)
3. Execute the bridge transaction
4. Track cross-chain transaction status

## Coming Soon

This feature is under active development. Stay tuned for updates.

# SwapBox Skills — Agent Instructions

This is a **SwapBox skill collection** providing 3 skills for multi-chain DeFi operations: token price queries, on-chain swaps, and cross-chain bridges across 30+ blockchains.

All skills interact directly with SwapBox HTTP APIs (https://swapbox.io) — no CLI binary required. The AI agent constructs and executes API calls using `curl` or equivalent HTTP requests.

## Available Skills

| Skill | Purpose | When to Use |
|-------|---------|-------------|
| swapbox-price | Multi-chain token/USDT price query | User asks about token prices, exchange rates, trading pairs; user asks "ETH 在 Ethereum 上多少钱", "查询 BSC 上 CAKE 的 USDT 价格", "what's the price of SOL", "how much is 1 BNB in USDT" |
| swapbox-swap | On-chain DEX swap execution | User wants to swap/trade/buy/sell tokens on the same chain; user asks "swap ETH for USDT", "兑换 BNB 为 USDT" — **Coming Soon** |
| swapbox-bridge | Cross-chain bridge transfer | User wants to transfer tokens across different blockchains; user asks "bridge ETH from Ethereum to Arbitrum", "跨链转 USDT 到 BSC" — **Coming Soon** |

## Architecture

- **skills/** — 3 SwapBox skill definitions (each is a `SKILL.md` with YAML frontmatter + API reference)
- **skills/swapbox-price/** — Token price query skill (active)
- **skills/swapbox-swap/** — On-chain swap skill (coming soon)
- **skills/swapbox-bridge/** — Cross-chain bridge skill (coming soon)

## Skill Discovery

Each skill in `skills/` contains a `SKILL.md` with:

- YAML frontmatter (name, description, metadata)
- Full API reference with parameters and response schemas
- Step-by-step operation flow with curl examples
- Edge cases and error handling

## API Base URL

All API calls use the base URL: `https://swapbox.io/api`

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/config/chains` | GET | List all supported blockchains |
| `/asset/query` | POST | Query token list for a specific chain |
| `/swap/route` | POST | Get swap/bridge route with price quote |

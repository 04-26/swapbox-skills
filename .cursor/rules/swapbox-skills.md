---
description: "当用户询问代币价格、交易对、兑换率、支持的链或Token时，自动使用 SwapBox Skills"
globs:
alwaysApply: false
---

# SwapBox Skills — Cursor Agent Rule

当用户的请求匹配以下关键词时，请读取并遵循对应的 SKILL.md 文件中的完整指令：

## Skill Routing

| User Intent | Read File |
|---------|---------|
| Token price / exchange rate / trading pair query | `skills/swapbox-price/SKILL.md` |
| Swap execution (same-chain & cross-chain) | `skills/swapbox-swap/SKILL.md` |

## 触发关键词

价格、price、兑换率、exchange rate、USDT、交易对、trading pair、多少钱、worth、查询价格、token price、代币价格

## 使用方式

1. 收到匹配请求后，先用 Read 工具读取对应的 `SKILL.md` 文件
2. 严格按照 SKILL.md 中的 **Operation Flow** 步骤执行
3. 使用 Shell 工具执行 curl 命令调用 SwapBox API
4. 按照 SKILL.md 中的 **Output Format Rules** 格式化输出结果

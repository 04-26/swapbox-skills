# SwapBox API Reference

Base URL: `https://swapbox.io/api`

## 1. GET /config/chains — List Supported Chains

Returns all supported blockchains with their configuration.

### Request

```bash
curl -s 'https://swapbox.io/api/config/chains'
```

No parameters required.

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | number | 0 = success |
| `msg` | string | Response message |
| `data` | array | List of chain objects |

#### Chain Object

| Field | Type | Description |
|-------|------|-------------|
| `id` | number | Internal chain ID |
| `nativeId` | number | Native chain network ID (e.g., 1 for Ethereum mainnet) |
| `chain` | string | Chain identifier used in API calls (e.g., "Ethereum", "BSC") |
| `chainName` | string | Display name |
| `prefix` | string | Address prefix (e.g., "0x" for EVM chains) |
| `chainId` | number | SwapBox internal chain ID (used in route requests) |
| `chainType` | number | Chain type (2=EVM, 5=BTC, etc.) |
| `icon` | string | Chain icon URL |
| `bridge` | number | 1 = bridge supported |
| `swap` | number | 1 = swap supported |
| `meme` | number | 1 = meme token trading supported |
| `status` | number | 1 = active |
| `configs` | object | Chain-specific configurations |
| `configs.okxChainId` | string | OKX DEX chain ID (if applicable) |
| `mainAsset` | object | Native token of this chain |
| `mainAsset.symbol` | string | Native token symbol (e.g., "ETH") |
| `mainAsset.chainId` | number | Same as parent chainId |
| `mainAsset.assetId` | number | Asset ID for the native token |
| `mainAsset.contractAddress` | string | Empty string for native tokens |
| `mainAsset.decimals` | number | Token decimal places |
| `mainAsset.usdPrice` | number | Current USD price |

### Example Response

```json
{
  "code": 0,
  "msg": "Success",
  "data": [
    {
      "id": 376,
      "nativeId": 1,
      "chain": "Ethereum",
      "chainName": "Ethereum",
      "prefix": "0x",
      "chainId": 101,
      "chainType": 2,
      "swap": 1,
      "bridge": 1,
      "status": 1,
      "mainAsset": {
        "symbol": "ETH",
        "chainId": 101,
        "assetId": 1,
        "contractAddress": "",
        "decimals": 18,
        "usdPrice": 2174.00
      }
    }
  ]
}
```

---

## 2. POST /asset/query — Query Token List

Returns all available tokens on a specific chain.

### Request

```bash
curl -s -X POST 'https://swapbox.io/api/asset/query' \
  -H 'Content-Type: application/json' \
  -d '{"chain":"Ethereum"}'
```

### Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `chain` | string | Yes | Chain name from `/config/chains` response `chain` field |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | number | 0 = success |
| `msg` | string | Response message |
| `data` | array | List of token objects |

#### Token Object

| Field | Type | Description |
|-------|------|-------------|
| `id` | number | Internal token ID |
| `nativeId` | number | Native chain network ID |
| `chain` | string | Chain name |
| `registerChain` | string | Token registration chain |
| `chainType` | number | Chain type |
| `chainId` | number | SwapBox chain ID (use in route request) |
| `assetId` | number | Asset ID (use in route request) |
| `contractAddress` | string | Token contract address (empty for native tokens) |
| `decimals` | number | Token decimal places |
| `assetName` | string | Full token name |
| `symbol` | string | Token ticker symbol |
| `assetType` | number | Asset type |
| `icon` | string | Token icon URL |
| `nulsCross` | boolean | Whether cross-chain via NULS is supported |
| `status` | number | 1 = active, 0 = inactive |
| `usdPrice` | number | Current USD price |
| `percent24h` | string | 24-hour price change percentage |
| `sort` | number | Sort order |
| `source` | string | Price source |
| `meme` | number | 1 = meme token |
| `bridgeInfoList` | array | Cross-chain bridge information |

### Example Response

```json
{
  "code": 0,
  "msg": "Success",
  "data": [
    {
      "symbol": "ETH",
      "chain": "Ethereum",
      "chainId": 101,
      "assetId": 1,
      "contractAddress": "",
      "decimals": 18,
      "usdPrice": 2174.00,
      "percent24h": "0.08",
      "status": 1
    },
    {
      "symbol": "USDT",
      "chain": "Ethereum",
      "chainId": 101,
      "assetId": 0,
      "contractAddress": "0xdac17f958d2ee523a2206206994597c13d831ec7",
      "decimals": 6,
      "usdPrice": 1.0,
      "status": 1
    }
  ]
}
```

---

## 3. POST /swap/route — Get Swap Route and Price Quote

Returns available swap routes with price quotes. Used for both price queries and swap execution.

### Request

```bash
curl -s -X POST 'https://swapbox.io/api/swap/route' \
  -H 'Content-Type: application/json' \
  -H 'language: en' \
  -H 'origin: https://swapbox.io' \
  -H 'referer: https://swapbox.io/' \
  -d '{
    "platform": "",
    "dex": "",
    "channel": "",
    "fromChain": "Ethereum",
    "toChain": "Ethereum",
    "fromAddress": "0x0000000000000000000000000000000000000001",
    "toAddress": "0x0000000000000000000000000000000000000001",
    "btcPubKey": "",
    "chainId": 101,
    "assetId": 1,
    "contractAddress": "",
    "swapChainId": 101,
    "swapAssetId": 0,
    "swapContractAddress": "0xdac17f958d2ee523a2206206994597c13d831ec7",
    "amount": "1",
    "slippage": "0.5",
    "smartSlippage": false,
    "fee": "",
    "isAntiMev": false
  }'
```

### Request Body Parameters

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `platform` | string | No | `""` | Platform identifier |
| `dex` | string | No | `""` | DEX filter (empty = all) |
| `channel` | string | No | `""` | Channel filter |
| `fromChain` | string | Yes | — | Source chain name |
| `toChain` | string | Yes | — | Destination chain name (same as fromChain for price query) |
| `fromAddress` | string | Yes | — | Sender address (use placeholder for price queries) |
| `toAddress` | string | Yes | — | Receiver address (use placeholder for price queries) |
| `btcPubKey` | string | No | `""` | BTC public key (required for BTC transactions) |
| `chainId` | number | Yes | — | Source token's chainId from asset query |
| `assetId` | number | Yes | — | Source token's assetId from asset query |
| `contractAddress` | string | Yes | — | Source token's contract address (empty for native) |
| `swapChainId` | number | Yes | — | Target token's (USDT) chainId from asset query |
| `swapAssetId` | number | Yes | — | Target token's (USDT) assetId from asset query |
| `swapContractAddress` | string | Yes | — | Target token's (USDT) contract address |
| `amount` | string | Yes | `"1"` | Amount of source token |
| `slippage` | string | No | `"0.5"` | Slippage tolerance in percent |
| `smartSlippage` | boolean | No | `false` | Use smart slippage calculation |
| `fee` | string | No | `""` | Fee override |
| `isAntiMev` | boolean | No | `false` | Anti-MEV protection |

### Required Headers

| Header | Value | Required |
|--------|-------|----------|
| `Content-Type` | `application/json` | Yes |
| `language` | `en` | Recommended |
| `origin` | `https://swapbox.io` | Recommended |
| `referer` | `https://swapbox.io/` | Recommended |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | number | 0 = success |
| `msg` | string | Response message |
| `data` | array | List of route objects (may be empty if no route available) |

#### Route Object

| Field | Type | Description |
|-------|------|-------------|
| `dex` | string | DEX name (e.g., "OKX", "1inch") |
| `channel` | string | Channel/aggregator name |
| `orderId` | string | Route order ID |
| `icon` | string | DEX icon URL |
| `best` | number | **1 = best/recommended route**, 0 = alternative |
| `priceImpact` | string | Price impact percentage |
| `fromTokenAmount` | string | Input token amount |
| `toTokenAmount` | string | **Output token amount (THIS IS THE PRICE)** |
| `minReceiveAmount` | string | Minimum receive amount after slippage |
| `approveAddress` | string | Contract address for token approval |
| `from` | string | Sender address |
| `to` | string | Contract address for execution |
| `fee` | string | Swap fee amount |
| `feePrice` | string | Fee in USD |
| `feeSymbol` | string | Fee token symbol |
| `crossFee` | string | Cross-chain fee (only for cross-chain routes) |
| `crossFeePrice` | string | Cross-chain fee in USD |
| `crossFeeSymbol` | string | Cross-chain fee token symbol |
| `path` | array | Swap path details |
| `swapType` | number | 1 = same-chain swap, 2 = cross-chain |

### Example Response

```json
{
  "code": 0,
  "msg": "Success",
  "data": [
    {
      "dex": "OKX",
      "channel": "OKX",
      "orderId": "0bbc2c8a-081e-4a08-b76c-f38f528ab6dc",
      "best": 1,
      "priceImpact": "0",
      "fromTokenAmount": "1",
      "toTokenAmount": "2182.158811",
      "minReceiveAmount": "2171.248016945",
      "fee": "10.910794055",
      "feePrice": "10.9108",
      "feeSymbol": "USDT",
      "swapType": 1
    },
    {
      "dex": "MetaPath",
      "channel": "Bridgers",
      "best": 0,
      "fromTokenAmount": "1",
      "toTokenAmount": "2170.637364",
      "minReceiveAmount": "2170.637364",
      "swapType": 1
    }
  ]
}
```

### Error Handling

| code | Meaning | Action |
|------|---------|--------|
| 0 | Success | Process the data |
| 500 | System exception | Retry once, then report error |
| Other | Various errors | Report `msg` to user |

If `data` is `null` or empty array `[]`, the trading pair has no available routes on this chain.

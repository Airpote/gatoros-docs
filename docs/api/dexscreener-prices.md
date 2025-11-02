![GatorOS Logo](../../assets/gator-app.jpg)

# DexScreener Prices API

Get real-time token prices and market data from DexScreener for Avalanche network tokens.

## Endpoint
```
GET /api/dexscreener-prices
```

## Parameters

### Query Parameters
- `tokens` (optional): Comma-separated list of token addresses
- `pairs` (optional): Comma-separated list of pair addresses
- `limit` (optional): Maximum number of results (default: 100, max: 1000)

## Example Request
```bash
curl "https://gatoros.app/api/dexscreener-prices?tokens=0x123...,0x456..."
```

## Response Format
```json
{
  "success": true,
  "data": {
    "pairs": [
      {
        "chainId": "43114",
        "dexId": "traderjoe",
        "url": "https://dexscreener.com/avalanche/0x...",
        "pairAddress": "0x...",
        "baseToken": {
          "address": "0x...",
          "name": "Token Name",
          "symbol": "TOKEN"
        },
        "quoteToken": {
          "address": "0x...",
          "name": "Wrapped AVAX",
          "symbol": "WAVAX"
        },
        "priceNative": "0.00000123",
        "priceUsd": "0.0123",
        "txns": {
          "h24": {
            "buys": 123,
            "sells": 456
          }
        },
        "volume": {
          "h24": 12345.67,
          "h6": 2345.67,
          "h1": 345.67
        },
        "priceChange": {
          "h24": 5.67,
          "h6": 2.34,
          "h1": -1.23
        },
        "liquidity": {
          "usd": 123456.78,
          "base": 12345.67,
          "quote": 23456.78
        },
        "fdv": 1234567.89,
        "marketCap": 987654.32,
        "pairCreatedAt": 1640995200,
        "info": {
          "imageUrl": "https://...",
          "websites": [{"url": "https://..."}],
          "socials": [{"platform": "twitter", "handle": "@..."}]
        }
      }
    ]
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## Data Fields

### Pair Information
- `chainId`: Avalanche chain ID (43114)
- `dexId`: DEX identifier (traderjoe, pangolin, etc.)
- `pairAddress`: Liquidity pool contract address
- `url`: DexScreener page URL

### Token Information
- `baseToken`: Primary token in the pair
- `quoteToken`: Secondary token (usually WAVAX)
- `address`: Token contract address
- `name`: Full token name
- `symbol`: Token symbol

### Price Data
- `priceNative`: Price in quote token
- `priceUsd`: Price in USD
- `priceChange`: Price change percentages (1h, 6h, 24h)

### Trading Data
- `txns`: Transaction counts by timeframe
- `volume`: Trading volume by timeframe
- `liquidity`: Pool liquidity information
- `fdv`: Fully diluted valuation
- `marketCap`: Market capitalization

## Error Responses

### Invalid Token Address
```json
{
  "success": false,
  "error": {
    "code": "INVALID_TOKEN",
    "message": "Invalid token address format"
  }
}
```

### Rate Limit Exceeded
```json
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT",
    "message": "Too many requests"
  }
}
```

## Rate Limits
- 100 requests per minute for public access
- 1000 requests per minute for authenticated users

## Supported DEXs
- Trader Joe
- Pangolin
- SushiSwap
- Curve
- Uniswap V3 (when available)

## Caching
Data is cached for 30 seconds to ensure freshness while maintaining performance.

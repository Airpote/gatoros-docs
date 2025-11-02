![GatorOS Logo](../../assets/gator-app.jpg)

# WAVAX Balance API

Get the WAVAX (Wrapped AVAX) balance for a specific wallet address on the Avalanche network.

## Endpoint
```
GET /api/wavax-balance
```

## Parameters

### Query Parameters
- `address` (required): Wallet address to query
- `format` (optional): Response format - "full" or "simple" (default: "full")

## Example Request
```bash
curl "https://gatoros.app/api/wavax-balance?address=0x123..."
```

## Response Format (Full)
```json
{
  "success": true,
  "data": {
    "address": "0x1234567890123456789012345678901234567890",
    "balance": "1000000000000000000",
    "balanceFormatted": "1.0",
    "balanceUSD": 45.67,
    "symbol": "WAVAX",
    "name": "Wrapped AVAX",
    "decimals": 18,
    "contractAddress": "0xB31f66AA3C1e785363F0875A1B74E27b85FD66c7",
    "price": 45.67,
    "priceChange24h": 2.34,
    "lastUpdated": "2024-01-01T12:00:00Z"
  },
  "timestamp": "2024-01-01T12:00:00Z"
}
```

## Response Format (Simple)
```json
{
  "success": true,
  "data": {
    "balance": "1.0",
    "balanceUSD": 45.67
  },
  "timestamp": "2024-01-01T12:00:00Z"
}
```

## Data Fields

### Full Response
- `address`: Queried wallet address
- `balance`: Raw balance in wei (18 decimals)
- `balanceFormatted`: Human-readable balance
- `balanceUSD`: USD value of balance
- `symbol`: Token symbol (WAVAX)
- `name`: Token name (Wrapped AVAX)
- `decimals`: Token decimals (18)
- `contractAddress`: WAVAX contract address
- `price`: Current WAVAX price in USD
- `priceChange24h`: 24h price change percentage
- `lastUpdated`: Last balance update timestamp

### Simple Response
- `balance`: Formatted balance string
- `balanceUSD`: USD value

## Error Responses

### Invalid Address
```json
{
  "success": false,
  "error": {
    "code": "INVALID_ADDRESS",
    "message": "Invalid Avalanche address format"
  }
}
```

### Network Error
```json
{
  "success": false,
  "error": {
    "code": "NETWORK_ERROR",
    "message": "Unable to connect to Avalanche network"
  }
}
```

### Contract Error
```json
{
  "success": false,
  "error": {
    "code": "CONTRACT_ERROR",
    "message": "Error reading from WAVAX contract"
  }
}
```

## Rate Limits
- 100 requests per minute per IP
- 1000 requests per minute for authenticated users

## WAVAX Contract Details
- **Address**: 0xB31f66AA3C1e785363F0875A1B74E27b85FD66c7
- **Network**: Avalanche C-Chain (43114)
- **Decimals**: 18
- **Standard**: ERC-20 compatible

## Use Cases

### DeFi Applications
- Check user's AVAX balance for transactions
- Calculate transaction fees
- Portfolio tracking

### Wallets
- Display AVAX holdings
- Transaction preparation
- Balance validation

### Analytics
- Track AVAX distribution
- Monitor large holders
- Historical balance analysis

## Caching
Balance data is cached for 30 seconds to balance freshness with performance. Price data is cached for 60 seconds.

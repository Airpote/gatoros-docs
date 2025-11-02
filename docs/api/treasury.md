# Treasury API

Get comprehensive portfolio data including token balances, LP positions, and staking information for a connected wallet.

## Endpoint
```
GET /api/treasury
```

## Authentication
Requires wallet signature authentication. The endpoint expects a signed message proving wallet ownership.

## Parameters

### Query Parameters
- `address` (required): Wallet address to query
- `includeLP` (optional): Include liquidity pool positions (default: true)
- `includeStaking` (optional): Include staking positions (default: true)
- `includeNFT` (optional): Include NFT holdings (default: false)

### Headers
- `Authorization`: Bearer token from wallet signature

## Example Request
```bash
curl -H "Authorization: Bearer <token>" \
     "https://gatoros.app/api/treasury?address=0x123..."
```

## Response Format
```json
{
  "success": true,
  "data": {
    "address": "0x...",
    "totalValue": 12345.67,
    "totalValueUSD": 12345.67,
    "tokens": [
      {
        "address": "0x...",
        "symbol": "GATOR",
        "name": "Gator Token",
        "balance": "1000.0",
        "balanceUSD": 1234.56,
        "price": 1.23456,
        "priceChange24h": 5.67,
        "logoURI": "https://..."
      }
    ],
    "liquidityPositions": [
      {
        "pairAddress": "0x...",
        "token0": {
          "address": "0x...",
          "symbol": "GATOR",
          "balance": "500.0"
        },
        "token1": {
          "address": "0x...",
          "symbol": "WAVAX",
          "balance": "10.0"
        },
        "totalValueUSD": 2345.67,
        "poolShare": 0.00123,
        "rewards": [
          {
            "token": "0x...",
            "symbol": "JOE",
            "earned": "1.23"
          }
        ]
      }
    ],
    "stakingPositions": [
      {
        "contractAddress": "0x...",
        "tokenAddress": "0x...",
        "stakedAmount": "1000.0",
        "rewards": "50.0",
        "apy": 12.5,
        "lockPeriod": 30
      }
    ],
    "nfts": [
      {
        "contractAddress": "0x...",
        "tokenId": "123",
        "name": "Gator Avatar #123",
        "image": "https://...",
        "collection": "Gator Avatars"
      }
    ]
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## Data Fields

### Portfolio Summary
- `totalValue`: Total portfolio value in AVAX
- `totalValueUSD`: Total portfolio value in USD
- `address`: Queried wallet address

### Token Holdings
- `address`: Token contract address
- `symbol`: Token symbol
- `name`: Token name
- `balance`: Raw token balance
- `balanceUSD`: USD value of holdings
- `price`: Current token price
- `priceChange24h`: 24h price change percentage

### Liquidity Positions
- `pairAddress`: LP contract address
- `token0/token1`: Token pair information
- `totalValueUSD`: Total USD value of position
- `poolShare`: Percentage ownership of pool
- `rewards`: Pending reward tokens

### Staking Positions
- `contractAddress`: Staking contract address
- `stakedAmount`: Amount of tokens staked
- `rewards`: Available rewards
- `apy`: Annual percentage yield
- `lockPeriod`: Lock period in days

## Error Responses

### Invalid Address
```json
{
  "success": false,
  "error": {
    "code": "INVALID_ADDRESS",
    "message": "Invalid wallet address format"
  }
}
```

### Authentication Required
```json
{
  "success": false,
  "error": {
    "code": "AUTH_REQUIRED",
    "message": "Wallet signature authentication required"
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
- 100 requests per minute per wallet
- 1000 requests per minute for premium users

## Supported Protocols

### DEXs
- Trader Joe
- Pangolin
- SushiSwap
- Curve

### Staking
- Gator staking contracts
- Platform staking pools
- Validator delegations

### NFTs
- ERC-721 tokens
- ERC-1155 tokens
- Custom NFT collections

## Caching
Portfolio data is cached for 60 seconds. Real-time updates available for premium users.

![GatorOS Logo](../../assets/gator-app.jpg)

# API Overview

GatorOS provides a comprehensive REST API for accessing DeFi data, wallet information, and platform features. All endpoints return JSON responses and support CORS for web applications.

## Base URL
```
https://gatoros.app/api
```

## Authentication
Most endpoints require wallet signature authentication. Use your connected wallet to sign authentication messages.

## Rate Limits
- **Public Endpoints**: 100 requests per minute
- **Authenticated Endpoints**: 1000 requests per minute
- **Premium Endpoints**: Unlimited (subscription required)

## Response Format
All responses follow this structure:
```json
{
  "success": true,
  "data": { ... },
  "error": null,
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## Error Handling
Error responses include:
```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message",
    "details": { ... }
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## SDK Support
- **JavaScript SDK**: `npm install @gatoros/sdk`
- **Python SDK**: `pip install gatoros-sdk`
- **REST Client**: Direct HTTP requests

## Webhooks
Subscribe to real-time events:
- Transaction confirmations
- Price alerts
- Portfolio changes
- Staking rewards

## Endpoints Overview

### Price Data
- `GET /api/dexscreener-prices` - Token prices and market data

### Wallet Data
- `GET /api/treasury` - Portfolio and balance information
- `GET /api/wavax-balance` - WAVAX balance specifically

### Social Data
- `GET /api/arena/feed` - Community feed
- `GET /api/arena/profile` - User profile data

### DeFi Operations
- `POST /api/swap/quote` - Get swap quotes
- `POST /api/swap/execute` - Execute token swaps
- `POST /api/stake` - Stake tokens
- `POST /api/unstake` - Unstake tokens

## Testing
Use the sandbox environment for testing:
```
https://sandbox.gatoros.app/api
```

## Support
- **Documentation**: Full API reference available
- **Community**: Discord support channel
- **Enterprise**: Dedicated support for large integrations

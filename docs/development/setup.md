# Development Setup

Complete guide to setting up a development environment for GatorOS.

## Prerequisites

### System Requirements
- **Node.js**: v18.0.0 or higher
- **npm**: v8.0.0 or higher (comes with Node.js)
- **Git**: Latest version
- **Modern Browser**: Chrome, Firefox, or Safari

### Recommended Tools
- **VS Code**: Recommended editor with extensions
- **GitHub Desktop**: Optional GUI for Git
- **Postman**: For API testing

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/your-org/gatoros.git
cd gatoros
```

### 2. Install Dependencies
```bash
npm install
# or
pnpm install
```

### 3. Environment Setup
Create a `.env.local` file in the root directory:
```env
# Wallet Connect
NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID=your_project_id

# DexScreener API (if needed)
DEXSCREENER_API_KEY=your_api_key

# Arena API
ARENA_API_URL=https://api.arena.social
ARENA_API_KEY=your_api_key

# Development
NODE_ENV=development
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 4. Start Development Server
```bash
npm run dev
# or
pnpm dev
```

The application will be available at `http://localhost:3000`.

## Project Structure

```
gatoros/
├── app/                    # Next.js app directory
│   ├── api/               # API routes
│   ├── globals.css        # Global styles
│   ├── layout.tsx         # Root layout
│   └── page.tsx           # Home page
├── components/            # React components
│   ├── gator-os.tsx       # Main OS component
│   ├── wallet-provider.tsx # Wallet connection
│   └── ...                # Other components
├── lib/                   # Utility libraries
│   ├── api-service.ts     # API service functions
│   ├── utils.ts           # Utility functions
│   └── verified-tokens.ts # Token lists
├── public/                # Static assets
│   ├── audio/            # Audio files
│   ├── background/       # Background images
│   └── tokenlogo/        # Token logos
├── styles/               # Additional styles
└── scripts/              # Build/utility scripts
```

## Development Workflow

### 1. Create a Feature Branch
```bash
git checkout -b feature/your-feature-name
```

### 2. Make Changes
- Follow the existing code style
- Add tests for new features
- Update documentation

### 3. Test Your Changes
```bash
npm run test
npm run build
```

### 4. Commit and Push
```bash
git add .
git commit -m "Add your feature description"
git push origin feature/your-feature-name
```

### 5. Create Pull Request
Open a pull request on GitHub for code review.

## Available Scripts

### Development
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npm run type-check` - Run TypeScript checks

### Testing
- `npm run test` - Run all tests
- `npm run test:watch` - Run tests in watch mode
- `npm run test:coverage` - Run tests with coverage

### Utilities
- `npm run clean` - Clean build artifacts
- `npm run format` - Format code with Prettier
- `npm run analyze` - Analyze bundle size

## Environment Variables

### Required
- `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID`: WalletConnect project ID

### Optional
- `DEXSCREENER_API_KEY`: For enhanced price data
- `ARENA_API_KEY`: For Arena.social integration
- `NEXT_PUBLIC_APP_URL`: Application URL for callbacks

## Wallet Integration

### Supported Wallets
- MetaMask
- Trust Wallet
- Coinbase Wallet
- WalletConnect compatible wallets

### Testing Wallets
Use test wallets on Avalanche Fuji testnet:
- Address: 0x...
- Private Key: For testing only

## API Development

### Local API Routes
API routes are located in `app/api/` directory. Example:
```typescript
// app/api/example/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  return NextResponse.json({ message: 'Hello World' });
}
```

### Testing APIs
Use tools like Postman or curl:
```bash
curl http://localhost:3000/api/example
```

## Component Development

### Component Structure
```typescript
// components/ExampleComponent.tsx
'use client';

import React from 'react';

interface Props {
  title: string;
}

export function ExampleComponent({ title }: Props) {
  return (
    <div className="example-component">
      <h2>{title}</h2>
    </div>
  );
}
```

### Styling
Use Tailwind CSS classes:
```typescript
<div className="bg-blue-500 text-white p-4 rounded-lg">
  Styled component
</div>
```

## Deployment

### Vercel (Recommended)
1. Connect GitHub repository to Vercel
2. Configure environment variables
3. Deploy automatically on push

### Manual Deployment
```bash
npm run build
npm run start
```

## Troubleshooting

### Common Issues

#### Port Already in Use
```bash
# Find process using port 3000
lsof -ti:3000 | xargs kill -9
# Or use different port
npm run dev -- -p 3001
```

#### Build Errors
- Clear node_modules: `rm -rf node_modules && npm install`
- Clear Next.js cache: `rm -rf .next`

#### Wallet Connection Issues
- Check WalletConnect project ID
- Ensure HTTPS in production
- Verify wallet browser compatibility

### Getting Help
- Check existing issues on GitHub
- Join the community Discord
- Review documentation

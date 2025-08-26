# Time-Locked Wallet Project

A Solana-based time-locked wallet implementation with a React frontend and Anchor smart contract backend.

## Demo

- [Live Demo](https://time-locked-wallet-zeta.vercel.app/)

- [Video Demo](https://www.youtube.com/watch?v=EJ9U0f788Dg&ab_channel=lou1s)

## Project Structure

This project consists of two main components:

- **Frontend**: [time-locked-wallet-frontend](https://github.com/0xLou1s/time-locked-wallet-frontend) - React + Next.js application
- **Program**: [time-locked-wallet-program](https://github.com/0xLou1s/time-locked-wallet-program) - Solana smart contract (Anchor framework)

```
├── frontend/          # React + Next.js frontend application
├── program/           # Solana smart contract (Anchor framework)
└── README.md    
```

## Prerequisites

Before running this project, ensure you have the following installed:

- **Node.js** (v18 or higher)
- **pnpm** or **npm** (for frontend dependencies)
- **yarn** (for program dependencies)
- **Rust** (latest stable version)
- **Solana CLI** (latest version)
- **Anchor CLI** (latest version)

## Quick Start

### 1. Clone and Setup

```bash
git clone https://github.com/0xLou1s/time-locked-wallet
cd time-locked-wallet
```

### 2. Setup Solana Environment

```bash
# Set to devnet for development
solana config set --url devnet

# Create a new wallet (if you don't have one)
solana-keygen new

# Airdrop SOL for testing (devnet only)
solana airdrop 2
```

### 3. Deploy Smart Contract

```bash
cd program

# Install dependencies
yarn install

# Build the program
anchor build

# Deploy to devnet
anchor deploy --provider.cluster devnet

# Run tests
anchor test
```

### 4. Run Frontend

```bash
cd frontend

# Install dependencies
pnpm install
# or
npm install

# Set environment variables
cp .env.example .env
# Edit .env with your deployed program ID

# Run development server
pnpm dev
# or
npm run dev
```

The frontend will be available at `http://localhost:3000`

## Detailed Setup Instructions

### Smart Contract Setup

The smart contract is built using the Anchor framework and implements time-locked wallet functionality.

```bash
cd program

# Install dependencies
yarn install

# Build the program
anchor build

# Check program ID
solana address -k target/deploy/time-lock-wallet-anchor-keypair.json

# Update Anchor.toml with the correct program ID
# Update lib.rs with the correct program ID

# Deploy to devnet
anchor deploy --provider.cluster devnet

# Verify deployment
solana program show <PROGRAM_ID>
```

### Frontend Setup

The frontend is a Next.js application with TypeScript that connects to the Solana blockchain. The application uses environment variables to configure RPC endpoints and network settings.

```bash
cd frontend

# Install dependencies
pnpm install

# Environment configuration
cp .env.example .env
```

Edit `.env` with your configuration:
```env
NEXT_PUBLIC_USE_MAINNET=false
NEXT_PUBLIC_SOLANA_RPC_URL=https://mainnet.helius-rpc.com/?api-key=YOUR_API_KEY
NEXT_PUBLIC_SOLANA_RPC_URL_DEVNET=https://devnet.helius-rpc.com/?api-key=YOUR_API_KEY
```

**Note**: Replace `YOUR_API_KEY` with your actual Helius API key. You can get one from [Helius](https://www.helius.dev/).

**Important**: The program ID is configured in `frontend/lib/constants.ts`. If you're deploying your own smart contract, update the `PROGRAM_ID` constant in that file.

### Configuration Files

The frontend uses several configuration files:

- **`frontend/lib/constants.ts`**: Contains program ID, network settings, RPC endpoints, and other constants
- **`.env.local`**: Environment variables for RPC endpoints and network selection

```bash
# Run development server
pnpm dev

# Build for production
pnpm build

# Start production server
pnpm start
```

## Development

### Smart Contract Development

```bash
cd program

# Run tests
anchor test

# Run specific test
anchor test --skip-local-validator

# Check program logs
solana logs <PROGRAM_ID>
```

### Frontend Development

```bash
cd frontend

# Run linting
pnpm lint

# Run type checking
pnpm type-check

# Note: Frontend tests are not currently implemented
```

## Testing

### Smart Contract Tests

```bash
cd program
anchor test
```

## Deployment

### Smart Contract to Mainnet

```bash
cd program

# Set to mainnet
solana config set --url mainnet-beta

# Deploy (ensure you have sufficient SOL)
anchor deploy --provider.cluster mainnet-beta
```

### Frontend to Production

```bash
cd frontend

# Build
pnpm build

# Deploy to your preferred hosting service
# (Vercel, Netlify, etc.)
```

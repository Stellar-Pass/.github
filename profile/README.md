<div align="center">

<img src="logo.svg" width="120" height="120" alt="Stellar Pass Logo">

# Stellar Pass

### NFT Event Ticketing & Proof-of-Attendance on Stellar

**The first ticketing protocol purpose-built for Stellar's native capabilities.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Rust](https://img.shields.io/badge/Rust-000000?logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Soroban](https://img.shields.io/badge/Soroban-00B4D8?logo=stellar&logoColor=white)](https://soroban.stellar.org/)
[![Next.js](https://img.shields.io/badge/Next.js-000000?logo=next.js&logoColor=white)](https://nextjs.org/)

</div>

---

## The Problem

The global events industry is **$686B** and the ticketing market is **$852B**, yet:

- 🔴 **30%+** of tickets are counterfeited or scalped annually
- 🔴 Organizers lose **$12B+/year** to fraud and unauthorized resale
- 🔴 Attendees have **no portable proof** they were there
- 🔴 Existing blockchain ticketing ignores chain-native capabilities

## The Solution

Stellar Pass leverages what makes Stellar unique — not just another "NFTs on a chain" project, but a protocol that **couldn't exist on any other network**.

| Stellar Feature | How We Use It |
|---|---|
| **Soroban NFTs (SEP-0048)** | Ticket and POAP badge minting with on-chain metadata |
| **Asset Freeze / Clawback** | Organizers can revoke stolen or scalped tickets — *a Stellar-unique capability* |
| **Claimable Balances** | Airdrop tickets to users who don't have wallets yet |
| **Built-in DEX** | Secondary market ticket resale with price controls |
| **Muxed Accounts** | Seamless purchase session management |
| **USDC Settlement** | Instant organizer payouts in ~5 seconds |
| **SEP-10 Auth** | Wallet-based authentication — no passwords, no custodians |
| **SEP-24** | Fiat on-ramp so anyone can buy tickets with a card |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                             │
│  Organizer Dashboard · Attendee Web App · Widget · Scanner       │
├─────────────────────────────────────────────────────────────────┤
│                          API LAYER                               │
│  Fastify Backend — Events, Tickets, Auth, Check-in, POAP         │
├─────────────────────────────────────────────────────────────────┤
│                   SMART CONTRACT LAYER (Soroban)                 │
│  Ticket NFT · POAP Badge · Resale Escrow                        │
├─────────────────────────────────────────────────────────────────┤
│                        INDEXER LAYER                             │
│  Horizon Watcher — Payments, Ownership, Attendance               │
├─────────────────────────────────────────────────────────────────┤
│                       STELLAR NETWORK                            │
│  Freeze/Clawback · Claimable Balances · DEX · USDC · Muxed Accts│
└─────────────────────────────────────────────────────────────────┘
```

## Monorepo Structure

| Component | Description | Tech Stack |
|---|---|---|
| [`stellar-pass-frontend`](https://github.com/Stellar-Pass/StellarPass-MonoRepo/tree/main/stellar-pass-frontend) | Next.js 14 app — organizer dashboard, attendee pages, check-in PWA | Next.js, TypeScript, Tailwind CSS |
| [`stellar-pass-backend`](https://github.com/Stellar-Pass/StellarPass-MonoRepo/tree/main/stellar-pass-backend) | API server — events, tickets, auth, analytics, webhooks | Fastify, TypeScript, PostgreSQL, Redis |
| [`stellar-pass-contracts`](https://github.com/Stellar-Pass/StellarPass-MonoRepo/tree/main/stellar-pass-contracts) | On-chain logic — ticket NFTs, POAP badges, resale escrow | Rust, Soroban |
| [`stellar-pass-indexer`](https://github.com/Stellar-Pass/StellarPass-MonoRepo/tree/main/stellar-pass-indexer) | Horizon stream processor — tracks payments, ownership, attendance | TypeScript, Stellar Horizon |
| [`stellar-pass-shared`](https://github.com/Stellar-Pass/StellarPass-MonoRepo/tree/main/stellar-pass-shared) | Shared types, constants, and validation schemas | TypeScript, Zod |

---

## Getting Started

**Prerequisites:** Node.js 20+, Docker, Rust + Cargo, Stellar CLI

```bash
# Clone the monorepo
git clone https://github.com/Stellar-Pass/StellarPass-MonoRepo.git
cd StellarPass-MonoRepo

# Start infrastructure
docker-compose up -d postgres redis

# Run the backend
cd stellar-pass-backend && cp .env.example .env && npm install && npm run dev

# Run the indexer
cd stellar-pass-indexer && cp .env.example .env && npm install && npm run dev

# Run the frontend
cd stellar-pass-frontend && cp .env.example .env.local && npm install && npm run dev
```

Or spin up everything at once:

```bash
docker-compose up
```

---

## How It Works

### For Event Organizers
1. **Create an event** — set name, date, venue, ticket tiers, and capacity
2. **Mint tickets** — each ticket is a Soroban NFT (SEP-0048) with embedded metadata
3. **Distribute** — share a link, airdrop via claimable balances, or sell with USDC
4. **Manage** — freeze/clawback stolen tickets, set resale price floors, track analytics
5. **Get paid** — USDC settles to your Stellar account in ~5 seconds

### For Attendees
1. **Discover** — browse events on the web app or through an embed widget
2. **Buy** — pay with USDC, other Stellar assets, or fiat via SEP-24 on-ramp
3. **Attend** — show your QR code at the door; the scanner PWA verifies on-chain
4. **Prove it** — receive a soulbound POAP badge as permanent proof of attendance
5. **Trade** — list unused tickets on the built-in DEX secondary market

---

## Key Differentiators

| | Traditional Ticketing | Generic Blockchain | **Stellar Pass** |
|---|---|---|---|
| Counterfeit protection | Barcodes (easily copied) | NFTs (but no revocation) | **NFTs + freeze/clawback** |
| Payout speed | 30-90 days | Varies by chain | **~5 seconds (USDC)** |
| Onboard non-crypto users | N/A | Complex wallets | **Claimable balances + SEP-24 fiat** |
| Secondary market control | None | Limited | **Built-in DEX with price controls** |
| Proof of attendance | Paper tickets, emails | Some POAP projects | **Soulbound Soroban POAPs** |
| Organizer control post-sale | None | Minimal | **Full freeze/clawback authority** |

---

## Contributing

We welcome contributions from the community. See our [Contributing Guide](https://github.com/Stellar-Pass/StellarPass-MonoRepo/blob/main/CONTRIBUTING.md) for:

- Development setup and environment configuration
- Coding standards and pull request workflow
- Issue reporting and feature requests

---

## Links

- **Repository:** [StellarPass-MonoRepo](https://github.com/Stellar-Pass/StellarPass-MonoRepo)
- **Stellar:** [stellar.org](https://stellar.org)
- **Soroban:** [soroban.stellar.org](https://soroban.stellar.org)

---

## License

MIT — see [LICENSE](https://github.com/Stellar-Pass/StellarPass-MonoRepo/blob/main/LICENSE) for details.

---

<div align="center">

**Built with ❤️ for the Stellar ecosystem**

</div>

# 🏆 BracketVault

A trustless tournament escrow system built on Stellar Soroban that protects prize pools and automatically distributes winnings after match results are finalized – for any esports or competitive gaming event.

**Status**	v0.1 — smart contract + Next.js wallet integration, Testnet ready  
**License**	MIT

---

## 🧩 Problem

Esports tournaments often rely on informal payment systems where players send entry fees directly to organizers.

This creates serious problems:

- Tournament organizers can disappear with prize pools.
- Players cannot guarantee that rewards will be distributed.
- Manual payout calculations cause delays and disputes.
- Small community tournaments lose money through expensive payment methods.
- Many players hesitate to join community tournaments because they do not trust the organizer holding the prize pool.

**The result**: esports remains fragmented and trust‑bound, limiting the growth of competitive gaming across all titles (League of Legends, VALORANT, Mobile Legends, Dota 2, Fighting Games, etc.).

---

## 🌟 Vision

Make every tournament payout as reliable as a smart contract — automatic, transparent, and non‑custodial. Anyone running a community tournament should be able to create a secure prize pool in under a minute, with players joining directly from their wallets, and winnings distributed automatically the moment the referee confirms results.

Long‑term, BracketVault becomes the **default financial layer for esports**, bridging the gap between competitive play and instant, borderless payments via Stellar.

---

## 🎯 Purpose

Built for the Stellar ecosystem, BracketVault demonstrates how Soroban smart contracts can solve real‑world trust problems in gaming communities. The contract is lightweight, auditable, and ready for integration with tournament platforms.

By combining USDC (or XLM) escrow with deterministic payout logic, we give players and organizers the confidence that prize pools are safe and payouts are guaranteed.

---

## 👥 Target Users

- **Esports Tournament Organizers** – local communities, campus leagues, gaming cafes, online events. They need a secure, easy‑to‑use tool to manage entry fees and distribute prizes without handling cash.
- **Competitive Players** – amateur and semi‑pro players who want guaranteed payouts and transparent tournament processes.
- **Community Platforms** – future integration with tournament management systems (e.g., Toornament, Challonge, Start.gg) to automate prize distribution.

---

## ✨ Features

- **Trustless Escrow** – entry fees are locked in a Soroban contract; only the contract can release funds based on predefined rules.
- **Automated Prize Distribution** – after referee confirmation, winnings are split according to preset percentages (e.g., 60% / 30% / 10%) and sent directly to winners’ wallets.
- **Multi‑party Authorization** – the organizer cannot withdraw funds arbitrarily; a designated referee must finalize results.
- **Transparent on‑chain tracking** – every player registration and payout is visible on Stellar.
- **Freighter Wallet Integration** – players and organizers connect via Freighter on Stellar Testnet (mainnet ready).
- **Send XLM / USDC** – (future) entry fees and winnings in USDC or XLM.
- **Modern UI** – built with Next.js 15 + Tailwind, responsive for desktop and mobile.

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Smart Contracts** | Rust 1.88 + Soroban SDK 22, `wasm32v1-none` target |
| **Frontend** | Next.js 15 (App Router, React 19 RSC, Server Actions), TypeScript, Tailwind 4, shadcn/ui |
| **Wallet Integration** | `@stellar/freighter-api`, `@stellar/stellar-sdk` (Horizon + Soroban RPC) |
| **Testing** | `cargo test` for contracts, `vitest` + `playwright` for frontend (optional) |
| **Infrastructure** | Railway / Vercel (frontend), Stellar Testnet (contract) |
| **Package Manager** | `npm` (frontend), `cargo` (contracts) |

---

## 🚀 How to Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/your-org/bracket-vault.git
cd bracket-vault
2. Smart Contract (Soroban)
bash
cd contracts/bracket_vault
cargo build --target wasm32v1-none --release
cargo test
Optionally deploy to Testnet using the soroban CLI:

bash
soroban contract deploy \
  --wasm target/wasm32v1-none/release/bracket_vault.wasm \
  --source <your-identity> \
  --network testnet
3. Frontend (Next.js)
bash
cd web
npm install
cp .env.example .env.local   # fill in required env vars (see below)
npm run dev
The app will be available at http://localhost:3000.

Environment variables (.env.local):

env
# Stellar (Testnet by default)
NEXT_PUBLIC_STELLAR_HORIZON_URL=https://horizon-testnet.stellar.org

# Optional: for future contract interaction
# NEXT_PUBLIC_CONTRACT_ID=<deployed contract address>
The frontend uses Freighter wallet – install the browser extension and switch to Testnet.

🌐 Deployment
Testnet – contract deployed to Stellar Testnet; frontend can be deployed to Vercel / Railway.

Mainnet – after thorough testing, the contract can be deployed to mainnet with USDC support.

Deployment instructions for the contract are in contracts/bracket_vault/README.md (if provided).

🎥 Demo
(Coming soon) – a walkthrough video will be linked here.

👨‍💻 Team
Name	Role	GitHub
Julyza Peña	Lead Developer	@aizypena
📜 License
MIT License

Copyright (c) 2026 BracketVault

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction.

Developer Reference
Project Layout
text
bracket-vault/
├── contracts/
│   └── bracket_vault/          # Soroban smart contract
│       ├── src/
│       │   ├── lib.rs
│       │   └── test.rs
│       ├── Cargo.toml
│       └── Makefile
├── web/                        # Next.js frontend
│   ├── src/
│   │   ├── app/                # App Router pages
│   │   ├── components/         # React components (wallet panel, etc.)
│   │   ├── hooks/              # Custom hooks (useStellarWallet)
│   │   ├── lib/                # Stellar SDK setup, utilities
│   │   └── types/              # Global TypeScript declarations
│   ├── package.json
│   ├── tsconfig.json
│   └── ...
└── README.md
Smart Contract Functions
initialize(organizer: Address, referee: Address, entry_fee: u64) – creates a tournament.

join_tournament(player: Address) – registers a player (requires paying entry fee).

finalize_results(first: Address, second: Address, third: Address) – referee sets final rankings.

get_pool() – returns current prize pool.

get_reward(player: Address) – returns calculated winnings for a player.

is_finished() – checks if settlement is complete.

Frontend Scripts (inside frontend/)
Script	Purpose
npm run dev	Start dev server with HMR
npm run build	Typecheck + production build
npm run start	Start production server
npm run typecheck	Run TypeScript compiler
npm run lint	ESLint
Environment Variables (Frontend)
See .env.example in the frontend/ directory.

NEXT_PUBLIC_STELLAR_HORIZON_URL – Stellar Horizon URL (default Testnet).

(Future) NEXT_PUBLIC_CONTRACT_ID – deployed contract address.

Contract Tests
bash
cd contracts/bracket_vault
cargo test
All tests pass – 5 unit tests covering initialization, registration, finalization, and payout calculation.

Roadmap (Next Steps)
USDC Escrow – integrate Stellar USDC asset contract for entry fees and winnings.

Tournament Management UI – create/join/finalize tournaments from the dashboard.

Player Reputation – on‑chain tournament history and win rate.

AI Match Verification – read screenshots to auto‑finalize results.

Multi‑chain Support – optionally support other chains (Solana, etc.).

Contributing
Contributions are welcome! Please open an issue or PR. For major changes, discuss first.

Support
For questions, open a GitHub issue or reach out via jbpena101@gmail.com.


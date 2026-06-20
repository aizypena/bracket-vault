# BracketVault

A trustless Mobile Legends: Bang Bang (MLBB) tournament escrow system built on Stellar Soroban that protects prize pools and automatically distributes winnings after match results are finalized.

---

# Overview

BracketVault helps grassroots Mobile Legends: Bang Bang (MLBB) tournament organizers create secure competitions where player entry fees are locked inside a Soroban smart contract.

Instead of players sending entry fees directly to organizers and hoping they receive their rewards, BracketVault keeps tournament funds transparent and enforces automatic prize distribution rules.

When the tournament ends, an authorized referee confirms the final rankings and the smart contract calculates the reward allocation.

Example:


🥇 1st Place: 60%
🥈 2nd Place: 30%
🥉 3rd Place: 10%


---

# Problem

Grassroots Mobile Legends tournaments often rely on informal payment systems where players send entry fees directly to organizers.

This creates serious problems:

- Tournament organizers can disappear with MLBB prize pools
- Players cannot guarantee that rewards will be distributed
- Manual payout calculations cause delays and disputes
- Small community tournaments lose money through expensive payment methods

Many players hesitate to join community tournaments because they do not trust the organizer holding the prize pool.

---

# Solution

BracketVault provides a Soroban-powered tournament escrow vault where:

1. Organizers create MLBB tournaments
2. Players join by paying entry fees
3. Funds are tracked transparently
4. Referees confirm final rankings
5. Winners receive automatically calculated prize allocations

BracketVault removes the need for players to trust organizers with tournament funds.

---

# Why Stellar?

Stellar provides the ideal financial layer for grassroots esports because it offers:

- Fast settlement
- Extremely low transaction costs
- Global payment accessibility
- USDC support
- Smart contract automation through Soroban

Players from different countries can receive winnings without expensive bank transfers or payment delays.

---

# Stellar Features Used

## Soroban Smart Contracts

Used for:

- Tournament escrow logic
- Player registration
- Prize pool management
- Winner settlement rules

---

## USDC Transfers (Production Version)

Future integration:

- Players pay entry fees using USDC
- Contract locks the tournament prize pool
- Winners receive USDC rewards automatically

---

## Multi-Party Authorization

The tournament organizer cannot simply withdraw the prize pool.

Settlement requires:

- Authorized referee confirmation
- Smart contract rules

---

# Target Users

## MLBB Tournament Organizers

Examples:

- Local Mobile Legends tournaments
- Campus MLBB leagues
- Gaming cafe competitions
- Community esports groups

Regions:

- Philippines
- Indonesia
- Malaysia
- Southeast Asia

Pain points:

- Managing player entry fees
- Preventing payout disputes
- Increasing player trust

---

## MLBB Players

Examples:

- Amateur esports teams
- Competitive ranked players
- Community tournament participants

Benefits:

- Guaranteed prize distribution
- Transparent tournament process
- Faster payouts

---

# MVP Workflow

## 1. Create MLBB Tournament

Organizer initializes a tournament.

Example:


Tournament:

SEA Mobile Legends Championship

Entry Fee:

10 USDC


---

## 2. Players Join

Teams register for the tournament:


Team Alpha
Team Bravo
Team Charlie


Prize pool grows:


30 USDC locked


---

## 3. Match Completion

Tournament finishes.

Referee verifies:


🥇 Team Alpha

🥈 Team Bravo

🥉 Team Charlie


---

## 4. Automatic Settlement

Contract calculates:


Prize Pool: 300 USDC

Team Alpha:
180 USDC

Team Bravo:
90 USDC

Team Charlie:
30 USDC


---

# Smart Contract Functions

## initialize()

Creates tournament escrow.

```rust
initialize(
    organizer,
    referee,
    entry_fee
)
join_tournament()

Allows players to enter the MLBB tournament.

join_tournament(player)
finalize_results()

Referee submits final rankings.

finalize_results(
    first,
    second,
    third
)
get_pool()

Returns current prize pool.

get_pool()
get_reward()

Returns player's calculated winnings.

get_reward(player)
is_finished()

Checks if tournament settlement is completed.

is_finished()
Project Structure
bracket_vault/

├── src/
│
│   ├── lib.rs
│   └── test.rs
│
├── Cargo.toml
│
└── README.md
Timeline
Week 1

Smart contract development:

Tournament creation
Player registration
Escrow logic
Prize calculation
Contract testing
Week 2

Web application:

Tournament dashboard
Wallet connection
Player registration
Match result submission
Week 3

Deployment:

Stellar Testnet deployment
UI improvements
Demo preparation
Installation
Requirements

Install Rust:

rustup update

Install Soroban CLI:

cargo install --locked soroban-cli

Check installation:

soroban --version
Build Contract

Compile the Soroban smart contract:

soroban contract build

Generated file:

target/wasm32-unknown-unknown/release/

bracket_vault.wasm
Run Tests

Run contract tests:

cargo test

Expected:

5 passed
0 failed
Deploy to Stellar Testnet

Create an identity:

soroban config identity generate bracket-admin

Deploy:

soroban contract deploy \
--wasm target/wasm32-unknown-unknown/release/bracket_vault.wasm \
--source bracket-admin \
--network testnet
Example CLI Usage
Initialize Tournament
soroban contract invoke \
--id CONTRACT_ID \
--source bracket-admin \
--network testnet \
-- initialize \
--organizer ORGANIZER_ADDRESS \
--referee REFEREE_ADDRESS \
--entry_fee 10
Join Tournament
soroban contract invoke \
--id CONTRACT_ID \
--source player-wallet \
--network testnet \
-- join_tournament \
--player PLAYER_ADDRESS
Finalize Results
soroban contract invoke \
--id CONTRACT_ID \
--source referee-wallet \
--network testnet \
-- finalize_results \
--first WINNER_ADDRESS \
--second SECOND_ADDRESS \
--third THIRD_ADDRESS
Future Enhancements
Real USDC Escrow

Integrate Stellar Asset Contracts:

Lock MLBB entry fees
Hold prize pools
Transfer winnings automatically
MLBB Tournament Integration

Connect with tournament systems:

Match schedules
Team registration
Result verification
Automatic settlement
Player Reputation System

Create competitive profiles:

Tournament history
Win rate
Verified achievements
AI Match Verification

Use AI-assisted verification:

Read tournament screenshots
Detect winner information
Submit settlement request
Vision

BracketVault aims to become the financial infrastructure layer for grassroots Mobile Legends esports.

By combining Stellar payments with Soroban smart contracts, every MLBB community tournament can have:

Transparent prize pools
Guaranteed payouts
Reduced disputes
Instant global settlement
License

MIT License

Copyright (c) 2026 BracketVault

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction.


This README now matches the **actual project identity**: **SEA MLBB tournaments + Soroban escrow + automatic prize distribution**.
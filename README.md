# Airdrop Research Skill

Research crypto airdrops (testnet, instant, event, FCFS, and whitelist airdrops) for Binance Agent ID wallets across all networks — Ethereum, BSC, Base, Arbitrum, Polygon, Optimism, Avalanche, Hyperliquid, Robinhood Chain, Elysium, Solana, and more: find candidates from radar and community sources, audit each one against the safe-and-free gate, and report only what passes. Never auto-claims or auto-mints.

## What it does

- **Finds candidates** from MintRadar, Alphapedia, and the Alpha Board airdrop topic, plus official testnet sources (docs, faucet, explorer), chain explorers, and X (see `x-research-prompt.md`).
- **Sorts by type**: testnet, instant, event, FCFS, and whitelist airdrops, each with its own deadline and urgency.
- **Audits every candidate** against the safe-and-free gate on its own network: verified source (Sourcify exact_match for EVM, Solscan verification for Solana), no flags, on-chain free-lane check, value-0 simulation, and a clean contract-call preview.
- **Reports only what passes**, and asks for an explicit yes by name before any mint or claim.

## Install

```bash
git clone https://github.com/Rainryu1/airdrop-research-skill ~/workspace/custom-skills/airdrop-research
```

Then search for `airdrop research` in your agent skill list.

## Requirements

- A companion `safe_free_mint_gate` skill for the final gate check (referenced by path in `SKILL.md`, also published at https://github.com/Rainryu1/safe-free-mint-gate-skill).
- Public RPC access for the chain being checked, for on-chain reads and simulations.
- `baw` CLI (Binance Agentic Wallet) for contract-call previews.

## Rules the skill enforces

- Free only: never spend capital, gas is the only cost.
- Notify only: never auto-claim or auto-mint.
- Verify the full contract address character by character; never mint from a truncated address.
- Testnet programs must never ask for a mainnet deposit, a spending approval, or a seed phrase.

## License

MIT

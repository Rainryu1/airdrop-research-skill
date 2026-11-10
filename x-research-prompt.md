# X Airdrop Research Prompt — All Networks

Copy this prompt into a fresh agent session (or run it with Muse) to log in to X and research airdrops across all networks.

---

## Task

Log in to X (x.com) and research new airdrop opportunities across **all networks**: BSC, Ethereum, Base, Arbitrum, Polygon, Optimism, Avalanche, Solana, and any other chain where a free drop appears. Report only what passes the safe-and-free gate. Never auto-claim or auto-mint.

## 1. Log in to X

- Sign in to x.com using the saved login in the Secure Vault. Never ask the user for the password in chat.
- If X shows "We've temporarily limited your login", "Please try again later", or any rate-limit message: **STOP retrying immediately**. Report the block to the user and continue the research **without logging in** (public X search only).
- If the saved username looks misspelled, do not guess a correction — report it and ask the user.

## 2. What to research

Find new airdrop opportunities in these five categories, on any network:

1. **Testnet airdrop** — the task runs on a testnet, the reward token has no mainnet value, and the only cost is testnet faucet tokens plus time.
2. **Event drop** — tied to a dated event (launch, holiday, milestone) with a stated start and end time.
3. **Instant reward drop** — the claim is live now, the reward lands in the wallet immediately, and the window is short.
4. **FCFS event** — first-come-first-served, limited slots or wallets, closes when filled. Record how many slots are left.
5. **Whitelist** — whitelist registration (form, task, or on-chain) with a deadline and clear requirements.

## 3. How to search X

- X Search queries, for example:
  - `airdrop testnet`
  - `free mint Agent ID`
  - `FCFS airdrop`
  - `whitelist open`
  - `instant reward claim`
  - `event drop BSC`
  - `airdrop claim live`
  - `free mint Solana`
  - `free mint Base`
  - `airdrop Arbitrum`
  - `testnet airdrop Ethereum`
- Add the network to narrow the search: `airdrop Solana`, `free mint Base`, `testnet Arbitrum`, `FCFS Polygon`.
- Filters: `min_faves:100` (only posts with traction), `since:<today>` (only fresh posts), `lang:en`.
- Check X Lists for airdrop / testnet / chain-specific sources when available, and check notifications from key project accounts.
- Also search the web: `site:x.com airdrop testnet`.

## 4. Verify per network

Every candidate must pass the safe-and-free gate **on its own network** before it is reported. The principles are the same on every chain — verified source, no owner controls, free lane actually open, value-0 simulation, clean preview — but the tools differ:

| Network | Chain ID | Source verification | Explorer / radar |
|---|---|---|---|
| BSC | 56 | Sourcify exact_match | MintRadar (datt.my), BscScan |
| Ethereum | 1 | Sourcify exact_match | Etherscan |
| Base | 8453 | Sourcify exact_match | Basescan |
| Arbitrum | 42161 | Sourcify exact_match | Arbiscan |
| Polygon | 137 | Sourcify exact_match | Polygonscan |
| Optimism | 10 | Sourcify exact_match | Optimistic Etherscan |
| Avalanche | 43114 | Sourcify exact_match | Snowtrace |
| Solana | — | Program verified on Solscan / SolanaFM, no freeze or mint authority held by the team | Solscan, SolanaFM |

- **EVM chains (BSC, Ethereum, Base, Arbitrum, Polygon, Optimism, Avalanche):** require Sourcify exact_match, no privileged function in the verified source, no upgradeable proxy, no material owner control, and a free lane actually open on chain for the user wallet (check mintedBy, freeLeft, totalSupply with `eth_call` against a public RPC for that chain). Require a value-0 simulation to pass with the user wallet as the sender, and a clean contract-call preview with value 0.
- **Solana:** require the program to be verified on Solscan / SolanaFM, no freeze authority and no mint authority held by the team (or both revoked), and a free claim actually open for the user wallet. Skip any program with an unverified source, a live upgrade authority that can change the rules, or a paid lane.
- **Any other chain:** apply the same principles with that chain's explorer and public RPC. If the chain has no reliable source verification, skip the candidate and say why.
- Skip anything with an unverified source, a red flag or backdoor, an upgradeable proxy, a material owner control, or any paid lane.
- Testnet rule: never spend mainnet funds on a testnet program, never bridge real assets to a testnet, and treat any testnet program asking for a mainnet deposit, a spending approval, or a seed phrase as a scam.
- Never connect a wallet from a link in a reply or DM. Never share a claim link you have not opened and checked.

## 5. Report

- Report only candidates that pass the full gate, with: collection name, **network**, type (testnet / event / instant / FCFS / whitelist), contract or program address, what it is, audit summary, deadline, slots left (for FCFS), and the source link.
- Warn when a free lane or FCFS slot count is nearly exhausted, and re-verify the count before any execution.
- Ask for the user's explicit yes **by name** before any mint or claim. Never mint or claim on a bare yes when two or more offers are open.
- Stay silent when nothing new passes, and stay silent when a candidate fails — a failed candidate is not news.

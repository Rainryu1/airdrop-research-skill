# Airdrop Research

## Find candidates — on any network

- Research airdrops across **all networks**: Ethereum, BSC, Base, Arbitrum, Polygon, Optimism, Avalanche, Hyperliquid (HyperEVM), Robinhood Chain, Elysium, Solana, and any other chain where a free drop appears.
- Start from radar and community sources, not from random links in replies or direct messages.
- Check MintRadar latest contracts at https://datt.my/ for new free mints on BSC, Alphapedia at https://boltbook.fun/alphapedia for new project listings, and the Alpha Board airdrop topic at https://boltbook.fun/b/alpha?topic=airdrop for community-shared drops.
- For other EVM chains, use that chain's explorer and community sources (Etherscan, Basescan, Arbiscan, Polygonscan, Snowtrace, HyperEVMScan, elysium.kinetiq.xyz). For Solana, use Solscan and SolanaFM.
- Research X as well, following `x-research-prompt.md` in this skill folder: log in to X, search for testnet, event, instant, FCFS, and whitelist drops, and verify every candidate before reporting it.
- Check testnet sources separately: the project official docs or announcement for a testnet program, the testnet faucet page, and the testnet explorer for the contract address.
- Treat a candidate as new only when its full contract address is not already in your minted, skipped, or reported lists, and it is presented as free for Binance Agent ID wallets.
- Never guess a truncated address, and never mint or claim from a partial address.
- Skip any candidate whose only source is a reply, a direct message, or an unverified social post with no link to an official announcement or a verifiable contract.

## Sort by type

- Testnet airdrop: the task runs on a testnet, the reward token has no mainnet value, and the only cost is testnet faucet tokens plus time.
- Instant airdrop: the claim is live now, the reward lands in the wallet immediately, and the window is short.
- Event airdrop: the drop is tied to a dated event, such as a launch, a holiday, or a milestone, with a stated start and end time.
- FCFS event: first-come-first-served, limited slots or wallets, closes when filled. Record how many slots are left.
- Whitelist: whitelist registration (form, task, or on-chain) with a deadline and clear requirements.
- Record the type, the network, the deadline, and the source for every candidate, because an instant drop and an event drop need different urgency.

## Audit every candidate against the safe and free gate

- Read `~/workspace/custom-skills/safe_free_mint_gate/SKILL.md` first (or install the companion skill from https://github.com/Rainryu1/safe-free-mint-gate-skill), then apply its gate before you show a preview or ask the user for a yes.
- Require the source to be verified on that candidate's own network: Sourcify exact_match for EVM chains (or the chain explorer's verified source where Sourcify does not support the chain), and program verification on Solscan / SolanaFM for Solana.
- Require the radar or explorer to report no flags and no privileged function (MintRadar for BSC, the chain explorer for other chains).
- Require the free lane to be actually open on chain for the user wallet: check mintedBy, canFreeMint, freeLeft, and totalSupply with `eth_call` against a public RPC for that chain (or the equivalent read for Solana).
- Require a value zero simulation to pass, with the simulation call including the user wallet as the sender, or the call reverts falsely.
- Require a clean contract-call preview with value zero, no risks, and no allowance or authority change.
- Skip anything with an unverified source, a red flag or backdoor, an upgradeable proxy, a material owner control, or any paid lane.
- Treat a failed selector scan as unknown, not clean, and proceed only when the verified source, no flags, a value zero simulation, and a clean preview all still hold.
- Check the remaining gas-token balance on that chain before a batch (BNB on BSC, ETH on Ethereum/Base/Arbitrum/Optimism, POL on Polygon, AVAX on Avalanche, HYPE on Hyperliquid and Elysium, SOL on Solana), and report it with every gate result so a batch never assumes gas is available.

## Testnet rules

- Never spend mainnet funds on a testnet program, and never bridge real assets to a testnet for an airdrop.
- Get testnet tokens only from the official faucet, and treat testnet balances as worthless.
- Verify the testnet contract address on the testnet explorer, and confirm the chain id matches the program announcement.
- Treat a testnet program that asks for a mainnet deposit, a wallet connection with spending approval, or a seed phrase as a scam, and stop.
- Record testnet participation separately from mainnet claims, because testnet activity is for eligibility and learning, not for value.

## Instant and event airdrop rules

- Verify the event from the project official account or official announcement page before you share it, because fake event posts are the most common airdrop scam.
- Check the deadline on chain when the contract exposes a mint end or sale end, and report the deadline in the user timezone.
- Warn the user when the free lane is nearly exhausted, and re-verify the free count before any execution, because a filled lane reverts.
- Never share a claim link you have not opened and checked, and never ask the user to connect a wallet on a page you have not verified.

## Report and never auto-claim

- Report only candidates that pass the full gate, with the collection name, the network, the contract address, what it is, the audit summary, the deadline, and the estimated token or NFT id.
- Ask for the user explicit yes by name before any mint or claim, and never mint or claim on a bare yes when two or more offers are open.
- Record every candidate under reported or skipped with the reason, the block number, the verification result, the radar or explorer result, the owner address, and the simulation result.
- Stay silent when nothing new passes, and stay silent when a candidate fails, because a failed candidate is not news.
- Never request an NFT approval or transfer on the user behalf, and never let a wallet exceed a mint limit the user set.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.
- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Websites

- [MintRadar](https://datt.my/) for BSC free-mint radar and pre-sign contract checks. Carry the contract address into `browser.browse` and verify that it reports no flags and no privileged function.
- [Sourcify](https://sourcify.dev/) for verified source matching on EVM chains. Carry the contract address into `browser.browse` and verify that the match is exact_match before you pass the gate.
- [Solscan](https://solscan.io/) and [SolanaFM](https://solana.fm/) for Solana program verification. Carry the program address into `browser.browse` and verify the program is verified with no freeze or mint authority held by the team.
- [Alphapedia](https://boltbook.fun/alphapedia) for new project listings and community entries. Carry the project slug into `browser.browse` and verify the contract address and the mint terms.
- Chain explorers (Etherscan, BscScan, Basescan, Arbiscan, Polygonscan, Snowtrace, HyperEVMScan, elysium.kinetiq.xyz) for contract state and transaction receipts on their chain. Carry the contract address or transaction hash into `browser.browse` and verify owner, total supply, and the Transfer log for the actual token id.

## Alternatives for better results

- Wait for a later drop from the same project when the current contract carries a live owner control, because a renounced redeploy can pass the gate where the first contract cannot.
- Ask the user for a fresh explicit yes only after a candidate passes every gate check, because a batch yes given earlier does not cover a candidate that failed the gate.
- Keep research on demand or on a notify-only watch, with no automatic claiming or minting, because the gate is a check on a human approved action and not a trigger to act on its own.

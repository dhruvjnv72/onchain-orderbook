# Onchain Orderbook

A minimal limit order book that matches orders entirely on-chain, with no off-chain matching engine, written in Solidity and tested with Foundry. Built to study the cost of on-chain matching on a fast chain such as Monad.

**Status: in progress, started October 2026. Design stage.** No contract is deployed. This is an educational prototype.

> **Do not use this with real funds.** It is unaudited and will stay that way.

## Scope of the first version

One trading pair, two ERC-20 tokens (base and quote).

- `placeLimit(side, price, size)`: place a limit order that matches against the opposite side first, then rests.
- `cancel(orderId)`: cancel and refund.
- Price-time priority: best price first; at the same price, the oldest order first.
- Price levels kept in a structure that allows finding the best price without scanning every order (design to be decided and documented).
- Escrowed balances, so a matched trade settles in the same transaction.

Out of scope for now: market orders, fees, partial-fill callbacks, upgradeability, a frontend.

## Questions this project tries to answer

- How much gas does one match cost, and how does it grow with the number of orders crossed?
- Where is the practical limit: how many resting orders can one transaction match?

## Milestones

- [ ] Design note: data structures and why
- [ ] Foundry project, ERC-20 test tokens
- [ ] Place and cancel with escrow
- [ ] Matching with price-time priority
- [ ] Unit tests and fuzz tests (balances conserved, no order matched twice, ordering respected)
- [ ] Gas report for 1, 10 and 50 crossed orders
- [ ] Deploy to Monad Testnet and record the transactions

## Honest limits

- Unaudited prototype; not for real funds.
- One pair, no fees.
- Gas numbers will be measured on a local test and on testnet, not on mainnet.

## License

MIT, see [LICENSE](LICENSE).

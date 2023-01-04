# Reserve Protocol contest details

- Total Prize Pool: $210,500 USDC
  - HM awards: $127,500 USDC
  - QA report awards: $15,000 USDC
  - Gas report awards: $7,500 USDC
  - Judge + presort awards: $30,000
  - Scout awards: $500 USDC
  - Mitigation review contest: $30,000 USDC
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-01-reserve-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts January 06, 2022 20:00 UTC
- Ends January 20, 2022 20:00 UTC

## C4udit / Publicly Known Issues

The C4audit output for the contest can be found [here](add link to report) within an hour of contest opening.

_Note for C4 wardens: Anything included in the C4udit output is considered a publicly known issue and is ineligible for awards._

Items listed below aren't necessarily issues but rather just describe some protocol specific behavior that we are aware of.

- StRSR is slightly reflexive, and in case of large percentage of collateral defaults, it may not be able to cover as much as expected.
- The governance has the ability to freeze, and with long freezing enabled (default) it is possible for governance to soft-lock the backing for the duration of the freezing period by preventing the RToken holders from redeeming. The idea is to turn off freezing capabilities couple months into RToken existence.
- The individual asset plugins, and hance the protocol itself, relies heavily on Oracles for accurate price determination.

Additionally, anything mentioned in the previous audits is considered known issues:

- [Trail of Bits - August 11th, 2022](/audits/Trail%20of%20Bits%20-%20Aug%2011%202022.pdf)
- [Ackee - October 7th, 2022](/audits/Ackee%20-%20Oct%2007%202022.pdf)
- [Solidified - October 16th, 2022](/audits/Solidified%20-%20Oct%2016%202022.pdf)
- [Halborn Security - November 15th, 2022](/audits/Halborn%20Security%20-%20Nov%2015%202022.pdf)

# Overview

The Reserve Protocol allows anyone to create stablecoins backed by baskets of ERC20 tokens on Ethereum. Stable asset backed currencies launched on the Reserve protocol are called “RTokens”.

Once an RToken configuration has been deployed, RTokens can be minted by depositing the entire basket of collateral backing tokens, and redeemed for the entire basket as well. Thus, an RToken will tend to trade at the market value of the entire basket that backs it, as any lower or higher price could be arbitraged.

RTokens can be overcollateralized, which means that if any of their collateral tokens default, there's a pool of value available to make up for the loss. RToken overcollateralization is provided by Reserve Rights (RSR) holders, who may choose to stake their RSR on any RToken. Staked RSR can be seized in the case of a collateral default, in a process that is entirely mechanistic based on on-chain price-feeds, and does not depend on any governance votes or human choices.

RTokens can generate revenue, and this revenue is the incentive for RSR holders to stake. Revenue can come from yield from lending collateral tokens on-chain or revenue shares with collateral token issuers. Governance can direct any portion of revenue to RSR stakers, to incentivize RSR holders to stake and provide overcollateralization. If an RToken generates no revenue, or if none of it is directed to RSR stakers, it probably won't have any RSR staked on it, and thus won't be protected by overcollateralization.

[Introduction Video](https://www.youtube.com/watch?v=JOy0wCVhnwM)

The `protocol` folder in this repo is linked to the primary Reserve Protocol public repo at commit hash `d224c14c398d2727d39d133aa7511e1e6b161833`.

# Scope

The base directory is assumed to be `protocol` relative to the root of this repo.

The following directories and implementations are considered in-scope for this audit.

| Contract                  | Purpose                           |
| ------------------------- | --------------------------------- |
| contracts/p1/\*\*         | P1 Implementation of the Protocol |
| contracts/libraries/\*\*  | Libraries used in the Protocol    |
| contracts/interfaces/\*\* | Interfaces used in the Protocol   |
| contracts/mixins/\*\*     | Mixins used in the Protocol       |
| contracts/p1/mixins/\*\*  | Mixins used in the Protocol       |
| contracts/plugins/\*\*    | Plugins used in the Protocol      |

For the P1 Implementation, here's a brief description of each file.

| Contract           | SLOC | Purpose                                                   | Libraries used    |
| ------------------ | ---- | --------------------------------------------------------- | ----------------- |
| AssetRegistry.sol  | 93   | Asset Registry                                            | `@openzeppelin/*` |
| BackingManager.sol | 138  | Backing Manager                                           | `@openzeppelin/*` |
| BasketHandler.sol  | 351  | Basket Handler                                            | `@openzeppelin/*` |
| Broker.sol         | 87   | Broker                                                    | `@openzeppelin/*` |
| Deployer.sol       | 177  | Deployer                                                  | `@openzeppelin/*` |
| Distributor.sol    | 110  | Distributor                                               | `@openzeppelin/*` |
| Furnace.sol        | 46   | Furnace                                                   | `@openzeppelin/*` |
| Main.sol           | 42   | Main                                                      | `@openzeppelin/*` |
| RevenueTrader.sol  | 60   | Revenue Trader (used for both RSR Trader & RToken Trader) | `@openzeppelin/*` |
| RToken.sol         | 387  | RToken                                                    | `@openzeppelin/*` |
| StRSR.sol          | 398  | StRSR                                                     | `@openzeppelin/*` |
| StRSRVotes.sol     | 162  | StRSRVotes                                                | `@openzeppelin/*` |

## Out of scope

The following directories and implementations are considered out-of-scope for this audit.

| Contract              | Purpose                              |
| --------------------- | ------------------------------------ |
| contracts/facade/\*\* | Periphery Contracts for the Protocol |
| contracts/p0/\*\*     | P0 Implementation of the Protocol    |

# Additional Context

We do have some very specific Recollateralization Logic described in the `docs/recollateralization.md` file, you can also find other documentation in the same folder. There's additional information available in the primary `README.md` file as well. Here's a [video walkthrough](https://www.youtube.com/watch?v=341MhkOWsJE) of the code which provides additional context around specific files, structure and logic.

Additionally, we also recommend going through the following documents in order to understand the protocol better.

- `docs/system-design.md`
- `docs/collateral.md`
- `docs/Token Flow.png`
- `docs/solidity-style.md`
  - Especially the section on `Fixed.sol` which describes our `uint192` based fixed-point decimal value.

## Scoping Details

```
- If you have a public code repo, please share it here:  https://github.com/reserve-protocol/protocol
- How many contracts are in scope?:   77
- Total SLoC for these contracts?:  5460
- How many external imports are there?: 35
- How many separate interfaces and struct definitions are there for the contracts within scope?:  27 structs, 42 interfaces
- Does most of your code generally use composition or inheritance?: The main structure of the protocol is divided up with contract composition, though inheritance is used basically everywhere, in moderation.
- How many external calls?:  12
- What is the overall line coverage percentage provided by your tests?:  95
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?:  false
- Please describe required context:
- Does it use an oracle?:  true; Specific Asset and Collalteral plugins use oracles heavily; the main body of the protocol treats that as an implementation detail. Built-in assets use Chainlink oracles; other assets (if they’re canonical by the time this review is happening) are likely to use other oracles.
- Does the token conform to the ERC20 standard?:  The present tokens are ERC20s, yes.
- Are there any novel or unique curve logic or mathematical models?: Not precisely what you’re asking, but it’ll be important to understand: 1) Basically everything in https://github.com/reserve-protocol/protocol/blob/master/docs/solidity-style.md, some of which is unique to us 2) Our system of Collateral units, described here: https://github.com/reserve-protocol/protocol/blob/master/docs/collateral.md#accounting-units-and-exchange-rates
- Does it use a timelock function?:  No
- Is it an NFT?: No
- Does it have an AMM?:   No, though it does allow the permissionless launching of Gnosis EasyAuctions
- Is it a fork of a popular project?:   false
- Does it use rollups?:   false
- Is it multi-chain?:  false
- Does it use a side-chain?: false
```

# Tests

Detailed steps to run tests against the protocol are available here in the `docs/dev-env.md` document. If you plan on directly cloning this repo, we'd recommend cloning with the following command and running all `yarn` commands in the `protocol` directory.

```
git clone --recurse-submodules https://github.com/code-423n4/2023-01-reserve.git
```

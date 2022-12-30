# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos:

- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted (shared with you after the contest)

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest report is published and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

# Repo setup

## ⭐️ Sponsor: Add code to this repo

- [ ] Create a PR to this repo with the below changes:
- [ ] Provide a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 24 hours prior to contest start time.**
- [ ] Be prepared for a 🚨code freeze🚨 for the duration of the contest — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the contest. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)

---

## ⭐️ Sponsor: Edit this README

Under "SPONSORS ADD INFO HERE" heading below, include the following:

- [ ] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2022-08-foundation#readme))
  - [ ] When linking, please provide all links as full absolute links versus relative links
  - [ ] All information should be provided in markdown format (HTML does not render on Code4rena.com)
- [ ] Under the "Scope" heading, provide the name of each contract and:
  - [ ] source lines of code (excluding blank lines and comments) in each
  - [ ] external contracts called in each
  - [ ] libraries used in each
- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [ ] Describe anything else that adds any special logic that makes your approach unique
- [ ] Identify any areas of specific concern in reviewing the code
- [ ] Optional / nice to have: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Reserve Protocol contest details

- Total Prize Pool: $230,500 USDC
  - HM awards: $127,500 USDC
  - QA report awards: $15,000 USDC
  - Gas report awards: $7,500 USDC
  - Judge + presort awards: $30,000
  - Scout awards: $500 USDC
  - Mitigation review contest: $50,000 USDC
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-01-reserve-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts January 06, 2022 20:00 UTC
- Ends January 20, 2022 20:00 UTC

## C4udit / Publicly Known Issues

The C4audit output for the contest can be found [here](add link to report) within an hour of contest opening.

_Note for C4 wardens: Anything included in the C4udit output is considered a publicly known issue and is ineligible for awards._

[ ⭐️ SPONSORS ADD INFO HERE ]

# Overview

_Please provide some context about the code being audited, and identify any areas of specific concern in reviewing the code. (This is a good place to link to your docs, if you have them.)_

TODO

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
| AssetRegistry.sol  | TODO | Asset Registry                                            | `@openzeppelin/*` |
| BackingManager.sol | TODO | Backing Manager                                           | `@openzeppelin/*` |
| BasketHandler.sol  | TODO | Basket Handler                                            | `@openzeppelin/*` |
| Broker.sol         | TODO | Broker                                                    | `@openzeppelin/*` |
| Deployer.sol       | TODO | Deployer                                                  | `@openzeppelin/*` |
| Distributor.sol    | TODO | Distributor                                               | `@openzeppelin/*` |
| Furnace.sol        | TODO | Furnace                                                   | `@openzeppelin/*` |
| Main.sol           | TODO | Main                                                      | `@openzeppelin/*` |
| RevenueTrader.sol  | TODO | Revenue Trader (used for both RSR Trader & RToken Trader) | `@openzeppelin/*` |
| RToken.sol         | TODO | RToken                                                    | `@openzeppelin/*` |
| StRSR.sol          | TODO | StRSR                                                     | `@openzeppelin/*` |
| StRSRVotes.sol     | TODO | StRSRVotes                                                | `@openzeppelin/*` |

## Out of scope

The following directories and implementations are considered out-of-scope for this audit.

| Contract              | Purpose                              |
| --------------------- | ------------------------------------ |
| contracts/facade/\*\* | Periphery Contracts for the Protocol |
| contracts/p0/\*\*     | P0 Implementation of the Protocol    |

# Additional Context

We do have some very specific Recollateralization Logic described in the `docs/recollateralization.md` file, you can also find other documentation in the same folder. There's additional information available in the primary `README.md` file as well. Here's a [video walkthrough](https://www.youtube.com/watch?v=341MhkOWsJE) of the code which provides additional context around specific files, structure and logic..

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

The `protocol` folder in this repo is linked to the primary Reserve Protocol repo at commit hash `d224c14c398d2727d39d133aa7511e1e6b161833`.

---
aip: 3
title: Transferring ownership of deployed factory contracts to a multi-sig wallet
status: Draft
type: Core
author: Jason Romero <jason@gitcoin.co> Daniele Salatti <daniele@gitcoin.co>
created: 2023-04-03
---

## Abstract

This AIP proposes to transfer ownership of the deployed factory contracts to a multi-sig wallet.

## Motivation

- We encountered an issue during development and cannot create rounds on new program deployments due to an address
  that is 0x and should be set to the implementation address of the deployed factory contract. We need to be able to
  call updateRoundImplementation to set the address to the correct implementation address if not done so already.

### Goals

- The ability for more than just the deployer wallet the ability to make changes to the deployed factory contracts
- Removes the single point of failure of the deployer wallet

### Specification

Contracts that will have the ownership transferred to a multi-sig wallet:

- ProgramFactory
- RoundFacory
- AlloSettings
- QuadraticFundingVotingStrategyFactory

### Rationale

1. Securtiy: if the deployer wallet address is comprimised
2. Updates/Changes: only the deployer wallet can make changes currently and could be a bottleneck/blocker for changes

## Copyright

TODO

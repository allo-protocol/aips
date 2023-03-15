---
aip: 3
title: Allo Settings Contract
status: Draft
type: Core
author: Aditya Anand <aditya@gitcoin.co>, Andrea Franz <andrea@gitcoin.co>, Kurt Merbeth <kurt@gitcoin.co>
created: 2023-03-15
---

## Abstract

This AIP proposes
- adding a `AlloSettings` contract that allows us to store the `protocolFeePercentage` and `protocolTreasuryAddress`
- allowing the `Round` contract to rely on this new `AlloSettings` contract to know how much fee and where it should be sent to during payout

## Motivation

The current implementation of the fee is stored on `RoundFactory` which seems to add additional responsibility to the factory who's sole responsibility should be just to 

As a result, we want to improve the current implementation to enable consistent
and reliable storage and retrieval of all the applications and their statuses.

### Goals

- Deploy a new `AlloSettings` contract to store global settings / config 
- Move `protocolFeePercentage` from `RoundFactory` to `AlloSettings`
- Move `protocolFee` from `RoundFactory` to `AlloSettings`
- Update `RoundFactory` and `RoundImplementation` to rely on `AlloSettings` contract 


### Other Goals

Having the settings contract allows us to explore ideas like 

- Allowing DAO to hold ownership right to `AlloSettings` contract
- Enable DAO to take decision on updating settings via tally 
- Keeps factory contracts cleaner  

## Specification


```
contract AlloSettings is OwnableUpgradeable {
    string public constant VERSION = "1.0.0";

    // --- Data ---

    /// @notice Address of the protocol treasury
    address payable public protocolTreasury;

    /// @notice Protocol fee percentage
    uint8 public protocolFeePercentage;

    // --- Event ---

    /// @notice Emitted when protocol fee percentage is updated
    event ProtocolFeePercentageUpdated(uint8 protocolFeePercentage);

    /// @notice Emitted when a protocol wallet address is updated
    event ProtocolTreasuryUpdated(address protocolTreasuryAddress);
}
```

Update the `RoundFactory` to store a reference to the `AlloSettings` and that gets passed onto the `RoundImplementation` contract which can reference the settings contract to get settings variable

```
// --- Data ---

/// @notice Address of the Allo settings contract
address public alloSettings;

// --- Event ---

/// @notice Emitted when allo settings contract is updated
event AlloSettingsUpdated(address alloSettings);

```

### Proof of concepts and possible implementations:

We have explored few possibilities on how AlloSettings could be implemented 

- https://github.com/allo-protocol/contracts/blob/58f856167afb8bb2fc2cf26f489d51c39c430447/contracts/settings/AlloSettings.sol
- https://github.com/compound-finance/compound-protocol/blob/master/contracts/ComptrollerStorage.sol
- https://fravoll.github.io/solidity-patterns/eternal_storage.html

While eternal storage seems to be the smartest way to go about it. It does affect readability and for the sake of simplicity 
We are proposing going with a naive approach and then upgrade as we see fit

## Rationale

Overall, the proposed modifications aim to produce a global settings file which can be used to store global variables like approved voting strategies / payout strategies / anything which the DAO might be be able to vote on take a decision.
By storing this data in an isolated contract, we avoid polluting the factory contracts 

Here is a POC of the proposed changes: https://github.com/allo-protocol/contracts/pull/2
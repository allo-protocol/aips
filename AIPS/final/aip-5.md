---
aip: 5
title: Match Votes and msg.value
status: Final
type: Core
author: Kurt Merbeth <kurt@gitcoin.co>
created: 2023-04-06
---


## Abstract

This AIP proposes a change in the `QuadraticFundingVotingStrategyImplementation` contract.
The function `vote()` does not validate whether the native token sent matches the amount in encodedVotes, potentially leading to lost funds or theft by malicious users. 

The issue is discussed in detail in the Sherlock audit issue [005-M](https://github.com/sherlock-audit/2023-03-Gitcoin-judging/tree/main/005-M). 
The proposed solution is to add a check for msg.value in the vote function.

## Motivation

The current implementation of the `QuadraticFundingVotingStrategyImplementation` contract does not perform a check to ensure that the `msg.value` sent in the `vote` function is equal to the total amount specified in the `encodedVotes`. 
This can lead to security vulnerabilities, where users lose their surplus native tokens, and malicious actors can exploit the contract to steal native tokens. To ensure the security of the contract, we propose adding additional validation to the `vote` function to prevent these issues from occurring.


### Goals

- To improve the security of the `QuadraticFundingVotingStrategyImplementation` contract by adding a check to ensure that the `msg.value` equals the total amount specified in the `encodedVotes`.
- To prevent users from losing their surplus native tokens and grant addresses from receiving less than what they sent.
- To prevent malicious users from exploiting the contract to steal native tokens.

## Specification

To achieve the above goals, we propose modifying the `QuadraticFundingVotingStrategyImplementation::vote()` function as follows:

Add a variable `msgValue` to keep track of the total native tokens sent in the vote function.

```solidity
uint256 msgValue = 0;
```

Increment `msgValue` with the `_amount` when the token is a native token.

```solidity
if (_token == address(0)) {
    msgValue += _amount;
    AddressUpgradeable.sendValue(payable(_grantAddress), _amount);
  } else {
   ...
  }
```

Add a check at the end of the function to ensure that the `msgValue` equals the `msg.value` sent in the vote function.
If `msgValue` does not equal `msg.value`, revert the transaction.

```solidity
require(msgValue == msg.value, "msg.value does not match vote amount");
```


## Rationale

The proposed modification adds an additional validation step to the vote function, which ensures that the `msg.value` sent in the vote function matches the total amount specified in the `encodedVotes`. This modification prevents users from losing their surplus native tokens and grant addresses from receiving less than what they sent. Additionally, this modification prevents malicious users from exploiting the contract to steal native tokens.

In conclusion, we believe that the proposed modification will significantly improve the security of the `QuadraticFundingVotingStrategyImplementation` contract and prevent potential security vulnerabilities.

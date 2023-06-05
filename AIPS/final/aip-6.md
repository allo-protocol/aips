---
aip: 6
title: Using Multicall to Update All Round Data
status: Final
type: Core
author: Gitcoin Grants Stack
created: 2023-05-04
---


## Abstract

The RoundImplementation contract requires an efficient and easy way to update all data on Round. This proposal suggests using the `multicall` function from the `MulticallUpgradeable` library in the `@openzeppelin/contracts-upgradeable/utils` package to achieve this goal.

## Motivation

Currently, updating all data on Round requires calling each function individually, which is time-consuming and expensive. Using the `multicall` function to update all data with a single function call will simplify the process, improving the user experience.

### Goals

The goals of this proposal are as follows:

- To improve the usability of the RoundImplementation contract
- To simplify the process of updating all data on Round
- To enhance the user experience
- To save money

## Specification

To implement this proposal, we will:

- Import the `MulticallUpgradeable` library from the `@openzeppelin/contracts-upgradeable/utils` package in `RoundImplementation.sol`.


## Usage 

- Encode the function calls for each data update using the contract's interface.
- Pass the encoded function calls as an array to the `multicall` function.

```JavaScript
const updateApplicationMetaPtr = roundImplementation.interface.encodeFunctionData(
  "updateApplicationMetaPtr",
  [newApplicationMetapointer]
);

const updateRoundMetaPtr = roundImplementation.interface.encodeFunctionData(
  "updateRoundMetaPtr",
  [newRoundMetapointer]
);

const tx = await roundImplementation.multicall([
  updateApplicationMetaPtr,
  updateRoundMetaPtr,
]);
```

## References

- PR: https://github.com/allo-protocol/allo-contracts/pull/29

## Rationale

The `multicall` function is a powerful tool that enables us to execute multiple function calls in a single transaction. By using `multicall` to update all Round data, we can simplify and optimize the process, reducing the number of function calls required and saving time and gas costs. Additionally, the use of `MulticallUpgradeable` library from OpenZeppelin ensures the function is secure and reliable.

OpenZeppelin's `MulticallUpgradeable` library is a collection of functions that allows us to execute multiple calls in a single transaction, saving gas costs and improving efficiency. The library also handles the return values of each call, making it easier to process and interpret the results.

## Copyright

Copyright and related rights found in [LICENSE](./LICENSE).
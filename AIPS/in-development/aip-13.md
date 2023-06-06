
---
aip: 13
title: Enhancing Vote Traceability
status: In Development
type: Core
author: Hans <hans@gitcoin.co>
created: 2023-06-06
---

## Abstract

The proposed enhancement focuses on improving the traceability of our voting system for batched checkout within the scope of a future enhancement, with the implementation of a new Multi-checkout contract. The challenge lies in tracing the originating account when multi-round checkout contract invocations occur. Currently, invoking the `Round.vote` through a Multi-checkout contract results in the `msg.sender` within `Round.vote` reflecting the Multi-checkout contract's address, rather than the EOA that initiated the transaction. To rectify this, the proposal suggests including `tx.origin` in the `Vote` event emitted by the `QuadraticFundingImplementation` contract. This adjustment will improve the traceability of the originating account, even when intermediate contracts are involved. 

## Motivation

The need to enhance traceability and accurately identify the EOA in the context of contract interactions has motivated this proposal. The current system doesn't trace back to the EOA when a Multi-checkout contract initiates a `Round.vote`, leading to potential issues in auditing and tracking of voting events. Integrating `tx.origin` in the `Vote` event ensures improved tracking of the transaction's origin, adding a layer of transparency and clarity to our voting system.

## Goals

1. **Improve Traceability**: Enhance the tracking of the EOA in transactions involving multi-round checkout contract invocations by including `tx.origin` in the `Vote` event.

2. **Upgrade Audit and Tracking Mechanisms**: By reflecting the original EOA that initiated the transaction, we aim to upgrade our system's audit and tracking capabilities, enhancing transparency and accountability.

3. **Flexible Voting System**: The changes proposed would make our voting system more flexible and robust, further ensuring its reliability and stability in the face of intermediary contracts.

## Specification

To implement the proposal, the following steps will be taken:

1. **Upgrade `QuadraticFundingImplementation` Contract**: Upgrade the `QuadraticFundingImplementation` contract's version and adjust the `Vote` event to include the `tx.origin`.

2. **Modify `Voted` Event**: Add an `origin` field in the `Voted` event representing `tx.origin`.

3. **Adjust Emission of `Voted` Event**: When emitting the `Voted` event, include `tx.origin` as the origin parameter.

4. **Testing and Validation**: Conduct thorough testing to ensure that the `origin` field accurately reflects the EOA initiating the transaction.

## Usage

The proposed change will improve the traceability within the voting system for batched checkout:

1. **Auditing and Tracking**: With `tx.origin` included in the `Vote` event, tracking the original EOA that initiated the transaction becomes straightforward, enhancing audit capabilities.

2. **Transparency**: The change enhances transparency by ensuring that the EOA is accurately reflected, irrespective of intermediary contracts involved.

**Note**: While `tx.origin` enhances traceability, it should not be used in security-critical functionality due to potential security vulnerabilities. The use of `tx.origin` should be confined to auditing or tracking purposes. 

## Implications

The implementation of this proposal will significantly enhance the traceability of our voting system. However, caution must be exercised when dealing with `tx.origin`, given potential security vulnerabilities. It's recommended that `tx.origin` is used strictly for auditing and tracking, not for security-critical operations.

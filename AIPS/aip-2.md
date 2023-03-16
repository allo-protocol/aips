---
eip: 2
title: On-chain application statuses
status: Draft
type: Core
author: Andrea Franz <andrea@gitcoin.co>, Aditya Anand <aditya@gitcoin.co>
created: 2023-03-15
---

## Abstract

This AIP propose a change in the `Round` contract that allows application status to be on-chain,
and to allow projects to apply multiple times to a round with one or multiple active applications.

## Motivation

The current implementation of the contracts lacks on-chain storage for applications and their statuses.
Instead, newly submitted applications trigger on-chain events and the corresponding list of round applications
is indexed and made available exclusively on our subgraph (or accessible from the contract's logs).
When a round operator accepts or rejecs applications,
the updated statuses are stored on IPFS, and a corresponding event is emitted with a MetaPtr pointing to the IPFS file.
However, there exists a significant issue of inconsistency between the statuses indexed in the subgraph and the ones stored on IPFS.
Most of the time, the new file is not available on the subgraph's IPFS node at the time the indexes runs,
leading to unreliable data.
As a result, we want to improve the current implementation to enable consistent
and reliable storage and retrieval of all the applications and their statuses.

### Goals

- Store applications on-chain with unique IDs and with pointers to the ipfs metadata file.
- Store all application statuses on-chain.
- Allow projects to re-apply to a round without changing the previous application and its status.

### Non-goals

- Verify that the sender of the transaction is part of the project.

By default, all applications are pending, and the round operator is responsible for approving or rejecting each one.

The metadata of each application, which is stored on IPFS, includes a signature from the user who submitted the application,
that provides an additional layer of verification to ensure the authenticity of each application.

To assist round operators in the approval process, tools like the GrantsStack Manager
can help operators to quickly and easily identify legitimate applications and skip or hide
applications sent by bad actors.

## Specification

To ensure that the list of applications is consistently accessible both on-chain and in a subgraph,
we propose the initial modification of storing the list of applications in the contract.

A possible solution is having a list of `Application` structs containing the id the project, a unique index for the application in the round,
and a pointer to the metadata on ipfs.

```
struct Application {
    bytes32 projectID;
    uint256 applicationIndex;
    MetaPtr metaPtr;
}

event NewProjectApplication(bytes32 indexed projectID, uint256 applicationIndex, MetaPtr applicationMetaPtr);

uint256 public nextApplicationIndex;

// An array of applications, each new application is appended to the array
Application[] public applications;
```

The second modification we propose is to store all application statuses in the contract.
This will enable round operators to efficiently approve or reject multiple applications in a single transaction,
regardless of whether there are a few or several thousand applications to process.

To enhance both the storage efficiency and computational performance during the process of status changes,
we suggest storing the application statuses in a bit array (or [bitmap, bit-string, etc...](https://en.wikipedia.org/wiki/Bitmap)).
By utilizing a bit array, we can achieve more compact storage, faster computational operations, and less gas usage,
while efficiently maintaining the integrity and accuracy of the data.
We can use 2 bits for each application status to express 4 different values:

* 0 - pending
* 1 - approved
* 2 - rejected
* 3 - canceled

### Proof of concepts and possible implementations:

- https://gist.github.com/gravityblast/9c286a8e83e0023621581d7e45fded65
- https://github.com/KurtMerbeth/BitMapMagic/blob/master/RoundBitMap/contracts/Round.sol

## Rationale

Overall, the proposed modifications aim to improve the efficiency, reliability, and consistency of the project's application approval process.
By storing the list of applications and their statuses in the contract, we eliminate the need for external indexing and provide
a more robust and dependable solution for accessing application data.
These changes will enable round operators to approve or reject multiple applications in a single transaction,
regardless of the number of applications involved.

## Copyright
TODO


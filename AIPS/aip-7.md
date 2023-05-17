---
aip: 7
title: Using `tx.origin` to get voter address
status: Draft
type: Core
author: Aditya Anand (@thelostone-mc), Andrea Franz (@gravityblast)
created: 2023-05-17 
---

<!--
READ AIP-1 (./AIPS/aip-1.md) BEFORE USING THIS TEMPLATE!

This is the suggested template for new AIPs. After you have filled in the
requisite fields, please delete these comments.

Note that an AIP number will be assigned by an editor. When opening a pull
request to submit your AIP, please use an abbreviated title in the filename,
`eip-draft_title_abbrev.md`.

The title should be 44 characters or less. It should not repeat the AIP number
in title, irrespective of the category.

TODO: Remove this comment before submitting
-->

## Abstract

This AIP proposes a modification to the voting mechanism in the round contract to capture the actual user's address when casting votes across multiple rounds on the chain.
Currently, the msg.sender value represents the intermediate contract instead of the original sender. 
To address this limitation, the proposed solution suggests using tx.origin to capture the true identity of the voter.
It's important to note that tx.origin will only be used for identification purposes and not for authorization.



## Motivation

The existing round contract captures the voter's address using msg.sender, which works well for single-round voting scenarios. 
However, when a contract in the middle is involved, casting votes across multiple rounds becomes problematic. 
In such cases, msg.sender refers to the intermediate contract rather than the actual sender, making it impossible to determine the original voter's identity.

To enable voting across multiple rounds on the chain, it is necessary to capture the true identity of the voter. 
By utilizing tx.origin, which represents the original sender of the transaction, we can ensure that the actual user's address is recorded accurately.



## Goals

- Enable capturing the actual user's address when casting votes across multiple rounds on the chain.
- Modify the voting mechanism in the round contract to utilize tx.origin for identifying the voter.
- Ensure that tx.origin is used solely for identification purposes and not for authorization.

## Non-goals

- Changing the existing authorization mechanism or introducing new security measures.
- Modifying other functionalities or contracts unrelated to the voting process.


## Specification

The proposed modification involves updating the existing round contract to replace the usage of msg.sender with tx.origin when capturing the voter's address.
By making this change, the contract will accurately record the identity of the actual sender regardless of any intermediate contracts involved in the voting process.

It is important to note that tx.origin should only be used for identification purposes and not for authorization or access control.
The contract should continue to rely on appropriate authorization mechanisms to validate and verify the voter's eligibility.

## Reference Implementation

The motivation behind this modification is to address the limitation of the current voting mechanism in the round contract, which fails to capture the actual user's address when an intermediate contract is involved.
By utilizing tx.origin, we can accurately identify the original sender of the transaction and overcome this limitation.

Alternatives, such as using msg.sender with additional context parameters, were considered.
However, these alternatives introduce complexity and may not be reliable in scenarios with multiple intermediate contracts. Therefore, utilizing tx.origin emerged as the most straightforward and effective solution to capture the actual voter's address.


## References

https://ethereum.stackexchange.com/questions/1891/whats-the-difference-between-msg-sender-and-tx-origin

## Copyright

[CC0](../LICENSE.md).

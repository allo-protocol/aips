---
aip: AIP-001
title: Add 'virtual' keyword to init() method in payout and voting strategy interfaces
status: Draft
type: Core
author: Zakk Fleischmann <zakk@gitcoin.co>, Aditya Anand <aditya@gitcoin.co>
created: 2023-05-26
---

## Abstract

This AIP proposes adding the 'virtual' keyword to the `init()` method of the payout strategy interface and the voting strategy interface. This change aligns the two interfaces and ensures consistency in their usage.

## Motivation

The motivation behind this proposal is to bring consistency to the payout strategy interface and the voting strategy interface. Currently, the `init()` method in the payout strategy interface does not have the 'virtual' keyword, while the same method in the voting strategy interface does. This inconsistency can lead to confusion and make it harder for developers to understand and implement these interfaces correctly. By adding the 'virtual' keyword to the `init()` method in the payout strategy interface, we align it with the voting strategy interface and establish a clear and consistent pattern.

## Goals

- Add the 'virtual' keyword to the `init()` method in the payout strategy interface.
- Align the payout strategy interface with the voting strategy interface.

## Non-goals

There are no specific non-goals for this AIP.

## Specification

The `init()` method in the payout strategy interface and the voting strategy interface should be declared as `virtual`. This change ensures that these methods can be overridden in derived classes, allowing for more flexibility in implementing custom payout and voting strategies.

The updated interface definitions should be as follows:

```solidity
interface PayoutStrategy {
    function init() external virtual;
    // ... other methods ...
}

interface VotingStrategy {
    function init() external virtual;
    // ... other methods ...
}
```

By adding the 'virtual' keyword, developers will have the option to override the `init()` method in their custom implementations of these interfaces.

## Reference Implementation

There is no reference implementation provided with this AIP.

## Rationale

The addition of the 'virtual' keyword to the `init()` method in the payout and voting strategy interfaces ensures consistency and allows for better extensibility. By making the method virtual, derived classes can override it and provide their own implementation if needed. This aligns the payout strategy interface with the voting strategy interface and establishes a clear and predictable pattern for interface usage.

## References

There are no additional references for this AIP.

## Copyright

Copyright and related rights found in [LICENSE](./LICENSE).

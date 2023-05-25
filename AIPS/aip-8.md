---
aip: 8
title: RoundImplementation: Decoupling features
status: Draft
type: Core
author: <a comma separated list of the author's or authors' name + GitHub username (in parenthesis), or name and email (in angle brackets).  Example, FirstName LastName (@GitHubUsername), FirstName LastName <foo@bar.com>, FirstName (@GitHubUsername) and GitHubUsername (@GitHubUsername)>
created: 2023-05-25
---

## Abstract

This proposal suggests improvements to the `RoundImplementation` contract by removing features such as `matchAmount`, `payoutStrategy`, `token`, `roundFeePercentage`, `updateMatchAmount`, `updateRoundFeePercentage`, `updateRoundFeeAddress`, `roundFeeAddress`, and `setReadyForPayout`. The objective is to create a more flexible and unified interface for funding rounds, allowing the creation of rounds without quadratic funding and simplifying project funding without matching requirements. This proposal also recommends integrating the payout strategy into the voting strategy and eliminating the protocol fee, resulting in a more streamlined and adaptable contract.

## Motivation

The current `RoundImplementation` contract has several features that are closely tied to quadratic voting. However, there is a need for a more basic and adaptable contract that supports rounds without quadratic funding or match amount. By removing these specific features, we can streamline the contract and enable a broader range of funding round scenarios, providing more flexibility to the users.

## Goals

- Remove `matchAmount` and token to allow rounds without quadratic funding or other matching mechanisms.
- Eliminate `payoutStrategy` to simplify the contract and integrate it into the voting strategy.
- Remove `roundFeePercentage`, `roundFeeAddress`, and related update functions, since they depend on `matchAmount`.
- Enhance flexibility by creating a unified interface for funding rounds.

## Non-goals

- This proposal does not aim to modify the existing quadratic funding functionality or impact rounds using quadratic voting.
- Removing specific features should not disrupt the core functionality of the RoundImplementation contract.
- The proposal does not include the implementation details of the voting strategy but focuses on its integration and interface with RoundImplementation.

## Specification

The proposed changes to the RoundImplementation contract include:

1. Removal of Variables and Functions:

- `matchAmount`: Remove the variable representing the amount used for matching.
- `payoutStrategy`: Eliminate the payout strategy from RoundImplementation.
- `token`: Remove the match amount token.
- `roundFeePercentage`: Eliminate the variable for the round fee percentage.
- `roundFeeAddress`: Remove the variable for the round fee address.
- `updateMatchAmount()`: Remove the function for updating the match amount.
- `updateRoundFeePercentage()`: Eliminate the function for updating the round fee percentage.
- `updateRoundFeeAddress()`: Remove the function for updating the round fee address.
- `setReadyForPayout()`: Eliminate the function for indicating readiness for payout.

2. Integration with Voting Strategy:

- Modify the voting strategy to include the `matchAmount`, `payoutStrategy`, `token`, `roundFeePercentage`, `roundFeeAddress`, and related functions.
- Provide appropriate interfaces and functions in the voting strategy to handle these features, allowing users to define their desired voting and payout strategies within the voting strategy itself.

3. Unified Interface:

- Create a new interface that allows the creation of rounds without quadratic funding and offers simplified project funding options.
- The interface should provide clear documentation and guidelines on how to define and integrate custom voting and payout strategies within the voting strategy implementation.

## Reference Implementation
wip
<!--
This section is optional.

The Reference Implementation section should include a minimal implementation
that assists in understanding or implementing this specification. It should
not include project build files. The reference implementation is not
a replacement for the Specification section, and the proposal should still be
understandable without it. If the reference implementation is too large to
reasonably be included inline, then consider adding it as one or more files in
`../assets/aip-####/`. External links will not be allowed.

TODO: Remove this comment before submitting
-->

## Rationale

By removing features tied to quadratic voting, such as `matchAmount`, `payoutStrategy`, and associated functions and variables, the `RoundImplementation` contract becomes more flexible. This allows for the creation of rounds without matching requirements, enabling a wider range of funding scenarios. Integrating the payout strategy into the voting strategy simplifies the round contract and eliminates unnecessary complexity. The proposed changes aim to create a cleaner and more flexible contract interface while preserving the core functionality of RoundImplementation.

## References
wip
<!--
This section is optional. 

If applicable, provide a list of any relevant sources and citations used
elsewhere in this AIP:

    A list of relevant links like for this proposal

    - [forum discussion](discordlink)
    - [tests](githublink)
    - [proposalCode](githublink)

TODO: Remove this comment before submitting
-->

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).

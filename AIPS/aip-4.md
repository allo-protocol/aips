---
aip: 4
title: Emit ApplicationIndex on Vote
status: Draft
type: Core
author: Aditya Anand <aditya@gitcoin.co>, Andrea Franz <andrea@gitcoin.co>, Jason Romero <jason@gitcoin.co>, Mo Boudra <mo@gitcoin.co>
created: 2023-04-06
---

## Abstract

This AIP proposes making the following changes to `QuadraticVotingStrategyImplementation`
- update `Voted` event to emit `uint256 applicationIndex` 
- update `vote()` function implementation to be able to decode the `applicationIndex` from the `encodedVote`

## Motivation

As per [AIP-2](./aip-2.md) the application status is stored moved on-chain. 
This means a project can have multiple applications being sent to a round.
Once the voting period starts within the round, it becomes unclear when a vote is sent to a project, for which applicationIndex it was sent. 
This AIP proposed adding that to the applicationIndex making it easier to determine which application for which the vote was cast.

### Goals

- update `Voted` event to emit `uint256 applicationIndex` in `QuadraticVotingStrategyImplementation`
- update `vote()` function implementation to be able to decode the `applicationIndex` from the `encodedVote` in `QuadraticVotingStrategyImplementation`

## Specification



Update the `QuadraticVotingStrategyImplementation` to update the `Voted` event and `vote` function 

```

/// @notice Emitted when a new vote is sent
event Voted(
    address token,
    uint256 amount,
    address indexed voter,
    address grantAddress,
    bytes32 indexed projectId,
++  uint256 applicationIndex,
    address indexed roundAddress
)


/**
  * @notice Invoked by RoundImplementation which allows
  * a voted to cast weighted votes to multiple grants during a round
  *
  * @dev
  * - more voters -> higher the gas
  * - this would be triggered when a voter casts their vote via grant explorer
  * - can be invoked by the round
  * - supports ERC20 and Native token transfer
  *
  * @param encodedVotes encoded list of votes
  * @param voterAddress voter address
  */
function vote(bytes[] calldata encodedVotes, address voterAddress) external override payable nonReentrant isRoundContract {
    /// @dev iterate over multiple donations and transfer funds
    for (uint256 i = 0; i < encodedVotes.length; i++) {
      /// @dev decode encoded vote
      (
        address _token,
        uint256 _amount,
        address _grantAddress,
        bytes32 _projectId,
++      uint256 _applicationIndex
      ) = abi.decode(encodedVotes[i], (
        address,
        uint256,
        address,
        bytes32,
++      uint256
      ));
```

## Rationale

Here is the link to the proposed changes: https://github.com/allo-protocol/contracts/pull/12
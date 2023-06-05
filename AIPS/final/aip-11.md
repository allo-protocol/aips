---
aip: 11
title: Changes to Registry, RoundFactory, and AlloSettings Contracts
status: Final
type: Core
author: Aditya Anand <aditya@gitcoin.co>, Kurt Merbeth <kurt@gitcoin.co>
created: 2023-05-30
---


## Abstract

This AIP proposes several changes to the Registry, RoundFactory, and AlloSettings contracts in order to enhance functionality, improve security, and streamline contract interactions in the project ecosystem.

## Motivation

The motivation behind these proposed changes is to address certain limitations and inefficiencies in the existing contracts. By renaming the ProjectRegistry contract to simply Registry, we aim to simplify the naming convention and make it more intuitive for users. The addition of the createRound function in the Registry contract allows projects to create rounds using a unique ID, which is constructed based on the chain ID, registry address, and project ID. This improves the management and identification of rounds within the system.

Furthermore, by purging the ProgramFactory and ProgramImplementation contracts, we eliminate redundant functionality and simplify the contract structure. Updating the project struct to include programMetadata provides a more comprehensive representation of projects, while the introduction of the updateProgramMetadata function enables easy updates to the program metadata.

The proposed changes to the RoundFactory contract involve removing the Ownable contract and utilizing OpenZeppelin's Access Control library instead. This enhances the contract's security by implementing a more robust access control mechanism. Additionally, the createRound function in the RoundFactory contract is modified to ensure that only approved registries can invoke it, which provides better control over round creation. The RoundCreated event is also updated to include additional relevant information.

The AlloSettings contract undergoes changes by introducing OpenZeppelin's Access Control library and creating a new role called approved_registry. This role allows for granular control over approved registries. Furthermore, an interface for AlloSettings is added, enabling easier integration with other contracts. The RoundFactory contract is updated to utilize AlloSettings for the trustedRegistry, enhancing the contract's modularity and interoperability. Finally, both the RoundFactory and RoundImplementation contracts are updated to use the IAlloSettings interface for improved consistency and compatibility.

## Goals

- Rename the ProjectRegistry contract to Registry for improved naming convention.
- Add the createRound function to the Registry contract to enable round creation using a unique ID.
- Purge the ProgramFactory and ProgramImplementation contracts to simplify the contract structure.
- Update the project struct to include projectMetadata for a more comprehensive representation of projects.
- Introduce the updateProjectMetadata function in the Registry contract to allow updates to project metadata.
- Update the metadata event to emit the metadata type.
- Ensure that the metadata updated event is fired only when the metadata is set.
- Remove the Ownable contract from the RoundFactory contract and use OpenZeppelin's Access Control library instead for enhanced security.
- Modify the createRound function in the RoundFactory contract to only allow invocation by approved registries.
- Update the RoundCreated event to include additional relevant information.
- Introduce OpenZeppelin's Access Control library in the AlloSettings contract for improved security.
- Create a new role called approved_registry in the AlloSettings contract.
- Add an interface for AlloSettings to facilitate integration with other contracts.
- Update the RoundFactory contract to use AlloSettings for the trustedRegistry.
- Update both the RoundFactory and RoundImplementation contracts to use the IAlloSettings interface for consistency and compatibility.

## Non-goals

The following goals are not included in this AIP:

- Changes to contracts other than the Registry, RoundFactory, and AlloSettings contracts.
- Changes to contracts outside the scope of the proposed modifications.

## Specification

### Changes to Registry Contract

- Rename the ProjectRegistry contract to Registry.
- Add the following function to the Registry contract

:

```solidity
    function createRound(
        IRoundFactory roundFactory,
        uint256 projectID,
        bytes calldata encodedParameters
    ) external onlyProjectOwner(projectID) returns (address)```

- Update the project struct in the Registry contract to include the following field:

```solidity
    struct Project {
        uint256 id;
        MetaPtr projectMetadata;
        MetaPtr programMetadata;
    }
```

- Add the following function to the Registry contract:

```solidity
    function updateProgramMetadata(
        uint256 projectID,
        MetaPtr calldata programMetadata
    ) external onlyProjectOwner(projectID)
  ```

- Update the metadata event in the Registry contract to emit the metadata type.
- Ensure that the metadata updated event is fired only when the metadata is set.

### Changes to RoundFactory Contract

- Remove the Ownable contract from the RoundFactory contract.
- Introduce OpenZeppelin's Access Control library to implement access control functionality in the RoundFactory contract.
- Modify the createRound function in the RoundFactory contract to include the following logic:

```solidity
 require(alloSettings.isTrustedRegistry(msg.sender), "not trusted registry");
 ```

- Update the RoundCreated event in the RoundFactory contract to include additional relevant information.

### Changes to AlloSettings Contract

- Introduce OpenZeppelin's Access Control library to implement access control functionality in the AlloSettings contract.
- Create the following role in the AlloSettings contract:

```solidity
  bytes32 public constant TRUSTED_REGISTRY_ROLE = keccak256("TRUSTED_REGISTRY");
```

- Add the following interface for AlloSettings:

```solidity
interface IAlloSettings {
    function isTrustedRegistry(address registry) external view returns (bool);
}
```

- Update the RoundFactory contract to use AlloSettings for the trustedRegistry:

- Update both the RoundFactory and RoundImplementation contracts to use the IAlloSettings interface:

```solidity
IAlloSettings public alloSettings;
```

## Rationale

The proposed changes aim to improve the usability, security, and modularity of the contracts in the project ecosystem.
By simplifying contract names, introducing new functions, and utilizing standardized libraries, the contracts become more intuitive, efficient, and secure. 
The changes also enhance the interoperability of the contracts by introducing interfaces and roles that facilitate integration with other contracts.

## References

There are no additional references for this AIP.

## Copyright

Copyright and related rights found in [LICENSE](./LICENSE).

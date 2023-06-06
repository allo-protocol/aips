---
aip: 7
title: Repository and contract renaming
status: Idea
type: Core
author: Jason Romero <jason@gitcoin.co>
created: 2023-05-22
---


## Abstract

This AIP explores the growing need and methodology for renaming repositories and contracts within the Allo Protocol. The process of repository and contract renaming is often overlooked, yet it plays a critical role in enhancing clarity, maintaining consistency, and ensuring effective communication within and between teams. We propose a structured approach for renaming that includes a comprehensive checklist to facilitate this process. The AIP also addresses potential challenges and risks associated with renaming, such as broken dependencies and disrupted workflows, offering mitigation strategies to overcome these issues. Our findings underscore the importance of a systematic approach to repository and contract renaming, contributing to improved project management, collaboration, and overall software development and contract lifecycle management efficiency.

## Motivation

In the realm of software development and digital contract management, the ease of use for developers and effective protocol management are key drivers of productivity and success. Currently, the naming and renaming of repositories and contracts within the Allo Protocol pose significant challenges that can hinder developer efficiency and complicate protocol management. These tasks, while seemingly simple, can often be the source of confusion and inconsistency, affecting both intra and inter-team communication and coordination.

This AIP is driven by the urgent need to streamline these processes, making them more intuitive and less prone to error. By introducing a structured approach to renaming repositories and contracts, complete with a comprehensive checklist and mitigation strategies for potential risks, this proposal aims to eliminate ambiguities and promote clarity.

Through this systematic approach, we anticipate that developers will spend less time troubleshooting issues related to misnamed or improperly renamed repositories and contracts, and more time focusing on core development tasks. Moreover, with improved naming conventions, protocol management will become more seamless, contributing to the overall efficiency and effectiveness of the Allo Protocol.

In essence, this AIP is motivated by the desire to create a more developer-friendly environment and a well-managed protocol, ultimately facilitating improved project management and collaboration, and contributing to the continued growth and success of the Allo Protocol.

## Goals

1. **Developer Efficiency**: Improve ease of use for developers by providing a clear, structured approach to renaming repositories and contracts. This will help reduce time spent on troubleshooting issues related to improper naming and allow developers to focus on core development tasks.
2. **Clear Communication**: Enhance intra and inter-team communication by establishing consistent naming conventions. This will reduce ambiguities, prevent misinterpretations, and promote effective collaboration.
3. **Protocol Management**: Streamline the protocol management process by maintaining organized, appropriately named repositories and contracts. This will make it easier to track changes, updates, and dependencies within the Allo Protocol.
4. **Risk Mitigation**: Identify potential risks and challenges associated with renaming repositories and contracts, such as broken dependencies and disrupted workflows. The goal is to offer strategies and solutions to mitigate these risks, ensuring smooth transitions during renaming processes.
5. **Scalability**: Create a renaming methodology that can scale with the growth and complexity of the Allo Protocol. This includes the development of tools and practices that can handle an increasing number of repositories and contracts while maintaining efficiency and clarity.
6. **Continuous Improvement**: Foster a culture of continuous improvement within the Allo community by regularly reviewing and updating the proposed renaming methodology. This will ensure that it remains relevant and effective in response to evolving needs and challenges.

## Non-goals

1. **Branding and Marketing Considerations**: This AIP does not aim to address the naming of repositories and contracts from a branding perspective. Rather, it focuses on the technical aspects of naming and renaming, with the goal of improving developer efficiency and protocol management.
2. **Immediate Implementation**: While this AIP proposes a systematic approach to renaming repositories and contracts, it```markdown
does not aim for an immediate overhaul of existing naming conventions. The transition is expected to be gradual and mindful of ongoing projects and dependencies.
3. **Enforcement of Strict Standards**: While this AIP advocates for clearer and more consistent naming, it does not intend to impose rigid naming standards that could potentially stifle creativity or flexibility within the development process. The goal is to balance clarity and consistency with the need for adaptability and innovation.
4. **Complete Automation**: Although the proposal encourages the use of automated tools to facilitate the renaming process, it does not aim to completely automate it. Manual review and input are essential to ensure the appropriateness and relevance of names, especially in the context of unique or complex projects.
5. **Resolution of All Naming Issues**: While this AIP addresses repository and contract renaming, it does not claim to solve all issues related to naming conventions in the Allo Protocol. Other areas, such as variable and function naming, are beyond the scope of this proposal.
6. **Elimination of All Risks**: The proposal includes strategies for risk mitigation related to renaming repositories and contracts, but it does not guarantee the elimination of all potential risks. The goal is to minimize, rather than eliminate, these risks and to equip the Allo community with strategies to handle them effectively.
7. **Static Guidelines**: This AIP provides a framework for repository and contract renaming, but it does not intend these guidelines to be fixed or unchangeable. The guidelines are meant to evolve based on feedback, learning, and changes in the software development and digital contract management landscape.

## Specification

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119) and [RFC 8174](https://datatracker.ietf.org/doc/html/rfc8174).

## Rationale

The rationale behind this AIP lies in the inherent complexities and potential pitfalls associated with repository and contract naming and renaming within the Allo Protocol. With multiple developers working on various contracts and repositories, a lack of clear and consistent naming conventions can lead to confusion, misinterpretation, and inefficiency, negatively impacting both developer productivity and protocol management. Furthermore, without a systematic approach to renaming, the risk of broken dependencies and disrupted workflows increases.

By introducing a structured methodology for renaming, we aim to mitigate these issues and bring about several key benefits:

1. **Increased Developer Productivity**: By eliminating confusion around repository and contract names, developers can focus on core development tasks, thereby enhancing productivity.
2. **Improved Protocol Management**: A standardized approach to naming and renaming aids in tracking changes, updates, and dependencies, simplifying protocol management.
3. **Enhanced Communication and Collaboration**: Clear and consistent naming conventions facilitate better understanding and communication within and between teams, promoting effective collaboration.
4. **Reduced Risk**: Identifying potential risks associated with renaming and providing strategies for risk mitigation helps prevent broken dependencies and disrupted workflows.
5. **Scalability**: A robust renaming methodology can accommodate the growth and complexity of the Allo Protocol, maintaining efficiency and clarity even as the number of repositories and contracts increases.

The proposed approach is not about enforcing rigid standards or making sweeping changes overnight. Instead, it's about introducing a more organized, consistent, and thoughtful way of handling repository and contract naming and renaming—one that respects ongoing projects and dependencies, supports creativity and flexibility, and evolves with the needs of the Allo community.

## Implementation [WIP]

Current [GitHub Discussion](https://github.com/orgs/allo-protocol/discussions/21)

#### Contract Renaming

    ProjectRegistry.sol -> Registry.sol
    VotingStrategy.sol -> AllocationStrategy.sol
    PayoutStrategy.sol -> DistributionStrategy.sol
    
    * Additional variable renaming TBD based on the above changes.
    ex: vote() -> allocate()

>Also note that the way we impliment the payout or allocation strategies is still under discussion. We may want to create a development process that is community driven and allows for multiple strategies to be developed and tested. This would allow for the community to decide which strategy is best for them and their use case.
  
#### Repository Renaming

    allo-contracts -> contracts


## References

Active [Pull Request](https://github.com/allo-protocol/aips/pull/35)

In computer programming, a naming convention is a set of rules for choosing the character sequence to be used for identifiers which denote variables, types, functions, and other entities in source code and documentation. The use of naming conventions can reduce the effort needed to read and understand source code, enable code reviews to focus on more significant issues than syntax and naming standards, and help formalize expectations and promote consistency within a development team, among other benefits [1](https://en.wikipedia.org/wiki/Naming_convention_(programming)).

As for the best practices in naming conventions for smart contracts, they follow the general principles of programming and document naming conventions. The aim is to have names that enhance readability, provide meaningful information, and promote consistency within a development team. This includes using clear and descriptive identifiers, adhering to specific length rules, and adopting standardized abbreviations when necessary.

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).

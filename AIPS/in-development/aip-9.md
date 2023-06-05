---
aip: 9
title: Adding the Foundry testing suite to the repo
status: In Development
type: Core
author: Jason Romero <jason@gitcoin.co>
created: 2023-05-25
---


## Abstract
The rapid growth of our contracts repository necessitates a robust testing framework to ensure the reliability and security of our smart contracts. While Hardhat has been instrumental in facilitating integration testing, we recognize the need for a specialized tool that can provide enhanced testing capabilities specifically tailored for contract development. This abstract proposes the integration of Foundry, an advanced testing framework, into our current Hardhat contracts repository to complement and augment our existing testing practices.

Foundry offers a comprehensive suite of testing features specifically designed for smart contracts, enabling us to write more expressive and efficient tests. By incorporating Foundry into our testing workflow, we can leverage its powerful functionalities such as contract deployment management, contract simulation, and gas usage profiling. This integration will allow us to thoroughly test the individual contracts in isolation, ensuring their correctness and adherence to desired behavior.

The proposed approach emphasizes a hybrid testing strategy, where Hardhat continues to be utilized for integration testing, while Foundry takes center stage for unit and functional testing of individual contracts. By segregating the testing responsibilities, we can achieve a more modular and comprehensive testing ecosystem, improving the reliability and maintainability of our smart contracts.

This abstract highlights the benefits of integrating Foundry into our existing Hardhat contracts repository, presenting a compelling case for adopting this dual testing approach. The combination of Hardhat's integration testing capabilities and Foundry's specialized contract testing features will empower our development team to conduct thorough and efficient testing, ensuring the quality and robustness of our smart contracts.


## Motivation
The motivation behind integrating Foundry into our current Hardhat contracts repository stems from the need to enhance our contract testing practices and ensure the reliability of our smart contracts. While Hardhat has served us well for integration testing, it lacks certain specialized features that are crucial for comprehensive contract testing.

Contract-specific Testing: Smart contracts have unique characteristics and behaviors that require specialized testing techniques. Foundry provides a dedicated testing framework specifically designed for smart contracts, allowing us to write more focused and efficient tests that target contract-specific functionality. By incorporating Foundry, we can improve the thoroughness and accuracy of our contract testing, reducing the risk of vulnerabilities and errors.

Advanced Testing Capabilities: Foundry offers a rich set of testing features that go beyond basic contract deployment and interaction. It provides contract simulation capabilities, allowing us to test contract behavior under different scenarios and conditions. Additionally, Foundry enables gas usage profiling, helping us optimize contract efficiency and identify potential gas-related issues. By leveraging these advanced testing capabilities, we can ensure that our contracts perform as expected and meet our performance requirements.

Modularity and Maintainability: Integrating Foundry into our testing workflow promotes modularity and maintainability. By segregating the testing responsibilities between Hardhat and Foundry, we can achieve a clear separation of concerns. Hardhat can continue to handle integration testing, ensuring smooth interaction between contracts and external components. At the same time, Foundry can focus on unit and functional testing of individual contracts, enabling us to test contract logic in isolation and maintain a more modular codebase. This separation simplifies testing setup and maintenance, making it easier to identify and fix issues within specific contracts.

Community Support and Innovation: Foundry benefits from a vibrant community of developers and continuous innovation in the field of smart contract testing. By integrating Foundry into our testing ecosystem, we gain access to a wealth of community resources, including documentation, tutorials, and best practices. We can also take advantage of the frequent updates and improvements made to Foundry, ensuring that our testing practices remain up-to-date and aligned with industry standards.

In conclusion, the motivation behind integrating Foundry into our current Hardhat contracts repository revolves around the need for specialized contract testing capabilities, advanced testing features, modularity, and access to a thriving community. By combining the strengths of Hardhat and Foundry, we can establish a comprehensive testing framework that enhances the quality and reliability of our smart contracts, ultimately contributing to the overall success of our project.


## Goals

The goals of this proposal are as follows:

Enhance Contract Testing: The primary goal is to enhance our contract testing practices by leveraging the specialized testing capabilities provided by Foundry. This includes writing more focused and efficient tests that target contract-specific functionality, ensuring comprehensive coverage and accuracy in testing.

Improve Contract Reliability: By adopting Foundry, we aim to improve the reliability of our smart contracts. Through advanced testing features such as contract simulation and gas usage profiling, we can identify and address potential vulnerabilities, optimize gas efficiency, and ensure that our contracts perform as expected under different scenarios.

Promote Modularity and Maintainability: Integrating Foundry into our testing workflow promotes modularity and maintainability. By segregating testing responsibilities between Hardhat and Foundry, we can achieve a clear separation of concerns, enabling more modular code and easier maintenance of contract-specific tests.

Leverage Community Support and Innovation: Foundry benefits from a thriving community of developers and continuous innovation in smart contract testing. By integrating Foundry, we can tap into this community support and access a wealth of resources, including documentation, tutorials, and best practices. This allows us to stay up-to-date with the latest testing techniques and industry standards.

Enhance Contract Development Process: Integrating Foundry into our workflow streamlines the contract development process. By adopting specialized testing tools, we can catch and resolve issues earlier in the development cycle, reducing the likelihood of bugs and vulnerabilities making their way into production. This leads to more efficient development, improved code quality, and faster deployment of reliable smart contracts.

Overall, the goals of integrating Foundry into our current Hardhat contracts repository are to enhance contract testing, improve contract reliability, promote modularity and maintainability, leverage community support and innovation, and enhance our overall contract development process. By achieving these goals, we aim to ensure the robustness, security, and success of our smart contract projects.

## Specification

To implement the proposal of integrating Foundry into our current Hardhat contracts repository, we will follow the following steps:

Evaluate Foundry Features: Conduct a thorough evaluation of Foundry's features and capabilities to understand how it can enhance our contract testing process. This includes exploring features such as contract simulation, gas profiling, contract cloning, and test coverage analysis.

Setup Foundry Environment: Set up a dedicated Foundry environment within our development infrastructure. This involves installing the necessary dependencies, configuring the environment, and integrating Foundry with our existing testing framework.

Identify Target Contracts: Identify the contracts within our repository that would benefit the most from Foundry integration. These could be complex contracts with intricate logic, contracts handling significant value or sensitive data, or contracts with a higher risk of vulnerabilities.

Refactor Existing Tests: Review and refactor our existing test suite to accommodate the Foundry integration. This may involve reorganizing tests, updating test configurations, and modifying test assertions to align with Foundry's testing conventions.

Write Foundry-Specific Tests: Write additional tests specifically designed to leverage Foundry's advanced testing features. These tests should target critical functionality, edge cases, and potential vulnerabilities to ensure comprehensive coverage and reliability of the contracts.

Integration with CI/CD Pipeline: Integrate Foundry into our continuous integration and deployment (CI/CD) pipeline. This ensures that Foundry tests are automatically executed whenever changes are made to the contracts, enabling continuous testing and early detection of issues.

Establish Testing Guidelines: Define clear guidelines and best practices for writing Foundry tests. Document these guidelines to ensure consistent and standardized testing practices across the development team.

Training and Knowledge Sharing: Provide training sessions or workshops to familiarize the development team with Foundry's features and demonstrate its benefits. Encourage knowledge sharing among team members to promote the adoption of Foundry and ensure everyone is equipped with the necessary skills to write effective tests.

Iterative Improvement: Continuously improve the integration by incorporating feedback, refining testing practices, and adopting new features and enhancements provided by Foundry. Stay connected with the Foundry community to stay informed about updates and advancements in smart contract testing.

Monitor and Evaluate Results: Monitor the results of the integration by tracking test coverage, identifying bugs or vulnerabilities caught by Foundry tests, and measuring the overall improvement in contract reliability. Evaluate the impact of Foundry on development efficiency, code quality, and deployment success rates.

By following these steps, we can successfully implement the integration of Foundry into our current Hardhat contracts repository. This will result in enhanced contract testing, improved contract reliability, and streamlined development practices, ultimately leading to more secure and robust smart contracts.

## Usage 

Integrating Foundry into our current Hardhat contracts repository unlocks powerful capabilities for testing and enhancing the reliability of our smart contracts. With Foundry, we can leverage advanced testing features and streamline our development practices, ensuring more secure and robust contracts. Here's how to make the most out of Foundry in our workflow:

Test Automation: Foundry allows us to automate the execution of comprehensive tests for our contracts. We can easily define test cases, simulate contract behavior, and evaluate the results. By automating our tests, we save time and effort, ensuring thorough testing coverage without manual intervention.

Contract Simulation: Foundry enables us to simulate various contract scenarios, including different input values, interactions with other contracts, and complex contract logic. We can verify contract behavior under different conditions, identify edge cases, and uncover potential vulnerabilities or bugs before deployment.

Gas Profiling: With Foundry, we gain insights into the gas consumption of our contracts. We can profile gas usage for different contract functions, identify gas-intensive operations, and optimize our contracts for cost-efficiency. Gas profiling helps us understand the impact of contract modifications and make informed decisions to reduce transaction costs.

Contract Cloning: Foundry's contract cloning feature allows us to create independent clones of our contracts for testing purposes. We can isolate specific contract instances and manipulate their state for targeted testing. Contract cloning enhances test reproducibility and facilitates more focused and precise testing of critical functionality.

Test Coverage Analysis: Foundry provides test coverage analysis tools to measure the effectiveness of our tests. We can identify areas of our contracts that lack coverage and ensure that our tests adequately exercise all code paths. Test coverage analysis helps us identify potential blind spots and strengthen our testing strategy.

Integration with CI/CD Pipeline: Foundry seamlessly integrates into our continuous integration and deployment (CI/CD) pipeline. We can incorporate Foundry tests into our existing CI/CD workflows, enabling automated testing on each code change. This ensures that our contracts are thoroughly tested before deployment and helps catch issues early in the development lifecycle.

Improved Contract Reliability: By leveraging Foundry's advanced testing capabilities, we enhance the reliability of our smart contracts. Thorough testing, contract simulation, and test coverage analysis help us identify and fix bugs, vulnerabilities, and edge cases. This results in more robust contracts that are less prone to errors and exploits.

Streamlined Development Practices: Foundry streamlines our development practices by providing a unified testing framework. We can consolidate our testing efforts within Foundry, reducing the need for disparate testing tools and simplifying our testing workflow. This leads to greater development efficiency, code maintainability, and collaboration among team members.

By utilizing Foundry's comprehensive testing features and integrating it into our existing Hardhat contracts repository, we can significantly improve the reliability, security, and efficiency of our smart contracts. Foundry empowers us to write more effective tests, identify potential issues early on, and deliver high-quality contracts that instill confidence in our stakeholders.

## Rationale

The decision to integrate Foundry into our current Hardhat contracts repository is driven by several compelling reasons:

Enhanced Testing Capabilities: Foundry provides advanced testing features specifically designed for Solidity smart contracts. By incorporating Foundry into our testing workflow, we can leverage its powerful testing capabilities to thoroughly test our contracts and uncover potential vulnerabilities, bugs, or edge cases. This enables us to ensure the reliability and security of our contracts before deployment.

Complementary Tooling: While Hardhat is an excellent framework for building and deploying contracts, Foundry complements it by focusing on contract testing. By integrating Foundry into our repository, we can leverage the strengths of both tools. Hardhat can continue to handle contract compilation, deployment, and integration testing, while Foundry can handle more specialized contract testing scenarios.

Increased Test Coverage: Foundry's testing features enable us to achieve higher test coverage for our contracts. We can easily define and execute a wide range of tests, including functional tests, edge case tests, and scenario-based tests. The ability to automate and thoroughly test our contracts helps identify potential issues early on and ensures that our contracts behave as intended in different scenarios.

Efficiency and Productivity: Foundry streamlines the testing process by providing a unified testing framework specifically tailored for Solidity contracts. By consolidating our testing efforts within Foundry, we can improve efficiency and productivity. Foundry's intuitive interface and testing automation capabilities save time and effort, enabling us to focus on writing effective tests and delivering high-quality contracts.

Gas Optimization: Foundry's gas profiling capabilities allow us to optimize our contracts for gas efficiency. We can analyze the gas consumption of our contract functions and identify areas for optimization. By optimizing gas usage, we can reduce transaction costs and improve the overall performance of our contracts.

Integration with Existing CI/CD Pipeline: Foundry seamlessly integrates into our existing CI/CD pipeline, enabling us to incorporate contract testing into our automated deployment process. By integrating Foundry tests into our CI/CD workflow, we ensure that our contracts are thoroughly tested before deployment, reducing the risk of introducing bugs or vulnerabilities into the production environment.

Community Support and Updates: Foundry benefits from an active community of developers and regular updates from the development team. By integrating Foundry into our repository, we gain access to the latest features, bug fixes, and improvements contributed by the community. This ensures that our testing practices stay up-to-date and aligned with industry best practices.

Overall, integrating Foundry into our current Hardhat contracts repository aligns with our goal of delivering secure, reliable, and high-quality smart contracts. Foundry's specialized testing features, combined with the strengths of Hardhat, provide us with a comprehensive testing framework that empowers us to build and deploy robust contracts with confidence.

## References
WIP
<!--
This section is optional. 
If applicable, provide a list of any relevant sources and citations used
elsewhere in this AIP:
    A list of relevant links like for this proposal
    - [forum discussion](discordlink)
    - [tests](githublink)
    - [proposalCode](githublink)
-->

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
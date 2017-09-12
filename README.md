# Paymoja Overview
Paymoja advocates and promotes financial inclusion for everyone. Today more than 2 billion adults do not have a bank account or access to a formal financial institution.  Paymoja is aimed at changing this denominator by making banking accessible by everyone via a standard flip phone.  Our project is aimed at building a national digital financial solution that is open to everyone.  Specifically, any person in any location with a phone can open a back account, send money, receive money or get paid for services.  This open system will help the poorest people in the most remote locations to ensure a safe and reliable solution.  

Paymoja is a sofware implementation of the Level One Project. For more information on the Level One Project, see the https://LevelOneProject.org

## Why should I contribute?
Paymoja is an initiative by the Bill and Melinda Gates Foundation to make it easier for developing countries to provide useful digital financial services to the people who live there. To participate in the formal, global economy, everyone needs access to digital financial services so they can transact quickly and safely, across distances long and short.  

This project started with a model and prototype for a financial system that could be implemented in any country.  In addition, this code takes that a step further by implementing a strong reliable messaging using the [Interledger](http://interledger.org) protocol as well as a functioning central hub that financial providers can connect to facilitate common settlement and regulatory compliance.

> In order to expand this service and ensure that we a level playing field for everyone we need your help to enhance this project and help to realize the vision of having one digital financial system in every country around the world.

## Getting Started
The project is in GitHub and is organized on the basis of component microservices.  As such, the team has created over twenty different repositories in GitHub that align to the different services.  The _Docs_ repository documents the overall architecture, component design, message flow, and an overview of the Paymoja software. Individual repositories in the [Paymoja GitHub organization](https://github.com/LevelOneProject/) each describe component-specific details including source and APIs.

New developers, see the [contributors guide](./contribute.md) for onboarding materials.

## Paymoja Services
The following architecture diagram shows the Paymoja services:

![Paymoja Services](https://github.com/LevelOneProject/Docs/blob/master/Wiki/Basic%20Overview.png)

See the [physical machines](https://github.com/LevelOneProject/Docs/blob/master/AWS/Infrastructure/machines.md) for information about the test and demonstration implementations in Amazon Web Services (AWS).

The basic idea behind Paymoja is that we need to connect multiple Digital Financial Services Providers (DFSPs) together into a competitive and interoperable network in order to maximize opportunities for poor people to get access to financial services with low or no fees. We don't want a single monopoly power in control of all payments in a country, or a system that shuts out new players. It also doesn't help if there are too many isolated subnetworks. Our model addresses these issues in several key ways:

- A set of central services provides a hub through which money can flow from one DFSP to each other. This is similar to how money moves through a central bank or clearing house in developed countries. Besides a central ledger, central services can provide identity lookup, fraud management, and enforce scheme rules.
- A standard set of interfaces a DFSP can implement to connect to the system, and example code that shows how to use the system. A DFSP that wants to connect up can adapt our example code or implement the standard interfaces into their own software. The goal is for it to be as straightforward as possible for a DFSP to connect to the interoperable network.
- Complete working open-source implementations of both sides of the interfaces - an example DFSP that can send and receive payments and the client that an existing DFSP could host to connect to the network.

### DFSP Service
The DFSP code is an example implementation of a mobile money provider. Customers connect to it from their mobile feature phones using Unstructured Supplementary Service Data (USSD). USSD is a Global System for Mobile (GSM) communication technology that is used to send text between a mobile phone and an application program in the network, allowing users to create accounts, send money, and receive money.

[DFSP Documentation](https://github.com/LevelOneProject/Docs/blob/master/DFSP)

### Level One Client Service
The client service connects a DFSP to other other DFSPs and the central services. It has a few simple interfaces to connect to a DFSP for account holder lookup, payment setup, and ledger operations. The level one client can be hosted locally by the DFSP or in a remote data center such as Amazon.

[Level One Client Documentation](https://github.com/LevelOneProject/Docs/blob/master/LevelOneClient)

### Central Services
The central services are a collection of separate services that help the DFSPs perform operations on the network.

- The [Central Directory Service](https://github.com/LevelOneProject/Docs/blob/master/CentralDirectory) determines which DFSP handles a user's accounts.
- The [Central Ledger Service](https://github.com/LevelOneProject/Docs/blob/master/CentralLedger) handles clearing and settlement.
- The [Central Rules Service](https://github.com/LevelOneProject/Docs/blob/master/CentralRules) sets policy across the system.
- The [Fraud service](https://github.com/LevelOneProject/central-fraud-sharing) aids DFPS in identifying suspicious behavior.

## End-to-End Scenarios
The aforementioned individual services can't alone describe how key scenarios work across the system. Therefore, for each of the [Paymoja Scenarios](https://github.com/LevelOneProject/paymoja/contribute/Scenarios.md), we provide a technical walk through.

1. Send Money to Anyone: [scenario](https://github.com/LevelOneProject/Docs/blob/master/scenarios.md#send-money-to-anyone),  [walkthrough](https://github.com/LevelOneProject/Docs/blob/master/LevelOneClient/scenarios/Send%20Payment.md)
2. Buy Goods [scenario](https://github.com/LevelOneProject/Docs/blob/master/scenarios.md#buy-goods---pending-transactions), [message flow](https://github.com/LevelOneProject/Docs/blob/master/DFSP/PendingTransactions/README.md)
3. Bulk Payment [scenario](https://github.com/LevelOneProject/Docs/blob/master/scenarios.md#bulk-payments), [message flow](https://github.com/LevelOneProject/Docs/blob/master/DFSP/BulkPayment/README.md)

## System-wide Testing
Individual services have their own tests, but the [testing strategy](https://github.com/LevelOneProject/paymojacontribute/Manual-and-automated-testing-strategy.md) also includes the following system-wide tests:

- [Scenario testing](https://github.com/LevelOneProject/Docs/blob/master/test/end-to-end/readme.md)
- [End-to-end functional testing](https://github.com/LevelOneProject/interop-functional-tests)
- [Performance testing](https://github.com/LevelOneProject/Docs/blob/master/test/performance)
- [Resilience Modeling and Anaylysis (RMA)](https://github.com/LevelOneProject/Docs/blob/master/RMD.md)
- Threat Modeling

## Related Projects
The [Interledger Protocol Suite](https://interledger.org/) (ILP) is an open and secure standard that enables DFSPs to settle payments with minimal _counter-party risk_ (the risk you incur when someone else is holding your money). With ILP, you can transact across different systems with no chance that someone in the middle disappears with your money. Paymoja uses the Interledger Protocol Suite for the clearing layer. For an overview of how it works, see the [Clearing Architecture Documentation](https://github.com/LevelOneProject/Docs/blob/master/ILP).
# Greenfield Whitepaper

## Revision

| Revision | Date       |
|----------|------------|
| 0.1      | 2022/12/04 |
| 0.2      | 2023/01/15 |
| 0.3      | 2023/01/19 |

## Table of Content

- [Overview](./overview.md#overview)
- [Part 1 Design of the BNB Greenfield and the Decentralized Storage Economy](./part1/intro.md)
  - [1 Design Principles](./part1/ch1.md#1-design-principles)
  - [2 Assumptions](./part1/ch2.md#2-assumptions)
  - [3 The Architecture in General](./part1/ch3.md#3-the-architecture-in-general)
    - [3.1 Greenfield Core](./part1/ch3.md#31-greenfield-core)
    - [3.2 BNB Greenfield dApps](./part1/ch3.md#32-bnb-greenfield-dapps)
    - [3.3 The Cross-Chain with BSC](./part1/ch3.md#33-the-cross-chain-with-bsc)
    - [3.4 The Trinity](./part1/ch3.md#34-the-trinity)
  - [4 BNB Greenfield Core](./part1/ch4.md#4-bnb-greenfield-core)
    - [4.1 The BNB Greenfield Blockchain](./part1/ch4.md#41-the-bnb-greenfield-blockchain)
    - [4.2 The Storage Providers, SPs](./part1/ch4.md#42-the-storage-providers-sps)
    - [4.3 The Pair Synergy](./part1/ch4.md#43-the-pair-synergy)
  - [5 The Greenfield Data Storage](./part1/ch5.md#5-the-greenfield-data-storage)
    - [5.1 Data with Consensus](./part1/ch5.md#51-data-with-consensus)
      - [5.1.1 Accounts and Balance](./part1/ch5.md#511-accounts-and-balance)
      - [5.1.2 Validator and SP Metadata](./part1/ch5.md#512-validator-and-sp-metadata)
      - [5.1.3 Storage Metadata](./part1/ch5.md#513-storage-metadata)
      - [5.1.4 Permission Metadata](./part1/ch5.md#514-permission-metadata)
      - [5.1.5 Billing Metadata](./part1/ch5.md#515-billing-metadata)
    - [5.2 Off-Chain Payload Object Data Storage](./part1/ch5.md#52-off-chain-payload-object-data-storage)
      - [5.2.1 Primary and Secondary SPs](./part1/ch5.md#521-primary-and-secondary-sps)
      - [5.2.2 Data Redundancy](./part1/ch5.md#522-data-redundancy)
  - [6 Storage Economics and Its Primitives](./part1/ch6.md#6-storage-economics-and-its-primitives)
    - [6.1 Account Creation](./part1/ch6.md#61-account-creation)
    - [6.2 Data Object Creation](./part1/ch6.md#62-data-object-creation)
    - [6.3 Data Storage](./part1/ch6.md#63-data-storage)
    - [6.4 Data Read and Download](./part1/ch6.md#64-data-read-and-download)
    - [6.5 Permissions and Group](./part1/ch6.md#65-permissions-and-group)
    - [6.6 Fees and Payments](./part1/ch6.md#66-fees-and-payments)
    - [6.7 Data Integrity and Availability Challenge](./part1/ch6.md#67-data-integrity-and-availability-challenge)
    - [6.8 Data Delete](./part1/ch6.md#68-data-delete)
  - [7 Economy of Data Assets](./part1/ch7.md#7-economy-of-data-assets)
    - [7.1 Cross-Chain with BSC](./part1/ch7.md#71-cross-chain-with-bsc)
    - [7.2 Framework](./part1/ch7.md#72-framework)
    - [7.3 Communication Layer](./part1/ch7.md#73-communication-layer)
    - [7.4 Resource Mirror Layer](./part1/ch7.md#74-resource-mirror-layer)
      - [7.4.1 Resource Entity Mirror](./part1/ch7.md#741-resource-entity-mirror)
      - [7.4.2 Cross-Chain Operating Primitives](./part1/ch7.md#742-cross-chain-operating-primitives)
  - [8 "Not" Ending for the Design](./part1/ch8.md#8-not-ending-for-the-design)
    - [8.1 Acknowledgement](./part1/ch8.md#81-acknowledgement)
- [Part 2 Showcases in Labs](./part2/intro.md)
  - [9 Showcases: Decentralized Storage](./part2/ch9.md#9-showcases-decentralized-storage)
    - [9.1 Web Hosting and Personal Cloud Drive](./part2/ch9.md#91-web-hosting-and-personal-cloud-drive)
    - [9.2 Data Availability Layer for Public Blockchain](./part2/ch9.md#92-data-availability-layer-for-public-blockchain)
      - [9.2.1 Layer 1 Blockchain Data Swapping](./part2/ch9.md#921-layer-1-blockchain-data-swapping)
      - [9.2.2 Data Availability Layer for the Layer 2 Rollups](./part2/ch9.md#922-data-availability-layer-for-the-layer-2-rollups)
      - [9.2.3 Snapshots and Block Data Backups](./part2/ch9.md#923-snapshots-and-block-data-backups)
  - [10 Showcases: New Ways of Digital Publishing](./part2/ch10.md#10-showcases-new-ways-of-digital-publishing)
    - [10.1 Grass-Root Digital Publishing](./part2/ch10.md#101-grass-root-digital-publishing)
    - [10.2 Data Market](./part2/ch10.md#102-data-market)
    - [10.3 Risk: Anti-Piracy](./part2/ch10.md#103-risk-anti-piracy)
  - [11 Showcases: User-Generated Content](./part2/ch11.md#11-showcases-user-generated-content)
    - [11.1 Anti-Monopoly and Anti-Censorship](./part2/ch11.md#111-anti-monopoly-and-anti-censorship)
    - [11.2 Token Curated Registries](./part2/ch11.md#112-token-curated-registries)
  - [12 Showcases: Personal Data Market](./part2/ch12.md#12-showcases-personal-data-market)
  - [13 From Showcases to Real Production](./part2/ch13.md#13-from-showcases-to-real-production)
- [Part 3 Simplified Technical Specifications](./part3/intro.md)
  - [14 Ecosystem Players](./part3/ch14.md#14-ecosystem-players)
    - [14.1 Greenfield Validators](./part3/ch14.md#141-greenfield-validators)
    - [14.2 Storage Providers (SPs)](./part3/ch14.md#142-storage-providers-sps)
    - [14.3 Greenfield dApps](./part3/ch14.md#143-greenfield-dapps)
  - [15 User Identifier](./part3/ch15.md#15-user-identifier)
    - [15.1 User Balance](./part3/ch15.md#151-user-balance)
  - [16 Greenfield Blockchain](./part3/ch16.md#16-greenfield-blockchain)
    - [16.1 Token Economics](./part3/ch16.md#161-token-economics)
    - [16.2 Consensus and Validator Election](./part3/ch16.md#162-consensus-and-validator-election)
    - [16.3 Governance Transactions](./part3/ch16.md#163-governance-transactions)
      - [16.3.1 Create and Edit Validator](./part3/ch16.md#1631-create-and-edit-validator)
      - [16.3.2 Staking Reward Distribution](./part3/ch16.md#1632-staking-reward-distributio-n)
      - [16.3.3 Create Storage Provider](./part3/ch16.md#1633-create-storage-provider)
      - [16.3.4 Remove Storage Provider](./part3/ch16.md#1634-remove-storage-provider)
  - [17 Storage MetaData Models](./part3/ch17.md#17-storage-metadata-models)
    - [17.1 Bucket](./part3/ch17.md#171-bucket)
    - [17.2 Object](./part3/ch17.md#172-object)
    - [17.3 Group](./part3/ch17.md#173-group)
    - [17.4 Permission](./part3/ch17.md#174-permission)
      - [17.4.1 Ownership](./part3/ch17.md#1741-ownership)
      - [17.4.2 Permission Definitions](./part3/ch17.md#1742-permission-definitions)
      - [17.4.3 Permission Removal](./part3/ch17.md#1743-permission-removal)
      - [17.4.4 Examples](./part3/ch17.md#1744-examples)
  - [18 Payload Storage Management](./part3/ch18.md#18-payload-storage-management)
    - [18.1 Segments](./part3/ch18.md#181-segments)
    - [18.2 Erasure Code and Data Redundancy](./part3/ch18.md#182-erasure-code-and-data-redundancy)
      - [18.2.1 Data Redundancy Design](./part3/ch18.md#1821-data-redundancy-design)
      - [18.2.2 Erasure Code](./part3/ch18.md#1822-erasure-code)
        - [18.2.2.1 Encoding](./part3/ch18.md#18221-encoding)
        - [18.2.2.2 Decoding: Data Recovery](./part3/ch18.md#18222-decoding-data-recovery)
  - [19 Data Availability Challenge](./part3/ch19.md#19-data-availability-challenge)
    - [19.1 The Initial Data Integrity and Redundancy Metadata](./part3/ch19.md#191-the-initial-data-integrity-and-redundancy-metadata)
    - [19.2 Data Availability Challenge Process](./part3/ch19.md#192-data-availability-challenge-process)
  - [20 Storage Transactions](./part3/ch20.md#20-storage-transactions)
  - [21 Billing and Payment](./part3/ch21.md#21-billing-and-payment)
    - [21.1 Concepts and Formulas](./part3/ch21.md#211-concepts-and-formulas)
      - [21.1.1 Terminology](./part3/ch21.md#2111-terminology)
      - [21.1.2 Formula](./part3/ch21.md#2112-formula)
      - [21.1.3 Types and Interfaces](./part3/ch21.md#2113-types-and-interfaces)
    - [21.2 Key Workflow](./part3/ch21.md#212-key-workflow)
      - [21.2.1 Deposit and Withdrawal](./part3/ch21.md#2121-deposit-and-withdrawal)
      - [21.2.2 Payment Stream](./part3/ch21.md#2122-payment-stream)
      - [21.2.3 Forced Settlement](./part3/ch21.md#2123-forced-settlement)
      - [21.2.4 Payment Account](./part3/ch21.md#2124-payment-account)
      - [21.2.5 Account Freeze and Resume](./part3/ch21.md#2125-account-freeze-and-resume)
      - [21.2.6 Storage Fee Price and Adjustment](./part3/ch21.md#2126-storage-fee-price-and-adjustment)
  - [22 Cross-Chain Models](./part3/ch22.md#22-cross-chain-models)
    - [22.1 Communication Channels and Packages](./part3/ch22.md#221-communication-channels-and-packages)
      - [22.1.1 Vote Poll](./part3/ch22.md#2211-vote-poll)
      - [22.1.2 Channel and Sequence](./part3/ch22.md#2212-channel-and-sequence)
      - [22.1.3 Reliability Protocol](./part3/ch22.md#2213-reliability-protocol)
      - [22.1.4 Validator Update](./part3/ch22.md#2214-validator-update)
    - [22.2 Economic](./part3/ch22.md#22-2-economic)
      - [22.2.1 Fee and Reward of Cross-Chain Packages](./part3/ch22.md#2221-fee-and-reward-of-cross-chain-packages)
      - [22.2.2 Race to Deliver Cross-Chain Packages](./part3/ch22.md#2222-race-to-deliver-cross-chain-packages)
      - [22.2.3 Callbacks and Limited Gas](./part3/ch22.md#2223-callbacks-and-limited-gas)
      - [22.2.4 Cross-Chain Infrastructure Contracts on BSC](./part3/ch22.md#2224-cross-chain-infrastructure-contracts-on-bsc)
    - [22.3 Error and Failure Handling](./part3/ch22.md#223-error-and-failure-handling)
  - [23 SP APIs](./part3/ch23.md#23-sp-apis)
    - [23.1 Universal Endpoint](./part3/ch23.md#231-universal-endpoint)
      - [23.1.1 URI Standard](./part3/ch23.md#2311-uri-standard)
      - [23.1.2 HTTPS REST API](./part3/ch23.md#2312-https-rest-api)
      - [23.1.3 P2P RPC](./part3/ch23.md#2313-p2p-rpc)
    - [23.2 List Operations](./part3/ch23.md#232-list-operations)
- [Ending](./ending.md#ending)

## Contribute

1. Clone the repo and checkout a branch

  ```shell
  git clone https://github.com/bnb-chain/greenfield-whitepaper.git
  git checkout -b <your-branch-name>
  ```

2. Make your changes

3. Lint files before a pull request

  ```shell
  # install markdownlint-cli from https://github.com/igorshubovych/markdownlint-cli
  markdownlint '**/*.md'  -c .github/workflows/markdownlint.yaml
  ```

4. Submit a pull request

## License

All the content are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

# Part 3 Simplified Technical Specifications

## Table of Content

- [14 Ecosystem Players](#14-ecosystem-players)
  - [14.1 Greenfield Validators](#141-greenfield-validators)
  - [14.2 Storage Providers (SPs)](#142-storage-providers-sps)
  - [14.3 Greenfield dApps](#143-greenfield-dapps)
- [15 User Identifier](#15-user-identifier)
  - [15.1 User Balance](#151-user-balance)
- [16 Greenfield Blockchain](#16-greenfield-blockchain)
  - [16.1 Token Economics](#161-token-economics)
  - [16.2 Consensus and Validator Election](#162-consensus-and-validator-election)
  - [16.3 Governance Transactions](#163-governance-transactions)
    - [16.3.1 Create and Edit Validator](#1631-create-and-edit-validator)
    - [16.3.2 Staking Reward Distribution](#1632-staking-reward-distribution)
    - [16.3.3 Create Storage Provider](#1633-create-storage-provider)
    - [16.3.4 Remove Storage Provider](#1634-remove-storage-provider)
- [17 Storage MetaData Models](#17-storage-metadata-models)
  - [17.1 Bucket](#171-bucket)
  - [17.2 Object](#172-object)
  - [17.3 Group](#173-group)
  - [17.4 Permission](#174-permission)
    - [17.4.1 Ownership](#1741-ownership)
    - [17.4.2 Permission Definitions](#1742-permission-definitions)
    - [17.4.3 Permission Removal](#1743-permission-removal)
    - [17.4.4 Examples](#1744-examples)
- [18 Payload Storage Management](#18-payload-storage-management)
  - [18.1 Segments](#181-segments)
  - [18.2 Erasure Code and Data Redundancy](#182-erasure-code-and-data-redundancy)
    - [18.2.1 Data Redundancy Design](#1821-data-redundancy-design)
    - [18.2.2 Erasure Code](#1822-erasure-code)
      - [18.2.2.1 Encoding](#18221-encoding)
      - [18.2.2.2 Decoding: Data Recovery](#18222-decoding-data-recovery)
- [19 Data Availability Challenge](#19-data-availability-challenge)
  - [19.1 The Initial Data Integrity and Redundancy Metadata](#191-the-initial-data-integrity-and-redundancy-metadata)
  - [19.2 Data Availability Challenge Process](#192-data-availability-challenge-process)
- [20 Storage Transactions](#20-storage-transactions)
- [21 Billing and Payment](#21-billing-and-payment)
  - [21.1 Concepts and Formulas](#211-concepts-and-formulas)
    - [21.1.1 Terminology](#2111-terminology)
    - [21.1.2 Formula](#2112-formula)
    - [21.1.3 Types and Interfaces](#2113-types-and-interfaces)
  - [21.2 Key Workflow](#212-key-workflow)
    - [21.2.1 Deposit and Withdrawal](#2121-deposit-and-withdrawal)
    - [21.2.2 Payment Stream](#2122-payment-stream)
    - [21.2.3 Forced Settlement](#2123-forced-settlement)
    - [21.2.4 Payment Account](#2124-payment-account)
    - [21.2.5 Account Freeze and Resume](#2125-account-freeze-and-resume)
    - [21.2.6 Storage Fee Price and Adjustment](#2126-storage-fee-price-and-adjustment)
- [22 Cross-Chain Models](#22-cross-chain-models)
  - [22.1 Communication Channels and Packages](#221-communication-channels-and-packages)
    - [22.1.1 Vote Poll](#2211-vote-poll)
    - [22.1.2 Channel and Sequence](#2212-channel-and-sequence)
    - [22.1.3 Reliability Protocol](#2213-reliability-protocol)
    - [22.1.4 Validator Update](#2214-validator-update)
  - [22.2 Economic](#222-economic)
    - [22.2.1 Fee and Reward of Cross-Chain Packages](#2221-fee-and-reward-of-cross-chain-packages)
    - [22.2.2 Race to Deliver Cross-Chain Packages](#2222-race-to-deliver-cross-chain-packages)
    - [22.2.3 Callbacks and Limited Gas](#2223-callbacks-and-limited-gas)
    - [22.2.4 Cross-Chain Infrastructure Contracts on BSC](#2224-cross-chain-infrastructure-contracts-on-bsc)
  - [22.3 Error and Failure Handling](#223-error-and-failure-handling)
- [23 SP APIs](#23-sp-apis)
  - [23.1 Universal Endpoint](#231-universal-endpoint)
    - [23.1.1 URI Standard](#2311-uri-standard)
    - [23.1.2 HTTPS REST API](#2312-https-rest-api)
    - [23.1.3 P2P RPC](#2313-p2p-rpc)
  - [23.2 List Operations](#232-list-operations)

This part of the whitepaper is the most detailed so it is subject to frequent changes. It should be highlighted here and
widely understood that the content in the part will be continuously updated, much more frequently than the other parts,
with either new sections added or existing sections revised.

## 14 Ecosystem Players

There are several player roles for the whole Greenfield ecosystem.

<div align="center"><img src="./assets/14.1%20All%20Players%20of%20Greenfield.jpg"></div>
<div align="center"><i>Figure 14.1: All Players of Greenfield</i></div>

### 14.1 Greenfield Validators

As a PoS blockchain, the Greenfield blockchain has its own validators.
These validators are elected based on the Proof-of-Stake logic.

These validators are responsible for the security of the Greenfield
blockchain. They get involved in the governance and staking of the
blockchain. They form a P2P network that is similar to other PoS
blockchain networks.

Meanwhile, they accept and process transactions to allow users to
operate their objects stored on Greenfield. They maintain the metadata
of Greenfield as the blockchain state, which is the control panel for
both Storage Providers (SPs) and users. These two parties use and update
these states to operate the object storage.

Greenfield validators also have the obligation to run the relayer system
for cross-chain communication with BSC.

The network topology of Greenfield validators is similar to the existing
secure validator setup of PoS blockchains. "Sentry Nodes" are used to
defend against DDoS and provide a secure private network, as shown in
the below diagram.

<div align="center"><img src="./assets/14.2%20Greenfield%20Blockchain%20Network.jpg"></div>
<div align="center"><i>Figure 14.2: Greenfield Blockchain Network</i></div>

### 14.2 Storage Providers (SPs)

Storage Providers are professional individuals and organizations who run
a series of services to provide data services based on the Greenfield
blockchain.

Each SP should have a good connection with the Greenfield network by
maintaining its own local full node so that it can watch the state
change directly, index data properly, and send transaction requests
timely.

Different SPs are interconnected as well via both REST APIs and a P2P
network while providing services to users by responding to their
requests in REST APIs or P2P RPCs.

The typical network topology of connected SPs is as the below figure.

<div align="center"><img src="./assets/14.3%20Greenfield%20Storage%20Provider%20Network.jpg"></div>
<div align="center"><i>Figure 14.3: Greenfield Storage Provider Network</i></div>

SPs may provide plenty of convenient services for users and dApps to get
data about Greenfield.

### 14.3 Greenfield dApps

Greenfield dApps are applications that provide functions based on
Greenfield storage and its related economic traits to solve some
problems of their users.

These dApps may interact with Greenfield or interact with both the
Greenfield blockchain and the SPs, or most commonly, interact with
Greenfield blockchain, SPs, and BSC.

The dApps can read data from all these data sources to facilitate
users' interaction with the smart contracts and navigate them through
the different kinds of use case scenarios.

In Greenfield, similar to other decentralized environments, dApps don't
need to ask for registration but communicate with users' wallets to get
users' instructions and other information.

## 15 User Identifier

Each user has their own address as the identifier for his/her account.
The addresses can create objects to store on Greenfield, bear and manage
the permissions, and pay fees.

Greenfield defines its account in the same format as BSC and Ethereum.
It starts with ECDSA secp256k1 curve for keys and is compliant with
[EIP84](https://github.com/ethereum/EIPs/issues/84) for
full
[BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki)
paths. The root HD path for Greenfield-based accounts is
m/44'/60'/0'/0. In the readable presentation, a Greenfield address is
a 42-character hexadecimal string derived from the last 20 bytes of the
public key of the controlling account with 0x as the prefix.

With this compatible address scheme, the users can reuse existing
accounts and infrastructure from BSC on Greenfield. For example, they
can use TrustWallet and Metamask (or other compatible wallets) to
deposit their BNB from BSC to Greenfield and interact with dApps on
Greenfield. It is also easy to identify the same owner by referring to
the same addresses on both BSC and Greenfield.

Greenfield blockchain is an application-specific chain without EVM, the
transaction data structure and API are different from BSC. Greenfield
will not support full functions in existing wallets, e.g. Transfer, Send
Transactions, etc. But it will enable the existing wallets to sign
transactions with the
[EIP712](https://eips.ethereum.org/EIPS/eip-712) standard.
This standard allows wallets to display data in signing prompts in a
structured and readable format. This is an
[example](https://medium.com/metamask/eip712-is-coming-what-to-expect-and-how-to-use-it-bb92fd1a7a26)
of how to use it in Metamask. Eventually, wallets will start supporting
Greenfield directly.

### 15.1 User Balance

The user identifier is mapped to an account in the ledger of Greenfield.
The account can hold a balance of BNB. These BNBs can be used to
participate in staking, pay for gas fees of Greenfield transactions, and
pay for Greenfield services.

This balance can be added via native BNB transfer on Greenfield, or
cross-chain transfer between Greenfield and BSC.

## 16 Greenfield Blockchain

As an independent blockchain, Greenfield blockchain is built on Cosmos
SDK and the Tendermint library. It runs in a similar fashion as other
PoS blockchains that are based on the same framework.

### 16.1 Token Economics

BNB remains the main utility token on Greenfield.

BNB can be transferred from BSC to Greenfield blockchain, and vice
versa. It will be used to:

1. self-delegate and delegate as stake, which can earn gas rewards and
   may suffer slash for improper behaviors.

2. pay the gas to submit transactions on the Greenfield blockchain,
   which includes Greenfield local transactions or cross-chain
   transactions between Greenfield and BSC. This is charged at the
   time of transaction submission and dispatched to Greenfield
   validators, and potentially Greenfield Storage Providers for some
   transactions.

3. pay fees for the object storage and download bandwidth data package.
   This is charged as time goes and dispatched to Greenfield Storage Providers.

### 16.2 Consensus and Validator Election

As Proof-of-Stake is adopted in Greenfield, there will be a founding
validator set in the genesis state. These validators deposit their BNBs
on a BSC smart contract, which would be locked as their stakes. The new
validator can be voted by the majority of the current validators to join
in and gets elected as the active validator based on its delegation
size. Here are the steps for becoming a new validator:

1. Self-delegate

2. Initiate a proposal to become a validator.

3. Wait for the current validators to vote on this proposal.

4. Once the proposal has passed, the new validator would be created automatically.

A validator may not always be a member of the active validator set,
which will propose and produce blocks. Only the ones elected by the rank
of delegation size will be the active validators. The election happens
every block. The number of active validators is fixed and governed by
the existing validators.

It should be highlighted that the Greenfield validators are separated
from the Greenfield Storage Providers. The Greenfield validators are
responsible for generating Greenfield blocks, maintaining the Greenfield
blockchain security, challenging the data availability, and maintaining
cross-chain communication; while the Storage Providers are responsible
for storing the data objects and responding to downloading requests.
There is no strong binding relationship between them, although the same
organization can play two roles at the same time.

### 16.3 Governance Transactions

#### 16.3.1 Create and Edit Validator

To be a validator, the runner must self-delegate BNB, and then a
proposal should be submitted to get votes from the existing validators.
After the passing of the proposal, a transaction for creating the
validator should be submitted. The self delegation is required, and the
open delegation from other delegators will be also supported.

The validator creation logic should be changed later to reduce the
concern of Cartels.

Message MsgCreateValidator:

```go
type MsgCreateValidator struct {
    Description       Description
    Commission        CommissionRates
    MinSelfDelegation github_com_cosmos_cosmos_sdk_types.Int
    DelegatorAddress  string
    ValidatorAddress  string
    Pubkey            *types.Any
    Value             types.Coin
    PoposalId         uint64
}

```

A validator can edit its description and commission by submitting an
"Edit Validator" transaction. The CommissionRate will be verified as a
proper number.

Message MsgEditValidator:

```go
type MsgEditValidator struct {
    Description       Description
    ValidatorAddress  string
    CommissionRate    *github_com_cosmos_cosmos_sdk_types.Dec
    MinSelfDelegation *github_com_cosmos_cosmos_sdk_types.Int
}
```

#### 16.3.2 Staking Reward Distribution

Validators will receive transaction fees as the staking reward. The
rewards will be distributed passively. This is different from BNB Beacon
Chain, where the system will distribute the rewards automatically.
Validators can submit withdrawal requests to get all the up-to-date
transaction rewards, and when validators change commission rates or
quit, all the transaction rewards that are not withdrawn will also be
distributed.

In summary, the overall logic should be very similar to Cosmos 0.46,
except following changes:

1. a proposal is needed for creating a validator.

2. only self-delegation is allowed in the early stage.

3. no token mint/inflation in rewards.

#### 16.3.3 Create Storage Provider

Anyone can submit a storage provider creation proposal first, the current
active validators can vote on this proposal. After this proposal passes,
the new storage provider needs to submit a creating storage provider
transaction to become a storage provider.

Greenfield separates the roles of validator and storage providers.
Although it is natural for the validators to maintain a meaningful and
healthy number of storage providers, there should still be incentives
for the validators to manage a reasonable number of SPs. Validators
would get more data challenge rewards if there are more storage
providers, the payment flow that is used for data challenge rewards
would be like:

$$ data challenge reserves = (1 - \frac{1}{SP Number + 1}) * Maximum Percent $$

Data availability challenge will be covered in the later section.

#### 16.3.4 Remove Storage Provider

Anyone can submit a proposal to remove a storage provider, for the
storage provider doesn't provide a good service or prefers to stop
service. The current active validators can vote on this proposal. After
this proposal passes, other SPs or the data owners should start
requesting to move the data off this "to-be-removed" SP. The
"to-be-removed" SP has to facilitate the data moving so that it can get
the full deposit back and no further slash. Actually, even if it chooses
to not cooperate, the data can be recovered from the other SPs. After
all the data has been migrated, anyone can submit a removal storage
provider transaction to remove the storage provider.

## 17 Storage MetaData Models

The basic data models for Greenfield storage are:

- bucket

- object

- group

- permission

These metadata are stored as blockchain state into the persistent
storage of the Greenfield blockchain.

### 17.1 Bucket

Bucket is the unit to group storage "objects". BucketName has to be
globally unique. Every user account can create a bucket. The account
will become the "owner" of the bucket.

Each bucket should be associated with its own Primary SP, and the payment
accounts for Read and Right. The owner's address will be the default
payment account.

### 17.2 Object

Object is the basic unit to store data on Greenfield. The metadata for
the object will be stored on the Greenfield blockchain:

- name and ID

- owner

- bucket that hosts it

- size and timestamps

- content type

- checkSums for the storage pieces

- storage status

- associated SP information

Object metadata is stored with the bucket name as the prefix of the key.
It is possible to iterate through all objects under the same bucket, but
it may be a heavy-lifting job for a large bucket with lots of objects.

### 17.3 Group

A Group is a collection of accounts with the same permissions. The group
name is not allowed to be duplicated under the same user. However, a
group **can not create or own** any resource. A group **can not be a
member** of another group either.

A resource can only have a limited number of groups associated with it
for permissions. This ensures that the on-chain permission check can be
finished within a constant time.

### 17.4 Permission

Bucket, object, group are all resources (payment account is another type
of resource but is covered in the payment section later). Each resource
has a unique ID and the Permission Module uses these IDs to control how
the resources can be accessed.

#### 17.4.1 Ownership

The resources owner refers to the account that creates the resource. By
default, only the resource owner has permission to access its resources.

- The resource creator owns the resource.

- Each resource only has one owner and the ownership cannot be transferred once the resource is created.

- There are features that allow an address to "approve" another
  address to create and upload objects to be owned by the approver's address, as long as it is within limits.

- The owner or payment account of the owner pays for the resource.

#### 17.4.2 Permission Definitions

- Ownership Permission: By default, the owner has all permissions to the resource.

- Public or Private Permission: By default, the resource is
  ***private***, only the owner can access the resource.
  If a resource is ***public***, anyone can access it.

- Shared Permission: These permissions are managed by the permission
  module. It usually manages who has permission for which resources.

Each permission information is stored separately in a triple(E.g
"Resource + who + PermissionType") in the blockchain state.

#### 17.4.3 Permission Removal

Users can actively remove one or more permissions. However, when a
resource is deleted, its associated permissions should also be deleted,
perhaps not by the user taking the initiative to delete it, but by other
clean-up mechanisms. Because if too many accounts have permission to the
deleting object, it takes too much time to process within one
transaction handling.

#### 17.4.4 Examples

Typical permissions for the resources are listed below.

| Permission Type | Bucket                                    | Object                                  | Group                                        |
|-----------------|-------------------------------------------|-----------------------------------------|----------------------------------------------|
| Write           | ✅ Allow PutObject                         | ❌                                       | ✅ Allow AddMember                            |
| Read            | ✅ Allow ListObject                        | ✅ Allow GetObject                       | ✅ Allow ListMember As a member of this group |
| Full Control    | ✅ Allow Put/ListObject, Allow DeleteBucket | ✅ Allow GetObject, Allow DeleteObject   | ✅ Allow DeleteMember, Allow ListMember       |
| Execute         | ❌                                         | ✅ Allow Execute                         | ❌                                            |

Let's say Greenfield has two accounts, Bob(0x1110) and Alice(0x1111). A
basic example scenario would be:

- Bob uploaded a picture named avatar.jpg into a bucket named "profile";

- Bob grants the GetObject action permission for the object avatar.jpg to Alice,
  it will store a key 0x1 | ResourceID(profile_avatar.jpg) | 0x1111 into a permission state tree.

- when Alice wants to read the avatar.jpg, the SP should check the
  Greenfield blockchain that whether the key 0x1 | ResourceID(profile_avatar.jpg) | 0x1111 existed in the
  permission state tree, and whether the action list contains GetObject.

Let's move on to more complex scenarios:

- Bob created a bucket named "profile"

- Bob grants the PutObject action permission for the bucket "profile"
  to Alice, the key 0x0 | ResourceID(profile) | Address(Alice)
  will be put into the permission state tree.

- When Alice wants to upload an object named avatar.jpg into the
  bucket profile, it creates a PutObject transaction and will be
  executed on the chain.

- The Greenfield blockchain needs to confirm that Alice has permission
  to operate, so it checks whether the key 0x0 |
  ResourceID(profile) | Address(Alice) existed in the permission
  state tree and got the permission information if it existed.

- If the permission info shows that Alice has the PutObject action
  permission of the bucket profile, then she can do PutObject operation.

Another more complex scenario that contains groups:

- Bob creates a group named "Games", and creates a bucket named "profile".

- Bob adds Alice to the Games group, the key 0x0 | ResourceID(Games)
  | Address(Alice) will be put into the permission state tree

- Bob put a picture avatar.jpg to the bucket profile and grants the
  CopyObject action permission to the group Games

- When Alice wants to copy the object avatar.jpg . First, Greenfield
  blockchain checks whether she has permission via the key 0x0 |
  ResourceID(avatar.jpg) | Address(Alice); if it is a miss,
  Greenfield will iterate all groups that the object avatar.jpg
  associates and check whether Alice is a member of one of these
  groups by checking, e.g. if the key 0x0 | ResourceID(group, e.g.
  Games) | Address(Alice) existed to mirror the permission of the
  group to the member Alice.

## 18 Payload Storage Management

Although the metadata will be stored on the Greenfield blockchain, the
content data to be stored on Greenfield is here called "payload" and
they are stored off-chain, on the Storage Providers.

The unit of such storage is "Object", and each object is split and
stored in an integral and redundant way to ensure the availability.

### 18.1 Segments

Segment is the basic storage structure of an object. An object payload
is composed of one or many segments in sequence. The default segment
size is 16MB. If the object's size is less than 16MB, it has only one
segment and the segment size is the same as the object's size. For
larger objects, the payload data will be broken into segments.

Please note the payload data of an object will be split into the same
size segment but the last segment, which is the actual size. For
example, if one object has a size 50MB, only the size of the last
segment is 2 MB and the other segments' sizes are all 16MB.

<div align="center"><img src="./assets/18.1%20Object%20Segmentation.jpg"></div>
<div align="center"><i>Figure 18.1 Object Segmentation</i></div>

### 18.2 Erasure Code and Data Redundancy

#### 18.2.1 Data Redundancy Design

Although each SP may provide a more stable service and won't go offline
as enough BNB are staking to be one SP, Greenfield still establish its
own redundancy strategy to get rid of the dependency on a single SP and
support the data availability in a decentralized way. Here below is the
basic design idea.

First, all segments of each object are stored in primary SP as "pieces",
which can be regarded as one replica of the object. Users may download
this data directly from the primary SP as it is supposed to provide the
full data in a low latency way.

Second, Erasure Code (EC) is introduced to get efficient data
redundancy. Segment is the boundary to perform erasure encoding. By
erasure encoding one segment at a time, it allows streaming the
processing of the object upload without waiting for the whole object
payload to finish. The default EC strategy is 4+2, 4 data chunks, and 2
parity chunks for one segment. The data chunk size is ¼ of the segment.
As one typical segment is 16M, one typical data chunk of EC is 4M.
Specialized customization on EC parameters for each user may be provided
via special transactions.

All EC chunks of each object are stored in some secondary SPs as pieces,
which can be regarded as more than one EC replica of the object. If one
or more segments of the object are lost from the primary SP, any 4
chunks from 6 SPs can recover the segments.

All these segments and SPs information are stored on the Greenfield
blockchain as the metadata of the object. The same object's each
segment's EC replicas are stored in the same sequence of secondary SPs.
This convention is to save the metadata size. An example of a 50M object
stored with one primary SP, SP0, and 6 secondary SPs, SP1-SP6 is shown
in the below diagram.

<div align="center"><img src="./assets/18.2%20EC%20for%20Segments%20in%20Different%20Secondary%20SPs.jpg"></div>
<div align="center"><i>Figure 18.2 EC for Segments in Different Secondary SPs</i></div>

#### 18.2.2 Erasure Code

The EC module is defined as the following structure.

```go
type Erasure struct {
    encoder func () Encoder
    
    dataBlocks, parityBlocks int
    chunkSize                int64
}
```

The *encoder* indicated the EC algorithm function type. The *dataBlocks*
and *parityBlock* are the main parameters of the EC algorithm. The
*chunkSize* indicated the size of each shard after encodes. Considering
the application scenario of Greenfield, the *dataBlocks* is set to 4;
*parityBlocks* is 2; and the *chunkSize* is configured to 16MB which is
corresponding to the piece size. Reed-Solomon is used as the EC
algorithm. The EC module has an Encode function to split data and encode
it into 6 blocks (4 data blocks and 2 parity blocks) and a Decode
function to reconstruct data from blocks.

The EC module has two additional functions：

1. Automatic padding. If the size of the last block is not divisible by 4,
   the EC encoding module will add some padding data into the
   segment which is no more than 3 bytes;

2. Parallel processing based on shard size for the optimal speed.

##### 18.2.2.1 Encoding

Here is a detailed EC encoding setup.

<div align="center"><img src="./assets/18.3%20EC%20Encoding.jpg"></div>
<div align="center"><i>Figure 18.3 EC Encoding</i></div>

As the example shown in the figure above, the 50M payload of the object
will be split into segments(16M each) and each segment will be encoded
by the Encode function of the EC module. All the segments can be
processed concurrently. Each segment is encoded into 4 data blocks
(indicated by an orange rectangle)and 2 parity blocks (indicated in the
green rectangle).

If the size of the last segment is less than 16MB, it will be encoded as
an independent part. But if it is smaller than 500k, it will be
considered to be merged with the previous segment.

If the size of the last block is not divisible by 4, it will be added by
1-3 bytes by the automatic padding function of the EC module. After all
the segments have been encoded, we have got 16 pieces which are 16M, and
6 pieces which are 0.5M.

Both the users' client software and the primary SP are responsible for
encoding the EC. Client software may not upload the EC parity but only
the checksum for the primary SP to verify.

From the primary SP to the secondary SPs, each EC chunk is treated as a
piece object and a data stream is maintained for each secondary SP for
parallel processing. Pieces will be stored in a data structure as "piece
store" on different SPs. As a reference implementation, the key of the
piece object is *objId_s+segIndex\_ spIndex+ ECIndex* for each segment.
The *spIndex* can indicate which secondary will be forwarded to. The
*ECIndex* is the index of EC chucks, with which 0-3 are data blocks and
4-5 are parity blocks. For example, the piece called obj0Id_s1_sp1 is
the 2nd segment of the object and will be forwarded to SP1.

##### 18.2.2.2 Decoding: Data Recovery

When the primary SP loses some segment, it or other SPs can recover the
data via the EC chunks. As designed, the ECIndex with values 0-3 are
data blocks while 4-5 are parity blocks. There are two processing cases
to reconstruct the object payload:

1. All data blocks are fully stored in secondary SPs. The recovery
   initiator can just read the pieces which are data blocks
   sequentially and stitch them together;

2. Some data blocks have been lost by secondary SPs. The recovery
   initiator needs to read all the data blocks and parity blocks and
   use the Decode function of the EC module to recover the content of
   all the segments.

## 19 Data Availability Challenge

It is always the first priority of any decentralized storage network to
guarantee data integrity and availability. Many of the existing
solutions rely on intensive computing to generate proofs. However,
Greenfield chooses the path of social monitoring and challenges.

The holistic targets for Greenfield to ensure the storage provider(SP)
stores the data as expected are as the below:

a. The primary SP stores the correct object that the user uploaded.

b. The SP stores assigned pieces either as the role of primary SP or
secondary SP correctly, and the data pieces stored should not be
corrupted or falsified.

c. The redundant Erasing Code pieces stored in the secondary SPs can
recover the original segment stored in the primary SP.

A user needs to ensure that the object stored on Greenfield is really
his object without downloading the whole object and comparing the
contents. And also each SP should store the correct piece for each
object as required and this information should be verified on the
Greenfield blockchain. A special metadata structure is introduced for
every object for data challenges as the below:

```go
type ObjectInfo struct {
    …
    root         Hash  // primary SP object root, the hash of segments' hashes
    subRootList []hash //secondary SP object root, the hash of local pieces' hashes
    …
}
```

Each storage provider will keep a local manifest for the pieces of each
object that are stored on it. For the primary SP, the local manifest
records each segment's hashes. The "*root*" field of the object's
metadata in the above code stores the hash of the whole local manifest
of the primary SP, e.g. it is the "*PiecesRootHash(SP0)*" in the below
diagram. For the secondary SPs, the local manifest records each piece's
hashes, and the hash of their local manifest files are recorded in the
subRooList field in order, e.g. the 4th element of this list will store
the 4th secondary SP's "*PiecesRootHash(SP4)*" in the below diagram.

<div align="center"><img src="./assets/19.1%20Hashes%20for%20Data%20Integrity.jpg"></div>
<div align="center"><i>Figure 19.1 Hashes for Data Integrity</i></div>

These root hashes serve as the checksum for the data segments and
redundancy pieces.

### 19.1 The Initial Data Integrity and Redundancy Metadata

The user-side client software will perform some work:

1. Split the object file into segments if necessary;

2. Compute the root hash across all the segments;

3. Compute the EC and calculate the hashes for the parity pieces;

4. Send transactions to the Greenfield blockchain to request creating
   the object with the above information.

Besides sending the information to the Greenfield blockchain, the client
software also sends the same to the primary SP and uploads the payload
data onto it. For the primary SP stores the original segments of the
object, the SP has to verify the root hash to check the integrity of the
segment. The SP also has to compute the EC pieces by itself and verify
the hash. All the hashes will be recorded on a manifest file stored
locally with the SP, and the root hash of the file will be submitted to
the Greenfield blockchain in the "Seal" transaction. Greenfield
blockchain will verify the hashes in the Seal transaction against the
object creation request transaction to ensure data integrity as they are
the agreed value across Primary SPs and the users.

These hashes and the corresponding manifest files will be used to verify
the data in the data availability challenge as described below.

### 19.2 Data Availability Challenge Process

<div align="center"><img src="./assets/19.2%20Data%20Availability%20Challenge.jpg"></div>
<div align="center"><i>Figure 19.2 Data Availability Challenge</i></div>

This data availability challenge is illustrated in above figure 19.2.

The Greenfield validators have the responsibility to verify the data
availability from the SPs. They form a voting committee to execute this
task by the incentive of fees and potential fines (slashes) on SPs.

A multi-signing logic, e.g. BLS-based multi-sig, is used to reach
another level of off-chain consensus among the Greenfield validators.
When the validator votes for the data challenge, they co-sign an
attestation and submit on-chain.

The overall data availability challenge mechanism works as below:

1. Anyone can submit a transaction to challenge data availability. The
   challenge information will be written into the on-chain event
   triggered after the transaction is processed. This is the first
   type of challenge.

2. The second way to trigger the challenge is more common: at the end
   of the block process phase of each block, Greenfield will use a
   random algorithm to generate some data availability challenge
   events. All challenge information will be persisted on the chain
   until the challenge has been confirmed or expired.

3. Each validator should run an off-chain data availability check
   module. This program keeps tracking the on-chain challenge
   information and then initiates an off-chain data availability
   check. It checks whether a data piece is available in the
   specified SP in response to the challenge event, no matter whether
   the event is triggered by the individual challenger or the
   Greenfield chain itself. There are three steps to perform the
   check:

   a. Ask the challenged SP for this data piece and the local manifest
   of the object. If the expected data can't be downloaded, the
   piece should be regarded as unavailable.

   b. Compute the hash of the local manifest, and compare it with the
   related root hash that is recorded in the metadata of the
   object. If they are different, the piece should be regarded as
   unavailable.

   c. Compute the checksum hash of the challenged piece, and compare
   it with the related checksum that is recorded in the local
   manifest. If they are different, the piece should be regarded
   as unavailable.

   Any of the above "unavailable" cases will mark the challenge success
   that the data is unavailable, and the validator will vote
   "unavailable".

4. The validator uses its BLS private key to sign a data challenge vote
   according to the result. The data to vote should be the same for
   all validators to sign: it should include the block header of the
   block that contains the challenge, data challenge information, and
   the challenge result.

5. The validators should collect data challenge votes, aggregates the
   signatures, assembles data challenge attestation, and submits the
   vote when there are more than 2/3 validators that have reached an
   agreement, called "attestment". In order to solve the concern that
   validators may just follow the others' results and not perform the
   check themselves, a "commit-and-reveal" logic will be introduced.

6. Any validator can submit the attestation with its own vote and
   enough others' votes on-chain through a transaction and this data
   challenge attestation transaction will be executed and update the
   related states. The first validator who submits the attestation
   can get a submission reward, while the later submission will be
   rejected. The more votes the submitter aggregates, the more reward
   it can get. Besides the submission rewards, there are attestment
   rewards too. Only the validators whose votes wrapped into the
   attestation will be rewarded, so it may be that some validators
   voted, but their votes were not assembled by the validator, they
   won't get rewarded for this data availability challenges. Also for
   the different results, the rewards may be different: the
   "unavailable" result that slashes the SPs will get validators more
   rewards.

7. After a number of blocks, for example, 100 blocks, it is time to
   confirm the data availability challenge results even if the
   submissions of attestments haven't arrived. In such a case, the
   challenge will just expire with no further actions.

8. Once a case of data availability is successfully challenged, i.e.
   the data is confirmed not available with quality service, there
   will be a cooling-off period for the SPs to regain, recover, or
   shift this piece of data.

9. Once the cooling-off period time expires, this data availability can
   be challenged again, if this piece of data is still unavailable,
   the SP would be slashed again.

## 20 Storage Transactions

The Greenfield blockchain supports a series of transactions to create,
update, and delete the Greenfield resources.

The bucket and object creation transactions have to interact with the
SPs to ensure they are ready, while group and permission-related
operations do not require that.

The users should always create a bucket before they can store any
objects.

Greenfield bucket name follows the same naming specification as AWS S3
bucket name. It must be globally unique.

The CreateBucket transaction must have the below information:

- sender, which can be derived from the transaction signer

- bucket name

- the ID of the SP that the bucket and all objects under this bucket
  will use as the Primary SP

There is a corresponding DeleteBucket transaction. It requires that all
the objects under the bucket must be deleted first. As described in the
earlier section, the bucket owner can delete any object under his/her
bucket.

Object creation is described in Part 1. There is a corresponding
DeleteObject transaction. The deletion will tell Greenfield to refund
the reserved fees and reduce the payment stream.

There are group creation, deletion, and member management transactions.

There are transactions about permission creation and deletion, as they
are the cornerstone functionality for the economy.

More worthy of highlighting, all of these transactions can be triggered
via cross-chain infrastructure from BSC smart contracts and EOAs.

There are a few transactions about changing the Primary SP of users'
buckets. It will be asynchronous as the action may take some time based
on the number and size of the objects in the bucket. The bucket needs to
be "Sealed" again by the new Primary SP.

## 21 Billing and Payment

Greenfield will charge the users in two parts. Firstly, every
transaction will require gas fees to pay the Greenfield validator to
write the metadata on-chain. Secondly, the SPs charge the users for
their storage service. Such payment also happens on the Greenfield. This
section is about the latter: how such off-chain service fees are billed
and charged.

There are two kinds of fees for the off-chain service: object storage
fee and read package fee:

1. Every object stored on Greenfield is charged a fee based on its
   size, content type, and other parameters.

2. There is a free quota for users' objects to be read based on their
   size, content types, and more. If exceeded, i.e. the object data
   has been downloaded too many times, SP will limit the bandwidth
   for more downloads. Users can raise their data package level to
   get more download quota. Every data package has a fixed price.

As described in Part 1, the fees are paid on Greenfield in the style of
"Stream" from users to the SPs at a constant rate. The fees are charged
every second as they are used.

### 21.1 Concepts and Formulas

Streaming is a constant by-the-second movement of funds from a sending
account to a receiving account. Instead of sending payment transactions
now and then, Greenfield records the static balance, the latest update
timestamp, and flow rate in its payment module, and calculates the
dynamic balance with a formula using this data in the records. If the
net flow rate is not zero, the dynamic balance will change as time
elapses.

#### 21.1.1 Terminology

- **Payment Module:** This is a special module and ledger system
  managing the billing and payment on the Greenfield blockchain.
  Funds will be deposited or charged into it from users' balance or
  payment accounts in this Payment Module.

- **Stream Account**: The Payment Module has its own ledger for
  billing management. Users can deposit and withdraw funds into
  their corresponding "accounts" on the payment module ledger. These
  accounts are called "Stream Account", which will directly interact
  with the stream payment functions and bill the users for the
  storage and data service.

- **Payment Account**: Payment account has been discussed in other
  sections of Part 1 and Part 3 already. It is actually a type of
  Stream Account. Users can create different payment accounts and
  associate it with different buckets for different purposes.

- **Payment Stream:** Whenever the users add/delete/change a storage
  object or download a data package, they add or change one or more
  "payment streams" for that service provided by SPs.

- **Flow Rate**: The per-second rate at which a sender decreases its
  net outflow stream and increases a receiver's net inflow stream
  when creating or updating a payment stream.

- **Netflow Rate**: The per-second rate that an account's balance is
  changing. It is the sum of the account's inbound and outbound
  flow rates.

- **Sender**: The stream account that starts the payment stream by
  specifying a receiver and a flow rate at which its net flow
  decreases.

- **Receiver**: The stream account on the receiving end of one or more payment streams.

- **CRUD Timestamp**: The timestamp of when the user creates, updates,
  or deletes a payment stream.

- **Delta Balance**: The amount of the stream account's balance has
  changed since the latest CRUD timestamp due to the flow. It can be
  positive or negative.

- **Static Balance**: The balance of the stream account at the latest
  CRUD timestamp.

- **Dynamic Balance**: The actual balance of a stream account. It is
  the sum of the Static Balance and the Delta Balance.

When a user's stream account is initiated in the payment module by
deposit, several fields will be recorded for this stream account:

- CRUD Timestamp - will be the timestamp at the time.

- Static Balance - will be the deposit amount.

- Netflow Rate - will be 0.

- Buffer Balance - will be 0.

#### 21.1.2 Formula

*Static Balance = Initial Balance at latest CRUD timestamp*

*Delta Balance = Netflow Rate \* Seconds elapsed since latest CRUD timestamp*

*Current Balance = Static Balance + Delta Balance*

*Buffer Balance = - Netflow Rate \* pre-configed ReserveTime if Netflow Rate is negative*

<div align="center"><img src="./assets/21.1%20How%20a%20User%20Receives%20Inflow%20and%20Outflow%20of%20Funds.jpg"></div>
<div align="center"><i>Figure 21.1 How a User Receives Inflow and Outflow of Funds</i></div>

Every time a user creates, updates, or deletes a payment stream, many
variables in the above formulas will be updated and the users' stream accounts in the
payment module will be settled.

- The net flow for the user's stream account in the payment module
  will be re-calculated to net all of its inbound and outbound flow
  rates by adding/removing the new payment stream against the
  current NetFlow Rate. E.g. when a user creates a new object whose
  price is \$0.4/month, its NetFlow Rate will add -\$0.4/month.

- If the NetFlow rate is negative, the associated amount of BNB will
  be reserved in a buffer balance. It is used to avoid the dynamic
  balance becoming negative. When the dynamic balance becomes under
  the threshold, the account will be forced settled.

- CRUD Timestamp will become the current timestamp.

- Static Balance will be re-calculated. The previous dynamic balance
  will be settled. The new static Balance will be the Current
  Balance plus the change of the Buffer Balance.

#### 21.1.3 Types and Interfaces

```go
type PaymentConfig struct {
    // Time duration which the buffer balance need to be reserved for NetOutFlow e.g. 6 month
    ReserveTime      uint64
    // Time duration threshold of forced settlement.
    // If dynamic balance is less than NetOutFlowRate * forcedSettleTime, the account can be forced settled.
    ForcedSettleTime uint64
}
```

```go
type StreamPayment struct {
    CRUDTimestamp uint64
    NetflowRate   int64
    StaticBalance uint64
    BufferBalance uint64 // reserved balance for a period, e.g. 1 day
}
```

```go
type PaymentKeeperI interface {
    GetStorePrice(replicaNum, size uint64) (uint64, error)
    GetReadPackagePrice(packageType ReadPackageType) (uint64, error)
    UpdatePaymentFlow(from, to Address, rate int64) error
    LiquidateAccount(addr Address) error
}
```

### 21.2 Key Workflow

#### 21.2.1 Deposit and Withdrawal

All users(including SPs) can deposit and withdraw BNB in the payment
module. The StaticBalance in the StreamPayment data struct will be
"settled" first: the CRUDTimeStamp will be updated and StaticBalance
will be netted with DeltaBalance. Then the deposit and withdrawal number
will try to add/reduce the StaticBalance in the record. If the static
balance is less than the withdrawal amount, the withdrawal will fail.

Deposit/withdrawal via cross-chain will also be supported to enable
users to deposit/withdraw from BSC directly.

Specifically, the payment deposit can be triggered automatically during
the creation of objects or the addition of data packages. As long as
users have assets in their address accounts and payment accounts, the
payment module may directly charge the users by moving the funds from
address accounts.

#### 21.2.2 Payment Stream

Payment streams are flowing in one direction. Whenever the users deposit
from their address accounts into the stream accounts (including users'
default payment account and other payment accounts), the funds first go
from the users' address accounts to a system account maintained by the
Payment Module, although the fund size and other payment parameters will
be recorded on the users' stream account, i.e. the StreamPayment record,
in the Payment Module ledger. When the payment is settled, the funds
will go from the system account to SPs' address accounts according to
their in-flow calculation.

Every time users do the actions below, their StreamPayment record will
be updated:

- Creating an object will create a new stream to the system account

- Deleting an object will delete a stream to the system account

- Adjusting the data packages for read/download will
  create/delete/update the associated streams

The stream from the system account to storage providers will be updated
together when the users do the above actions. The in-flow flow rate of
SP will be recorded accurately in the payment module as well, such as
the total size stored(as primary or secondary SP), etc. The total
inbound flow will be split among the SPs according to the records.

#### 21.2.3 Forced Settlement

If a user doesn't deposit for a long time, his previous deposit may be
all used up for the stored objects. Greenfield has a forced settlement
mechanism to ensure enough funds are secured for further service fees.

There are two configurations, ReserveTime and ForcedSettleTime. Let's say
7 days and 1 day. If a user wants to store an object at the price of
approximately $0.1 per month($0.00000004/second), he must reserve fees
for 7 days in buffer balance, which is `$0.00000004 * 7 * 86400 =
$0.024192`. If the user deposits $1 initially, the stream payment
record will be as below.

- CRUD Timestamp: 100

- Static Balance: $0.975808

- Netflow Rate: -$0.00000004/sec

- Buffer Balance: $0.024192

After 10000 seconds, the dynamic balance of the user is `0.975808 - 10000 * 0.00000004 = 0.975408`.

After 24395200 seconds(approximately 282 days), the dynamic balance of
the user will become negative. Users should have some alarms for such
events that remind them to supply more funds in time.

If no more funds are supplied and the dynamic balance plus buffer
balance is under the forced settlement threshold, the account will be
forcibly settled. All payment streams of the account will be closed and
the account will be marked as out of balance. The download speed for all
objects associated with the account or payment account will be
downgraded. The objects will be deleted by the SPs if no fund is
provided within the predefined threshold.

The forced settlement will also charge some fees which is another
incentive for users to replenish funds proactively.

Let's say the ForceSettlementTime is 1 day. After 24913601
seconds(approximately 288 days), the dynamic balance becomes `0.975808 -
24913601 *0.00000004 = -0.02073604`, plus the buffer balance is
$0.00345596. The forced settlement threshold is `86400* 0.00000004 =
0.003456`. The forced settlement will be triggered, and the record of the
user will become as below:

- CRUD Timestamp: 24913701

- Static Balance: \$0

- Netflow Rate: \$0/sec

- Buffer Balance: \$0

The validators will get the remaining $0.00345596 as a reward. The
account will be marked as "insufficient" and his objects get downgraded
by SPs.

Every time a stream record is updated, Greenfield calculates the time
when the account will be out of balance. So Greenfield can keep an
on-chain list to trace the timestamps for the potential forced
settlement. The list will be checked by the end of every block
processing. When the block time passes the forced settlement timestamp,
the settlement of the associated stream accounts will be triggered
automatically.

#### 21.2.4 Payment Account

Payment account is a special "Stream Account" type in the Payment
Module. Users can create multiple payment accounts and have the
permission to link buckets to different payment accounts to pay for
storage and data package.

The relevant data structures and interface are as the following:

```go
// PaymentAccountNum mapping
// key: PaymentAccountNumPrefix | Address
// value: uint64  // counter
// use cases:
// - record the number of payment accounts of a user
// - derive new payment account address from user address
// - PaymentAccountAddress = Hash(OwnerAddress | current_num), increased by 1 when create a new payment account

// key: PaymentAccountPrefix | Address
type PaymentAccount struct {
    Owner        Address
    Withdrawable bool
}

type PaymentKeeperI interface {
    Deposit(from, to Address, amount uint64) error
    Withdraw(from, to Address, amount uint64) error
    CreatePaymentAccount(addr Address) (paymentAccountAddr Address, err error)
    ForbidWithdraw(sender, paymentAccount Address) error
    SetBucketStorePayer(bucket BucketID, sender, payer Address) error
    SetBucketReadDataPayer(bucket BucketID, sender, payer Address) error
}
```

The payment accounts have the below traits:

- Every user can create multiple payment accounts. The payment
  accounts created by the user are recorded with a map on the
  Greenfield blockchain.

- The address format of the payment account is the same as normal
  accounts. It's derived by the hash of the user address and
  payment account index. The payment account only exists in the
  storage payment module. Users can deposit into, withdraw from and
  query the balance of payment accounts in the payment module, which
  means payment accounts cannot be used for transfer or staking.

- Users can only associate their buckets with their payment accounts
  to pay for storage and bandwidth. Users cannot associate their own
  buckets with others' payment accounts, and users cannot associate
  others' buckets with their own payment accounts.

- The owner of a payment account is the user who creates it. The owner
  can set it non-refundable. It's a one-way setting and can not be
  revoked. Thus users can set some objects as "public goods" which
  can receive donations for storage and bandwidth while preserving
  the ownership.

#### 21.2.5 Account Freeze and Resume

If a payment account is out of balance, it will be settled and set a
flag as out of balance.

The NetflowRate will be set to 0, while the current settings of the
stream pay will be backed up in another data structure. The download
speed for all objects under this account will be downgraded.

If someone deposits into a frozen account and the static balance is
enough for reserved fees, the account will be resumed automatically. The
stream pay will be recovered from the backup.

During the OutOfBalance period, no objects can be associated with this
payment account again, which results in no object can be created under
the bucket associated with the account.

If the associated object is deleted, the backup stream pay settings will
be changed accordingly to ensure it reflects the latest once the account
is resumed.

#### 21.2.6 Storage Fee Price and Adjustment

The object storage fee is calculated with a function of object metadata
and time. The unit of the price will be US dollars. The payment actually
charged on Greenfield is BNB, and the price of BNB will be submitted by
the oracle.

For example, if the price is 0.03 USD / GB / month, the current BNB
price on-chain is 258 USD, 70% of the storage fee will be received by
the primary SP, and the rest are split by secondary SPs.

When an object of 123, 456, 789 bytes(approximately 123 MB) is sealed,
there will be 7 payment streams updated. The fee rate is `0.03 / 258 *
123456789 / (1024*1024*1024) / (30*24*60*60) = 5.158003812501789e-12`
BNB/second.

Let's set the rate as R.

- User -\> Primary SP flow rate: 0.7 \* R

- User -\> Secondary SP 1 flow rate: 0.05 \* R

- User -\> Secondary SP 2 flow rate: 0.05 \* R

- User -\> Secondary SP 3 flow rate: 0.05 \* R

- User -\> Secondary SP 4 flow rate: 0.05 \* R

- User -\> Secondary SP 5 flow rate: 0.05 \* R

- User -\> Secondary SP 6 flow rate: 0.05 \* R

The stream records of the payment accounts will be adjusted. If the
reserved time is 6 months, the user has to reserve `(R * 6 * 30 * 24 * 60 * 60) = 8.021727529202782e-05` BNB in
the Buffer Balance. If the balance of the payment account is not enough, either the trigger
transaction will fail or the account will be marked as "insufficient".

The BNB price will be submitted by an oracle from the Greenfield
validator relayers periodically. When the price updates, all payment
prices will be calculated with the latest price. But all the flow rates
of existing payments will remain unchanged until the next settlement,
triggered by either the user's new actions like putting a new object or
the auto-settlement.

The object storage fee price formula is expected to be steady since the
price unit is USD and the cost of storage changes slowly over time. The
formula might be flexible enough so it can be hard-coded on-chain.

There may be a chance the SPs want to change the formula(e.g. for
business model update). That will be achieved by SPs and validators'
coordinated governance.

## 22 Cross-Chain Models

The Cross-chain framework has been introduced in Part 1. Here more
details about the communication layer and economics will be explained.

### 22.1 Communication Channels and Packages

#### 22.1.1 Vote Poll

A new p2p communication across the cross-chain relayers will be
introduced, called "Vote Poll". This Vote Poll will gossip about the
signed votes within the network. To avoid message flooding, all the
signed votes will expire after a fixed time. The Greenfield relayers can
either put votes to or fetch votes from the poll and assemble it as
cross-chain package transactions.

#### 22.1.2 Channel and Sequence

To allow multiplexing and replay attack resistance, "Channel" and
"Sequence" concepts are introduced to manage any type of communication.
Following is an example definition:

```go
type Package struct {
    PackType     uint8 // SYN, ACK or FAIL_ACK
    SrcChainId   uint16
    DstChainId   uint16
    Sequence     int64
    ChannelId    uint16
    Payload      []byte
    BLSSignature sdk.Sig
    BLSBits      sdk.Bits // indicate the signer of the package
}
```

The packages in the same channel must be processed in sequence, while
they can be processed in parallel if they belong to different channels.

The operation messages on different Greenfield resources are mapped to
different channels. For example, buckets and storage objects belong to
different channels.

#### 22.1.3 Reliability Protocol

Here a protocol is defined to ensure reliable stream delivery of data
between BSC and Greenfield.

The protocol must recover the scenarios when the cross-chain data is
damaged, duplicated, or delivered out of order by the relayers. It
assigns a sequence number to each package and requires a positive
acknowledgment (ACK) from the target chain. Here there are three kinds
of packages:

1. SYN: the initial cross-chain packages started by either users or dApps.

2. ACK: the positive acknowledgment sent by the resource layer of the
   target chain.

3. FAIL_ACK: the negative acknowledgment sent by the communication
   layer of the target chain, usually caused by damaged data or
   protocol inconsistency triggered by the edge case.

Each communication package must start with SYN and end with ACK or
FAIL_ACK. The handler code and contracts on each side must handle these
primitives.

#### 22.1.4 Validator Update

With an aggregatable multi-signature scheme, e.g. BLS, the cross-chain
can be quite light-weighted. However sufficient data must be appended
onto the package to indicate the validators who sign the events, this
can be achieved by combining a bitmap and a validator set on-chain.
However the Greenfield validator set is volatile, Greenfield validators
have to sync the information to BSC once there is an update about the
Greenfield validator set. This is implemented by building a Greenfield
light client on BSC, which is similar to the light client implemented
for BNB Beacon Chain on BSC.

### 22.2 Economic

The Greenfield relayers play an important role in relaying inter-chain
packages. A proper incentive is required to keep relayers making their
long-term contribution.

#### 22.2.1 Fee and Reward of Cross-Chain Packages

Both SYN and ACK/FAIL_ACK packages cost gas to relay, the users (or
smart contracts) will need to pay the fee to cover both of them when
they start the SYN cross-chain packages.

To encourage Greenfield relayers to sign cross-chain packages:

1. The package deliverer will get a fixed ratio of the relay fee as a reward.

2. The rest relay fee will be distributed equally among those who sign the vote.

#### 22.2.2 Race to Deliver Cross-Chain Packages

There are multiple Greenfield relayers, and they may compete to submit
the aggregated multi-signed packages onto the Greenfield blockchain and
BSC. To avoid racing transactions caused by the competition, which
wastes gas, the relayers are rotated to relay transactions, e.g. taking
shifts every 10 minutes. Each cross-chain package gets a timestamp, if
it is not relayed within a limited delay when the designated relayer
doesn't perform the duty, any other Greenfield relayers are allowed to
relay such a package.

#### 22.2.3 Callbacks and Limited Gas

BSC dApps, i.e. smart contracts on BSC, are allowed to implement their
own logic to handle ACK or FAIL_ACK packages. The smart contracts can
register callback functions to handle the ACK packages. As it is
impossible for the cross-chain infrastructure to predict the gas
consumption of the callback, a gas limitation estimate should be defined
from the smart contracts that register the callbacks.

For any cross-chain packages that start from BSC, the smart contract
needs to specify the gas limitation for the ACK or FAIL_ACK package, the
relayer fee is prepaid accordingly on BSC. Relayers may refund the
excessive fees later.

#### 22.2.4 Cross-Chain Infrastructure Contracts on BSC

The cross-chain logic is also implemented on Greenfield as smart
contracts. But these contracts will not be implemented on BSC as the
genesis contract anymore, but just upgradeable contracts. The upgrade
will be controlled by the agreement of the Greenfield validators through
a governance process. The design can take full advantage of normal
contracts, such as working around the 24k size limitation by delegating
different logic to different implementation contracts.

### 22.3 Error and Failure Handling

There are errors and failures that can happen during cross-chain
communication.

One type of error is from the cross-chain protocol itself and is marked
by "FAIL_ACK". This means the protocol itself meets some fatal errors,
and it cannot complete the cross-chain package transport even before it
touches the layer above the communication layer. It is usually caused by
system bugs that result in data corruption or inconsistency.

The other type is the error above the communication layer, for example,
the errors triggered by improper logic or bugs in the resource mirror
layer or the application layer. Such cases should still return "ACK" at
the communication layer, but the ACK package should contain enough
information for the resource mirror layer or the application layer to
recover to the original state.

<div align="center"><img src="./assets/22.3%20Error%20and%20Failure%20Handling.jpg"></div>
<div align="center"><i>Figure 22.1 Cross-chain Error and Failure Handling</i></div>

When Greenfield emits an ACK or FAIL_ACK package, the registered
callbacks of BSC dApps (i.e. the smart contracts) will be called up to
handle the package, but these functions may fail to handle the
ACK/FAIL_ACK packages due to the bugs or exceptions in the callbacks,
these packages will be put under in another queue that belongs to the
BSC dApps.

The corresponding BSC dApps can retry the package, e.g. with a higher
gas limit, or just skip the package to tolerate failure, or even upgrade
its contract to handle corner cases. The BSC dApps can not start new
cross-chain packages if there are any pending failed packages in their
queue. It asks the BSC dApps must handle the failed packages in
sequence.

The communication layer can catch any exception thrown by the middle or
application layer, so that package delivery won't be blocked by any
customized applications.

## 23 SP APIs

SP should provide plenty of APIs to facilitate users to look up
information, download the objects, recover the data, and send
transactions onto the Greenfield blockchain. This section will be
extended as time goes on.

All SPs should provide APIs listed in this section.

### 23.1 Universal Endpoint

#### 23.1.1 URI Standard

All objects can be identified and accessed via a universal path:

*gnfd://\<bucket_name\>/\[prefix\]/\<other prefixes\>\[0..n\]/object-id*

*where:*

- *"gnfd://" is the fixed leading identifier, which is mandatory*

- *bucket_name is the bucket name of the object, which is mandatory*

- *prefix and other prefixes are all prefixes defined for the object, which are optional*

- *object-id is the ID for the object, which is mandatory*

This path should be 1:1 mapped to an object.

#### 23.1.2 HTTPS REST API

Each SP will register multiple endpoints to access their services, e.g.
"SP1" may ask their users to download objects via
[https://greenfield.sp1.com/download](https://greenfield.sp1.com/download).

The most important endpoint is the one for users to download objects. To
download an object, users can just substitute the "gnfd://" in the URI
standard with the SP endpoint. For example, to access
gnfd://mybucket/foo/bar/my-cool-object-id, users can just visit SP1 at
[https://greenfield/sp1.com/download/mybucket/foo/bar/my-cool-object-id](https://greenfield/sp1.com/download/mybucket/foo/bar/my-cool-object-id).

When SP1 receives the request to this path, SP1 should understand the
users want to download the object at
gnfd://mybucket/foo/bar/my-cool-object-id. SP1 should first get which SP
is the current primary SP of this object, if it's SP1 herself, SP1
should start sending the data to the user; otherwise, SP1 will send an
HTTP 302 to redirect the request to the primary SP's download endpoint.

#### 23.1.3 P2P RPC

Please note that both Greenfield blockchain full nodes (including
validators) and SPs will provide P2P RPCs to access different data.

Greenfield blockchain full node RPC will be access points to read and
change the blockchain data, e.g. users can check the current block
height and validator set information, or send transactions to create a
bucket.

SP P2P RPCs are under a different P2P protocol mostly for data reading,
which is designed based on the BitTorrent protocol. Any client software
that wants to use this feature must build in this P2P protocol.

One thing to note is that Greenfield enforces permission and access
control so that the data forwarded to the P2P network should be
encrypted with the users' public keys.

### 23.2 List Operations

There are multiple operations related to "list" some information about
Greenfield. For example, list all objects under a bucket, list all the
members in a group or list all the objects associated with a payment
account. These operations are usually too heavy to be supported directly
via a Greenfield blockchain full node RPCs. Here SPs should provide
these functions via corresponding APIs so that the users have a better
experience to store, check, download, and manage the objects.

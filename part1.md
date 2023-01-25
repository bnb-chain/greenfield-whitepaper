# Part 1 Design of the BNB Greenfield and the Decentralized Storage Economy

## Table of Content

- [1 Design Principles](#1-design-principles)
- [2 Assumptions](#2-assumptions)
- [3 The Architecture in General](#3-the-architecture-in-general)
  - [3.1 Greenfield Core](#31-greenfield-core)
  - [3.2 BNB Greenfield dApps](#32-bnb-greenfield-dapps)
  - [3.3 The Cross-Chain with BSC](#33-the-cross-chain-with-bsc)
  - [3.4 The Trinity](#34-the-trinity)
- [4 BNB Greenfield Core](#4-bnb-greenfield-core)
  - [4.1 The BNB Greenfield Blockchain](#41-the-bnb-greenfield-blockchain)
  - [4.2 The Storage Providers, SPs](#42-the-storage-providers-sps)
  - [4.3 The Pair Synergy](#43-the-pair-synergy)
- [5 The Greenfield Data Storage](#5-the-greenfield-data-storage)
  - [5.1 Data with Consensus](#51-data-with-consensus)
    - [5.1.1 Accounts and Balance](#511-accounts-and-balance)
    - [5.1.2 Validator and SP Metadata](#512-validator-and-sp-metadata)
    - [5.1.3 Storage Metadata](#513-storage-metadata)
    - [5.1.4 Permission Metadata](#514-permission-metadata)
    - [5.1.5 Billing Metadata](#515-billing-metadata)
  - [5.2 Off-Chain Payload Object Data Storage](#52-off-chain-payload-object-data-storage)
    - [5.2.1 Primary and Secondary SPs](#521-primary-and-secondary-sps)
    - [5.2.2 Data Redundancy](#522-data-redundancy)
- [6 Storage Economics and Its Primitives](#6-storage-economics-and-its-primitives)
  - [6.1 Account Creation](#61-account-creation)
  - [6.2 Data Object Creation](#62-data-object-creation)
  - [6.3 Data Storage](#63-data-storage)
  - [6.4 Data Read and Download](#64-data-read-and-download)
  - [6.5 Permissions and Group](#65-permissions-and-group)
  - [6.6 Fees and Payments](#66-fees-and-payments)
  - [6.7 Data Integrity and Availability Challenge](#67-data-integrity-and-availability-challenge)
  - [6.8 Data Delete](#68-data-delete)
- [7 Economy of Data Assets](#7-economy-of-data-assets)
  - [7.1 Cross-Chain with BSC](#71-cross-chain-with-bsc)
  - [7.2 Framework](#72-framework)
  - [7.3 Communication Layer](#73-communication-layer)
  - [7.4 Resource Mirror Layer](#74-resource-mirror-layer)
    - [7.4.1 Resource Entity Mirror](#741-resource-entity-mirror)
    - [7.4.2 Cross-Chain Operating Primitives](#742-cross-chain-operating-primitives)
- [8 "Not" Ending for the Design](#8-not-ending-for-the-design)
  - [8.1 Acknowledgement](#81-acknowledgement)

Part 1 describes the general principles and considerations for the design of BNB Greenfield. It covers the architecture
and functionality analysis. Although the true model innovation is at the cross-chain with BSC, the unique storage
fundamentals are also important to highlight.

## 1 Design Principles

1. **Simplicity** - The design prefers this first principle over the other considerations. Simple solutions are not only
   easy to implement, run, maintain, and extend, but also friendly to software performance, which is a main goal of the
   design. For example, high computing-intensive proof, like what [Filecoin](https://filecoin.io/filecoin.pdf) adopts,
   is ruled out according to this principle.

2. **Upgradable and continuously evolving** - Perfect system at one go is not the goal of the design. We expect the
   whole architecture, different components, and even this whitepaper to evolve and get improved based on the community
   and market feedbacks and future technology development. The infrastructure should have "just enough" establishment to
   develop and upgrade as time goes on.

3. **Open platform** - The biggest lesson learned from the crypto industry and BNB ecosystem is that the community have
   the most talent and power to build more applications and infrastructure in different self-driven ways. The design
   should focus on the core platform and technical foundation that provide enough interface, tools, and other
   facilitation to the developer community to build upon them.

4. **Massive adoption** - The economy targets beyond the existing BNB Chain clients, but also traditional Web2 users and
   developers. The system design should try to be as compatible as possible with popular Web2 and Web3 standards.

5. **Decentralization is a journey** - Take the storage system as an example, there are two ends to the decentralization
   spectrum. On one extreme end, users have to create and store all their data on a single service supplier; on the
   other end, users can create and store their data on any household's computing terminal (it does not even have to be a
   desktop). The design will not force itself to be on the latter end right from day one. It picks up the simplest
   solution that moves the needle toward higher decentralization and will improve as time goes on. From this sense, the
   first step Greenfield goes ahead with is to provide the freedom to choose among plenty of service suppliers at any
   time with trivial costs because they own the data.

<div align="center"><img src="./assets/1%20Decentralization%20Spectrum.png"></div>
<div align="center"><i>Figure 1.1: Decentralization Spectrum</i></div>

## 2 Assumptions

The biggest assumption for the design is:

***Greenfield is an economically sustainable, service-oriented
ecosystem.***

By "self-sustained", it means that the service providers and
corresponding service consumers of Greenfield are rational; they
complement each other. The providers and the blockchain validators will
get paid a fair amount for the service they supply, while the users are
willing to pay for the service they use.

By "service-oriented", it means that the value was created in Greenfield
by providing service to the users of the ecosystem. It doesn't have
built-in value by itself.

The implicit assumption underlying these two traits is that the majority
of the providers and blockchain validators are reasonable entities and
individuals. They will not do evil given the profit they earn is larger
than the fortune they can plunder.

This is a self-justifiable trust for the whole ecosystem to exist: if a
substantial percentage of providers and blockchain validators do evil
and the ecosystem cannot heal itself by ruling out these malicious
players, the whole ecosystem will not be used and have no value to
existing. If that happens, nobody wins even for a short time.

With this implicit built-in trust assumed, many designs are simplified
as described in the below sections.

Another assumption is that both the service provider and consumer sides
would expect the actual "service contracts" between the two to allow
limited liability and provide exit options, even if the contracts are
carried out mostly by code. In consumers' interest, they do not want to
pay a large size of fund upfront and would like to choose a better
provider within the ecosystems or even outside whenever they want. On
the other side, in the service providers' interest, they do not want to
become a data wasteyard or help circulate any content against their own
principles.

The payment, data availability check, and a few other key features are
designed based on this assumption.

The last big assumption is that data has value and users will want to
extract this value with smart contract automation, privacy, and
transparency. This results in the considerable design for cross-chain
between BNB Greenfield and BNB Smart Chain (BSC). This should be the
most important assumption and hopefully close to the truth.

## 3 The Architecture in General

<div align="center"><img src="./assets/3%20Greenfield%20Economy%20General%20Architecture.png"></div>
<div align="center"><i>Figure 3.1: Greenfield Economy General Architecture</i></div>

The ecosystem of Greenfield is a "trinity" as shown in the above figure.

### 3.1 Greenfield Core

BNB Greenfield Core is the new system infrastructure described in depth
in this paper. It is the center of the new ecosystem of data. It has two
layers.

1. A new storage-oriented blockchain, and

2. A network composed of "storage providers".

The BNB Greenfield blockchain maintains the ledger for the users and the
storage metadata as the common blockchain state data. It has BNB,
transferred from BNB Smart Chain, as its native token for gas and
governance. BNB Greenfield blockchain also has its own staking logic for
governance.

Storage Providers (SP) are storage service infrastructures that
organizations or individuals provide and the corresponding roles they
play. They use Greenfield as the ledger and the single source of truth.
Each SP can and will respond to users' requests to write (upload) and
read (download) data, and serve as the gatekeeper for user rights and
authentications.

Initially, a number of validators, run either by the BNB community or
SPs, go through the genesis to launch BNB Greenfield, while a few SPs
will also launch the corresponding storage infrastructure and register
themselves onto the Greenfield blockchain. SPs form another P2P network
to provide the full feature set to applications and users to create,
store, read, and trade data while using Greenfield blockchain as the
metadata and ledger layer.

<div align="center"><img src="./assets/3.2%20BNB%20Greenfield%20Core.jpg"></div>
<div align="center"><i>Figure 3.2: BNB Greenfield Core</i></div>

BNB Greenfield blockchain and the SPs together comprise the center of
this new economy, which is actually a decentralized, object storage
system (with EVM connectivity as explained later).

In contrast to the centralized alternative, this object storage system
manages its data in two collaborative parts, on-chain, and off-chain.

The Greenfield blockchain contains two categories of states "on-chain":

1. Accounts and their BNB balance ledger

2. The metadata of the object storage system and SPs, the metadata of the objects stored on this storage system, and the
   permission and billing information associated with this storage system.

Greenfield blockchain transactions can change the above states. These
states and the transactions comprise the major economic data of BNB
Greenfield.

While the metadata is stored on-chain, the object storage system stores
all the object content data (the payload) off-chain, more precisely, on
SPs' off-chain systems in a decentralized and redundant way.

When users want to create and use the data on Greenfield, they may
interact with the BNB Greenfield Core Infrastructure via BNB Greenfield
dApps (decentralized applications).

### 3.2 BNB Greenfield dApps

BNB Greenfield dApps are new types of decentralized applications. They
can be the client toolings that facilitate users to interact with the
decentralized storage system, Greenfield Core Infra; or applications
that bring real values to users' real life by using Greenfield systems
as their infrastructure. These applications will use blockchain
addresses as user identifiers and interact with features and smart
contracts on the Greenfield blockchain, Greenfield SPs, and BSC.

There are data endpoints, transaction interfaces, P2P networks, and
corresponding SDKs to help developers to build BNB Greenfield dApps.

BNB Greenfield dApps should be part of the establishment of BNB Chain
infrastructure built mostly by the community and ecosystem partners.
They can be decentralized or centralized as they prefer.

Part 2 shows considerations through a list of BNB Greenfield dApp
showcases.

### 3.3 The Cross-Chain with BSC

There is a native cross-chain bridge between BSC and BNB Greenfield
blockchain. While the data can be created and read more cheaply on
Greenfield Core Infra, the relevant data operation can be transferred to
BSC and integrated with smart contract systems there, such as DeFi, to
create new business models.

### 3.4 The Trinity

From the viewpoint of BNB Greenfield dApps, these applications can help
users to create, read, and execute data on the BNB Greenfield,
Greenfield SPs, and BSC, and serve a purpose to users' needs.

From the viewpoint of BNB Greenfield Core Infrastructure, they accept
requests and observations from the Greenfield dApps on behalf of the
users, and also instructions from BSC to operate together for different
business scenarios.

From the viewpoint of BSC, they can accept transferred data assets from
BNB Greenfield, and provide more business scenarios via smart contracts
to new types of Greenfield dApps.

The users can interact with all parts of the trinity for different
purposes directly or/and indirectly.

## 4 BNB Greenfield Core

### 4.1 The BNB Greenfield Blockchain

BNB Greenfield blockchain uses Proof-of-Stake based on
Tendermint-consensus for its own network security. Blocks are created
every 2 seconds on the Greenfield chain by a group of validators.

BNB will be the gas and governance token on this blockchain. There is a
native cross-chain bridge between the Greenfield blockchain and BSC. The
initial BNB will be locked on BSC and re-minted on Greenfield. BNB and
data operation primitives can flow between Greenfield and BSC.

Total circulation of BNB will stay unchanged as it is now but flow among
BNB Beacon Chain, BSC, and Greenfield.

The validator election and governance are based on a proposal-vote
mechanism, which is revised based on Cosmos SDK's governance module:
anyone can create and propose to become a validator, and the election
into the active set will be based on the stake ranking (initially new
validators may request the existing validator set's votes to be
qualified for election). As validators will host all the critical
metadata and respond to all data operation transactions, they should run
professionally in terms of performance and stability.

To facilitate cross-chain operation and convenient asset management, the
address format of the Greenfield blockchain will be fully compatible
with BSC (and Ethereum). It also accepts EIP712 transaction signing and
verification. These enable the existing wallet infrastructure to
interact with Greenfield at the beginning naturally.

### 4.2 The Storage Providers, SPs

SPs play a different role from Greenfield validators, although the same
organizations or individuals can run both SPs and validators if they
follow all the rules and procedures to get elected.

SPs store the objects' real data, i.e. the payload data. Each SP runs its own object storage system. Similar to Amazon
S3 and other object store systems, the objects stored on SPs are immutable. The users may delete and re-create the
object (under the different ID, or under the same ID after certain publicly outgiving settings), but they cannot modify
it.

SPs have to register themselves first by depositing on the Greenfield
blockchain as their "Service Stake". Greenfield validators will go
through a dedicated governance procedure to vote for the SPs of their
election. SPs are encouraged to advertise their information and prove to
the community their capability, as SPs have to provide a professional
storage system with high-quality SLA.

SPs provide publicly accessible APIs for users to upload, download, and
manage data. These APIs are very similar to Amazon S3 APIs so that
existing developers may feel familiar enough to write code for it.
Meanwhile, they provide each other REST APIs and form another
white-listed P2P network to communicate with each other to ensure data
availability and redundancy. There will also be a P2P-based
upload/download network across SPs and user-end client software to
facilitate easy connections and fast data download, which is similar to
BitTorrent.

More SPs are welcome to ensure decentralization and data redundancy. But
too many SPs may make SPs unable to make enough to sustain the business.
Greenfield has an incentive design to make a proper number of SPs
available. While SPs can choose to stay with the network or leave.

When the SPs join and leave the network, they have to follow a series of
actions to ensure data redundancy for the users; otherwise, their
"Service Stake" will be fined. This is achieved through the data
availability challenge (described in detail in Part 3) and validator
governance votes.

### 4.3 The Pair Synergy

Greenfield validators and SPs form a pair synergy to provide the whole
storage service. Validators store the metadata and financial ledger with
consensus, while SPs provide real data storage and downloading.
Validators have the motivation to ensure enough good SPs to provide
decent service, while users and SPs rely on a stable and decentralized
Greenfield blockchain as a single source of truth on metadata.

## 5 The Greenfield Data Storage

The data stored on Greenfield has two main categories:

1. data with blockchain consensus - They are Greenfield blockchain data.
   All Greenfield validators have such active data in full (at least the latest state).
   Anyone can join the blockchain as full nodes to synchronize these data for free.

2. object payload data - object data for short. This is the data that users store on Greenfield.
   Such data has access control and requires fees to store.
   They are not stored on the blockchain but on enough instances of SPs off-chain.

### 5.1 Data with Consensus

These data are on-chain and can be only changed through transactions
onto the Greenfield blockchain. It has several types as described below.

#### 5.1.1 Accounts and Balance

Each user has their "Owner Address" as the identifier for their owner
account to "own" the data resources. There is another "payment account"
type dedicated to billing and payment purposes and owned by owner
addresses.

Both owner accounts and payment accounts can hold the BNB balance on
Greenfield. Users can deposit BNB from BSC, accept transfers from other
users, and spend them on transaction gas and storage usage.

#### 5.1.2 Validator and SP Metadata

These are the basic information about the Greenfield validators and
Greenfield SPs. SPs may have more information, as it has to publish
their service information for users' data operations. There should be a
reputation mechanism for SPs as well.

#### 5.1.3 Storage Metadata

The "storage metadata" includes size, ownership, checksum hashes, and
distribution location among SPs. Similar to AWS S3, the basic unit of
the storage is an "*object*", which can be a piece of binary data, text
files, photos, videos, or any other format. Users can create their
objects under their "*bucket*". A bucket is globally unique. The object
can be referred to via the bucket name and the object ID. It can also be
located by the bucket name, the prefix tag, and the object ID via
off-chain facilitations.

#### 5.1.4 Permission Metadata

Data resources on Greenfield, such as the data objects and the buckets,
all have access control, such as which address can create, read, list,
or even execute the resources, and which address can grant/revoke these
permissions.

Two other data resources also have access control. One is "Group". A
group represents a group of user addresses that have the same
permissions to the same resources. It can be used in the same way as an
address in the access control. Meanwhile, it requires permission too to
change the group. The other is "payment account". They are created by
the owner accounts.

Here the access control is enforced by the SPs off-chain. People can
test and challenge the SPs if they mess up the control. Slash and reward
will happen to keep the SPs sticking to the principles.

#### 5.1.5 Billing Metadata

Users have to pay fees to store data objects on Greenfield. While each
object enjoys a free quota to download by users who are permitted to,
the excessive download will require extra data packages to be paid for
the bandwidth. Besides the owner address, users can derive multiple
"Payment Addresses" to pay these fees. Objects are stored under buckets,
while each bucket can be associated with these payment addresses, and
the system will charge these accounts for storing and/or downloading.
Many buckets can share the same payment address. Such association
information is also stored on chains with consensus as well.

The payment of Greenfield is on a stream pay model, which will greatly
reduce the complexity to implement the billing logic - more described in
Part 3.

### 5.2 Off-Chain Payload Object Data Storage

The payload data of the object, i.e. the bytes comprising the data
files, photos, and videos, are stored off-chain in multiple SPs with a
data redundancy design. Each SP can have its edition of an object
storage system with a good SLA and high-performance interface to
interact with the users and other SPs.

#### 5.2.1 Primary and Secondary SPs

Among the multiple SPs that one object is stored on, one SP will be the
"Primary SP", while the others are "Secondary SP".

When users want to write an object into Greenfield, they or the client
software they use must specify the primary SP. Primary SP should be used
as the only SP to download the data. Users can change the primary SP for
their objects later if they are not satisfied with their service.

#### 5.2.2 Data Redundancy

After the users issue a "write" request, Primary SP should respond to
the client upload request to accept the user upload, verify the data
integrity, and store a full copy of the data object. After that, Primary
SP will chop the object data into segments, and compute a data
redundancy solution for these segments based on Erasure Coding (EC).
Then Primary SP or the users will select a few secondary SPs to store
these segment replicas and their EC parity pieces. This data
distribution communication will be done via the p2p network and REST
APIs among SPs.

The data redundancy setup is to ensure that even if the primary SP and a
few secondary SPs become unavailable at a later time, Greenfield can
still recover the full data.

## 6 Storage Economics and Its Primitives

In this section, the underlying economics and the operating primitives
are discussed aligned with the lifecycle of a data object. The below
primitives can be executed after the genesis of the Greenfield
blockchain and enough SPs have registered themselves and started working
properly.

### 6.1 Account Creation

To write a data object into Greenfield, the users must have an account,
or more specifically, an address on the BNB Greenfield blockchain. This
can be done by transferring some BNB either from other addresses on
Greenfield or from BSC.

This may be a special route that users can skip this step but issue the
"transfer and write" request directly from BSC. As Greenfield and BSC
share the same address protocol, this action de facto creates an account
on Greenfield with the same address on BSC.

### 6.2 Data Object Creation

Users must create "Buckets" before creating objects. Similar to the
"Bucket" concepts in AWS S3, "buckets" here are a data resource to group
data objects from a user. All the objects under the same bucket will be
stored on the same primary SP and downloadable from that SP. Users can
create many buckets and store their data objects in different ones.

Each bucket has a Primary SP associated with it, which means all the
objects under this bucket will use that SP as the Primary SP. If the
chosen Primary SP cannot serve the requests well, the user may choose to
migrate the bucket to another SP completely via an on-chain transaction.

Data object creation is performed in two phases.

1. Request phase:

   a. Users first sign a "write" request with the initial object metadata, such as the object name, the bucket name,
   size,
   checksum, and the segment information and the redundancy setup as mandatory fields, while optionally content type and
   the
   storage preference, etc. It is worth noting that the checksum, the segment information, and the redundancy setup (
   based on
   Erasure Code, discussed in Part 3) will be calculated by the client software first. The client software will directly
   upload the segments together with the hashes as checksums. The data may or may not be encrypted at the users' choice.

   b. This request should be forwarded to the primary SP. After the primary SP determines to accept the request to store
   the data
   as the primary SP, it acknowledges the client by signing the same transaction message.

   c. After getting the SP's acknowledgment, users can submit the
   transaction to declare the creation of the objection on Greenfield.

   d. Greenfield accepts the "create" request and locks fees from users.

2. Seal phase:

   a. Users start connecting to the primary SP and uploading their data. Users have to sign some messages in the
   hand-shaking
   stage for authentication purposes.

   b. Once the data uploading has finished, the primary SP will sign the "uploaded" confirmation to the users.

   c. The primary SP syncs with secondary SPs to set up the data redundancy, and then it signs a "Seal" transaction with
   the
   finalized metadata for storage. If the primary SP determines that it doesn't want to store the file due to whatever
   reason,
   it can also "SealReject" the request. If the primary SP cannot receive the uploaded file in time, it can also send a
   "CancelCreation" request to cancel the client requests.

   d. Greenfield processes the "Seal" or "SealReject" transaction to begin the storage life cycle for the object.

Users can still "CancelRequest" to give up the creation request and get partially refunded.

There are scenarios in which the primary SP doesn't cooperate with the user well: 1. The primary SP acknowledges the
upload request, but doesn't accept the upload in time; 2. the primary SP signs the “uploaded” confirmation but doesn't
seal the transaction in time. Greenfield expects the primary SP to finish the object creation by either “Seal” or
“SealReject” transaction in a predefined time window; otherwise, the primary SP will be punished with a fine. Primary SP
has no rational reasons to not acknowledge the upload request or doesn't seal in time, while the users have no rational
reasons to create the requests but do not upload in time either.

There may be a special case in which the "create" is triggered from BSC
as a cross-chain transaction, the primary SP cannot get requests
directly. The primary SP can observe such requests and perform other
actions in the same way.

### 6.3 Data Storage

Once a data object is "Sealed", the owner of the object has de facto
entered a contract with the SPs for the storage, in which case the
owners should pay fees for such storage and the SPs should guarantee the
data availability.

The data object owners always have the right to change the primary SP to
store their data, after settling the outstanding fees.

The SPs, especially the primary SPs, can also inform people to stop
storing the data, due to either their own opinions or decision. Both
other SPs and the owners can observe corresponding notifications. Other
SPs can voluntarily propose themselves to be successors to store the
data objects on Greenfield if the owners do not react to the
notification in a predefined time, as other SPs do like to take the
business.

### 6.4 Data Read and Download

By design, the bytes that are stored and downloaded later for the object
are exactly the same bytes that were originally uploaded. SPs may use
their encryption logic as they wish, but when the data is being
downloaded, it shows the same bytes as it was uploaded. Users may choose
their own encryption scheme or use the default one provided by the
client software if they want the data to be unrecognizable by SPs or any
others, even though SPs have the obligation to not circulate these data
out of users' instruction.

Data objects can be only read and downloaded by the addresses with
proper read permissions. The Primary SP of the objects is the main
source to download from. If Primary SP is not available, the owner and
Greenfield blockchain validators can challenge (described in Part 3) and
change the object's primary SP to recover the downloading.

Each object has a time-based traffic bandwidth quota, which is provided
free, i.e. nobody needs to pay for downloading a certain amount within a
certain period. It is expected that this quota can satisfy most of the
individual download needs as part of the normal usage conditions.

For extra bandwidth to download the object, someone has to pay for the
data package, which is covered in the payment section.

### 6.5 Permissions and Group

Permission is the main logic introduced in Greenfield to enable
potential business models.

The data resources, including the objects, buckets, payment accounts,
and groups, all have permissions related. These permissions define
whether each account can perform particular actions.

Group is a list of accounts that can be treated in the same way as a
single account.

Examples of permissions are:

- Put, List, Get, Delete, Copy, and Execute data objects;

- Create, Delete, and List buckets

- Create, Delete, ListMembersOf, Leave groups

- Create, Associate payment accounts

- Grant, Revoke the above permissions

These permissions are associated with the data resources and
accounts/groups, and the group definitions are stored on the Greenfield
blockchain publicly. Now they are in plain text. Later a privacy mode
will be introduced based on Zero Knowledge Proof technology.

One thing that makes the permission operation more interesting is that
they can be operated from BSC directly, either through smart contracts
or by an EOA.

### 6.6 Fees and Payments

<div align="center"><img src="./assets/6.6%20Payment%20Stream%20Flow.png"></div>
<div align="center"><i>Figure 6.1: Payment Stream Flow</i></div>

The storage fee will be charged on Greenfield in a steam payment style
like
*[Superfluid](https://docs.superfluid.finance/superfluid/protocol-overview/in-depth-overview/super-agreements/constant-flow-agreement-cfa)*
.

The fees are paid on Greenfield in the style of "Stream" from users to
receiver accounts at a constant rate. The fees are "charged" every
second as they are used.

There are two kinds of fees for Greenfield: object storage fee and data
package fee.

For storage, every object stored on Greenfield is charged at the price
calculated by size, replica numbers, a base price ratio, and other
parameters. Once the object is stored, the total charge of storage will
be mainly only related to time and the base price.

For data downloading, there is a free, time-based quota for each bucket
of users' objects. If it's exceeded, users can promote their data
package to get more quota. Every data package has a fixed price for the
defined period. Once the data package is picked, the total charge of
downloading will be only related to time and the data package price,
until the data package setting is changed again.

Here there is trust between the users and the SPs for data download. As
the extra downloading bandwidth will charge a fee and the download
journal is not fully stored on the Greenfield blockchain. SPs should
provide an endpoint interface for users to query the download billing
details with detailed logs and downloaders' signatures. If the users and
the SPs cannot agree on the bill, users may just select another Primary
SP.

By default, the object owner's address will be used to pay for the
objects it owns. But users can also create multiple "payment accounts"
and associate objects to different payment accounts to pay for storage
and bandwidth.

The address format of the payment account is the same as normal
accounts. It's derived by the hash of the user address and payment
account index. However, the payment accounts are actually only logical
ones and only exist in the storage payment module. Users can deposit
into, withdraw from and query the balance of payment accounts on the
Greenfield blockchain, but users cannot use payment accounts to perform
staking or other on-chain transactions. Payment accounts can be set as
"non-refundable". Users cannot withdraw funds from such payment
accounts.

Other users can also sponsor the payment by donating a "stream payment"
flow to selected "non-refundable" payment accounts. They can pause at
any time they want.

All the storage fees and data packages are priced and paid in BNB. There
are system parameters and price oracles from the Greenfield Relayers
(described below) to adjust the pricing based on the marketing
situation.

Once the payment accounts run out of BNB, the objects associated with
these payment accounts will suffer from a downgraded service of
downloading, i.e. the download speed and connection numbers will be
limited. Once the fund is transferred to the payment accounts, the
service quality can be resumed right away. If the service is not resumed
for a long time, it is the SPs' discretionary decision to clear the data
out, in a similar way to how SPs claim to stop services to certain
objects. In such a case, the data may be gone from Greenfield
completely.

### 6.7 Data Integrity and Availability Challenge

There are 3 aspects of data integrity, availability, and redundancy as
listed below:

1. The primary SP stores the correct object that the user uploaded.

2. The SP stores assigned data segments either as the role of primary
   SP or secondary SP correctly, and the data pieces stored should
   not be missing, corrupted, or counterfeit.

3. The Erasure Coding pieces stored in the secondary SPs can recover the original object stored in the primary SP.

The data integrity and redundancy should be first guarded by the
checksum and redundancy setup of the objects. They are part of the data
object metadata, which should be verified by the SPs and users when the
objects are created. This metadata will be stored on the Greenfield
blockchain as well.

Both Greenfield and SPs have to work together to ensure data integrity
and availability, especially for the above #2. Different from other
decentralized storage systems, here a "Proof-of-Challenge" is introduced
to build users' confidence that the data is stored well as promised.

Challengers can come from different stakeholders. Firstly, users can
submit challenge transactions; secondly, similar to users, SPs can
submit challenge transactions to other SPs; and lastly, Greenfield
blockchain will issue internal challenge events randomly as well.

The challenge can be triggered by Greenfield transactions or internal
events at the end of blocking. Once Greenfield validators observe such a
challenge, they should run a standard off-chain check against the data
from the SPs being challenged. These validators will vote for the
challenge results via an aggregated multisig via an off-chain P2P
network and submit them to the Greenfield blockchain. The failed result
for a challenge will slash the corresponding SPs. The submitter and
validators will get rewards for such challenges.

The data that failed the challenge will not be challenged within a
certain amount of time to give the SPs some time to recover.

Another section in Part 3 will cover the data availability challenges in
greater detail.

### 6.8 Data Delete

Users can request to delete their data objects. Greenfield will remove
the metadata from the blockchain state, while the primary SP should
respond to this request and drop all the replicas and redundant
segments. The payment stream will be closed with a reward rebate to
encourage the deletion.

## 7 Economy of Data Assets

The real power of the Greenfield ecosystem lies in that the platform is
not only designed to store the data, but also to support the creation of
value based on the data assets and its related economy.

The asset traits of the data are firstly established on the permissions,
e.g. the permission to read the data. When this right is disconnected
from the data itself, they become tradable assets and enlarge the value
of the data. This can be amplified when the data itself can be
executable (a new type of "Smart Code"), interact with each other, and
generate new data. This creates a lot of room to imagine building a new,
data-intensive, trustless computing environment.

Secondly, the data permissions can be transferred cross-chain onto BSC
and become digital assets there. This creates a variety of possibilities
to integrate these assets with the existing DeFi protocols and models on
BSC.

This gets even further enhanced by the smart contracts on BSC, which
enjoy the same address format as accounts on the Greenfield blockchain
and can be the owners of the data objects and inherit different
permissions. This will unleash many new business opportunities based on
the data and its operations.

### 7.1 Cross-Chain with BSC

The cross-chain model expects to achieve the following goals:

- integratable with the existing systems: try to reuse the current
  infrastructure and dApps as much as possible, such as NFT
  Marketplace, data indexing, and blockchain explorers.

- programmable: dApps can define how they want to wrap the assets from Greenfield.

- secure and recoverable.

The native cross-chain bridge is maintained and secured by the
validators of Greenfield, via a new relayer system based on an
aggregated multisig scheme (more details in the later sections).
Greenfield validators will run the relayers to facilitate the high
bandwidth and fast bridge.

BNB will be transferred from BSC to Greenfield as the first cross-chain
action. The initial validator set of Greenfield at the genesis will
first lock a certain amount of BNB into the "Greenfield Token Hub"
contract on BSC. This contract will also be used as part of the native
bridge for BNB transferring after the genesis. These initial locked BNB
will be used as the self-stake of validators and early days gas fees.

### 7.2 Framework

<div align="center"><img src="./assets/7.1%20Cross-chain%20Architecture.jpg"></div>
<div align="center"><i>Figure 7.1: Cross-chain Architecture</i></div>

The bottom layer is a cross-chain **Communication Layer**, which focuses
on primitive communication package handling and verification. The middle
layer implements the **Resource Mirror**. It is responsible for managing
the resource assets that are defined on Greenfield but mirrored onto
BSC. The top layer is the **Application Layer**, which are the smart
contracts implemented by community developers on BSC to operate the
mirrored resource entities with their primitives; Greenfield does not
have such a layer. The real dApps will have some part in this
Application Layer and also interact with Greenfield Core and all sorts
of supporting infrastructures.

Because of the asymmetric framework, BSC focuses more on the
application/control plane, while Greenfield is the data plane. To avoid
state racing, the following rules are introduced:

- Any resources that are initiated to create by BSC can only be controlled by BSC.

- Any resources that are controlled by BSC can not transfer control rights to Greenfield.

- Any resources that are controlled by Greenfield can transfer control rights to BSC.

### 7.3 Communication Layer

The communication layer is composed of a set of **Greenfield Relayers**:

- Each validator should run a relayer. Each relayer possesses a BLS
  private key, with the address of the key stored on-chain as part
  of the validator's mandatory information.

- The relayer watches all cross-chain events happen on BSC and the
  Greenfield blockchain independently. After enough blocks of
  confirmation to reach finality, the relayer will sign a message by
  the BLS key to confirm the events, and broadcast the signing
  attestment, which is called "the vote", through a p2p network to
  other relayers.

- Once enough votes from the relayer are collected, the relayer will
  assemble a cross-chain package transaction and submit it to BSC or
  Greenfield network.

### 7.4 Resource Mirror Layer

#### 7.4.1 Resource Entity Mirror

The purposes of almost all the cross-chain packages are to change the
state of the resource entities on the Greenfield blockchain. Thus the
below resource entities should be able to be mirrored on BSC:

1. Account

2. BNB

3. Bucket

4. Object

5. Group

The account mapping is natural: as BSC and Greenfield use the same
address scheme. The same address values on both sides mean the same
account. They do not require an actual mirror.

BNB is a natively pegged token from the genesis of Greenfield. The
"Token Hub" contract is a system contract built within BSC to ensure
that Greenfield cannot inflate BNB and secure the total circulation of
BNB.

Bucket, Object, and Group are mirrored onto BSC as NFTs of a new BEP
revised from the ERC-721 standard. These NFTs have corresponding
metadata information for the resources. The ownerships of the NFTs on
BSC stand for the ownerships of these resources on Greenfield. As these
ownerships are not transferable on Greenfield, these NFTs are not
transferable on BSC.

#### 7.4.2 Cross-Chain Operating Primitives

A few series of cross-chain primitives are defined for dApps to call to
operate on these resource entities.

It is worth highlighting that smart contracts can call these primitives
in a similar way as EOAs.

Accounts

- create payment accounts on BSC

BNB:

- transfer bidirectionally between BSC and Greenfield among accounts
  (including even payment accounts)

Bucket:

- create a bucket on BSC

- mirror bucket from Greenfield to BSC

Object:

- mirror object from Greenfield to BSC

- create an object on BSC

- grant/revoke permissions of objects on BSC to accounts/groups

- copy objects on BSC

- Kick off the execution of an object on BSC

- associate buckets to payment accounts on BSC

Group:

- create a group on BSC

- change group members on BSC

- leave a group on BSC

Once these primitives are called by EOA or smart contracts, the
predefined events will be emitted. Greenfield Relayers should pick up
these events and relay them over to Greenfield and BSC. As the change
will happen asynchronously, there will be specific cross-chain packages
for acknowledgments or errors, which can trigger a callback. The caller
of the primitives should pay the fees upfront for cross-chain operations
and also for the potential callback. More details are discussed in Part 3.

## 8 "Not" Ending for the Design

Many details are not covered in Part 1. While some topics will be added
and expanded in Part 3, some are very strategic items that shoot too far
for the team to consider now.

For example, the "execute" trait of a data object. That concept points
out that some data are runnable programs. Greenfield may create a more
transparent computing environment. Users are comfortable using or
devoting their data to particular programs stored on Greenfield because
they can verify the program, they do not have to worry about the program
may change after their confirmation, and they know the program can only
run with their data in a trustful environment provided by Greenfield.

This particular function, together with other new features will be
researched and studied with the future development of BNB Greenfield.

### 8.1 Acknowledgement

We'd like to especially thank the efforts and ideas from the below teams
and communities (in no particular order and definitely not an
exhaustive, full list). BNB Greenfield stands on these giants' shoulders
to build.

1. Ethereum

2. Cosmos SDK

3. Superfluid

4. Amazon Web Services

5. MinIO, and other open-source storage systems

6. Filecoin, Arweave, StorJ, and other decentralized storage networks

7. Bitcoin, and

8. all the other folks and projects that strive for the new Web3 economy

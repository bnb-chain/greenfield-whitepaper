# Part 2 Showcases in Labs

## Table of Content

- [9 Showcases: Decentralized Storage](#9-showcases-decentralized-storage)
  - [9.1 Web Hosting and Personal Cloud Drive](#91-web-hosting-and-personal-cloud-drive)
  - [9.2 Data Availability Layer for Public Blockchain](#92-data-availability-layer-for-public-blockchain)
    - [9.2.1 Layer 1 Blockchain Data Swapping](#921-layer-1-blockchain-data-swapping)
    - [9.2.2 Data Availability Layer for the Layer 2 Rollups](#922-data-availability-layer-for-the-layer-2-rollups)
    - [9.2.3 Snapshots and Block Data Backups](#923-snapshots-and-block-data-backups)
- [10 Showcases: New Ways of Digital Publishing](#10-showcases-new-ways-of-digital-publishing)
  - [10.1 Grass-Root Digital Publishing](#101-grass-root-digital-publishing)
  - [10.2 Data Market](#102-data-market)
  - [10.3 Risk: Anti-Piracy](#103-risk-anti-piracy)
- [11 Showcases: User-Generated Content](#11-showcases-user-generated-content)
  - [11.1 Anti-Monopoly and Anti-Censorship](#111-anti-monopoly-and-anti-censorship)
  - [11.2 Token Curated Registries](#112-token-curated-registries)
- [12 Showcases: Personal Data Market](#12-showcases-personal-data-market)
- [13 From Showcases to Real Production](#13-from-showcases-to-real-production)

The goal of the BNB Greenfield platform is to unleash the power of decentralized blockchain and storage technology on
data ownership and data economy.

This part of the whitepaper is neither accurate as industrial designs nor serious as academic research. It just lists a
few potential showcases that can be modeled upon BNB Greenfield in a “laboratory environment”. The showcases are used to
inspire further experimentation and solid design to create the next generation of decentralized applications.

## 9 Showcases: Decentralized Storage

BNB Greenfield should first be a convenient, decentralized storage
infrastructure with decent service quality.

### 9.1 Web Hosting and Personal Cloud Drive

Since BNB Greenfield provides APIs and concepts that are very similar to
AWS S3, it is not hard for users to deploy their websites easily onto it
and manage convenient billing via BNB.

With a sophisticated client application, users can also create their own
network drive with their addresses. They can upload and download their
files, photos, and videos via their desktop and mobile devices and
categorize these data with different buckets. The data can be encrypted
with their private keys and restricted access to themselves only.

A good feature of Greenfield as cloud storage is that it allows
community-sponsored data storage. The data owner can put an object
public, while other users can sponsor the storage and download bandwidth
as they wish. This is not something that can be easily done with the
current centralized cloud providers. Open-source software mirrors can be
set up on Greenfield. Websites for social good can be run more easily.

### 9.2 Data Availability Layer for Public Blockchain

The data availability layer is a hot topic in 2022 for a few reasons:

1. Layer 1 data, both block data, and state data has accumulated too much;

2. Layer 2 rollup solutions require low-cost, trustless, or close to trustless storage for the rollup data;

3. modularized blockchains hope a standalone data layer can scale the total capacity up.

#### 9.2.1 Layer 1 Blockchain Data Swapping

BNB Chain ecosystem, especially BSC itself, is particularly interested
in the #1 and #2. Among all public general blockchains, BSC is the
largest computing blockchain in terms of state data, unique addresses,
smart contracts, total transactions, and daily active users. The total
historic data of BSC was already more than several dozen terabytes in 2022.
Among all these data, some are stale, dead, or dormant.
They will never be used or only be used in rare cases.
They should not always take up space together with other active data or bring in performance pressure.

Similar to modern PC operating systems, such stale data should be
swapped out to long-term and cheaper storage, such as Greenfield.
Special transactions, EVM opCode, and corresponding economics can be
introduced to achieve the consensus to swap these data out. When any
user or smart contract wants to operate on these swap-out data, an error
of "page fault" will be triggered and users should explicitly swap in
the data from Greenfield back to BSC. These ideas are being considered
by BSC Core Dev already.

#### 9.2.2 Data Availability Layer for the Layer 2 Rollups

Similar to Ethereum, BSC also welcomes Layer 2 Rollups as the solution
to scale the total computing power and ledger size. Storing data on BSC
is cheaper than Ethereum, but it can be much more effective if there is
a common storage infrastructure that is reliable and verifiable. Such
infrastructure and corresponding data availability layer management can
significantly reduce the cost of the rollups.

#### 9.2.3 Snapshots and Block Data Backups

Data storage for the long term was not a topic that was seriously
considered when blockchain was invented. However, it has become a
problem today. Most developers prefer to run a blockchain node from a
snapshot, instead of running for months from the genesis. Many networks,
including Ethereum, have been researching that the block and historic
data that has existed for more than a certain time should be allowed to
drop. The community needs a publicly accessible and credible data source
to read these very old data and recent snapshots. BNB Greenfield can be
a good option. Its sponsorship feature is natural for this data of
social good.

## 10 Showcases: New Ways of Digital Publishing

Digital publishing is a mature industry now. E-books, games, music, long
video streaming, and short clips are all very common and widely accepted
by mainstream authors and consumers.

The below two examples show how the BNB Greenfield ecosystem can help
this sector.

### 10.1 Grass-Root Digital Publishing

Without mentioning Professional publishing, even some amateur publishing
can be very formal and cumbersome. For some grass-root creators or
authors, their works are long-tail in the eyes of traditional or even
internet-based publishers and not worth covering.

With Greenfield and BSC, any amateur authors can store their works on
Greenfield and mirror them onto BSC. They can sell the works on a market
on BSC, and the market can automatically grant the read permissions to
the buyer addresses after they pay. The authors do not need to talk with
any publisher, but only perform a few clicks on the dApp and manage
their (small) community.

### 10.2 Data Market

This is very similar to the digital publishing market. But it extends to
any type of data besides digital arts, such as historical statistics for
certain domains, any scientific experiment data, etc.

With Greenfield, some NFT-based markets on BSC can become an "Ebay" of
data.

### 10.3 Risk: Anti-Piracy

The current design of Greenfield has no anti-piracy purpose with it at
all. Once the address gets the read permission, they can download the
data and circulate it to anyone for profit or for non-profit if they do
not obey the rules. Some of the DRM mechanisms can still work, but many
will not.

However, as a public and decentralized infrastructure, it naturally
provides an auditable history for the data, with content, signature,
timestamps, and checksums. It helps a lot to provide evidence for the
copyright dispute.

Authors, publishers, and dApps should be aware of these limitations and
choose to use them at their own risk for now. More copyright-related
features may be introduced to Greenfield with the help of the community.

## 11 Showcases: User-Generated Content

### 11.1 Anti-Monopoly and Anti-Censorship

There is one job that benefits the most from the development of Social
Media: Key Opinion Leaders, a.k.a KOLs. They publish opinions, articles,
videos, and music works that please, influence and inspire people. KOLs
create their own fandom and can make their fortune by using the
attention and traffic of their fans.

However, there is an Achilles' heel for these KoLs: they cannot own
their data and fan relationship if the platforms do not allow them to.
We all know that you cannot change this, even if you are the president
of the most powerful country in the world.

BNB Greenfield provides a convenient infrastructure to make the data
fully owned by the creators. Meanwhile, dApps can still use such data,
publish it to the public audience and maintain the social network. What
is more, even the fandom relationship or social network graph can be
saved on Greenfield as a type of data owned by the users. There is no
single firm here that can block data access. The dApps just provide
convenient UIs and toolings to facilitate information creation and
propagation.

Another big advantage of Greenfield is that it makes it easy to create
private fandoms by using the group features. For example, a KOL can
create a special group for a special fandom. This group can be only
operated by a smart contract on BSC and only allow addresses to join
based on special credentials, such as holding a certain token or paying
a subscription fee. These are all easy to implement with Greenfield.

### 11.2 Token Curated Registries

[Token Curated
Registries](https://hackernoon.com/what-are-token-curated-registries-and-decentralized-lists-d33fa42ba167)
were widely discussed and researched in 2018. But it didn't gain much
recognition in the real use cases. One of the reasons may be that it is
difficult and expensive to save the different lists and credibly present
them.

BNB Greenfield provides a perfect solution for token-curated lists. A
smart contract on BSC can bear the full governance and incentive logic
of the registration, and meanwhile owns the rights to create objects of
each list under the designated bucket for the business. The list of
objects and fully tracked change history are priceless functions for
such decentralized voting and governance ideas.

## 12 Showcases: Personal Data Market

This may be the most complicated problem to tackle nowadays: how to own
your data, such as page views, registrations, clicks, behavior data, and
much more. The ownership guarantees that no platforms (usually the
monopoly ones) can abuse using it. Many laws are defined to punish
misuse, but there are few proactive solutions.

BNB Greenfield poses for pioneering new angles to solve this: what if
you can ask the applications to store all your data encrypted on
Greenfield under your account, and only allow the processing of your
data via a publicly readable code?

Let us check a specific scenario. A data market stores your past buy and
sell orders on Greenfield, encrypted by your account's public key. Only
your private key can decrypt and read it. However the data market
application will like to read your data to recommend other items,
meanwhile, another data agency would like to use this data to perform
commercial research. Both of them are willing to pay you for their
processing of your data. You tend to grant permission to them to read
the data but worry they will do other things with your data. How can BNB
Greenfield solve this?

This may not be day 1 implementation but BNB Greenfield targets to solve
this trust computing problem by providing a verifiable computing runtime
("do not trust, verify").

In the above scenario, the data market application and the data agency
may put the programs that need to read the users' data on Greenfield and
share them with you or even the whole public. You can verify whether you
are comfortable with what the programs do. Then you grant the read
permission of this new object with a
"[group-oriented](https://onlinelibrary.wiley.com/doi/epdf/10.1002/sec.1593)"
encryption scheme to these programs. The data market and the data agency
can pay you and then will run these programs to get the result on a
verifiable sandbox of the runtime of Greenfield.

Once this model gets understood, a lot of enhancements can be done via
modern cryptography to improve the user experience.

For example, the deal can be negotiated beforehand between you and the
data market. Thus the grant of the permission and corresponding economic
benefits exchange can happen within a smart contract to reduce the trust
required. After the deal is achieved, the data will be saved via
BLS-based encryption from the time it is generated. Either the data
owner or the data market programs that the data owner approves (not the
data market owner) can, and only those two can decrypt the data.

Many more infrastructures related to the scenario above are not
considered in this paper yet but can be gradually designed and
implemented on BNB Greenfield.

## 13 From Showcases to Real Production

Different big and small showcases are discussed above as Part 2 of the
paper. Some of them may be worth to be implemented into a real
application, but more are expected to inspire new models to be invented
to unleash the power of BNB Greenfield. This part of the paper is
expected to be soon substituted by real applications in production.

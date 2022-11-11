# Televerse Development Footprint

This document lists the different aspects of the Televerse DAO that need to be completed to produce a working Televerse ecosystem.


## Tokenomics

The Televerse tokenomics are fundamental to enforcing the commercial consequences of decisions made within Televerse.  We use it to:
1. transfer value to investors
2. settle accounts between customers and carriers
3. incentivize testers to respond to customer requests to verify SLAs
4. penalize carriers that have failed to maintain the standards specified in their SLA documents
5. produce NFTs for governance functions (board member appointment)
6. board member NFTs for council voting

### Televerse Token (TT)
The TT is the utility token of the DAO. It is minted into the DAO treasury and distributed to member carriers in the DAO via IOU. The member carriers do not receive TT as a windfall. It is their responsibility to:
1. maintain the value and liquidity of the TT, either directly or through the services of a market maker (member carriers are "TT Liquidity Providers")
2. be responsible for restoring all TDT rendered into their custodianship back to the DAO if their allotment is shrunk by the mechanisms of the DAO

TT Liquidity Providers receive a Televerse Governing NFT (TGN). The voting weight of this token is proportional to the amount of TT the member carrier is entrusted with. 

### Televerse DAO Token (TDT)
The TDT is a token awarded to investors for powering the developement and initial operation of Televerse.

It grants the priviledge of a dividend from the DAO denominated in Televerse Token (TT), the utility token of the DAO.

All TDT holders also receive a Televerse Governing NFT (TGN). The TGN is a token used to participate in board member selections. However, this token has zero voting weight until the TDT holder stakes TDT for a set period.

### Televerse Governing NFT (TGN)
The TGN is a token used to participate in board member selections, as well as increase or decrease the number of possible board members.

#### TDT Holders
For TDT holders, the voting weight of their TGN changes according to the number of TDT pledged and the period **remaining**. The period can be increased but not decreased.

#### TT Liquidity Providers
The DAO varies the TT assigned to the custodianship of different member carriers according to their activity on the DAO. This allotment is the basis for the voting weight of their TGN.

### Televerse Board NFT (TBN)
The TBN is a token held by each elected board member. Each token has a voting weight of ten (10), except for the single prime member with a voting weight of eleven (11). The prime membership can be moved between members on a full participation, 2/3rds vote of the board. This means that the board can be made up of any number of board members.

## Carrier Node
This is a carrier's interactive surface with our DLT and DAO.

1. Local storage of the pricing graph as seen by the carrier.
2. Carrier authenticated and authorized UI for inputing pricing graph data, sharing that data with other carriers in a controlled manner, setting policies for the escalation of access to that data on events, responses to customer requests for service.
3. SSDT interface to share data selectively with other carriers.
4. HFS + Filecoin interface to share publicly available data points on the DL.
5. ITN interface to resolve the DIDs of other carriers and then contact those carriers for the restricted information they contain.
6. LSO Sonata (Dolly) Buyer API compliant interface to communicate on-chain transactions back to the BSS of the carrier
7. Public facing customer portal UI. Search and ordering.

## Validation Oracle
Each running service must be able to be tested on customer challenge. If the customer feels that the SLAs that they paid for are not being met, they can request that the DAO initiate a test. This request for test goes to specific known endpoints and they respond (and are rewarded) with the requested test metrics, signed by their registered private key.

## L2 Testers
Our DPDK devices allow L2 circuits to be tested across carriers and can verify that DIA services are reaching the IPs that they should be reaching.

## DAO
The coding of the DAO is the most important aspect of the entire system. The governance, mechanisms for updating the DAO, and the balance of incentives and disincentives will have a large bearing on the success of the project.

### Technology Stack of the DAO
We will be using the following technologies.

#### HTS
The Hedera Token Service allows us to mint both ERC-20 like tokens as well as NFTs (ERC-721). Transaction fees are low and transaction throughput high. The initial plan includes the following tokens:
1. Televerse Token (TT)
2. Televerse DAO Token (TDT)
3. Televerse Governance NFT (TGN)
4. Televerse Board NFT (TBN)

#### HCS
The Hedera Consensus Service allows us to log events on the Televerse DAO in a timestamped and immutable way.

#### HSCS
The Hedera Smart Contract Service uses the Hyperledger Besu EVM, meaning that we can write v0.8.9 Solidity contracts for it.

#### HFS
The Hedera File Service allows us to push our contracts to the DL and then call them from there.

#### Filecoin
While HFS is capable of storing any kind of data, the cost of storage is sub-optimal, which is where we will require a L2 service to store the large amounts of data we expect to accumulate.
1. Pricing nodes.
2. Pricing edges.
3. Pricing profiles.
4. Physical lines.
5. Physical locations.
6. Switches.
7. Ports.
8. NNIs.
9. SLAs.

#### ITN
The Intergrated Trust Network has mechanisms for resolving Decentralized Identifiers (DIDs) to the endpoints of the **SSDT**s (an SDK that each carrier will run), where sensitive information can be shared selectively with confidence.

#### Baseline
Sometimes we cannot share sensitive commercial information on a public blockchain, but we absolutely need to verify that some kind of logical relationship is being maintained without moving the required information from the system of record. I.e. we need to determine that a particular tested bandwidth exceeds the SLA stipulation without anyone but the carrier and the customer knowing the precise value. Baselining and Zero Knowledge Proofs allow us to do this.

There may or may not be utility in providing a baseline implementation for NNI or pricing information, but since this would be exact match rather than greater or less than challenges, there's no information retained in excess of an approach that simply shares the information via SSDT.
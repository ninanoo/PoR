###### ※ PoR is a new open blockchain consensus algorithm and is still theoretical.<br/><br/>I hope this algorithm will be discussed and improved with the people who study and develop the blockchain.<br/>As a mathematically provable algorithm based on computational complexity theory, there is also a need to help those who can deal with nonlinear values well.<br/><br/>Except for some of the relational formulas, the idea is over and the technical documentation was written once.<br/>However, it is Korean. This English document is not yet complete.<br/>Unfortunately, I am not used to writing English.<br/><br/>So, while introducing the algorithm, its main purpose is to find someone to help with the [Korean-English translation](https://github.com/ninanoo/PoR---Korean-Version/issues/1) of [Korean document](https://github.com/ninanoo/PoR---Korean-Version).<br/><br/>I am sorry about the incomplete and unkind GitHub's main page.<br/><br/>This algorithm needs your help.

<br/>

# PoR ( Proof of Relevancy )

### Blockchain Consensus Algorithm determined by Relevancy

PoR is a blockchain consensus algorithm that the next block is determined by relevancy.
The relevancy is obtained from the proprietary information of each block between adjacent blocks.
The relevancy can also be created from the work of PoW or the stake of PoS.
In this document, the asymmetric key pair of each block used to generate the signature is also used as the proprietary information.

It uses a hash chain of Bitcoin, but has a dual chain structure such as Bitcoin-NG.
There are a key block chain and an authentication block chain linked each other.
In the key block chain, a candidate that can generate an authentication through consensus is registered.
In the authentication block chain, the authentication for a ledger is registered.
With the use of a dual chain, the registered candidate can generate a real authentication after a very long time and there is also competition at that time.

Relevancy is used for competition to be registered as a candidate to generate an authentication.
Reverse relevancy is used for competition to create real authentication.
Both competing situations are competition for time based on relevancy and they are all for personal benefit.
This prevents problems such as 'nothing at stake'.

It is not the computational complexity that simply solves the hash, but there are numerical parts related to the operation of the algorithm such as many candidate blocks or very large threshold value, and they are all designed based on computational complexity theory.
As a result, all attacks on the algorithm are probabilistically impossible.

Due to the use of the dual chain with attributes such as relevancy, reverse relevancy, and the threshold value for generating authentication block, the authentication for the ledger operates deterministically.
Attacks such as double spending or finney attack do not occur because authentication to the ledger is deterministic.

Due to the use of proprietary information, it is more resistant than bitcoin against 51% attack and localization problems.
High-speed processing is possible enough to generate each authentication block for the unit ledgers without the use of merkle tree depending on the size of the network.
There may be one reward for the participation of a majority of legitimate users, but there are no rewards for the functional behavior of the algorithm.

<br/>

## Structure of Blocks and Chains

The figure below shows the enlarged view of the last generated authentication block and its surrounding blocks in the entire dual chain.
The upper side is the key block chain and the lower side is the authentication block chain.

![blockAndChainDiagram](blockAndChainDiagram.png?raw=true "blockAndChainDiagram")

Most of the key block chain consists of blocks that have generated authentication blocks and blocks that have been decided as blocks for generating authentication blocks but are excluded by following blocks due to malicious purposes or network failures.
The back part of the key block chain consists of candidate blocks for generating the authentication block.
The candidate block that is generated first among the candidate blocks becomes the leader block.
All key blocks contain the own sequence number and the sequence number of the last confirmed authentication block at the time of addition and the proprietary information needed to calculate relevancy.
And they also include a new hash value created by combining these information with the hash value of the immediately preceding key block and the hash value of the last confirmed authentication block at the time of addition.

The authentication block chain consists of the ledger authentication blocks containing the authentication information of the ledgers and the exclusive authentication blocks containing exclusion information for key blocks excluded from the authentication generation.
Ledger authentication blocks are again divided into blocks that have been confirmed and one unconfirmed block that have been created most recently.
Ledger authentication blocks contain the sequence number of the associated key block and the authentication information of the ledgers to authenticate.
And they also include a new hash value created by combining these information with the hash value of the immediately preceding authentication block and the hash value of the associated key block.
Exclusive authentication blocks contain the sequence number of the excluded key block and the sequence number of the key block that excluded it and the related exclusion information.
And they also include a new hash value created by combining these information with the hash value of the immediately preceding authentication block and the hash value of the excluded key block and The hash value of the key block that excluded it.

The sequence numbers of the key block chain and the authentication block chain are incremented in the same order.
All key blocks with sequence numbers greater than the sequence number of the last block in the authentication block chain are all candidate blocks.
The certification for the actual ledger is proceeded by candidate blocks added to the chain through consensus after a very long time.
The use of a dual chain structure provides both entity authentication for block itself added before a very long time ago and integrity to the authentication of the ledger.

<br/>

## Relevancy and Consensus Mechanism

### Relevancy Formula

![relevancyFormula](relevancyFormula.png?raw=true "relevancyFormula")
```
r      : relevancy
c      : number of following blocks including the target block ( c > 0 )
n      : sequence number of candidate blocks starting with 0 ( n < c )
m of n : number of consecutive bits with the same value as the previous hash value starting from the beginning
a      : relevancy factor ( a > 1 )
```

### Relevancy Ratio Graph

`a ^ (-n / c)` of `a = 2 ^ 16` , `c = 10000`

![relevancyRatio1](relevancyRatio1.png?raw=true "relevancyRatio1")

`a ^ (-n / c)` of `a = 2 ^ 16` , `c = 10, 100, 10000`

![relevancyRatio2](relevancyRatio2.png?raw=true "relevancyRatio2")

`a ^ (-n / c)` of `c = 10000` , `a = 2 ^ 2, 2 ^ 4, 2 ^ 8, 2 ^ 16, 2 ^ 32`

![relevancyRatio3](relevancyRatio3.png?raw=true "relevancyRatio3")

<br/>

## Threshold Value and Relevancy Efficiency Ratio

### Simulated Relevancy Formula

![expectedRelevancyFormula](expectedRelevancyFormula.png?raw=true "expectedRelevancyFormula")
```
r : relevancy
c : number of following blocks including the target block ( c > 0 )
n : sequence number of candidate blocks starting with 0 ( n < c )
m : maximum number of consecutive bits except the difficulty bits ( m > 0 )
d : number of difficulty bits ( d > 0 )
a : relevancy factor ( a > 1 )
```

### Relevancy Graph

`d = 8` , `m = 8` , `a = 2 ^ 2, 2 ^ 4, 2 ^ 8, 2 ^ 16, 2 ^ 32`

![relevancy1](relevancy1.png?raw=true "relevancy1")

`d = 8` , `m = 12` , `a = 2 ^ 2, 2 ^ 4, 2 ^ 8, 2 ^ 16, 2 ^ 32`

![relevancy2](relevancy2.png?raw=true "relevancy2")

<br/>

## Reverse Relevancy and Game Theory

### Relevancy Ratio Derivative Formula

![relevancyRatioDerivativeFormula](relevancyRatioDerivativeFormula.png?raw=true "relevancyRatioDerivativeFormula")
```
d : derivative
c : number of following blocks including the target block ( c > 0 )
n : sequence number of candidate blocks starting with 0 ( n < c )
a : relevancy factor ( a > 1 )
```

### Relevancy Ratio Derivative Graph

`a ^ (-n / c)` of  `c = 10000` , `a = 2 ^ 2, 2 ^ 4, 2 ^ 8, 2 ^ 16, 2 ^ 32`

![relevancyRatioDerivative](relevancyRatioDerivative.png?raw=true "relevancyRatioDerivative")

<br/>

## Synchronization

<br/>

## Double Spending

<br/>

## 51% Attack and Localization

<br/>

## Proprietary Information

<br/>

## Compensation for Effort

<br/>

## Scalability

<br/>


###### ※ This algorithm was not designed for the purposes of ICO.<br/>Coin issuance may be required to raise money needed to implement and validate the algorithm.<br/>Even if a coin is issued, it should be aimed at the proof of concept of the algorithm, not profit.<br/>Compensation schemes are needed and follow the methods of other smart contract algorithms.<br/>I hope this algorithm solves many of the problems associated with the blockchain, so that the block chain technology is activated.

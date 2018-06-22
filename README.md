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

Candidate blocks to be newly added reach a consensus as the block most relevant to the previous block as they go through a continuous diffusion and convergence process in the network.
Every blockchain algorithm uses a pair of public and private keys to generate a signature for the ledger.
Here, the pair of public and private keys is used not only for signature generation purpose, but also as a proprietary key, which is proprietary information.
The self relevancy of a block is generated by the number of consecutive matching bits by comparing the hash value of the immediately preceding block with the public key value in bit-by-bit order from the start bit.
To reduce unnecessary competition on the network, it has a similar difficulty to that of PoW.
The difficulty is the minimum number of bits that must be matched and is not intended to be a proof of work.

Simply using the public key is to use a value that does not change regardless of the location of the block.
This can cause unnecessary resource consumption, such as running a key pool.
Actually, it is compared to the newly created value by combining the public key certificate as the proprietary information of the block or the signature to prove the corresponding private key with the hash value of the immediately preceding block.
The hash value of the block is obtained by combining the hash value of the immediately preceding block and the proprietary information of the block, and compares it with the hash value of the immediately preceding block.
This ensures that the front part of the hash value of all blocks remains the same value, and it can be used as an identifier to separate each chain when operating as a separate chain for each service.
The proprietary information is actually analogous to the nonce of PoW in view of the fact that it find a specific hash value through a single element that can change its value.
But here the consensus in the network continues to find the unique and fixed nonce per node, not the nonce that can be changed.

In fact, the relevancy of a block is determined by accumulating the relevancy of all blocks following the block, including itself.
Relevancy to subsequent blocks is multiplied by a decreasing exponential distribution in the order in which they are added to the chain.
This makes the chain more deterministic by making the number of replacements smaller for the former blocks.
Even if it is not the end of the chain, if the relevancy is higher than the existing block, block to be added can replace the existing block and subsequent blocks of existing block are also discarded.
Conversely, even if the self relevancy of the block to be added is relatively low, if a number of blocks follow, even existing block that have better self relevancy can lose in the competition.
With relevancy, the sooner a block join the consensus, the more likely a block is to be selected.
In order to numerically control this, a relevancy formula, which is calculated as the decrease rate of exponential form, and a relevancy factor for it is used.
The total relevancy is getting higher, and at the same time the consensus continues to be made so that the number of blocks is smaller.
It is filled with blocks having sufficient relevancy from the front part of the chain, and most of the actual transactions occur only in the blocks behind the chain.

### Relevancy Formula

Below is a formula that calculates the relevancy of a block.

![relevancyFormula](relevancyFormula.png?raw=true "relevancyFormula")
```
r      : relevancy
c      : number of following blocks including the target block ( c > 0 )
n      : sequence number of candidate blocks starting with 0 ( n < c )
m of n : number of consecutive bits with the same value as the previous hash value starting from the beginning
a      : relevancy factor ( a > 1 )
```

The `r` as the cumulative relevancy of `0`th block with `n = 0` is followed by subsequent blocks with a number of `c - 1`.
`2 ^ m` is the self relevancy of each `n`th subsequent block.
`a ^ (-n / c)` is the relevancy ratio of each `n`th subsequent block.
The relevancy ratio of the `0`th block to calculate the cumulative relevancy is always `1`, and the cumulative relevancy is equal to self relevancy if there are no following blocks.
The relevancy of each subsequent block is multiplied by its relevancy ratio, and the sum of all these values is the relevancy of any one block.
Each of the candidate blocks in the chain, while making themselves a `0`th block, calculates the relevancy through the above calculation formula.

### Relevancy Ratio Graph

Below is the relevancy ratio graph of `(2 ^ 16) ^ (-n / 10000)`.

![relevancyRatio1](relevancyRatio1.png?raw=true "relevancyRatio1")

The graph above uses `2 ^ 16` as the relevancy factor `a` and is currently followed by `10000 - 1` subsequent blocks.
The blocks added before the `5000`th corresponding to half of the blocks start to have a meaningful value, and the blocks added before the `100`th corresponding to 1% have a value of `0.9` or more.

Here are the relevancy ratio graphs when `c` is `10`, `100`, and `10000` using `2 ^ 16` as a relevancy factor.
As a graph that shows the characteristics of `n / c`, the relevancy ratio of each subsequent block is a constant ratio to the position of each block relative to the total number of subsequent blocks.

![relevancyRatio2](relevancyRatio2.png?raw=true "relevancyRatio2")

When the number of blocks is `10`, the relevancy ratio of `9`th block is close to `0`.
When subsequent blocks are added to this block and the number of blocks becomes `100`, the relevancy ratio of the `9`th block has a value close to `0.4`.
When subsequent blocks are added again and the number of blocks becomes `10000`, it has a value close to `1`.
As more subsequent blocks are added to one subsequent block, the position in the curve of the block continues to move leftward, and the relevancy ratio increases exponentially.

Here is the relevancy ratio graph of `a ^ (-n / 10000)`.
From the top curve, we use the relevancy factors of `2 ^ 2`,` 2 ^ 4`, `2 ^ 8`,` 2 ^ 16`, and `2 ^ 32`.

![relevancyRatio3](relevancyRatio3.png?raw=true "relevancyRatio3")

As you can see in the graph, the larger the relevancy factor, the greater the decrease in the relevancy ratio, which decreases exponentially.
As a result, the larger the relevancy factor is used, the smaller the cumulative relevancy, but the chain is more deterministic.

In the bitcoin's PoW, the occurrence of a branch in the chain is considered a collision situation and the longest chain is selected.
In the proof of relevancy, the occurrence of a branch in the chain is considered to be the process by which the algorithm operates.
A chain with a higher value is selected by comparing the relevancy of the block where the branch occurred.
The `m` value satisfying the difficulty is used to avoid unnecessary branching of small units.
Branches occur frequently in the chain, which is a significant portion of the consensus process, but mostly only in the blocks behind the chain.
To guarantee this, the threshold for generating an authentication block must be set high enough.
This is determined by the physical environment of the entire network in which the chain is operating and the required performance expectations.

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

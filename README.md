###### ※ PoR is a new open blockchain consensus algorithm and is still theoretical.<br/><br/>I hope this algorithm will be discussed and improved with the people who study and develop the blockchain.<br/>As a mathematically provable algorithm based on computational complexity theory, there is also a need to help those who can deal with nonlinear values well.<br/><br/>Except for some of the relational formulas, the idea is over and the technical documentation was written once.<br/>However, it is Korean. This English document is not yet complete.<br/>Unfortunately, I am not used to writing English.<br/><br/>So, while introducing the algorithm, its main purpose is to find someone to help with the [Korean-English translation](https://github.com/ninanoo/PoR---Korean-Version/issues/1) of [Korean document](https://github.com/ninanoo/PoR---Korean-Version).<br/><br/>I am sorry about the incomplete and unkind GitHub's main page.<br/><br/>This algorithm needs your help.

<br/>

# PoR ( Proof of Relevance )

### Blockchain Consensus Algorithm determined by Relevance

PoR is a blockchain consensus algorithm that the next block is determined by relevance.
The relevance is obtained from the proprietary information of each block between adjacent blocks.
The relevance can also be created from the work of PoW or the stake of PoS.
In this document, the asymmetric key pair of each block used to generate the signature is also used as the proprietary information.

It uses a hash chain of Bitcoin, but has a dual chain structure such as Bitcoin-NG.
There are a key block chain and an authentication block chain linked each other.
In the key block chain, a candidate that can generate an authentication through consensus is registered.
In the authentication block chain, the authentication for a ledger is registered.
With the use of a dual chain, the registered candidate can generate a real authentication after a very long time and there is also competition at that time.

Relevance is used for competition to be registered as a candidate to generate an authentication.
Reverse relevance is used for competition to create real authentication.
Both competing situations are competition for time based on relevance and they are all for personal benefit.
This prevents problems such as 'nothing at stake'.

It is not the computational complexity that simply solves the hash, but there are numerical parts related to the operation of the algorithm such as many candidate blocks or very large threshold value, and they are all designed based on computational complexity theory.
As a result, all attacks on the algorithm are probabilistically impossible.

Due to the use of the dual chain with attributes such as relevance, reverse relevance, and the threshold value for generating authentication block, the authentication for the ledger operates deterministically.
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
All key blocks contain the own sequence number and the sequence number of the last confirmed authentication block at the time of addition and the proprietary information needed to calculate relevance.
And they also include a new hash value created by combining these information with the hash value of the immediately preceding key block and the hash value of the last confirmed authentication block at the time of addition.

The authentication block chain consists of the ledger authentication blocks containing the authentication information of the ledgers and the exclusion authentication blocks containing exclusion information for key blocks excluded from the authentication generation.
Ledger authentication blocks are again divided into blocks that have been confirmed and one unconfirmed block that have been created most recently.
Ledger authentication blocks contain the sequence number of the associated key block and the authentication information of the ledgers to authenticate.
And they also include a new hash value created by combining these information with the hash value of the immediately preceding authentication block and the hash value of the associated key block.
Exclusion authentication blocks contain the sequence number of the excluded key block and the sequence number of the key block that excluded it and the related exclusion information.
And they also include a new hash value created by combining these information with the hash value of the immediately preceding authentication block and the hash value of the excluded key block and The hash value of the key block that excluded it.

The sequence numbers of the key block chain and the authentication block chain are incremented in the same order.
All key blocks with sequence numbers greater than the sequence number of the last block in the authentication block chain are all candidate blocks.
The certification for the actual ledger is proceeded by candidate blocks added to the chain through consensus after a very long time.
The use of a dual chain structure provides both entity authentication for block itself added before a very long time ago and integrity to the authentication of the ledger.

<br/>

## Relevance and Consensus Mechanism

Candidate blocks to be newly added reach a consensus as the block most relevant to the previous block as they go through a continuous diffusion and convergence process in the network.
Every blockchain algorithm uses a pair of public and private keys to generate a signature for the ledger.
Here, the pair of public and private keys is used not only for signature generation purpose, but also as a proprietary key, which is proprietary information.
The self relevance of a block is generated by the number of consecutive matching bits by comparing the hash value of the immediately preceding block with the public key value in bit-by-bit order from the start bit.
To reduce unnecessary competition on the network, it has a similar difficulty to that of PoW.
The difficulty is the minimum number of bits that must be matched and is not intended to be a proof of work.

Simply using the public key is to use a value that does not change regardless of the location of the block.
This can cause unnecessary resource consumption, such as running a key pool.
Actually, it is compared to the newly created value by combining the public key certificate as the proprietary information of the block or the signature to prove the corresponding private key with the hash value of the immediately preceding block.
The hash value of the block is obtained by combining the hash value of the immediately preceding block and the proprietary information of the block, and compares it with the hash value of the immediately preceding block.
This ensures that the front part of the hash value of all blocks remains the same value, and it can be used as an identifier to separate each chain when operating as a separate chain for each service.
The proprietary information is actually analogous to the nonce of PoW in view of the fact that it find a specific hash value through a single element that can change its value.
But here the consensus in the network continues to find the unique and fixed nonce per node, not the nonce that can be changed.

In fact, the relevance of a block is determined by accumulating the relevance of all blocks following the block, including itself.
Relevance to subsequent blocks is multiplied by a decreasing exponential distribution in the order in which they are added to the chain.
This makes the chain more deterministic by making the number of replacements smaller for the former blocks.
Even if it is not the end of the chain, if the relevance is higher than the existing block, block to be added can replace the existing block and subsequent blocks of existing block are also discarded.
Conversely, even if the self relevance of the block to be added is relatively low, if a number of blocks follow, even existing block that have better self relevance can lose in the competition.
With relevance, the sooner a block join the consensus, the more likely a block is to be selected.
In order to numerically control this, a relevance formula, which is calculated as the decrease rate of exponential form, and a relevance factor for it is used.
The total relevance is getting higher, and at the same time the consensus continues to be made so that the number of blocks is smaller.
It is filled with blocks having sufficient relevance from the front part of the chain, and most of the actual transactions occur only in the blocks behind the chain.

### Relevance Formula

Below is a formula that calculates the relevance of a block.

![relevanceFormula](relevanceFormula.png?raw=true "relevanceFormula")
```
r      : relevance
c      : number of following blocks including the target block ( c > 0 )
n      : sequence number of candidate blocks starting with 0 ( n < c )
m of n : number of consecutive bits with the same value as the previous hash value starting from the beginning
a      : relevance factor ( a > 1 )
```

The `r` as the cumulative relevance of `0`th block with `n = 0` is followed by subsequent blocks with a number of `c - 1`.
`2 ^ m` is the self relevance of each `n`th subsequent block.
`a ^ (-n / c)` is the relevance ratio of each `n`th subsequent block.
The relevance ratio of the `0`th block to calculate the cumulative relevance is always `1`, and the cumulative relevance is equal to self relevance if there are no following blocks.
The relevance of each subsequent block is multiplied by its relevance ratio, and the sum of all these values is the relevance of any one block.
Each of the candidate blocks in the chain, while making themselves a `0`th block, calculates the relevance through the above calculation formula.

### Relevance Ratio Graph

Below is the relevance ratio graph of `(2 ^ 16) ^ (-n / 10000)`.

![relevanceRatio1](relevanceRatio1.png?raw=true "relevanceRatio1")

The graph above uses `2 ^ 16` as the relevance factor `a` and is currently followed by `10000 - 1` subsequent blocks.
The blocks added before the `5000`th corresponding to half of the blocks start to have a meaningful value, and the blocks added before the `100`th corresponding to 1% have a value of `0.9` or more.

Here are the relevance ratio graphs when `c` is `10`, `100`, and `10000` using `2 ^ 16` as a relevance factor.
As a graph that shows the characteristics of `n / c`, the relevance ratio of each subsequent block is a constant ratio to the position of each block relative to the total number of subsequent blocks.

![relevanceRatio2](relevanceRatio2.png?raw=true "relevanceRatio2")

When the number of blocks is `10`, the relevance ratio of `9`th block is close to `0`.
When subsequent blocks are added to this block and the number of blocks becomes `100`, the relevance ratio of the `9`th block has a value close to `0.4`.
When subsequent blocks are added again and the number of blocks becomes `10000`, it has a value close to `1`.
As more subsequent blocks are added to one subsequent block, the position in the curve of the block continues to move leftward, and the relevance ratio increases exponentially.

Here is the relevance ratio graph of `a ^ (-n / 10000)`.
From the top curve, we use the relevance factors of `2 ^ 2`,` 2 ^ 4`, `2 ^ 8`,` 2 ^ 16`, and `2 ^ 32`.

![relevanceRatio3](relevanceRatio3.png?raw=true "relevanceRatio3")

As you can see in the graph, the larger the relevance factor, the greater the decrease in the relevance ratio, which decreases exponentially.
As a result, the larger the relevance factor is used, the smaller the cumulative relevance, but the chain is more deterministic.

In the bitcoin's PoW, the occurrence of a branch in the chain is considered a collision situation and the longest chain is selected.
In the proof of relevance, the occurrence of a branch in the chain is considered to be the process by which the algorithm operates.
A chain with a higher value is selected by comparing the relevance of the block where the branch occurred.
The `m` value satisfying the difficulty is used to avoid unnecessary branching of small units.
Branches occur frequently in the chain, which is a significant portion of the consensus process, but mostly only in the blocks behind the chain.
To guarantee this, the threshold for generating an authentication block must be set high enough.
This is determined by the physical environment of the entire network in which the chain is operating and the required performance expectations.

<br/>

## Threshold Value and Relevance Efficiency Ratio

The first candidate block, the leader block, has a threshold value to be confirmed as a block to generate the next authentication block.
Addition and replacement of subsequent blocks continues until the relevance of the leader block satisfies the threshold, and the relevance becomes higher and higher.
When the relevance of the leader block reaches the threshold value, the block starts generating the authentication block using the private key, and the addition of the subsequent block no longer occurs, but the replacement is continued if the relevance is higher.
When the authentication block generated by the leader block is started to be distributed, the next candidate block becomes the leader block, and the addition and replacement of the subsequent blocks are continued based on the relevance of the new leader block.

Simply `r / c` is the relevance efficiency ratio as a corresponding relevance by number of blocks involved in the relevance calculation.
On the network, consensus continues to be made to increase this value.
If this value is high, each block has sufficient self relevance and it may be a reference value for threshold calculation.

### Simulated Relevance Formula

The following is the relevance calculation formula for estimating the threshold value by simulating the relevance graph.

![expectedRelevanceFormula](expectedRelevanceFormula.png?raw=true "expectedRelevanceFormula")
```
r : relevance
c : number of following blocks including the target block ( c > 0 )
n : sequence number of candidate blocks starting with 0 ( n < c )
m : maximum number of consecutive bits except the difficulty bits ( m > 0 )
d : number of difficulty bits ( d > 0 )
a : relevance factor ( a > 1 )
```

The self relevance of each block is distributed as a uniform rate of the added order from the `m` bit of the first following block to the `m / c` bit of the last block, including the difficulty.
It assumes that the sooner a block is added, the more consensus it will take for a long time, and the more recently created block is satisfied with the degree of difficulty.
However, the actual number of matched bits and their distribution are determined by the network environment and the base values of the algorithm.
For a accurate experiment for this, a testnet configuration or software simulation close to the actual environment should be performed.

### Relevance Graph

The following is a graph of relevance when `d` is `8` and `m` is `8` in the above simulated relevance formula.
Relevance factors of `2 ^ 2`, `2 ^ 4`, `2 ^ 8`, `2 ^ 16`, and `2 ^ 32` are used from the top.

![relevance1](relevance1.png?raw=true "relevance1")

Through the above graph, the number of blocks that follow to satisfy a specific threshold value for each relevancy factor can be roughly checked.
For a graph using the relevance factor of `2 ^ 16`, `10000` blocks are needed to have the relevance of approximately `2 ^ 25`.
A new block must have `25` or more matching bits in order to replace an existing block with a relevance of `2 ^ 25`.
This can be compared to the work of the PoW.
The effort to find a hash with successive `0`s in the PoW works in the same logic as the effort to find a hash value that matches the previous hash value in the PoR.
The PoW consumes the system resources of each node for a short period of time to find the hash value satisfying the condition.
In the PoR, the network resources are consumed for a very long time to find the most suitable hash value among the unique hash values owned by the nodes.
The PoW consumes system resources uniformly in all mining nodes for the entire time of finding the hash value.
However, in the PoR, the transactions occur only for a short period of time, usually immediately after the block is added, in the entire time.
The number of matched bits that can be safely used for each relevancy factor must be determined, and the threshold value determined accordingly.
To do this, each base value in the PoR must be determined according to the security attributes of the already verified PoW.

The following graph shows the relevance graph when the `m` is` 12` using the same difficulty as the graph above.

![relevance2](relevance2.png?raw=true "relevance2")

In the case of a graph using the relevance factor of `2 ^ 16`, `1000` blocks are needed to have the relevance of approximately `2 ^ 25`.
When the number of matched bits increases by `4` bits, the number of blocks required is reduced to `1 / 10`.
To reduce the number of blocks needed to meet the threshold, there is a way to reduce the threshold value or use a smaller relevance factor.
However, they all weaken the deterministic characteristic of the algorithm.
It may be conceivable to use a larger degree of difficulty to increase the number of matched bits, but this does not match the algorithm's default behavior.
The algorithm does not place much constraint on adding new block to the chain.
The lower the level of difficulty, the more blocks are added to the chain more quickly, which makes the reader block able to issue authentication block faster.
It takes a very long time for the newly added block to issue the authentication, and the relevance efficiency ratio becomes sufficiently high during this time.
Difficulty is not for relevance, only to reduce consumable behavior on the network.

Due to very high threshold, relevance factor, and the use of exponentially decrementing cumulative value, a large number of blocks are required to satisfy the threshold at any one point.
As a result, when the key block chain is first created on the network, the first leader block must have enough time to satisfy the threshold.
However, the threshold value can be satisfied even if only one node is added when the blocks after the first block become the leader block.
At the moment of becoming a leader block, the threshold may already be met.
This is because only one block out of many blocks is excluded from the relevance calculation.
This enables faster processing of authentication block generation.
Merkle tree can be used, but depending on the size of the network, one block can be used for one ledger in performance.
If the consumption of the leader blocks is very fast, the base values should be raised so that sufficient relevance efficiency ratio is maintained at the lower end.

<br/>

## Reverse Relevance and Game Theory

There may be a situation in which the distribution of the ledger authentication block of the leader block satisfying the threshold value is delayed due to malicious purpose or network failure.
For this, all key blocks have a reverse relevance.
The relevance for consensus is the cumulative value of the blocks following in the chain, but the reverse relevance is calculated by the immediately preceding block as the cumulative value of the previous blocks in the opposite direction.
The candidate blocks calculate the reverse relevance of all previous candidate blocks by applying the `c` value used to calculate their own relevance.
The next block of the block satisfying the threshold value compares its relevance with the reverse relevance of the previous block.
If its own relevance satisfies the threshold value before the distributed new ledger authentication block is received and its own forward relevance is greater than the reverse relevance of the previous block, the previous block is processed as the excluded block and it generates and distributes the ledger authentication block.
The exclusion authentication block and the ledger authentication block are distributed together, and then other nodes accept or reject them after checking the relevant information.
If the ledger authentication block is not distributed in the second block, the third block distributes the ledger authentication block if the condition is satisfied in the same way for both the first and second blocks.
The blocks corresponding to approximately `1 / 10` from the beginning of the candidate blocks have the right to exclude the previous candidate blocks in the same way.

All previous blocks, that are cumulatively calculated in the reverse relevance, have high self relevance through a sufficient diffusion and convergence process in the network.
However, if there is a delay in the distribution of the authentication block, the candidate blocks at the back of the chain increase the relevance only by the replacement without addition, so the value of `c` is getting lower and the reverse relevance of the previous blocks is also lowered.
This causes the reverse relevance to urge the reader block, which is satisfied with the threshold, to issue the authentication block as soon as possible.
From the beginning of the candidate blocks, the blocks corresponding to approximately `1 / 10` are all in the same situation.

The exact number of blocks that have the right to exclude is determined by the relevance factor.
In the graph of relevance ratio, blocks having a meaningful magnification not close to `0` correspond to this.
This is related to the derivative of the relevance ratio curve.

### Relevance Ratio Derivative Graph

The following graph shows the relevance ratio curves for each of the relevance factors and the curves for their derivatives.

![relevanceRatioDerivative](relevanceRatioDerivative.png?raw=true "relevanceRatioDerivative")

The top is the relevance ratio curves for each relevance factor, and the bottom is the variation curves for `n / c` of each curve.

### Relevance Ratio Derivative Formula

Below is the formula used to calculate the derivative.

![relevanceRatioDerivativeFormula](relevanceRatioDerivativeFormula.png?raw=true "relevanceRatioDerivativeFormula")
```
d : derivative
c : number of following blocks including the target block ( c > 0 )
n : sequence number of candidate blocks starting with 0 ( n < c )
a : relevance factor ( a > 1 )
```

Clear relationships have not yet been found by the analysis of the primary variation.
So, at this time, approximate values are used for each relevancy factor.
In the case of the graph using the relevance factor of `2 ^ 16`, the blocks corresponding to approximately `1 / 10` are considered from the beginning of the candidate blocks.
However, in actual implementation, it should be set high enough to match the physical environment of the entire network or the level of security required.

There may be a situation where all blocks corresponding to `1 / 10` are disabled.
All of the blocks corresponding to `1 / 10` were selected through continuous competition based on hash values with random distribution, assuming a majority of legitimate users.
The number of blocks corresponding to this `1 / 10` is `1000` from the small value of `100` depending on the network size.
Therefore, the situation in which the algorithm stops is probabilistically impossible.

<br/>

## Synchronization

Due to the nature of the distributed system, a collision may occur between the distribution of the ledger authentication block by the leader block and the distribution of the exclusion authentication block by the second candidate block.
When used in large networks, more conflicts may occur compared to other consensus algorithms due to the faster transaction processing of the algorithm.
This depends on the decision of the third candidate block, but the algorithm specifies the following.
If the ledger authentication block of the leader block arrives first at the third candidate block, the third candidate block regards it as a normal situation.
If the exclusion authentication block of the second candidate block arrives first at the third candidate block, the leader block is excluded.
Alternatively, there is a method in which the third candidate block advertises the collision situation on the network.
However, this can cause another synchronization problem.
As with the reverse relevance, all blocks that are approximately `1 / 10` from the beginning of the candidate blocks are responsible for handling synchronization problems.
All other nodes in the network follow the decision of candidate blocks that are selected in turn.

<br/>

## Double Spending

A malicious reader block may attempt to make double spending by issuing each authentication block to two different networks connected.
The next leader block has been deterministically elected and receives one of the two authentication blocks first.
Then, the next leader block that receive this adds its own authentication block to the corresponding block and ignores other authentication blocks issued simultaneously by the previous leader block.
Depending on the purpose of the operation, it may be disadvantageous to the node of the leader block that has attempted malicious act.
Although it works deterministically, the last authentication block in the authentication block chain is considered to be an unconfirmed block.
Authentication is confirmed when one or more authentication blocks follow an authentication block.
However, this is done very quickly and still works with deterministic algorithms.

Confirmation can be made with only one succeeding authentication block, but it is also possible to use the threshold value for authentication confirmation by using the relevance.
All the added key blocks contain the sequence number and hash value of the last confirmed authentication block.
This is yet additional information to increase security, but not necessarily for the current algorithm.
Instead of the last confirmed authentication block, information can be included from the last authentication block that has not yet been confirmed.
If the relevance value of the candidate block exceeds the threshold value for authentication confirmation, it can be regarded that the authentication of the corresponding authentication block is confirmed.
However, this takes a lot of time, and this may be used for a denial of service attack because the information that has not yet been confirmed is included in the candidate blocks to be added.

<br/>

## 51% Attack and Localization

Similar to the PoW, 51% attack and localization problems occur.
However, these problems can be minimized by using the proprietary information that has an uneven distribution, such as stake in PoS.
In the case of localization, there are ways to include local information in relevance calculation.
When a pool of nodes is operated, it is possible to divide the area arbitrarily and to include the local information in the relevance calculation.
As such, problems can be minimized depending on how the proprietary information used and the relevance are calculated.

However, this algorithm is more resistant than PoW against 51% attack and localization problems. 
Although it is assumed that about 10000 nodes are required for satisfying the threshold value and one authentication block is generated in the 1 second, it takes about three hours for the newly added candidate block to become the leader block, and the consensus continues throughout that time.
Since it is not fixed during this time, it is constantly competing with blocks from other regions.
The same process is performed not only when a block is added to the end of a chain but also when a chain and a chain meet.
If chain and chain meet and compete, all following blocks are also discarded.
Even if it win the competition, a chain filled with blocks in one area will still go through the other areas for a long time, and consensus continues over all the blocks in the chain.
This long time consensus minimizes localization problems and, therefore, has a stronger tolerance for 51% attacks than PoW.
For this purpose, the base values of the algorithm should be adjusted according to the size of the network so that there is enough consensus time that localization does not occur.

<br/>

## Proprietary Information

The PoR can be used for both public blockchain that do not require permission to participate and private blockchain that only authorized users can join.
It can be used for a variety of purposes depending on what proprietary information is used to calculate relevance and how relevancy is calculated.
Proprietary information should be able to uniquely identify each node, be able to be authenticated by all nodes, and by which the relevance that can be quantified can be calculated.
Depending on what and how the proprietary information is defined, the object of identification can be an individual in the real world, not simply a node, and can be structured according to the structure of each country or organization.
A number of promised proprietary information may be used together or may be used in relation to each other.
Depending on the implementation, one node may have multiple proprietary information.
If the systematization of promised proprietary information is made in advance, access control of MAC, DAC and RBAC becomes possible.

When used as a private blockchain, you can use a method that publishes unique proprietary information to nodes that want to participate in advance.
In the real world, bank transaction services that use the public key certificate issued by the bank are example of this.
Even if you use other proprietary information than the proprietary key, you still need a public and private key pair to generate the authentication.
Here, it is also used as proprietary information, which can also be used in actual implementations.
If you use a public key certificate issued by a bank, it will be in the form of a private blockchain operated by each bank.
If you only have the key values for the public key and the private key that you have created yourself, you can substitute a public key certificate by including the evidence for the corresponding private key, such as the signature generated by the private key for the previous hash, and corresponding public key.
In this case, it can be used as a public blockchain.
If you do not use a valid public key certificate, a man-in-the-middle attack can be attempted by an attacker who has acquired all of the network control of a particular node.
However, this will be one of many nodes, and, like all consensus algorithms, this is not considered to be an attack on the blockchain itself from the point of view of the whole.

In this document, the proprietary key is used as proprietary information, which is itself identified and authenticated.
The self relevance is obtained by applying the number of bits obtained from the hash value comparison to `2 ^ m`.
To become proprietary information, three conditions must be met: identification, authentication, and self relevance.
In the case of self relevance, there must be a way to get it numerically depending on the proprietary information and its intended use.
And each base value of the algorithm should be adjusted according to the characteristics of each proprietary information.

The work of PoW can be used as proprietary information.
To get self relevance for the work, The `2 ^ m` in this document can be used as is.
Self relevance can be calculated using the number of consecutive `0` bits from the beginning as the value of `m`.
The input data of the hash puzzle will include the public key for identification and authentication, the hash value of the last candidate block in the chain, and nonce to obtain high self relevance.
These values must be published as proprietary information with the obtained hash puzzle, and then it can be verified by other nodes.
If candidate block with a low `m` or a low cumulative relevance among the candidate blocks in the chain is found, it will be targeted for competition.
You can use the purpose of the difficulty as it is used in this document, or you can use the method of PoW.
However, depending on what and how the difficulty is used, each base value of the algorithm must also be adjusted.

The stake of PoS can be used as proprietary information.
Identification and authentication of the stake will be the same as in PoS.
However, for self relevance, another way to quantify the consensus and stake in the PoS should be found.

The use of proprietary information may reveal an individual's identity.
A method such as zero knowledge proof should be used together with the purpose for which the chain is used.
If the proprietary information includes the location information of the node, there is also a possibility of an attack due to the structure of the algorithm.
It takes a very long consensus time until the newly added block issues the authentication.
During this time, the attacker can use the location information contained in the block's proprietary information to track the node to issue the next authentication.
There are ways to prevent this.
To do so, a system for proprietary information should be created, and each methodology should be created for each proprietary information.
However, the purpose of this document is not the systematization of proprietary information, but to demonstrate and verify the technical basic behavior of algorithm that use relevance.
It will be a separate project on proprietary information.

<br/>

## Compensation for Effort



<br/>

## Scalability



<br/>

###### ※ This algorithm was not designed for the purposes of ICO.<br/>Coin issuance may be required to raise money needed to implement and validate the algorithm.<br/>Even if a coin is issued, it should be aimed at the proof of concept of the algorithm, not profit.<br/>Compensation schemes are needed and follow the methods of other smart contract algorithms.<br/>I hope this algorithm solves many of the problems associated with the blockchain, so that the blockchain technology is activated.

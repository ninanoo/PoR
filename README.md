##### ※ 한국어 문서는 [이곳](https://github.com/ninanoo/PoR---Korean-Version)에 있습니다.
##### ※ I am posting changes or additional issues on [Facebook](https://www.facebook.com/hcmoon82).

<br/>
<br/>

##### *This algorithm is a methodology for*
### *&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A New Distributed Consensus and Distributed Ledger Technology*
##### *rather than just a proof of what.*

<br/>
<br/>
<br/>

> ### This has been studied to improve the Bitcoin's PoW algorithm.
<br/>
Compensation for effort, which is a social engineering technique, ensures that the current blockchain is maintained by a fair majority of participants, and this algorithm is also in that frame.<br/>
However, this algorithm does not use the amount of work by the computational power of each node as the criterion of selection for one consensus.<br/>
In the PoW(Proof-of-Work), it creates the most relevant block through the iterative operation at each node, but in this algorithm, the relevance of the block at each node is obtained decisively, and it finds the most relevant one among all these blocks in the entire network.<br/>
An effort in PoW is the ability to perform a high computation on a single node, but an effort in this algorithm is the ability of a single node to always maintain a high level of synchronization with the chain, and all these progressive states are probabilistic.<br/>
To that end, Nodes always do their best to be connected to the network and faithfully handle the protocol packets being transmitted.<br/>
<br/>
The most relevant block in PoW is the block with the hash value closest to 0, but in this algorithm, it is the block with the hash value closest to the hash value of the immediately preceding block.<br/>
For the relevance, this algorithm uses deterministic values that are based on random numbers, so do not have any patterns.<br/>
However, in actual implementations, the hash value closest to 0 can be used as the criterion for the selection, and this allows us to find the connection with the PoW's chain.<br/>
<br/>
Like PoW, this algorithm is also designed to operate as a public blockchain.<br/>
However, by issuing new proprietary information through the central organization or using the information already registered, it can also be operated as an permissioned blockchain.<br/>
The operational quantitative properties are dynamically adjusted according to the performance or security required for the chain, and attributes related to the network status, such as the total number of nodes participating in consensus or the transmission time between nodes, can be estimated from the chain.<br/>
Using those characteristics, the chain can also be operated in a closed or hybrid type.

<br/>
<br/>
<br/>
<br/>

> ### This solves the performance, scalability and localization problems, and guarantees the immediacy of issued authentication.
<br/>
One chain is operated, which consists of blocks with authentication for ledgers, and this chain has the same purpose and functionality as the PoW's chain.<br/>
However, in this algorithm, another chain is operated separately, which consists of blocks that have not yet issued authentication but are being consented to do so.<br/>
By consuming the first block of the chain consisting of these candidate blocks, the authentication block for the next ledger is issued.<br/>
This guarantees the immediacy of issued authentication and ensures the speed of issuance.<br/>
<br/>
Each block in the PoW's chain has a single link to the immediately preceding block, and the chain of this algorithm also has the same structure and functionality.<br/>
However, each block in this algorithm has one more link to another block in the far front, not just before.<br/>
This another link creates a horizontally partitioned chain structure, and these parallelized chains are tied together by authentication blocks which are connected to one another with its own complete security.<br/>
The physical structure of the actual chain is distributed chains parallelized in multiple, but the logical structure maintains a single chain.<br/>
Each node maintains only the information of one of these parallelized chains in its own node, and this makes this algorithm work as a distributed ledger rather than a shared ledger.<br/>
<br/>
The integrity of the PoW's chain is guaranteed with the entire blocks starting from the first block whose integrity is kept up with its own complete security at all times.<br/>
However, in this algorithm, the integrity of the entire chain is guaranteed with only some recent authentication blocks whose integrity is kept up with its own complete security but in a different methodology than PoW.<br/>
Security is guaranteed from the current participants and the current state, not the past participants and the past state.<br/>
This ensures that authentication for ledgers can have validity period and past blocks can be discarded.<br/>
This validity period provides the scalability for time, and the distributed chain provides the scalability for space.<br/>
<br/>
In PoW, consensus is made on only one block to be added each time.<br/>
However, in this algorithm, consensus continues on all candidate blocks managed as another chain.<br/>
To find one block, a number of consensus go on as distributed across the entire network, and until one authentication can be issued, it continues to converge as consensus on consensus.<br/>
To issue one authentication, there is not just one consensus but a large number of distributed consensus over the entire network space and entire time while it is a candidate block.<br/>
And then various techniques using the correlation of time and space are used, and the localization is also gradually reduced by these techniques.<br/>
With respect to all the consensus to be able to issue one authentication and the actual issuance of that authentication, the two actions are proceeded separately over a long period of time.<br/>
This allows the algorithm to be modified without chain's fork, and the modifications are gradually reflected in the entire network.

<br/>
<br/>
<br/>
<br/>

> ### All the detailed designs for this algorithm have already been completed.
<br/>

Detailed design of the underlying consensus theory has been completed and documented.<br/>

[Basic consensus](https://github.com/ninanoo/PoR/blob/master/BasicConsensus.md)<br/>
[Possibility of double spending](https://github.com/ninanoo/PoR/blob/master/PossibilityOfDoubleSpending.md)<br/>
[Attempts to tamper with already confirmed authentication](https://github.com/ninanoo/PoR/blob/master/AttemptsToTamperWithAlreadyConfirmedAuthentication.md)

The above documents show the theory of consensus and the technique by which authentication blocks for ledgers are issued.

<br/>

Detailed design of the addition of new candidate blocks has been completed and documented.<br/>

[Addition of the next candidate block](https://github.com/ninanoo/PoR/blob/master/AdditionOfTheNextCandidateBlock.md)

The above document shows the technique for reducing localization when a new candidate block is added to the chain.

<br/>

Detailed designs of the structures for scalability and synchronization of candidate chain have been completed.<br/>
However, the documentation of these two features has not yet been made.<br/>
As other parts are designed, there are some parts that need to be revised in existing documents, but they have not been done yet either.<br/>
Because English translation documents are being written at the same time, it takes more time than expected to write a document rather than to design an algorithm.<br/>
The documentation is not the main purpose, so the implementation may proceed first to make the algorithm easier and faster to understand.<br/>
Not a real engine development for commercialization, but it will be an implementation so that the entire algorithm is written in code and the way it works can be easily seen.<br/>
So here is a brief introduction to features that have not yet been documented.

<br/>
<br/>

This algorithm allows the candidate chain to branch so that the chain is formed into a tree structure.<br/>
However, the first candidate block to issue the next authentication must be unique, and for this, synchronization of the candidate chain proceeds over a long period of time corresponding to the threshold value.<br/>
The first design for synchronization was a locally distributed convergence depending on the addition of each new candidate block.<br/>
However, the final design has changed to be synchronized with the issuance of the next authentication block.<br/>
This significantly simplifies the algorithm and makes branched chains to converge more efficiently across the entire network.<br/>
Each method has advantages and disadvantages, so a mixed form of the two methods will be used in the implementation.<br/>
<br/>
Below is a simplified model to show that the entire distributed branches, forming one candidate chain, are converged on a regional basis.<br/>

```
4 |                                                      wxyz
- | -------------------------------------------------------------------------------------------------------------
3 |                          0xyz                         |                          1xyz
- | -------------------------------------------------------------------------------------------------------------
2 |            00yz           |            01yz           |            10yz           |            11yz
- | -------------------------------------------------------------------------------------------------------------
1 |     000z    |     001z    |     010z    |     011z    |     100z    |     101z    |     110z    |     111z
- | -------------------------------------------------------------------------------------------------------------
0 | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111

    N-00   N-01   N-02   N-03   N-04   N-05   N-06   N-07   N-08   N-09   N-10   N-11   N-12   N-13   N-14   N-15
```

The numbers from 4 to 0 in the leftmost column represent the number of difficulty bits on each line, and all other columns to the right of that column are the hash values of candidate block headers.<br/>
Only for the above model, the proprietary information and the hash value are 4 bits long, and the values were assumed to be completely random, with no collision at that number of bits.<br/>
Difficulty 0 is used to create a new candidate block, so it is not limited by the difficulty.<br/>
In addition, no localization was considered, and the network was assumed to be completely hierarchical, with a constant time distance for each hop.<br/>
This network consists of 16 nodes, from N-00 to N-15, corresponding to the entire hash bits.<br/>
Depending on the characteristics of the network and the total number of those nodes, the candidate chain at all nodes consists of five candidate blocks.<br/>

Until now, a [threshold](https://github.com/ninanoo/PoR/blob/master/BasicConsensus.md#threshold-value-and-relevance-efficiency-ratio) was used to allow one authentication block to be issued, and as a result, the number of candidate blocks at each node could be different due to the branching of the chain.<br/>
However, as the design for scalability was added to the algorithm, it has been changed so that all nodes have the same number of candidate blocks.<br/>
In the new design, one authentication block can be issued as long as a certain number of candidate blocks, which meet the difficulty, are gathered.<br/>
The threshold is still used, but a dynamic value lower than before is used.<br/>
As the role of threshold has been reduced, the relevance efficiency ratio or the speed of authentication issuance is even more affected by the difficulty as well as the size of the network.<br/>

The hash value of the leader block is wxyz, which has a specific value of either 0 or 1 in each digit.<br/>
The difficulty is 0, so all nodes can publish their own one candidate block each time and each one node forms one zone.<br/>
In the case of the synchronization method where candidate blocks are distributed and converged on a zone basis, candidate blocks published by each node arrive in the adjacent zone first, and new consensus are made.<br/>
The term consensus has been used, but it is precisely a consensus for convergence.<br/>
There are two kinds of consensus in this algorithm: consensus to converge branched candidate blocks and consensus to confirm one issued authentication block.<br/>
The 0101 candidate block published by the N-05 node arrives at the N-04 and N-06 nodes first, and a new consensus is made.<br/>
The candidate chain of N-05 node consists of candidate blocks with hash values of wxyz, 0xyz, 01yz, 010z and 0101, respectively.<br/>
When difficulty 2 is used above, four nodes of N-04, N-05, N-06 and N-07 form one zone, and 01yz satisfying yz of 2-bit length is shared as the most recently created candidate block.<br/>

<br/>

Although the process is different, this algorithm also requires a large amount of effort that can be compared to the work of PoW.<br/>
However, if the profit to be obtained is greater than the amount of effort involved, or if there are malicious purposes such as disabling of the chain, then double spending may be attempted, and this is possible by two adjacent candidate blocks colluded.<br/>
If 8 of the 16 nodes in the chain above are actually run by one owner, double spending can be attempted with 50% chance.<br/>
To prevent this, the algorithm assumes that one logical node is operated by one owner.<br/>
In practice, however, the number of nodes is allowed so as not to significantly affect each probabilistic state for the various base values of this algorithm.<br/>

An owner can be specified in the real world through the user subscription information of institutions, companies or online services.<br/>
Information such as mobile phone number through SMS authentication can also be used as a proprietary information to prove an owner.<br/>
In order to specify any one owner in the real world, it must be accompanied by identification and authentication through secure systems and complete procedures.<br/>
There may be cases in which many of these proved owners have been colluded, but in quantitative terms it cannot be compared to the scale of the nonce in PoW.<br/>
These are in the form of a permissioned blockchain.<br/>

In order to operate more like a public blockchain, stake can be used.<br/>
Although it was expressed in terms of stake, it is used differently from the stake in PoS(Proof-of-Stake).<br/>
It is not for consensus among candidate blocks but only for a one-time ticket to publish one candidate block.<br/>
The owner, who wants to publish a candidate block, must be authenticated by registering his proprietary information as a new ledger in the chain in advance.<br/>
To register a single proprietary information, the owner must create a new public and private key pair.<br/>
The ledger contains the created public key and the time value at registration.<br/>
The right to publish a candidate block has an expiration date based on this time value, and this may be different from the validity period which provides scalability for the chain.<br/>
The proprietary information is combined with this time value and registered as a secret value encrypted with the public key.<br/>
The owner, who has acquired the right to publish, can create a new candidate block.<br/>
The header of the new candidate block contains the block number of the authenticated proprietary information ledger, and the hash value of the new candidate block header is added as a provable value encrypted with the private key.<br/>

As an owner's wallet address is used as proprietary information, techniques such as zero-knowledge proof can be added to provide anonymity to the owner.<br/>
This anonymity is guaranteed permanently even after the owner's new candidate block is transformed into a new authentication block.<br/>
However, regardless of this anonymity to owners, all candidate blocks are always anonymous.<br/>
When a new authentication block is issued by an owner, the proof of his proprietary information is included in the header.<br/>

Several rights to publish one or more new candidate blocks may be acquired by any one owner, but the quantity is limited and managed.<br/>
In order to acquire one right, an owner must prove that he is eligible or provide the chain with a corresponding value.<br/>
This value needed to operate as a public blockchain corresponds to the value of the real money in the real world.<br/>
The ratio of this value is dynamically adjusted to the spatial performance of the chain so that all owners act reasonably.<br/>
In addition, the validity period is used for each ledger or authentication block to which individual values are linked.<br/>
If no additional control structure is designed, the linked values also have the validity period.<br/>

When one or more other authentication blocks follow after an authentication block is issued, the authentication of the first issued block is confirmed.<br/>
This may result in a double spending if two adjacent candidate blocks were issued by one owner or colluded by more than one.<br/>
To prevent this, the owners are limited as shown above, and because very large numbers are also used, it is probabilistically very difficult to control the order of the blocks as intended.<br/>
Based on the probability that two candidate blocks issued in collusion will not be adjacent to each other, values such as the threshold or difficulty are determined.<br/>
Even if a double spending succeeds with an impossible probability for a very short time, those blocks are flagged as excluded blocks by all other following blocks.<br/>
The integrity and legitimacy of a newly issued authentication block are actually verified and excluded by all following candidate blocks rather than just one adjacent block.<br/>
Even if authentication of a block in which the double spending was attempted is confirmed by a few blocks, all colluded blocks will be excluded as an implicit agreement by all following legitimate blocks.<br/>
In all following blocks, if there are more than 50% of the blocks colluded for one double spending, there is also more than 50% of a probability that they will not be excluded.<br/>
However, once authentication is confirmed by a following block and then the confirmed block is actually excluded by another following block, the chain is currently in trouble.<br/>
The ratio of the blocks which can be colluded and the cases in which two colluded blocks can be adjacent are actively controlled by the algorithm itself to be probabilistically impossible.<br/>
As a result, the authentication in this algorithm can be confirmed with just one following authentication block.<br/>

<br/>

In the above model, it was described as a simplified hierarchical network structure with only leaf nodes.<br/>
In practice, however, a P2P network in the form of mesh is used where the hierarchy is not complete and the time distance of each hop is also not constant.<br/>
Additionally, each path in the tree was described as the candidate chain at each node, which shown the locally distributed convergence.<br/>
However, the above model can also be viewed as connections of zones in any one part of a P2P network having a hierarchical structure at the same time, rather than a tree-shaped branching of the chain.<br/>
In that case, the average number of hops for which a block in a zone reaches the entire network approximates the height of the tree.<br/>
<br/>
The network for this algorithm is logically structured through the following relations based on the total number of nodes.<br/>

```
b : branch quotient bits
z : the total number of zones           ( z = 2 ^ b )

d : difficulty bits
p : the total number of peers per zone  ( p = 2 ^ d )

r : average relevance bits              ( r = b + d )
n : the total number of nodes           ( n = 2 ^ r = z * p )

h : zero-based height of tree           ( h = b / d )
```

The difficulty determines how many peers a node should connect to.<br/>
However, this is a logical base value for the chain, and the actual number of physical peers in this P2P network may be different.<br/>

In [the recent document](https://github.com/ninanoo/PoR/blob/master/AdditionOfTheNextCandidateBlock.md), it was mentioned that a new candidate block is transmitted using one set of packed blocks as one unit.<br/>
The height of the tree shown above is used as the number of blocks to be packed for one set.<br/>
This corresponds to the minimum number of candidate blocks required for one authentication block to be issued.<br/>
However, the relations shown above are characteristics of the network derived from a simplified model, so the actual total number of candidate blocks is much larger than that.<br/>
In fact, election of a new candidate block is processed in units of a set of recent candidate blocks, and cumulative relevance by an exponential ratio is applied there.<br/>
The elected whole candidate block represents the whole node connected to the network, so the linear scaling for this is also applied.<br/>
In addition, the number of candidate blocks must be large enough to operate as distributed chains for scalability.<br/>
Because probabilistic values based on statistics are used, the more samples the algorithm has, the more accurate the algorithm works.<br/>
Because of these characteristics, nodes can know the status values such as the transmission time or the number of nodes of the current network from the chain.<br/>
The authentication chain has a synchronized state for the entire network, and the candidate chain has a distributed state for each chain branch.<br/>

In practice, starting from at least 1000, usually about 10000 candidate blocks are operated, and these blocks are distributed and converged on a zone basis.<br/>
In this progression, for flow and congestion control to manage the bandwidth of the network, the number of blocks to be compressed and the waiting time are dynamically adjusted for each transmission.<br/>
As the network grows, efficient buffering is also required because not only the number of blocks in a single chain but also the number of branches in the entire network increases together.<br/>
However, in order to synchronize all chain branches by converging up from the last block for a tree with a height of 10000, tons of resources in the network and nodes may be consumed even with these techniques, and this can be considered a waste of resources.<br/>
The complete synchronization of the entire chain does not necessarily mean a condition for issuing an authentication block.<br/>
In addition, nonlinear ratios such as relevance factor are used to converge the blocks, so the chain does not branch in the form of a complete tree, but it branches with an exponential increase toward the bottom.<br/>
Reflecting these characteristics, regionally distributed convergences only proceed for a few sets which are packed with recent candidate blocks at the bottom of the chain.<br/>
The greater part of a candidate chain except the bottom part is actually kept as one stem for most of the time.<br/>
Blocks belonging to that part are synchronized from the top of the chain.<br/>
In the following paragraphs, it is shown how this synchronization works in a real network.<br/>

<br/>

The following shows the candidate chain in each of their nodes for the five owners: James, Alice, Lewis, Maria, and Clark.<br/>

```
James  {0} ~ {67372} - [67373]           ~ (77372)
Alice  {0} ~ {67372} - (67373) ~ [75428] ~ (77372)
Lewis  {0} ~ {67372} - (67373) ~ [74593] ~ (77372)
Maria  {0} ~ {67372} - (67373) ~ [77285] ~ (77372)
Clark  {0} ~ {67372} - (67373) ~ [77285] ~ (77372)
```

The braces and parentheses correspond to the authentication block and the candidate block, respectively, and the square brackets are the candidate block published by each node.<br/>
The block header of this algorithm contains a sequence number, and only the sequence number is shown in the example above.<br/>
The sequence number of the first block is zero.<br/>
So far, up to 67372 authentication blocks have been issued and synchronized on all nodes.<br/>
The above candidate chains consist of 10000 candidate blocks, and the current leader block is block 67373.<br/>
The above five owners have published one candidate block in their chain branch, respectively.<br/>
The five candidate chains above are the different branches of the chain, which are randomly selected from the entire candidate chain, so the last added candidate blocks are also different.<br/>
<br/>
The following shows the chain branches for only the above five nodes among the entire candidate chains branched in a tree form.<br/>

```
  {0}
   :
{67372}
   |
[67373]
   :
(74592)-------------
   |               |
(74593)         [74593]
   :               :
(75427)-----       :
   |       |       :
(75428) [75428]    :
   :       :       :
   :       :    (77284)-------------
   :       :       |       |       |
   :       :    (77285) [77285] [77285]
   :       :       :       :       :
(77372) (77372) (77372) (77372) (77372)

 James   Alice   Lewis   Maria   Clark
```

As we can see above, all other nodes except James own each candidate block corresponding to the sequence numbers where the chain was branched.<br/>
The branched chains are synchronized by these blocks which caused each branching.<br/>
James, who owns the current leader block of sequence number 67373, uses this block to issue the next authentication block.<br/>
At this time, the entire header information, which corresponds to all following blocks from 67373 to 77372, is also bundled together with the authentication block.<br/>
James's candidate chain is used as a reference chain for synchronization of branched chains.<br/>
The header of any candidate block does not yet contain new ledgers and their authentication information, so it does not exceed 100 bytes.<br/>
So, information about 10000 blocks, which are the total candidate blocks at any one node, does not exceed 1MB.<br/>
Along with the new authentication block, the information of the reference chain also arrives at all other nodes in unspecified order.<br/>
Each of those nodes compares the received reference chain with its own candidate chain.<br/>
When any branched block is found in comparison with the reference chain, the nodes compare the cumulative relevance of those two blocks for each branch.<br/>
If the reference chain is more relevant, the nodes discard their own candidate chain and select the reference chain as the new candidate chain.<br/>
If their own candidate chain is more relevant, the header information of their own candidate blocks, which are from the immediately preceding block of the branched block to the last block, is transmitted to the network.<br/>
This information is used as a new reference chain for synchronization at all other nodes.<br/>
Multiple pieces of simultaneous reference information are continuously generated and correlated with each other over the entire network, and the branches of the chain converge into a single chain over a long period of time.

<br/>
<br/>

This algorithm provides scalability for time and space, respectively.<br/>
In order for the chain to be scalable for the entire time being operated, the validity period for each authentication of ledgers is used.<br/>
In order for the chain to be scalable across the entire network space at any time, the authentication chain is operated in distributed chains.<br/>
The first scalability design for space was to pipeline the issuance of authentication.<br/>
The leader block only collects and synchronizes all ledgers that are subject to one issuance, and then distributes the ledgers to other blocks that will issue the authentication.<br/>
The methods used in BFT(byzantine fault tolerance) and DAG(directed acyclic graph) were partially included.<br/>
That approach divides the single authentication chain into a large number of parallelized chains, and increases the throughput of authentication issuance.<br/>
However, it makes many parts of the current algorithm redesigned for synchronization, and increases a single response time until authentication for one ledger is completed.<br/>
So, in the first implementation, no authentication is issued in parallel.<br/>
Authentication is always issued only by a single node, but the single authentication chain is operated in multiple chains, which are parallelized and distributed, to provide space scalability.<br/>
However, at the end of this section, the structure for parallelizing the issuance of authentication, which is still under design, will be briefly introduced.<br/>

<br/>
<br/>

**( Scalability-related contents had to be added here.<br/>**

**Ledger and authentication block each have their own separate validity period.<br/>**
**The next expired authentication blocks located at the head of the current authentication chain are removed from the chain, at which time the ledgers whose period has not yet expired are included in the new authentication block again.<br/>**

**Scalability for time above is applied with scalability for space.<br/>**
**The whole owner belongs permanently to each particular group by the modular decomposition using the proprietary information as the modular factor.<br/>**
**A new chain is formed by the new group composed by this division method, and the initial single authentication chain works as distributed and parallelized chains concurrently.<br/>**
**Since then, an owner can publish new candidate blocks only for that one chain to which he belongs, and new authentication blocks transformed from these blocks also belong only to that chain.<br/>**
**In fact, more precisely, an owner keeps the authentication blocks contained in the chain to which he belongs and the two chains adjacent to that chain.<br/>**
**The number of groups dynamically increases or decreases depending on the status of the global chain and network, so the overall chain looks like a modular graph but has the characteristics of a directed acyclic graph.<br/>**
**Apart from this, because the initial single chain also continues to be used as was, one block is tied to all of the different chain structures concurrently and has links to two or more previous blocks.<br/>**
**The issued authentication blocks are distributed and stored in their respective groups, but new authentication blocks are issued one at a time from the candidate chain that always has one leader block along the initial single chain.<br/>**
**In other words, it follows the previous way to elect a new candidate block or issue a new authentication block.<br/>**
**However, it operates as a distributed storage rather than a shared storage to achieve the scalability for space.<br/>**

**The parallelization of authentication issuing involves the distribution of authentication storing.<br/>**
**The hash values of the ledgers for which authentication is requested are also modularized by n, so all ledgers also belong to their respective distributed chains.<br/>**
**Each distributed chain also works as a separate candidate chain, so it operates as a complete distributed chain where the initial single chain is no longer used, and the candidate chain of each distributed chain is again divided into its own chain branches.<br/>**
**However, each distributed chain works in connection with two adjacent distributed chains, and the information in a block spreads throughout all distributed chains after n/2 rounds.<br/>**
**As the issuance of authentication is parallelized, the throughput is increased by n times, but the response time in each issuance is the same as that of the initial single chain.<br/>**

**All these facilities are based on the cryptographic characteristics: the randomness of uniform distribution and the probabilistic approach in large-scale distributed system.<br/>**

**Not sure when I will be free, so it has been briefly introduced first. )<br/>**

<br/>
<br/>
<br/>

There are three types of time critical blocks in this algorithm.<br/>
A block issued with authentication for ledgers does not affect the operation of the algorithm, so those critical blocks are all candidate blocks.<br/>
In [the first document](https://github.com/ninanoo/PoR/blob/master/BasicConsensus.md), the leader block was introduced, which is the first candidate block of the candidate chain.<br/>
It was described that the leader block can be constrained by time and excluded by its subsequent blocks.<br/>
The leader block can be excluded by the candidate blocks corresponding to approximately 1/10 of the leading part of the candidate chain, and a base value corresponding to the number of these blocks is determined according to target values and status values.<br/>
However, in the current final design different from the first design, the number of those blocks is not limited.<br/>
In an extreme experiment, the exclusion of the unique leader block can proceed simultaneously in different candidate blocks which have the same sequence number in each branched candidate chain, and this can be seen as an uncertainty in terms of the entire network.<br/>
However, in this algorithm, branching of a chain is used as a favorable function, and all functions operate recursively on each branch.<br/>
Uncertainty makes attacks more difficult from the whole point of view, but candidate blocks operate probabilistically based on their own branch.<br/>
In addition, in the first design, an indirect method of comparing [reverse relevance](https://github.com/ninanoo/PoR/blob/master/BasicConsensus.md#reverse-relevance-and-game-theory) was used to constrain time.<br/>
However, from the design so far, a direct time base is used, which is similar to the average transmission time introduced in [the recent document](https://github.com/ninanoo/PoR/blob/master/AdditionOfTheNextCandidateBlock.md).<br/>
Those time constraint and exclusion rule are equally applicable to the other two types of critical blocks that have not yet been documented.<br/>
The first candidate block of each branch is responsible for synchronizing the branched candidate chains.<br/>
The first candidate block of each distro is responsible for synchronizing the distributed authentication chains.<br/>
In the three cases so far, the time bases for exclusion differ from each other, but these time-related rules make the chain work permanently.

<br/>
<br/>
<br/>

> ### This is a new design only for distributed consensus and distributed ledger technology.
<br/>
Below is a layered architecture that shows the methodology in which this algorithm is used for common blockchain application services.<br/>
<br/>

```
*********************************************************************
*                    Decentralized Applications                     *
*********************************************************************
*               ?              *           Smart Contracts          *
*********************************************************************
*            Distributed Consensus and Distributed Ledger           *
*********************************************************************
```

The empty component of the second layer is the token systems that the current public blockchain algorithms are implementing.<br/>
This algorithm has been designed only for the lowest layer, "Distributed Consensus and Distributed Ledger", so it does not include designs for "Token Systems", "Smart Contracts" and "Decentralized Applications".<br/>
This algorithm follows the layered architecture style.<br/>
Functioning in the lowest layer as a base technology, it provides interfaces to the upper layer in which the token systems and smart contracts are.<br/>
A new smart contract can be designed for this algorithm, but smart contracts of other blockchain algorithms may also be provided as modules.<br/>
Depending on the service characteristics of the upper layer, smart contracts with different characteristics may be used alternately.<br/>
<br/>
In order for participants' efforts to be compensated, it may not be necessary to have a token system, so its component was not labelled in the diagram above.<br/>
Current tokens are functioning as a means of measuring, transferring and storing the value corresponding to the effort.<br/>
To operate as a valuable thing, it is being measured and stored as specific data, and is being exchanged for commodity money.<br/>
However, even though there is no concrete medium called a token, there are technological methodologies that can make compensation possible.<br/>
Before money emerged in the real world, there had been barter exchanges to exchange value synchronously, and there had been promises to exchange labor with each other, which operate asynchronously.<br/>
However, the most efficient methodology for managing value in the real world is money, and in the blockchain, it is a token or a coin.<br/>
There are not enough social and economic knowledge to say that functioning as a currency or having similar effect is right or wrong, but at least that is still a necessary approach to be operated as a public blockchain.<br/>
The relevant structural parts, which are for issuing tokens in this algorithm, are not significantly different from the structural parts of other blockchain algorithms.<br/>
However, this algorithm does not include any direct structural design for compensation, but instead interfaces are provided for interworking with the token systems of the upper layer.<br/>
This last section's contents only are not a summary of the overall architecture design that has been completed, but rather a direction that will be applied to this algorithm.<br/>


<br/>
<br/>
<br/>

###### *I think the distributed consensus technology can be used for the social infrastructure<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;, which allows the will of the people to be fairly gathered,<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rather than being used as a tool for someone to make money.<br/><br/>And I hope this algorithm can be used for it.*

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
However, by issuing new proprietary information through the central organization or using the information already registered, it can also be operated as an authorized blockchain.<br/>
The operational quantitative properties are dynamically adjusted according to the performance or security required for the chain, and attributes related to the network status, such as the total number of nodes participating in consensus or the transmission time between nodes, can be estimated from the chain.<br/>
Using those characteristics, the chain can also be operated in a closed or hybrid type.

<br/>
<br/>
<br/>
<br/>

> ### This solves performance, scalability and localization, and guarantees the immediacy of issued authentication.
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
This validity period provides the scalability to time, and the distributed chain provides the scalability to space.<br/>
<br/>
In PoW, consensus is made on only one block to be added each time.<br/>
However, in this algorithm, consensus continues on all candidate blocks managed as another chain.<br/>
To find one block, a number of consensus go on as distributed across the entire network, and until one authentication can be issued, it continues to converge as consensus on consensus.<br/>
To issue one authentication, there is not just one consensus but a large number of distributed consensus over the entire network space and entire time while it is a candidate block.<br/>
In addition, various techniques using the correlation of time and space are used, and the localization is gradually reduced by these techniques.<br/>
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

This algorithm allows the candidate chain to branch so that the chain is formed into a tree structure, where the occurrence of a new branch exponentially increases at the back of the chain.<br/>
However, the first candidate block to issue the next authentication must be unique, and for this, synchronization of the candidate chain proceeds over a long period of time corresponding to the threshold value.<br/>
The first design for synchronization was a locally distributed convergence depending on the addition of each new candidate block.<br/>
However, the final design has changed to be synchronized with the issuance of the next authentication block.<br/>
This significantly simplifies the algorithm and makes branched chains to converge more efficiently across the entire network.<br/>
Each method has advantages and disadvantages, so a mixed form of the two methods may be used for the implementation.<br/>
<br/>
The following shows the candidate chain in each of their nodes for the five participants: James, Alice, Lewis, Maria, and Clark.<br/>

```
James  {00000} ~ {67372} - [67373]           ~ (77292)
Alice  {00000} ~ {67372} - (67373) ~ [75428] ~ (77362)
Lewis  {00000} ~ {67372} - (67373) ~ [74593] ~ (77290)
Maria  {00000} ~ {67372} - (67373) ~ [77285] ~ (77328)
Clark  {00000} ~ {67372} - (67373) ~ [77285] ~ (77311)
```

The braces and parentheses correspond to the authentication block and the candidate block, respectively, and the square brackets are the candidate block issued by each node.<br/>
The block header of this algorithm contains a sequence number, and only the sequence number is shown in the example above.<br/>
The sequence number of the first block is zero.<br/>
So far, up to 67372 authentication blocks have been issued and synchronized on all nodes.<br/>
The sequence number of the leader block, which is owned by James, is 67373, and the block has been synchronized on all nodes.<br/>
The other nodes have published one candidate block in their chain branch, respectively.<br/>
The five candidate chains above are the different branches of the chain, which are randomly selected from the entire candidate chain, so the last added candidate blocks are also different.<br/>
<br/>
The following shows the chain branches for only the above five nodes among the entire candidate chains branched in a tree form.<br/>

```
{00000}
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
   :       :    (77290)    :       :
(77292)    :               :       :
           :               :    (77311)
           :            (77328)
        (77362)

 James   Alice   Lewis   Maria   Clark
```

As we can see above, all other nodes except James own each candidate block corresponding to the sequence numbers where the chain was branched.<br/>
The branched chains are synchronized by these blocks which caused each branching.<br/>
James, who owns the current leader block of sequence number 67373, uses this block to issue the next authentication block.<br/>
At this time, the entire header information, which corresponds to all following blocks from 67374 to 77292, is also bundled together with the authentication block.<br/>
James's candidate chain is used as a reference chain for synchronization of branched chains.<br/>
The header of any candidate block does not yet contain new ledgers and their authentication information, so it does not exceed 100 bytes.<br/>
It was assumed that the candidate chain will be maintained at a number of approximately 10000 candidate blocks, so the total header information will not exceed 1 MB.<br/>
Along with the new authentication block, the information of the reference chain also arrives at all other nodes in unspecified order.<br/>
Each of those nodes compares the received reference chain with its own candidate chain.<br/>
When any branched block is found in comparison with the reference chain, the nodes compare the cumulative relevance of those two blocks for each branch.<br/>
If the reference chain is more relevant, the nodes discard their own candidate chain and select the reference chain as the new candidate chain.<br/>
If their own candidate chain is more relevant, the header information of their own candidate blocks, which are from the immediately preceding block of the branched block to the last block, is transmitted to the network.<br/>
This information is used as a new reference chain for synchronization at all other nodes.<br/>
Multiple pieces of simultaneous reference information are continuously generated and correlated with each other over the entire network, and the branches of the chain converge into a single chain over a long period of time.

<br/>
<br/>

This algorithm provides scalability to time and space, respectively.<br/>
In order for the chain to be scalable for the entire time being operated, the validity period for each authentication of ledgers is used.<br/>
In order for the chain to be scalable across the entire network space at any time, the authentication chain is operated in distributed chains.<br/>
The first scalability design for space was to pipeline the issuance of authentication.<br/>
The leader block only collects and synchronizes all ledgers that are subject to one issuance, and then distributes the ledgers to other blocks that will issue the authentication.<br/>
The methods used in BFT(byzantine fault tolerance) and DAG(directed acyclic graph) were partially included.<br/>
That approach divides the single authentication chain into a large number of parallelized chains, and increases the throughput of authentication issuance.<br/>
However, it makes many parts of the current algorithm redesigned for synchronization, and increases a single response time until authentication for one ledger is completed.<br/>
So, in the final design, no authentication is issued in parallel.<br/>
Authentication is always issued only by a single node, but the single authentication chain is operated in multiple chains, which are parallelized and distributed, to provide space scalability.<br/>
<br/>
<br/>

***( Within a few days, the scalability related contents would be written here... )***

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
Those time constraint and exclusion rule are equally applicable to the other two types of critical blocks that have not yet been documented.<br/>
The first candidate block of each branch is responsible for synchronizing the branched candidate chains.<br/>
The first candidate block of each distro is responsible for synchronizing the distributed authentication chains.<br/>
A probabilistically estimated value is used as a time base for the exclusion in both those cases.<br/>
To this end, [a recent document](https://github.com/ninanoo/PoR/blob/master/AdditionOfTheNextCandidateBlock.md) has shown how to get the average transmission time over the entire network.<br/>
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
To act as a currency, the value is being measured and stored as specific data, and is being exchanged for commodity money.<br/>
However, even though there is no concrete medium called a token, there are technological methodologies that can make compensation possible.<br/>
Before money emerged in the real world, there had been barter exchanges to exchange value synchronously, and there had been promises to exchange labor with each other, which operate asynchronously.<br/>
However, the most efficient methodology for managing value in the real world is money, and in the blockchain, it is a token or a coin.<br/>
There are not enough social and economic knowledge to say that functioning as a currency or having similar effect is right or wrong, but it is a necessary approach to be operated as a public blockchain.<br/>
The relevant structural parts, which are for issuing tokens in this algorithm, are not significantly different from the structural parts of other blockchain algorithms.<br/>
However, this algorithm does not include any direct structural design for compensation, but instead interfaces are provided for interworking with the token systems of the upper layer.<br/>
This last section's contents only are not a summary of the overall architecture design that has been completed, but rather a direction that will be applied to this algorithm.<br/>


<br/>
<br/>
<br/>

###### *I think the distributed consensus technology can be used for the social infrastructure<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;, which allows the will of the people to be fairly gathered,<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rather than being used as a tool for someone to make money.<br/><br/>And I hope this algorithm can be used for it.*

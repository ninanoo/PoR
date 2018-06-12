###### ※ PoR is a new open blockchain consensus algorithm and is still theoretical.<br/><br/>I hope this algorithm will be discussed and improved with the people who study and develop the block chain.<br/><br/>If those who can handle nonlinear values well are involved, I think a complete mathematically provable algorithm will be created.<br/><br/>And I am looking for those who can help with the [Korean-English translation](https://github.com/ninanoo/PoR---Korean-Version/issues/1) of [Korean document](https://github.com/ninanoo/PoR---Korean-Version).

<br/>

# PoR
PoR: Proof of Relevancy ( Blockchain Consensus Algorithm determined by Relevancy )

PoR is a blockchain consensus algorithm that the next block is determined by relevancy.
The relevancy is obtained from the proprietary information of each block between adjacent blocks.
The relevancy can also be created from the work of proof of work or the stake of proof of stake.
Here, the asymmetric key pair of each block is used as the proprietary information.
It uses a hash chain of Bitcoin, but has a double chain structure such as Bitcoin-NG.
There are a key block chain and an auth block chain linked each other.
Because of relevancy, reverse relevancy and the threshold value for auth block generation as well as the double chain, the certification for the ledger operates deterministically.
Attacks such as double spending or finney attack do not occur because authentication to the ledger is deterministic.
It is more resistant than bitcoin against 51% attack and localization problems.
High-speed processing is possible enough to generate each authentication block for the unit ledgers without the use of merkle tree depending on the size of the network.

<br/>

## Relevancy Formula
![relevancyFormula](relevancyFormula.png?raw=true "relevancyFormula")
```
r      : relevancy
c      : number of following blocks including the target block ( c > 0 )
n      : sequence number of candidate blocks starting with 0 ( n < c )
m of n : number of consecutive bits with the same value as the previous hash value starting from the beginning
a      : relevancy factor ( a > 1 )
```

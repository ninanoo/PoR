###### ※ PoR is an open blockchain consensus algorithm and is still theoretical.<br/><br/>I hope this algorithm will be discussed and improved with the people who study and develop the block chain.

<br/>

# PoR
PoR: Proof of Relevancy ( Blockchain Consensus Algorithm determined by Relevancy )

PoR is a blockchain consensus algorithm that the next block is determined by relevancy.
The relevancy is obtained from the unique information of each block between adjacent blocks.
Here, the asymmetric key pair of each block is used as the unique information.
It uses a hash chain of Bitcoin, but has a double chain structure such as Bitcoin-NG.
One is key block chain and the other is ledger block chain.
Because of relevancy, reverse relevancy and the threshold value for ledger block generation as well as the double chain, the certification for the ledger operates deterministically.

<br/>

## Relevancy Formula
![relevancyFormula](relevancyFormula.png?raw=true "relevancyFormula")
```
r      : relevancy
c      : number of following blocks including the target block ( c > 0 )
n      : sequence number of candidate blocks starting with 0 ( n < c )
m of n : number of consecutive bits with the same value as the previous hash value starting from the beginning
a      : difficulty factor ( a > 1 )
```

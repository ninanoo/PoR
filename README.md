# PoR
PoR: Proof of Relevancy ( Blockchain Consensus Algorithm determined by Relevancy )

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
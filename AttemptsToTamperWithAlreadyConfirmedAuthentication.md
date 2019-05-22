Although it is a new type of consensus algorithm, this algorithm is basically a blockchain.
So when I first wrote the document, it was missing both basic and most important parts.
They are things that I do not realize the need to write because it is taken for granted.
Proprietary information and compensation were also filled in by community feedback after the first writing.

The contents of the tamper attempt should be explained, but it is missing.
I can not afford to modify the main document, so for the time being I will have to keep the extra contents on the issue and apply it once it is a chance.

Like the PoW, in this algorithm, it is possible to try forgery of the already confirmed authentication.
However, from the conclusion, falsification and tampering is impossible because all base values will be determined based on the computational complexity.

As described in the document, relevance is calculated only for candidate blocks.
However, in practice, the relevance of all blocks in the chain, including those blocks that have been confirmed by issuing an authentication, can be calculated.
The relevance of a block that has been confirmed by issuing an authentication contains all the blocks that follow it at the time it is calculated.
As authentication continues to be issued, the blocks that previously issued authentication become more and more relevant.
In the entire chain, the entire block of the chain is involved in calculating the relevance of the first block.

It may be assumed that another authentication block having a relevance greater than the relevance of a block, even if the block has already issued the authentication, is found at a certain point in time.
When this block is the attacker's, it may be a block with only its own relevance or a block followed by a number of subsequent blocks.
However, if you attack with only one block, it is as hard as finding out the private key corresponding to the public key of the target block.
When an attacker's authentication block is followed by a number of subsequent blocks, it becomes a situation that chain and chain meet in the section where the authentications have already been issued.
The current document is aimed at very high throughput, so this situation may be occurred.
There are no restrictions other than the difficulty in order to add new blocks to the chain to meet the threshold of the leader block.
The difficulty should be set at a compromise value that does not result in consuming transactions in the network without degrading the throughput of the authentication issuance, and this also requires a formula.
Difficulty is not a hash puzzle.
Therefore, an attacker can generate a large number of subsequent blocks to follow itself in order to be more relevant than the relevance of the target authentication block.
At this time, the attacker's blocks will barely satisfy the difficulty.
In the document, the graph using the relevance factor of 2^16 required 10000 blocks to have the relevance of 2^25 approximately.
2^25 is the relevance of 3.9*(10^7) approximately.
Assuming that the same relevance factor of 2^16 is used and the same 10000 blocks follow, it has the relevance of 2.3*(10^5) in the case of an attacker who is only satisfied with difficulty.
The attacker must add more subsequent blocks because the attack can not succeed due to the lower relevance.
In fact, in order for the attacker to be close to the relevance of 3.9*(10^7), approximately 1708000 subsequent blocks must follow.
It is the number when all blocks of the attacker have self relevance of 2^8, which equally satisfies only the difficulty.
This is a very large number that can not be handled by a single node.
Although not intended, all 1708000 subsequent blocks must also satisfy the difficulty.
The design for actual implementation related to the diffusion and convergence process in the network has not yet been carried out, but it is traffic that can not be supported in the network.
This is due to the self relevance calculation formula of 2^m which is obtained exponentially increasing in proportion to the number of matched bits.
In terms of complexity, finding one more matching bit is the same case as for hash power which has to be added in the PoW.

Applying complexity theory to exponential distribution makes all consuming attacks impossible.
With the current algorithm alone, tampering of already confirmed authentication can not occur.
However, lower base values can be used depending on the network environment and the required performance or required security.
In some cases, such as the IOT environment, it may be lower than the minimum values.
Although this has not yet fully been considered, you can use relevance efficiency ratio as an additional device only for the tampering of authentication.
When a chain meets a chain, in addition to the relevance, it can be set to satisfy the minimum relevance efficiency ratio promised in advance so as to be able to participate in the competition.
In the case of a legitimate chain, it has been agreed for a very long time, so it exceeds the minimum relevance efficiency ratio, but the attacker has a very low ratio value.
A similar effect is generated by difficulty, but it is different from the relevance efficiency ratio for which the exponential distribution ratio is applied, and the difficulty does not have more than the capabilities described in the document.

The possibility of double spending was discovered.

In the document, there are two ways in which the content designed is followed by one or more authentication blocks or using a threshold for authentication confirmation.
As a more secure method, if more than one authentication block is followed, the authentication is determined to be confirmed.

Even if double spending is attempted by the current leader block, only one authentication block selected by the next leader block is confirmed.
However, it is possible that the current leader block and the next leader block have been compromised for malicious purposes.
Assuming an extreme situation, the authentication blocks may be issued in tree form in any one of the intervals of authentication by several adjacent candidate blocks that are conspired with malicious intent.
However, after the double spending by some neighboring malicious candidate blocks has been issued, the next leader block, which is a legitimate user, selects only one of the many authentication blocks that are double paid.
There has been an attempt to double spending, but the chain continues to be a single stem.
However, this is in the same situation as when using the threshold for authentication confirmation.
Candidate blocks added to the chain at the time of the double spending have a reference to the maliciously issued authentication block.
A newly added candidate block having a reference to an authentication block which has been finally confirmed is currently for security purpose and may be excluded from the functionality.
However, double spending attempts by two or more adjacent blocks can not guarantee the completeness of payment.

In terms of equity, it is more difficult to succeed in this algorithm compared to other algorithms.
In the case of other algorithms, a method of imposing penalties on compensation is used.
But this is a probability.
As the probability that two or more adjacent candidate blocks conspired with malicious intent will reach the leader block's position after the endless consensus, it can be close to zero, but not zero.
The method in the document can be used only if it is proved from the viewpoint of the probability theory that it is practically impossible that two or more adjacent candidate blocks conspired with malicious intent reach the leader block position.
The authentication should be confirmed when the number of adjacent minimum blocks that can be guaranteed to be safe, even if not both, is calculated by probability and the corresponding authentication blocks follow.
This algorithm is designed so that it does not take compensation to supplement for insufficient functionalities except for the initial compensation for participation.
This algorithm aims to prevent all malicious attempts or exceptions just by following its default behavior.

There are two solutions to the case where the current method is not proven safe in terms of probability.

The first solution is the one mentioned above, which has a threshold for authentication confirmation.

This is different from the threshold for authentication confirmation by newly added candidate blocks, which was the second method proposed in the document.
When an authentication block is to be issued by a leader block, the blocks corresponding to 1/10 of all the candidate blocks are considered as blocks having an exclusion authority to exclude the previous candidate blocks in consideration of malicious intent or network failure.
The number of blocks for authentication confirmation can be calculated in the same manner as the number of blocks having the exclusion authority is calculated.
After one authentication block has been issued, if one or more subsequent authentication blocks corresponding to the number of blocks for authentication confirmation are issued, the authentication of the authentication block can be regarded as confirmed.
As by the probability as well as the number of blocks with exclusion authority, it is necessary to make a formula to obtain the number of blocks that can completely guarantee authentication confirmation.
In the case of exclusion authority, it was caused by malicious intent or network failure. However, in the case of authentication confirmation, the network failure does not apply and also two or more adjacent blocks must reach the leader block position.
Therefore, it will be the smallest of the base values used in the algorithm as a value smaller than the number of blocks with exclusion authority.
However, using this method, authentication to the ledger is no longer deterministic.
Even if it is small, it may take a considerable amount of time to confirm the authentication.
In order to know exactly, a formula for the authentication confirmation is created and tests should proceed through it.

The second solution is to use the threshold for authentication confirmation, which was the second method of the document.

In the document, if the newly added candidate block contains a reference to an authentication block that has not been confirmed yet and the relevance of the candidate block reaches a threshold for authentication confirmation, authentication of the authentication block is regarded as confirmed.
However, in this case, the newly added candidate block contains a reference to the authentication block that is last confirmed as the current method, not a reference to an authentication block that has not yet been confirmed.
If the relevance of the candidate block satisfies the threshold for authentication confirmation, it is assumed that the authentication of the authentication block that has not yet been confirmed, just after the authentication block, has been confirmed.
Integrity is maintained in the chain, but like the first solution, it takes a considerable amount of time to confirm the authentication.

Another way is to use a double authentication that crosses from the first block.

An authentication block is issued by a new leader block.
Then, the previous leader block, which has already confirmed, of the current leader block is received it not by the next leader block.
The previous leader block authenticates the newly issued authentication block once again and issues it as a confirmed block.
If the next leader block of the current leader block receives it, the above process is continued.
The authentication confirmation is made deterministically on the assumption that the block having the history of authentication confirmation is a legitimate user.
However, it may not be a legitimate user.
After hiding its malicious intent, it can sign all two authentication blocks issued by the double spending of the next leader block.
This method can maintain the immediacy of the transaction, but it still has problems and needs to be thought of more than enough.

As with other parts of the algorithm based on computational complexity, it is the part that must be proved probabilistically with respect to double spending.
It has been too long since I left school, and there are a lot of things that are not enough to complete by yourself.
By helping those who are still in academia or who can handle probability, I hope that the missing parts can be filled.

I am a freelance developer and can not afford to make all the answers on my own.
I hope that this algorithm will be used for all as it is an algorithm that is created by gathering ideas from many people, not individual.

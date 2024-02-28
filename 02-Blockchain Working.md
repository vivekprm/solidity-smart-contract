# How do blockchains work
We will be going to this blockchain demo website https://andersbrownworth.com/blockchain/

Hash: It's a unique fixed length string, meant to identify a piece of data. They are created by placing said data into a **hash function**. In this case hashing algorithm used is sha256.

Ethereum uses Keccak-256 hashing algorithm. So whatever data we put here: https://andersbrownworth.com/blockchain/hash. The hash below changes. 

Now we are going to split the data into Block, Nounce & data. And we are going to hash all three of these into hash. As shown here. https://andersbrownworth.com/blockchain/block

Now if we hit the Mine button, we see that Nounce actually changes and the hash now starts with 0000. In this case miners had to find the value of Nounce that's when hashed with Block #1 and the data that we passed starts with 0000. So only way to do that is trying to bruteforce the Nounce value.

Ethereum has different problem to solve, bitcoin has different problem to solve for these miners but this concept is the same.

Now we are going to see how block chain works. [Here](https://andersbrownworth.com/blockchain/blockchain) we have multiple block with one extra field Prev, which points to previous block in the chain. Now hash is calculated using Block number, Nounce, Data & Prev. The block with hash of all zeros in Prev is the first block also known as Genisis block in the Block chain.
If we change any intermediate block in the chain it invalidates all the blocks after that block including that block. Now we need to remine all the invalid blocks to validate the chain. As we go farther in the chain mining becomes more and more difficult.

Now let's look at the same problem in case of distributed blockchain [here](https://andersbrownworth.com/blockchain/distributed). Now we have multiple peers with same copy of blockchain data. Now let's say PeerA decides that a Block doesn't have valida data and changes it, so all the block after that become invalid so peer A remines it and fixes it. But now hash value of blocks in peer A's block chain are different. Here distributed nature comes into play. Since data in peerA chain doesn't match with other peers, other peers decide that PeerA doesn't have valid data and it can't take part in mining anymore.

Instead of string data if we want to understand blockchain with some real transaction data refer [this link](https://andersbrownworth.com/blockchain/tokens).

# How do blockchains work
We will be going to this blockchain demo website https://andersbrownworth.com/blockchain/

Hash: It's a unique fixed length string, meant to identify a piece of data. They are created by placing said data into a **hash function**. In this case hashing algorithm used is sha256.

Ethereum uses Keccak-256 hashing algorithm. So whatever data we put here: https://andersbrownworth.com/blockchain/hash. The hash below changes. 

Now we are going to split the data into Block, Nounce & data. And we are going to hash all three of these into hash. As shown here. https://andersbrownworth.com/blockchain/block

Now if we hit the Mine button, we see that Nounce actually changes and the hash now starts with 0000. In this case miners had to find the value of Nounce that's when hashed with Block #1 and the data that we passed starts with 0000. So only way to do that is trying to bruteforce the Nounce value.

Ethereum has different problem to solve, bitcoin has different problem to solve for these miners but this concept is the same.

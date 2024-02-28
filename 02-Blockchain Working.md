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

# Mining
The process of finding the **solution** to the **blockchain problem**. In our example, problem was to find a hash that starts with four zeros. Nodes get paid for mining blocks.

# Block
A list of transactions mined together.

# Nounce
A **number used once** to find the solution to the **blockchain problem**.
It's also used to define the transaction number for an account/address.

# Signing Transactions
In each of the transactions in the block, how do we know the transaction was done by that user?
[Here](https://andersbrownworth.com/blockchain/public-private-keys/keys) we have example fo public private keys.

## Private Key
Only known to the key holder, it's used to "sign" transactions. Ethereum uses [Elliptic Curve Digital Signature ALgorithm](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) and create public key using the private key that we passed. Now we want everybody to have access to this public key. We can sign the transaction using the Private Key and then others can verify using this public key.

E.g. Let's pick a random key: 62136415887603193604652230570448986910612604399908441544998473008845507575009
public key: 0456a20f86ecdf634012ad26f744e7f1a4e4dff7d8db510259411a785d13d478822625bf5b5423f28fbbdced5f455d3053a79106738f353db4ec2112bee6d911bd

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/2f116c61-7874-4a0c-a6de-eb2424075227)

So for example we signed our data "Hello world" with this private key [here](https://andersbrownworth.com/blockchain/public-private-keys/signatures) shown below:

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/65a5c7fe-6f46-4852-81a8-051261bc576b)

No body can derive private key using this signed data.

Now let's verify this signed data using this public key.

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/aafaa9a3-028c-40e0-9cec-b91d49131157)

Same thing can be done with transaction [here](https://andersbrownworth.com/blockchain/public-private-keys/transaction).

How our Metamask address is derived?
If we go do our Metamask account and look at secret phrase (mnemonic) it allows us to created different private keys. So mnemonic phrase combined with account number gives us private key for that account. Which we can see in account details in Metamask. We use this private key to sign the transactions.
Our Ethereum Address is actually a piece of public key. Now to get our address in Ethereum all we have to do is take the public key that we created with our private key, hash it using the same Ethereum hasing algorithm and then take the last 20 bytes and that's how we derive our address. 
Knowing exact methodolgy behind the address doesn't really matter as it varies blockchain to blockchain but concept is almost similar.

Anybody can join these networks provided they have the hardware and software that's needed. You can go to github rightnow and run your own Ethereum Node in few seconds.
Blockchains are resilient to failure, if a node goes down, since there are so many independent nodes running it doesn't matter.

Each blockchains keeps a full list of every transaction and interaction that's happened on that blockchain. So in essence we can think of Blockchain as decentralized database and within Ethereum it has an extra additional feature where it also can do computation in a decentralized manner.

# Consensus / Proof of Work / Proof of stake
Mining that we saw in blockchaind demo, is the proof of work. Proof of work and proof of stake falls under this umbrella of consensus.

Consensus is really important topic when we talk about blockchain. It is defined as the mechanism used to reach an agreement on the state or value on the blockchain, especially in a decentralized system. It can be broken down into two pieces:
- Chain Selection: How do we know which blockchain is the real blockchain. On bitcoin or Etheruem they both use a form of concensus called **Nakamoto Consencus" and this is the combination of proof of work and Longest chain rule. Decentralized network decides that whichever blockchain has the longest chain or the most number of blocks on it, is going to be the chain that they use. This makes lot of sense because every additional block that a chain is behind it's gonna take more and more computation for it to come up.THat's why when we saw in our transaction, we actually saw confirmations. The number of confirmations is the number of additional blocks added on after our transaction went through in a block. So if we see confirmations as two it means that the block that our transaction was in has two block ahead of it in the longest chain.
- Sybil Resistance: It is known as Sybil Resistance mechanism because it defines way to figureout who is the block author. Which node is going to be the node who did the work to find that mine and be the author of that block. So all the other nodes can verify that it's accurate. Sybil Resistance is a blockchains ability to defend against users creating a large number of pseudo-anonymous identities to gain a disproportionately advantageous influence over said system and in layman's term it's basically a way for a blockchain to defend against somebody making a bunch of fake blockchains so that they can get more and more rewards. There are two types of Sybil Resistance:
  - Proof of Work: It's Sybil Resistant because a single node has to go through a very computationally expensive process called mining which we saw earlier to figure out correct nounce or whatever the blockchain system has in place. In POW this works because no matter how many pseudo anonymous accounts you make each one still has to undergo this very computationally expensive activity of finding the answer to the POW problem. Block time depdends on how hard the riddle in the blockchain is.  
  - Proof of stake
 
Proof of work is a piece of the overall Concensus Protocol, which in Bitcoin and Ethereum is Nakamoto Concensus. Which is combination on Proof of Work and Longest Chain rule. Proof of work also tells us where these transaction fees and these block rewards go to. Remember how when we made this transaction we had to talk about gas and transaction fee, so who is getting paid, who is getting this transaction and this transaction fees is going to the miners or the validators. In a proof of work network they are called Miners and in the Proof of Stake network they are called Validators.

In POW system all these nodes are competing against each other to find the answer to the blockchain riddle. Remember in our example, it was to find the hash that had four zeros in the start and depending upon the blockchain implementation that riddle can be little different. But all the nodes are trying as many as possible to try to get this answer first. Why? Becuase the first node to figure out the answer is going to get the transaction fee. When a node gets paid they actually get paid in two different ways, one is going to be with transaction fee and another piece is going to be the block reward. Block reward is given by the Protocol Blockchain itself.

You probably head of bitcoin halving before. The halving is referring to this block reward getting cut in half and it's supposed to be cut in half roughly every four years. This block reward increases the circulating amount of whatever cryptocurrency that is being rewarded. E.g. on Ethereum the block reward is giving out Ethereum.

Some blockchains forexample bitcoin have a set time when they are no longer going to give out block rewards and the miners or the nodes are only going to get paid from transaction fees.

In Proof of stake also there is gas fee but it's paid out to Validators instead of miners.

Two types of attack that can happen in blockchain world:
- Sybil Attack: When user creates whole bunch of pseudo anonymous accounts to try to influence a network. Now obviously on Bitcoin and Ethereum this is really really difficult because user needs to do all this work in POW or have a ton of collateral in Proof Of Stake
- 51% Attack: As we saw as part of consensus protocol these blockchains are going to agree that the longest chain is the one that they are going to go with, so long it matches up with 51% of the rest of the network. This means that if you have the longest chain and you have more than 51% of the rest of the network you can do what's called a fork in the network and bring the network onto your now longest chain.

Now Sybil attack obviously are when a single node or single entity tries to affect the decentrality of the network by pretending to be multiple different people, although they're just the same person or entity. It's really difficult to do it in POW and in POS. 

So you can see now the blockchains are very democratic. Whichever blockchain has the most buy-in and is the longest is the blockchain that the whole system is going to corroborate. When nodes produce new block and add to the longest chain, the other ndoes will follow this longest chain that the rest of the network is agreeing with. Add those blocks to their chain and followup. So very small reorganisations are actually pretty common when a blockchain picks a block from different longest chain, puts it on and then has to swap it out for another block and continue with a different blockchain.

However, if a group of nodes had enough nodes or enough power they could essentially be 51% of the network and influence the network in whatever direction that they want. This 51% attack happend on blockchains like Ethereum classic which is not Ethereum. This is why the bigger the blockchain is the more decentralized and the more secure it becomes.

POW costs a lot of electricity this obviously leads to environmental impact. Since POW in Nakamoto Consensus a lot of other protocols have taken this idea and gone in different direction with a different Sybil Resistance protocol. A lot of them with the intention to be a lot more environment friendly. And the most popular one right now is **Proof of Stake**. There are some chains that are already using this Proof of Stake protocol and that are live and thriving. Some of them are like Avalanche, Solana, Polygon, Polkadot.

# Proof Of Stake
This is a different Sybil Resistance mechanism. Instead of solving this difficult problem, proof of stake nodes put up some collateral that they are going to behave honestly, aka they stake. In the example of Ethereum 2, nodes put up some Ethereum as a stake that they are going to behave honestly in the network. If they misbehave to the network they are going to be slashed or removed some of their stake. Obviously this is very good sybil resistance mechanism because if you try to create a whole bunch of anonymous accounts then each one of those accounts you have to put up some stake and if you misbehave you are going to run the risk of losing all the money that you put up as collateral. In this system miners are actually called Validators. In Proof of Stake Nodes are randomly chosen to propose the new block and the rest of the Validators will validate if that node has proposed the block honestly. It also have some Pros and Cons:

Pros:
- It's great Sybil resistance mechanism and a great way to figure out who the author of the block should be.
- Way less computationally expensive to figure out the new block. Because instead of every single node on the network trying to do this, only one node needs to do this and then the rest of the nodes just need to validate it.

Cons:
- It's usually considered a slightly less decentralized network due to upfront staking costs. It costs to participate

# Layer 1
Layer 1 refers to any base layer blockchain implementation. Bitcoin, Ethereum, Avalanche are layer 1. These are base layer blockchain solutions.

# Layer 2
Layer 2 is any application that is added on top of layer 1, added on top of blockchain. E.g. Chainlink, Arbitrum, Optimism. Arbitrum and Optimism are layer 2 and also looks to solve scalability issue. Arbitrum and Optimism are what's known as **Rollups**. And they roll up their transactions into a Layer 1. They are different from side chains. Because side chains derive their security from their own protocols. Rollups derive their security from the base layers.

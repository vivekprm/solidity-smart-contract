First thing we need is an Ethereum Wallet. Let's go to Metamask and create Ethereum wallet.

We can use https://etherscan.io and put any wallet address and we can see what's going on with that wallet. So this is like a public address of this account. However there is also a private key to work with this account and we can go ahead and view it by clicking the three dots, go to account details and export private key.

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/012e5ddf-5f28-44ab-879e-cd1bbdb3d464)

Pneumonic phrase gives access to all the accounts created. Private key gives access to a particular account.

In the top left we can see different networks. However, when we buy Ethereum or work with Ethereum we are working with Ethereum Mainnet or whether we work with defi, web3, smartcontract we are working on Ethereum Mainnet. However, since we are Engineers and oftentimes we are going to want to test our applications or do some type of integration tests or just make sure our code actually work, so there is also called TestNets.

These are networks that resemble Ethereum and work exactly the same way as Ethereum, however they are not with real money and it's just for testing your application.

# Making our first transaction on SepoliaETH Testnet
https://github.com/Cyfrin/foundry-full-course-f23?tab=readme-ov-file#testnet-faucets

Go to https://www.alchemy.com/faucets/ethereum-sepolia
Faucet is a testnet application that gives us free test tokens.

Now go to https://sepolia.etherscan.io and add our test account wallet address and we can see the transaction.

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/d36bf2de-4e42-4c78-a974-d3caa17b22dd)

We can even look at this transaction detail:
![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/aaf29517-061a-4382-9275-1d754c7f5688)

Etherscan is known as Block Explorer. It allows us to view the transactions that happen on the Blockchain.

The Transaction Hash is the unique identifier that identifies this transaction.

**GAS** refer to a fees paid to Node Operators. It's a unit of Computational Measure. The more computation a transaction uses, the more "gas" you have to pay for. 
Every transaction that happens on-chain pays a "gas fee" to Node Operators.

The amount of GAS used and and how much you pay depends on how "computationally expensive" your transaction is.
Sending ETH to one address would be cheaper than sending ETH to 1000 adresses. We can choose how much fee we want to send to these miners.

We can use https://www.alchemy.com/gwei-calculator to convert GWEI to ETHER. So in summary:
- GAS: Measure of computation use
- GAS Price: How much it costs per unit of GAS.
- GAS Limit: Max amount of GAS  in a transaction.
- Transaction Fee: Gas Used x Gas Price i.e. 20,000 gas @1 GWEI per gas = 21,000 GWEI

### Why do we ever want to increase per unit GAS price?
https://ethgasstation.info

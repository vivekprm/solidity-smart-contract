# Lesson 0 - Welcome to Blockchain
Bitcoin was one of the first protocols to use this revolutionary technology called Blockchain.

In the Bitcoin paper it's described, How Bitcoin can be used to make peer-to-peer transactions in a decentralized network. This network is powered by cryptography and allows people to engage in censorship resistant finance in a decentralzied manner.

Due to some of the features of Bitcoin a lot of people took it to be as a superior store of value over another asset like let's say Gold and that's why it's commonly referred to as Digital Gold similar to Gold there is a scarce and set amount of it on the planet and people use it to buy and sell similar to other assets. Read more in the whiepaper [here](https://bitcoin.org/bitcoin.pdf).

Some people took this Blockchain technology and thought that they can do even more. A few years later a man named Vitalik Buterin released a [whitepaper](https://blockchainlab.com/pdf/Ethereum_white_paper-a_next_generation_smart_contract_and_decentralized_application_platform-vitalik-buterin.pdf) describing a new protocol called Ethereum, which used the same Blockchain infrastructure but with an additional feature and in 2015 tehy released project called Ethereum. Him and number of other co-founders took this Blockchain technology and applied it in ways that people can make entirely decentralized applications, decentralized organizations abd build smart contracts and enagage in agreements without a third-party intermediary or centralized governing force. 

Their idea was to take the same pieces that made Bitcoin great and add smart contracts to it and infact technically it wasn't even a new idea, back in 1994 a man named Nick Szabo proposed a technology called Smart Contracts.

Smart Contract is a self-executing set of instructions that is executed without a third party intermediary. They come to life on a Blockchain and these Smart Contracts are really going to be the core thing that we will be working with.

Smart contracts are similar to regular contracts that people make between each other but instead of writing these contract down on pen and paper or typing that on the computer, it's entirely written in code. The terms of the agreement are written in code and automatically executed by the decentralized blockchain network instead of being written in pen and paper and executed by two or three parties or however many partied involved.

This is the main differentiator between Bitcoin & Ethereum protocol. Technically Bitcoin does also have smart contracts, however they are not Turing Complete meaning that they don't have full range of capabilities as a Turing Complete application like Ethereum. This was actually intentional move by Bitcoin developers, they view Bitcoin Network as an asset whereas Ethereum developers viewed that as an asset and also a utility for people to build these Smart Contracts.

Smart contracts come with a fatal flaw known as the Oracle problem. These Blockchains are deterministic systems and we will learn why they're deterministic very soon, and this determinism means that they're a walled guarded. Meaning that everything that happens in these smart contracts and on this blockchain happens in this little box. Now of course if you want these smart contracts to actually be these digital superior agreements then they need someway to interact with the real world and get real data and external outside the blockchain computation, this is where Oracles come into play.

Oracles are devices that bring data into a Blockchain or execute sometype of external computation. So great so oracles are the solution, now blockchains can talk to the real world right? 

<img width="587" alt="Screenshot 2023-12-25 at 4 08 51 PM" src="https://github.com/vivekprm/solidity-smart-contract/assets/2403660/f0481f57-f653-4854-8c35-bb3405dd3c7d">

Well not quite! Our Blockchains and smart contracts are these decentralized applications and in order for them to stay decentralized that means they would also need to get their data and external computation in decentralized manner as well. Your onchain logic will be decentralized on the Blockchain but you will also need your offchain data and external computation decentralized as well. 

<img width="509" alt="Screenshot 2023-12-25 at 6 18 46 PM" src="https://github.com/vivekprm/solidity-smart-contract/assets/2403660/020a9bd0-9cd9-4dfb-bff7-74df7cd22911">

Combining these on-chain logic settlement layers and these off-chain data and external computation builds what's called **Hybrid Smart Contracts**. Large majority of De-FI applications are these Hybrid Smart Contracts. This is where the protocol **Chainlink** comes into play.

**ChainLink** is decentralized, modular Oracle Network that allows you to bring data into your smart contracts and do external computation and it's these Hybrid Smart Contracts that can have these on-chain settlements and interact with realworld in some meaningful way. Chainlink is an incredibly powerful Oracle Network because it allows us to get data, get randomness, do sometype of upkeep or really customize our smart contracts in anyway we want and elevate them to do anything that we want them to do.

**Decentralized application** is usually a combination of several smart contracts. Since it's inception the Ethereum protocol has given rise to many new paradigms and industries, including DeFi, NFTs, DOWs or Decentralized Autonomous Organizations, layer twos and so much more and a couple of other protocols have taken this Ethereum Vision and gone in a different direction with it. Like Polygon, PolkaDot or Avalanche.

There are couple of smart contract platforms that don't use solidity but fundamentals are almost the same. Ethereum is the most valued smart contract platform out there.

Chainlink is the most popular and powerful Oracle Network and it's Blockchain and Smart Contract agnostic meaning it will work on Ethereum, Avalanche, Polygon, Polkadot or really any blockchain or smart contract platform.

Over the year new term has come to life called L2 or Layer 2, this solves the issue that most blockchains see where they don't scale very well. Basic concept is that blockchain can really only get so big. If it's Ethereum, you can get blockchains hook into them to essentially make them bigger. At the moment there are two types of L2:
- Optimistic Rollups: For example [Arbitrum](https://arbitrum.io/?ref=blog.thirdweb.com), [Optimism](https://www.optimism.io/?ref=blog.thirdweb.com)
- Zero Knowledge Rollups: For example [Zksync](https://docs.zksync.io/zkevm/), [Polygon](https://polygon.technology/solutions/polygon-zkevm)

Web3 is the idea that Blockchains and samrt contracts are the next iteration of the Web. Inc ontrast to web2 where centralized servers run the logic, in web3 decentralized servers run the logic.

Smart Contract is an agreement, contract or a set of instructions that is deployed on a decentralized blockchain. Once the contract is deployed, it can't be altered, it automatically executes and everyone can see the terms of the agreement. Code is executed by decentralized collective i.e. group of people running certain software. That means no one person entity can alter any of these agreements or change the terms of the arrangement.

In traditional contracts whoever owns the contract can anytime flip the switch and say that we are not going to do that anymore. In blockchain you can't do that.

Uniswap is decentralized exchange.

# Advantages of Blockchain & Smart Contracts Over Traditional Environments
- **Decentralized**: There is no centralized source that controls the Blockchain. Individuals that makeup blockchain are known as Node Operators and they are the independent individuals running the Software that connects the whole Blockchain together. It's all these different independent individuals that make a Blockchain, a Blockchain like networks decentralized. Great example of why this is so fundamentally ground breaking is if we go back to what happened recently with Robinhhod & Gamestop. Gamestop shared were no longer allowed to be bought because a centralized entity didn't want them to be bought.
- **Transparency & Flexibility**: Everything that is done on a blockchain and all the rules that are made can be seen by everyone. There is no backdoor deals, there is no shady happenings. Everything that happens on chain you can see. This means that there's no special information that you have. Everyone has to play by the same rules. and everyone can see exactly what those rules are. Now that doesn't mean that everything that you do is tracked. Blockchain is pseudo-anonymous, so you can create different accounts and you can interact with it in many different ways.
- **Speed & Efficiency**: Because Blockchains are verified by a decentralized collective, the settlement or withdrawl period in this case is substantially faster and depending on the blockchain that you are using it can be from 10 minutes all the way down to just a couple of seconds. In the stock trading or hedge fund world it can actually take up to a week for your buy or sell of a stock to go through.
- **Security & Immutability**: Blockchains are immutable which means they can't be changed and because of this it means that they can't be tempered with or corrupted in anyway shape or form. This allows us to have massive security on our data, on our transactions and anything of the like. Also it's much more secure in asset sense as well. Instead of having gold in a vault or contract written on a piece of paper or on your computer, you have a asset that is locked on the blockchain forever and all you need to do to access it is have a private key or mnemonic, which is essentially a password. So you don't have to lug your gold around or lug your contracts around with you. It's always on the Blockchain.
- **Removal of conterparty Risk**: Blockchain smart contracts in particular remove a massive conflict of interest. In the traditional world when we engage with users or individuals, they don't always have our best interests at heart, a lot of them usually self-motivated in some sense and there is nothing wrong with that. That's how a lot of people are, however when we make an agreement with them this agreement can have a massive conflict of interest with the user who's supposed to execute that agreement.
  - Let's take insurance for example if I pay an insurance provider 100 dollars a month, I am paying them a hundred dollars and in the event I get hit by a bus we've made an agreement or a contract that they are going to pay my medical bills or bail me out. However, they have this massive conflict of interest. Insurance companies aren't in the business of giving out money. They're in the business of making money, so eventhough they have signed this agreement, when this event occurs they still don't want to pay this money out to me and if they can find a loophole in the contract they will because that is what they are motivated to do. So this conflict of interest is native in all the agreements that we do today.
- **Trust Minimized Agreements**: Smart contracts allow us to engage in trustless and trust minimized agreements. We currently live in a world of brand-based agreements. If I engage in some agreement and if I don't like the service that I am provided my alternative to this is to waltz down to the street to another brand to another service who's going to make the exact same set of promises to me and then I have to trust them that they are going to execute faithfully.
  - Smart contracts allow us to move from these brnad based agreements to math based agreements. These math based agreements we don't even have to trust that they are going to do the right thing hence the name trustless. One plus one is always going to be equal to two in maths world.
  - These really all add up to two major pieces:
    - Freedom
    - Trustless

All these pieces allow us to live in a world that is more accountable, more trusting, more friendly and overall better world. 

This brings out new world of economic opportunity as well and as our lives become more and more digital, we're constantly being bombarded with centralized services that want us to use their interface so they can profit on how we interact and force us or push us to making the decisions that they're motivated for us to make. Smart contracts, decentralized applications and blockchain allows us to be free of these repressors and live in an environment that's truly free and trustless.

What industries have come around due to these smart contracts?
**DeFi**: Decentralized Finanace, gives user ability to engage with finance and markets without having to go through a centralized intermeidary.
**DAOs**: Decentralized Autonomous Organisations, are groups that are governed completely decentralized by a set of instructions or smart contracts on chain.
**NFTs**: Non Fungible Tokens, can be dscribed as digital art or unique asset. They can do so much more but we keep it high level for now.

# Summary
- Blockchains are decentralized: Meaning that they are not controlled by a single centralized entity. It is run by a network of independent users.
- Transparency: Blockchains are transparent. Everything that happens on the blockchain, everybody else can see and everybody else can work with and see that everyone is playing by the same rules.
- Speed: Blockchains are quick and efficient especially when it comes to monetary policy settlement on blockchains are fast and easy.
- Immutable & Secure: Blockchains can't be changed or tampered with or corrupted and are incredibly secure.
- Remove conterparty Risk: Smart contracts remove the massive conflict of interest traditional agreements have. Smart contracts allow us to move away from political brand based agreements to secure math based agreements.
- Allow for trust minimized agreements: Smart contracts allow us to engage in trustless and trust minimized agreements. Smart contracts are a set of instructions which when placed on a blockchain are self executing pieces of code not run by any centralized intermediary.
- Hybrid Smart Contracts: In addition smart contracts are typically paired with some type of oracle to get some information about the real world. When smart contracts are paried with an oracle they are called Hybrid Smart contracts.
  - Chainlink is a secure, decentralized, modular oracle network used to bring data into your smart contracts and also make some type of external computation.
 
# Decentralized Autonomous Organization (DAO) 
These are organizations that live online and live in these smart contracts. They are similar to a regular organization in the traditional world, however they have people who may be hold governance tokens to make voting decisions or they do all the governance on chain on this decentralized settlement layer giving us the freedom to engage with each other as we please.

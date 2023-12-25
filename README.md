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

Chainlink is the most popular and powerful Oracle Network and it's Blockchain and Smart Contract agnostic meaning it will work on Ethereum, Avalanche, Polygon, Polkadot or really any blockchain or smart contract platform.

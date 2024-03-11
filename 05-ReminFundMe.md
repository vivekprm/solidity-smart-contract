We will make Web3 based decentralized KickStarter. Allow users to send Ethereum, Polygon, Avalanche etc. any native blockchain based cryptocurrency, and allow owner to withdraw that fund.

https://github.com/Cyfrin/remix-fund-me-f23

Here is the basic skeleton of FundMe
```sol
// Get Funds From Users
// Withdraw Funds
// Set a minimum funding value in USD

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract FundMe {
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public  {
        
    }
    // function withdraw() public {}
}
```

But how do we sned ETH to this contract?
Whenever we send a transaction to a Blockchain, there's always actually a value field that gets populated and most of the time it gets sent with zero.
First thing we need to do to allow a function in solidity to accept this native Blockchain currency in the first place is to make this function payable as below:

```sol
// Get Funds From Users
// Withdraw Funds
// Set a minimum funding value in USD

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract FundMe {
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public payable  {
        
    }
    // function withdraw() public {}
}
```

As wallets hold funds, contracts can also hold funds. So whenever you deploy a contract similar to a wallet address it actually acts almost the same as wallet address. You can send money to it and you can interact with it etc.

You can access this value using one of the globals in solidity called message.value. [Here](https://docs.soliditylang.org/en/v0.8.24/units-and-global-variables.html) is the list of globals in Solidity. We can use require to set min amount of crypto that needs to be send.

```sol
contract FundMe {
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public payable  {
        require(msg.value > 1e18, "Didn't send enough ETH."); // 1e18 = 1 ETH = 1000000000000000000 WEI
    }
    // function withdraw() public {}
}
```

If required amount is less we do reverts. 

# Reverts
Reverts are little bit tricky and confusing. 
Revert undoes any action that have been done previously and sends the remaining gas associated with that transaction back. So what does that actually mean?
Let's say for example in our FundMe contract every time we go through the transaction successfully, we add 2 to our value:

```sol
contract FundMe {
    uint256 public myValue = 1; 
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public payable  {
        myValue = myValue + 2;
        require(msg.value > 1e18, "Didn't send enough ETH."); // 1e18 = 1 ETH = 1000000000000000000 WEI
    }
    // function withdraw() public {}
}
```

However, if we get to revert statement, eventhough we added to to our value viz. myValue previously, since our contract reverts, this would actually revert this action or reset myValue to its initial state.

Eventhough transaction didn't go through we do spend gas. If you send a failed transaction you will spend gas. Users can actually specify how much gas they send with every function. Let's say there was ton of computation after the require line, we need to send ton of gas to operate and run our FundMe function. However, once it gets to this require line and it reverts however much gas that we sent to execute the rest of the computation would just get refunded to whoever initiated the transaction. 

# Transaction Fields
Every single transaction that we send will have these fields:
- **Nounce**: tx count for the account.
- **Gas Price**: price per unit of gas (in wei)
- **Gas Limit**: max gas that this tx can use.
- **To**: address that the tx is sent to.
- **Value**: amount of wei to send.
- **Data**: what to send to the To address.
- **v,r,s**: components of tx signature.

## Transactions - Value Transfer
- **Nounce**: tx count for the account.
- **Gas Price**: price per unit of gas (in wei)
- **Gas Limit**: **21000**
- **To**: **address that the tx is sent to.**
- **Value**: amount of wei to send.
- **Data**: **empty**
- **v,r,s**: components of tx signature.

## Transactions - Function Call
- **Nounce**: tx count for the account.
- **Gas Price**: price per unit of gas (in wei)
- **Gas Limit**: max gas that this tx can use.
- **To**: **address that the tx is sent to.**
- **Value**: amount of wei to send.
- **Data**: **what to send to the To address.**
- **v,r,s**: components of tx signature.

# Getting Real-world Price Data (Chainlink)
Instead of require our value to more than one Ether, we require it to be greater than or equal to some value. Let's say we want min spend of 5$.

```sol
contract FundMe {
    uint256 public minimumUsd = 5; 
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public payable  {
        require(msg.value >= minimumUsd, "Didn't send enough ETH."); // 1e18 = 1 ETH = 1000000000000000000 WEI
    }
    // function withdraw() public {}
}
```

However, here msg.value is in ETH and minimumUsd is in $. So how do we convert amount of Ethereum to US dollar? This is where Oracle or **ChainLink** comes into play. Dollar price of an asset like Ethereum is something that we've assigned to Ethereum outside of the blockchain in the real world. So in order to get this abstract concept of the price of the Native cryptocurrency of the blockchain working with so we need to use a decentralized Oracle network or something called an Oracle to get this price.

## Understanding Oracle or Chainlink
Blockchains are deterministic systems which means that they themselves can't actually interact with real world data and events. They don't know what the value of an Ethereum is, they don't know what random numbers are, they don't know if it's sunny outside, they don't know the temperature, they don't know any of these informations. These blockchains also can't do any external computation. May be you have some amazing artifical intelligence model that you want to integrate with a smart contract. Smart contracts by themselves can't do anything wit that as we have mentioned this is because blockchains are deterministic by design.

![Screenshot from 2024-03-02 22-26-52](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/4aa04cca-1a24-45f1-b741-734d0cf1ac77)

This is so that all the nodes can reach consensus. If you start adding variable data or random data or values that return from an API call different nodes could get different results and they would never be able to reach a consensus. This is known as the smart contract connectivity problem or the Oracle problem. And this is bad news because we want our smart contracts to be able to replace traditional agreements and traditional agreements need data and they need to interact with real world.

This is where **Chainlink** and **Blockchain Oracles** come into place. A **Blockchain Oracle** is going to be any device that interacts with the offchain world to provide external data or computation to smart contracts. However the whole story doesn't even end there. If we use a Centralized Oracle, we are reintroducing a point of failure. We've done all this work to make our logic layer decentralized but if we get our through a centralized node or through a centralized API or we decide we want to make the API calls ourselves, we are reintroducing these trust assumptions that we've worked so hard to get rid of. We're essentially ruining the entire purpose of building a smart contract.

So we don't want to get our data or do external computation through centralized nodes, those are bad news. Chainlink is the solution here.

![Screenshot from 2024-03-02 22-42-45](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/1a257763-3cbf-4961-8026-58e2ef3f6373)

Chainlink is decentralized Oracle Network for bringing data and external computation into our smart contracts. As we've mentioned before this gives rise to these **Hybrid Smart Contracts**. Which combine on-chain and off-chain to make incredibly feature-rich powerful applications. **Chainlink** is a modular decentralized **Oracle Network** that can be customized to deliver any data or do any external computation that you like.

So lot of people say oh I can just make a HTTPS call to some API from the contract and will be good to go. But Blockchain nodes can't make these HTTPS calls because they wouldn't be able to reach consensus, if they called the node at different times or they did something else, all the consensus would be broken. So instead we need a decentralized network of **Chainlink Oracles** to do this and then in the transaction this network of nodes will return the data to our smart contracts for us.

## Chainlink Features
Chainlink networks can be completely customized to bring any data or any external computation that you want. However, doing the customization can be a little bit extra work. There are a ton of Chainlink features that come out of the box completely decentralized ready to Plug and Play into your smart contract applications. What are those features?
- **Chainlink Data Feeds**: This is the feature that we will be using for our application. Chainlink data feeds currently at the time of recording are powering over 50 billion dollars in the DeFI world. The way they work is that a network of chainlink nodes gets data from different exchanges and data providers and brings that datathrough a network of decentralized chain link nodes. The ChainLink nodes use a median to figure out what's the actual price of the asset is and then deliver that in a Single transaction to what's called a reference contract, a price feed contract or a data contract on chain that other smart contracts can use and then those smart contracts use that pricing information to power their DeFi application.

![Screenshot from 2024-03-02 23-06-55](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/28876c85-2d84-4e2b-b450-c72a1c9c7e89)

We can see an example at [https://data.chain.link ](https://data.chain.link/feeds) and you can change network, you can change price feed, you can change whole bunch of different infromation to see some of the most popular price feeds.

Let's look at ETH USD for example [here](https://data.chain.link/feeds/ethereum/mainnet/eth-usd). We can see this whole network of independent chainlink node operators that are each getting different answers for the price of that USD. They are getting aggregated by the network and then delivered on chain. We can see how often they are updated. We can see **contract address** directly on chain. We can look the contract on etherscan. We can see the history and all the responses of the Oracles. And at the bottom we can see different users and sponsors keeping this network up. 

Similar to transaction gas whenever a node operator delivers data to a Smart Contract the Chainlink node operators are paid a little bit of Oracle gas in the Chainlink token. Rightnow these users of the protocol are sponsoring keeping these feeds up and are paying the Oracle gas associated with delivering this data on chain. Here is an illustration of what the current model of these datafeeds look like.

![Screenshot from 2024-03-02 23-25-21](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/2024861a-79a4-4830-8188-4cda5d17412a)

A network of these Chainlink nodes each reaches out and gets the information about an asset and then signs the data with their own private key. In a single transaction then one node will deliver all the data with all the different signatures to a reference contract. If that node doesn't deliver the data another node will send it instead. Reputation is incredibly important when you're a Chainlink node operator. If you miss data updates, if you forget to send transactions you'll probably be quickly kicked off these networks and have no chance of making anymore money in the future.

These datafeeds are used by some of the largest protocols in the space such as below serveral billion dollar each:

![Screenshot from 2024-03-02 23-34-13](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/e8ebe617-b6dd-4142-92d2-ee27cea6b757)

We can take a look at an example over at https://docs.chain.link/data-feeds/using-data-feeds#solidity. We can directly open the code in Remix.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import {AggregatorV3Interface} from "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

/**
 * THIS IS AN EXAMPLE CONTRACT THAT USES HARDCODED
 * VALUES FOR CLARITY.
 * THIS IS AN EXAMPLE CONTRACT THAT USES UN-AUDITED CODE.
 * DO NOT USE THIS CODE IN PRODUCTION.
 */

/**
 * If you are reading data feeds on L2 networks, you must
 * check the latest answer from the L2 Sequencer Uptime
 * Feed to ensure that the data is accurate in the event
 * of an L2 sequencer outage. See the
 * https://docs.chain.link/data-feeds/l2-sequencer-feeds
 * page for details.
 */

contract DataConsumerV3 {
    AggregatorV3Interface internal dataFeed;

    /**
     * Network: Sepolia
     * Aggregator: ETH/USD
     * Address: 0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419
     */
    constructor() {
        dataFeed = AggregatorV3Interface(
            0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419
        );
    }

    /**
     * Returns the latest answer.
     */
    function getChainlinkDataFeedLatestAnswer() public view returns (int) {
        // prettier-ignore
        (
            /* uint80 roundID */,
            int answer,
            /*uint startedAt*/,
            /*uint timeStamp*/,
            /*uint80 answeredInRound*/
        ) = dataFeed.latestRoundData();
        return answer;
    }
}
```

E.g. here Network is Sepolia. Get Sepolia ETH from faucet. Compile it and deploy it in **Injected Provider - MetaMask**, as there are chainlink VMs watching the testnet.
If you are looking for different addresses of different price feeds you can check the [contract addresses section](https://docs.chain.link/data-feeds/price-feeds/addresses?network=ethereum&page=1) of the documentation. 

# Chainlink VRF
The next decentralized application right out of the box is going to be Chainlink VRF or **Chainlink Verifiable Randomness Function**.

## Malicious RNG Operators are a risk
Once we talk about our littery example littlebit later, we'll talk about how randomness can be manipulated in Blockchain.

![Screenshot from 2024-03-04 12-53-52](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/c65652b0-8ae4-4e18-a166-d7fa4f083025)

Blockchains are deterministic systems which by definition means that they can't have Randomness. If you can determine what a random number is it's not really random anymore. So **we need a way to get a provably random number by looking outside of the Blockchain**.

## Chainlink VRF Provides Verifiable Randomness
![Screenshot from 2024-03-04 13-00-12](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/5a5006c3-268c-40d1-a45e-512ca5c3ad02)

Oracles are perfectly positioned to to exactly that. Chainlink VRF is a way to get provably random number into our smart contract to guarantee fairness and guarantee randomness of applications.
Many protocols like pull together, Axie Infinity, Ether Cards, Aavegotchis, and many more use Chainlink VRF for lotteries, randomizing NFFs, for gaming and many more.

For more details go [here](https://docs.chain.link/vrf/v2/subscription/examples/get-a-random-number).

## Chainlink Keepers
Decentralized out of the box feature of Chainlink is Chainlink Keepers, which is decentralized, event driven execution. As we've see in order to kickoff some type of transaction, somebody needs to spend the gas and somebody needs to sitdown and hit the go button or hit the transact button or hit the send button. But this is obviously a centralized vector, if you have a decentralized application that needs to run at specific times or after spcific events are triggered, **Chainlink Keepers** are solution to this.

![Screenshot from 2024-03-04 13-54-21](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/55983063-5e60-4544-bda8-1e2416bc206a)

**Chainlink Keepers** are chainlink nodes that listen to a registration contracts for different events that you specify to fire maybe you say every 10 minutes you want to do something or once a week do something or if the price of some asset hits some number or may be a liquidity pool is at a certain level whatever event that you want to code you absolutely can. The Chainlink nodes constantly listen for these triggers to happen and check the different contracts for these triggers. Once a trigger returns true the Chainlink Node will then perform whatever action that you tell the chainlink nodes to do.

Check [this doc](https://docs.chain.link/chainlink-automation/guides/compatible-contracts) for more details.

## End-to-end Reliability Is The Promise of Smart Contracts
Last out of the box feature of chainlink is the most customizable but also the hardest to get correct. End-to-end reliablity is the ultimate promise of our smart contracts and we want and need them to be able to do anything. 

![Screenshot from 2024-03-04 22-22-17](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/26a23bc3-12e9-4ed6-8a0d-ddc4fc13438e)

We want to be able to take any input and get any output. [Chainlink functions](https://docs.chain.link/chainlink-functions) is the last decentralized out of the box tool and it allows you to make any API call in a decentralized context through a network of chainlink nodes.

So, back to our FundMe application, we want to get the Etheruem price..Will add a function to get Ethereum price from Chainlink Price datafeed. We will go to the documentation to get the data feed.
So we need to reach out the datafeed contract to get the data. So we need two things:
- Address
- ABI

To get the address go to https://docs.chain.link/data-feeds/price-feeds/addresses?network=ethereum&page=1

To the ABI, before with SimpleStorage we imported the entire contract from the top and we compiled and we got the ABI like that. We could do that here but that's kind of a lot of code and we don't actually care about what the whole contract looks like. We only really want to know what the functions are, so we can call that latest round data function. In remix under compilation details, in ABI we get the list of functions that we can call.

How can be get the ABI?
There is a concept in Solidity called interface. If we go to [chainlink github](https://github.com/smartcontractkit/chainlink),we can see lots of different contracts in the Chainlink repository. We can go to https://github.com/smartcontractkit/chainlink/blob/develop/contracts/src/v0.8/shared/interfaces/AggregatorV3Interface.sol, we can see whole bunch of function decorators.

We can copy the whole code and paste it in Remix. And use this interface to make API call. For more deatils we can take help from AI tools such as ChatGPT:

![Screenshot from 2024-03-04 23-04-36](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/c73f8176-7a6c-40ec-be48-eca91f6e7f22)

```sol
pragma solidity ^0.8.18;

interface AggregatorV3Interface {
  function decimals() external view returns (uint8);

  function description() external view returns (string memory);

  function version() external view returns (uint256);

  function getRoundData(
    uint80 _roundId
  ) external view returns (uint80 roundId, int256 answer, uint256 startedAt, uint256 updatedAt, uint80 answeredInRound);

  function latestRoundData()
    external
    view
    returns (uint80 roundId, int256 answer, uint256 startedAt, uint256 updatedAt, uint80 answeredInRound);
}

contract FundMe {
    uint256 public minimumUsd = 5; 
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public payable  {
        require(msg.value >= minimumUsd, "Didn't send enough ETH."); // 1e18 = 1 ETH = 1000000000000000000 WEI
    }
    // function withdraw() public {}
    function getPrice() public view {
        // Address 0x694AA1769357215DE4FAC081bf1f309aDC325306
        // ABI
        AggregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306).version();
    }

    function getConversionRate() public {

    }

    function getVersion() public view returns (uint256) {
        return AggregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306).version();
    }
}
```

Instead of copy pasting the whole interface code, we can directly import it from github, as given in [this](https://docs.chain.link/data-feeds/using-data-feeds#solidity) example.

```sol
import {AggregatorV3Interface} from "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";
```

It referes contracts from [here](https://www.npmjs.com/package/@chainlink/contracts). Remix download all this code from npm package which is created from github code.

Price has that our contract function retruns has 8 decimal places and msg.value has 18 decimal places. So to match them up we need to return price * 1e10. Now price is int256 and msg.value is uint256. So now here is the code:

```sol
pragma solidity ^0.8.18;

import {AggregatorV3Interface} from "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract FundMe {
    uint256 public minimumUsd = 5; 
    // Allow users to send $
    // Have a minimum $ sent
    // 1. How do we send ETH to this contract?
    function fund() public payable  {
        require(msg.value >= minimumUsd, "Didn't send enough ETH."); // 1e18 = 1 ETH = 1000000000000000000 WEI
    }
    // function withdraw() public {}
    function getPrice() public view returns (uint256) {
        // Address 0x694AA1769357215DE4FAC081bf1f309aDC325306
        // ABI
        AggregatorV3Interface priceFeed = AggregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306);
        (, int256 price, , , ) = priceFeed.latestRoundData();

        // Price of ETH in terms of USD
        // 2000.00000000
        return uint256(price * 1e10);
    }

    function getConversionRate() public {

    }

    function getVersion() public view returns (uint256) {
        return AggregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306).version();
    }
}
```

When working with Solidity decimals doesn't work. So we always make sure we are using the correct number of units whenever we interact with our contracts. msg.value and msg.sender are known as globally available units in solidity. Now we need to add conversionRate function.

```sol
uint256 public minimumUsd = 5e18;

function fund() public payable  {
    require(getConversionRate(msg.value) >= minimumUsd, "Didn't send enough ETH."); // 1e18 = 1 ETH = 1000000000000000000 WEI
}

function getConversionRate(uint256 ethAmount) public view returns (uint256) {
    uint256 ethPrice = getPrice();
    uint256 ethAmountInUsd = (ethPrice * ethAmount) / 1e18;
    return ethAmountInUsd;
}
```

The next thing that we can do with this contract is, we want to keep track of users who send us money in this contract. So we can keep an array of addresses called funders and keep updating that depending on actually sends us money.

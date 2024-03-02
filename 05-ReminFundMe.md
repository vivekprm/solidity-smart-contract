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

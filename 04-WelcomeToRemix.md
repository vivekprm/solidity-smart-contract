[Here](https://github.com/cyfrin/remix-simple-storage-f23) is the code for this lesson.

# Getting Started
- Go to [Remix](https://remix.ethereum.org/)
- Paste the code from ```SimpleStorage.sol``` into a new file in Remix
- Hit Compile
- Hit Deploy

Solidity is the programming language that we will be using.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18; // Works with solidity version >= 0.8.18, we can also specify range of versions.

contract SimpleStorage {
    
}
```

Go to https://docs.soliditylang.org/en/v0.8.24/ for more details.

Very basic solidity contract:
```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18; // Works with solidity version >= 0.8.18, we can also specify range of versions.

contract SimpleStorage {
    // Basic types: boolean, uint, int, address, bytes
    // favoriteNumber initializes to 0 if no value specified.
    uint256 favoriteNumber; //0

    function store(uint256 _favoriteNumber) public {
        favoriteNumber = _favoriteNumber;
    }
}
```

We will deploy it into a fake environment. Go to the Deploy option and keep the default selected. RemixVM is a fake local blockchain where we don't have to wait for transactions to complete and we don't have to deal with any of the oddities on deploying our code to a real testnet or a real mainnet.

We also get a fake account. When we hit Deploy button we deploy the contract. Similar to send ETH back and Forth we have send contract. Deploying contract uses exactly the same process as sending a transaction for just ETH. Main difference is, we populate this data or input field with ton of that bytecode and if you copy the input field data (below), it's massive.
```
//0x608060405234801561001057600080fd5b5060e38061001f6000396000f3fe6080604052348015600f57600080fd5b506004361060285760003560e01c80636057361d14602d575b600080fd5b60436004803603810190603f91906085565b6045565b005b8060008190555050565b600080fd5b6000819050919050565b6065816054565b8114606f57600080fd5b50565b600081359050607f81605e565b92915050565b6000602082840312156098576097604f565b5b600060a4848285016072565b9150509291505056fea2646970667358221220b5ad1d88318a6a7a7eef991b58918781bbf73eaff87e72adfc1405945fb4e97564736f6c63430008120033
```

It represents all the data associated with this smart contract. Deploying a contract is modifying the blockchain and any modification on the blockchain is done through transaction.

Now if we add a number and click Store button we send another transaction. But we can't see our favorite number because by default it's visibility is internal. To see this we need to add public keyword.

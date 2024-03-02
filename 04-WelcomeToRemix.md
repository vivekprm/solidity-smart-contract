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

If we add more instructions in the store method, every transaction costs more gas.

Let's add a new function to retrieve this public variable even though we are able to access it without it.
```sol
function retrieve() public view returns (uint256) {
        return favoriteNumber;
    }
```

Now if we deploy again we see new blue button called retrieve. The colour is blue because of the 'view' keyword. Solidity has a special keyword which notates functions that don't actually have to run or don't actually have to send a transaction for us to call them and those two keywords are going to be **view** and **pure**. 

A function marked view means, we are just going to read state from the blockchain e.g. in case of retrieve we are just going to read what favoriteNumber variable is.
Pure disallows even reading from store or storage. favoriteNumber here is know as storage variable because it's stored in a place called storage. 

```sol
function retrieve() public pure returns (uint256) {
        return 7;
    }
```
Calling a view or pure function doesn't cost gas if we call by clicking the button. But if store function calls this pure or view function, we do need to pay the gas.

Now we can change our contract and allow adding favoriteNumber for others as well

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18; // Works with solidity version >= 0.8.18, we can also specify range of versions.

contract SimpleStorage {
    // Basic types: boolean, uint, int, address, bytes
    // favoriteNumber initializes to 0 if no value specified.
    uint256 public myFavoriteNumber; //0

    struct Person {
        uint256 favoriteNumber;
        string name;
    }

    // Dynamic array
    Person[] public listOfPeople;

    function store(uint256 _favoriteNumber) public {
        myFavoriteNumber = _favoriteNumber;
    }

    // view, pure
    function retrieve() public view returns (uint256) {
        return myFavoriteNumber;
    }

    function addPerson(string memory _name, uint256 _favoriteNumber) public {
        listOfPeople.push(Person(_favoriteNumber, _name));
    }
}
```

# Memory, Storage & Call data Intro
We didn't talk about **memory** keyword above. There are 6 places you can store data in solidity.
- Stack
- Memory: Variable only going to exist temporarily. It's only going to exist for the duration of function call. Most variables automatically default to "memory". strings are special type in solidity, so we have to explicitly set it to memory or calldata.
- Storage: Permanent variable and can be modified.
- Calldata: Variable only going to exist temporarily line memory. Difference is with calldata variable can't be modified.
- Code
- Logs

If we give memory keyword to uint256, we get compile error. As this keyword can only be used with string, array, mappings and struct types. We can't even give it "storage" keyword either because solidity knows it's local varaible and going to short live, it doesn't allow that.

# Basic Solidity Mappings
What if we wanted to get favorite number of a specific person. We have to iterate over the loop and find the data. We could use better datastructure for search called mapping in this case.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18; // Works with solidity version >= 0.8.18, we can also specify range of versions.

contract SimpleStorage {
    // Basic types: boolean, uint, int, address, bytes
    // favoriteNumber initializes to 0 if no value specified.
    uint256 public myFavoriteNumber; //0

    struct Person {
        uint256 favoriteNumber;
        string name;
    }

    // Dynamic array
    Person[] public listOfPeople;

    mapping(string => uint256) public nameToFavoriteNumber;

    function store(uint256 _favoriteNumber) public {
        myFavoriteNumber = _favoriteNumber;
    }

    // view, pure
    function retrieve() public view returns (uint256) {
        return myFavoriteNumber;
    }

    function addPerson(string memory _name, uint256 _favoriteNumber) public {
        listOfPeople.push(Person(_favoriteNumber, _name));
        nameToFavoriteNumber[_name] = _favoriteNumber;
    }
}
```

# Deploying Your First Smart Contract
Lets deploy it to real testnet. Change environment to "Injected Provider - MetaMask" as below:

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/aec43824-0685-42e9-9cec-bb3a1a3495b7)

With this we inject our metamask into Remix. Click view on etherscan in Remix terminal to see details of the transaction. We can copy the transaction and search on etherscan. It shows that it was contract creation.

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/3969fff8-7a68-4dc0-b81e-bf9c3bd49216)

Now if we store a favorite number, we again get MataMask confirmation block as we are changing the blockchain. We can copy the transaction hash and check etherscan again:

![image](https://github.com/vivekprm/solidity-smart-contract/assets/2403660/dffb5927-e4ec-4d21-9d27-95416975f8b0)

# EVM
When we compile the solidity code, it compiles it down to something called the EVM or Ethereum Virtual Machine. EVM is the standard for how to compile and how to deploy smart contracts to Blockchain. Any Blockchain that is EVM compatible, we should be able to deploy Solidity code to. Some examples of EVM compatible Blockchains and layer 2s are Ethereum, Polygon, Arbitrum, Optimism, Zksync etc.

However before deploying check the datails of Blockchain. E.g. Zksync is EVM compatible but couple of keywords don't work on Zksync.

# Remix Storage Factory
https://github.com/cyfrin/remix-storage-factory-f23

Building contacts that can deploy and interact with other contracts are called composability.

Lets create a new file called StorageFactory.sol. And write below code:

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "./SimpleStorage.sol";

contract StorageFactory {
    SimpleStorage public simpleStorage;

    function createSimpleStorageContract() public {
        simpleStorage = new SimpleStorage();
    }
}
```

Now we have StorageFactory which deploys new contract.

Using named import in case we want to import specific contract from a file.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import {SimpleStorage} from "./SimpleStorage.sol";

contract StorageFactory {
    SimpleStorage public simpleStorage;

    function createSimpleStorageContract() public {
        simpleStorage = new SimpleStorage();
    }
}
```

But here we are not keeping track of the simple storage contracts that we are creating and deploying.

We always need two things in case we want to interact with other contracts in StorageFactory:
- Address
- ABI (Application Binary Interface): We can go to the compilation details to find about ABI of contract.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import {SimpleStorage} from "./SimpleStorage.sol";

contract StorageFactory {
    SimpleStorage[] public listOfSimpleStorageContracts;

    function createSimpleStorageContract() public {
        SimpleStorage simpleStorageContract = new SimpleStorage();
        listOfSimpleStorageContracts.push(simpleStorageContract);

    }

    function sfStore(uint256 _simpleStorageIndex, uint256 _newSimpleStorageNumber) public {
        // We always need two things in case we want to interact with other contracts in StorageFactory:
        // - Address
        // - ABI (Application Binary Interface): We can go to the compilation details to find about ABI of contract.
        SimpleStorage mySimpleStorage = listOfSimpleStorageContracts[_simpleStorageIndex];
        mySimpleStorage.store(_newSimpleStorageNumber);
    }

    function sfGet(uint256 _simpleStorageIndex) public view returns (uint256) {
        SimpleStorage mySimpleStorage = listOfSimpleStorageContracts[_simpleStorageIndex];
        return mySimpleStorage.retrieve();
    }
}
```
# Inheritance
Let's say you liked this SimpleStorage contract, you love all the functionalities except for one thing. You wish that this store function doesn't just store the favourite number, you wish that it added 5 to favourite number before storing. One thing we could do, we duplicate all the code in a new file and write that implementation. Better would be to use inheritance. So AddFiveStorage contract can inherit from SimpleStorage contract an override whatever it doesn't like.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import {SimpleStorage} from "./SimpleStorage.sol";

contract AddFiveStorage is SimpleStorage{}
```
For a function to be overridable it needs to have 'virtual' keyword. And then in the contract where we override the function we need to add 'override' keyword.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import {SimpleStorage} from "./SimpleStorage.sol";

contract AddFiveStorage is SimpleStorage{
    // +5
    // Overrides
    // virtual override
    function store(uint256 _newNumber) public override  {
        myFavoriteNumber = _newNumber + 5;
    }
}
```

To search about information or errors use below resources.
# Resources For This Course
- AI Frens
    - [ChatGPT](https://chat.openai.com/)
        - Just know that it will often get things wrong, but it's very fast!
    - [Phind](https://www.phind.com/)
        - Like ChatGPT, but it searches the web
    - [Bard](https://bard.google.com/)
    - [Other AI extensions](https://twitter.com/aisolopreneur/status/1654823630155464704?s=42&t=-pu_sCYtfrfPJU7OXfifrQ)
- Github Discussions
    - Ask questions and chat about the course here!
- [Stack Exchange Ethereum](https://ethereum.stackexchange.com/)
    - Great place for asking technical questions about Ethereum
- [Peeranha](https://peeranha.io/)
    - Decentralized Stack Exchange!

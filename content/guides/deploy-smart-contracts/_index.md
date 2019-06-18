+++
title = "How to deploy SmartContract"
toc = true
weight = 5
+++

Lightstreams goal is to empower developers to create new dApps by the usage of our technology,
but beside a fast-scalable blockchain and a solid SmartVault SDK, one of the most essential 
pieces to implement new dApps are the Smart Contracts.  

Lightstreams network is a fully Ethereum compatible network, therefore every tool
or manual written for ethereum is applicable also for lightstreams blockchain. 

In this section we are going to use our experience to write some simple instructions to deploy your 
first smart contract into Lightstreams blockchain.

### Node Initialization

Firstly, in order to deploy a smart contract we need to have a full synchronized node running locally. 
In case you didn't do it yet, see [these instructions](/guides/lightchain-node-setup/).

Alternatively, you could also connect to our open RPC endpoints:

- MainNet: `https://node.mainnet.lightstreams.io`
- Sirius: `https://node.mainnet.lightstreams.io` 

Although we recommend you to have your local node for a better and more complete 
experience.

## Solidity

As you probably already know **Solidity** is an object-oriented, high-level language for 
implementing smart contracts. You can see more about this particular programming
language within their [official documentation](https://solidity.readthedocs.io/).

There are pluggings to support Solidity code for most of the popular IDE
such as _JetBrains IDEA_, _Sublime Text_ or _emacs_. Also you can find a very good
online editor provided by Ethereum project called [Remix](https://remix.ethereum.org). 
Remix also supports testing, debugging and deploying of smart contracts and much more.

For testing propose we are going to write a very simple `HelloWorld.sol`:
```solidity
pragma solidity ^0.5.0;

contract HelloBlockchainWorld {
    constructor() public {
    }

    function sayHello() public pure returns (string memory message) {
        return "hello";
    }
}
```

## Compilation

In order to deploy and then interact with the written smart contract we need to 
compile it to be deployed into our EVM (Ethereum Virtual Machine). 

As a result of the compilation we are obtaining two elements:
- **ABI**: Application Binary Interface, is the standard way to interact with contracts in the Ethereum ecosystem, both from outside the blockchain and for contract-to-contract interaction.
- **Bytecode**: Assembly representation of the contract in hexadecimal format. 

How do we compile our smart contract? There are several alternatives as you will see next.

### Option 1: Solidity Compiler

Solidity project provides a binary compiler, _solc_, to compile solidity code. You can find clear
instructions about how to install it on every popular OS within their [documentation](https://solidity.readthedocs.io/en/latest/installing-solidity.html).

Once you completed the installation steps you should be capable to run the following command on a terminal
to obtain the compiler version installed.

```bash
$> solc --version

solc, the solidity compiler commandline interface
Version: 0.5.0+commit.1d4f565a.Linux.g++
```

Assuming we stored our HelloWorld example in `/tmp/example/helloworld.sol`, first we are going
to create a destination folder for the _build_ elements:
```bash
$> mkdir /tmp/example/build
```

Then, we execute the next:
```bash
$> solc --abi --bin /tmp/example/helloworld.sol -o /tmp/example/build/ --overwrite
```

As the result from the above command it was generated two files, one containing the ABI representation
of the contract `HelloBlockchainWorld.abi` and another one with the bytecode `HelloBlockchainWorld.bin`.
```bash
/tmp/example/build/
├── HelloBlockchainWorld.abi
└── HelloBlockchainWorld.bin
```

### Option 2: Remix

Another alternative is to use the online tool of Remix. For that we
need to:
1. Paste our _helloworld.sol_ code
2. Click on _Start to compile_ and wait for compilation to finish.
3. Click on _ABI_ and paste the clipboard content into a file named `HelloBlockchainWorld.abi`.
4. Click on _Bytecode_ and paste the clipboard content into a file named `HelloBlockchainWorld.bin`.

![login](/img/guides/solc_remix_edited.png)

### Option 3: NodeJS - Truffle

Truffle is a testing framework for Ethereum written in javascript. Truffle 
provides a full set of tools to compile, deploy and debug smart contracts 
using the Ethereum Virtual Machine (EVM). 

To install truffle, and assuming you already got **npm** installed in your system, 
you only need to run the follow:

```bash
$> npm install -g truffle
``` 

Once truffle is installed you have to create a new empty "project".
```bash
$> truffle init /tmp/example/truffle
```

Now you should have the following folder structure under `/tmp/example/truffle`
```bash
├── contracts
│   └── Migrations.sol
├── migrations
│   └── 1_initial_migration.js
├── test
└── truffle-config.js
```
inside `truffle-config.js` you have to define which version of solidity compiler
you want to use, along with other solidity options, but for now we are only going
to define a fixed version of solidity according to the version we defined in the smart contract 
implementation

```
...
// Configure your compilers
  compilers: {
    solc: {
      version: "0.5.0",    // Fetch exact version from solc-bin (default: truffle's version)
      // docker: true,        // Use "0.5.1" you've installed locally with docker (default: false)
      // settings: {          // See the solidity docs for advice about optimization and evmVersion
      //  optimizer: {
      //    enabled: false,
      //    runs: 200
      //  },
      //  evmVersion: "byzantium"
      // }
    }
  }
...
```

Truffle will compile every contract under '/contracts', therefore 
we have to copy/move our `helloworld.sol` file into `/tmp/example/truffle/contracts`
```bash
$> cp /tmp/example/helloworld.sol /tmp/example/truffle/contracts/
```

We remove the unnecessary file `/migrations/1_initial_migration.js`:
```bash
$> rm migrations/1_initial_migration.js
``` 

And at the end we run the compilation:
```bash
$> truffle compile


Compiling your contracts...
===========================
> Compiling ./contracts/helloworld.sol
> Artifacts written to /tmp/example/truffle/build/contracts
> Compiled successfully using:
   - solc: 0.5.0+commit.1d4f565a.Emscripten.clang
```

As result of above command we will obtain a json file `build/contracts/HelloBlockchainWorld.json`
which contains the __abi__ and the __bytecode__.

```bash
cat build/contracts/HelloBlockchainWorld.json | jq '.abi'
[
  {
    "inputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "constructor"
  },
  ...
]
```

```bash
cat build/contracts/HelloBlockchainWorld.json | jq '.bytecode'
"0x608060405234801561001057600080fd5b5061013f806100206000396000f...."
```

*Note: `jq` is a tool to extract json content in bash*

## Deploy

In order to deploy an smart contract we will need to have an unlock account holding 
enough funds. To unlock the account we are going to use [`geth`](/getting-started/install/#geth).

We attach _geth_ to our running local node and execute `personal.unlockAccount()` over the 
account we desire to unlock.
```bash
$> geth attach http://localhost:8545

Welcome to the Geth JavaScript console!

instance: ./v1.8.27/linux-amd64/go1.10.3
 modules: debug:1.0 eth:1.0 net:1.0 personal:1.0 rpc:1.0 web3:1.0

> personal.unlockAccount("0xc916cfe5c83dd4fc3c3b0bf2ec2d4e401782875e")
Passphrase: 
true
```

### Option 1: Console (`Geth`)

First, we need to attach our terminal to our node

```bash
$> geth attach http://localhost:8545
```

*Note: Every following statement is executed on geth terminal*

We assign the content of the file generated during the compilation of the smart contract
 to two variables. 
```javascript
> var bin = <"HelloBlockchainWorld.bin" file content>
> var abi = <"HelloBlockchainWorld.abi" file content>
```

Create a contract template object based on the _abi_ and calculate the estimated gas
for the transaction of deployment:

```javascript
var contractTemplate = web3.eth.contract(abi);
var estimatedGas = eth.estimateGas({data: "0x" + bin})
```

Send contract deploy transaction, The contract deployment is an asynchronous call therefore
in order to track the process, we will add a callback function which logs the execution
progress:

```javascript
contractTemplate.new({from: "0xc916cfe5c83dd4fc3c3b0bf2ec2d4e401782875e", data: "0x" + bin, gas: estimatedGas}, 
  function(err, contract){  
   if(err){
     console.log("Error sending transaction: ", err);
     return;
   }
   if(!contract.address){
     console.log("Transaction hash: " + contract.transactionHash)
     return;
   }
   console.log("Contract deployed at: " + contract.address);
  });
```
 
### Option 2: Remix

Remix also integrates the utilities required to deploy and interact with smart contracts. 
In case you want to connect to the node running on your local machine you will need to 
authorized by the usage of the following flags `--rpcvhost` and `--rpccorsdomain`:

```bash
$> lightchain run --datadir=${HOME}  --rpc --rpcaddr 0.0.0.0 -rpcapi eth,net,web3,personal,debug --rpccorsdomain=* --rpcvhosts=localhost
```

Now we have our environment ready we go back to _Remix_ dashboard and click in __Run__.
Select _Web3 Provider_ from the _Environment_ selector and paste the local rpc address `http://localhost:8545`.
_from_ account unlocked at the beginning.

Click __Deploy__ and if everything went successfully you will see a transaction receipt as
the one on the next screenshot.

![remix](/img/guides/solc_remix_deploy_edited.png)

### Option 3: Truffle

In `truffle-config.js` you need to update uncomment the _development_ network, and modify it if it is needed,
to connect to a running ethereum node. Also we indicate which __from__ account is going to be 
use as default message sender for every transaction. Also it is important to mention that 


```
...
  networks: {
    development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
      from: "0xc916cfe5c83dd4fc3c3b0bf2ec2d4e401782875e",
      gasPrice: "500000000000"
    },
    ...
  }
...
```
*Note: Lightchain networks use 500 gwei as _gasPrice_*

We create a new migration file `/migrations/2_hello_world.js` with the following code:
```javascript
const HelloBlockchainWorld = artifacts.require("HelloBlockchainWorld");

module.exports = function(deployer) {
  deployer.deploy(HelloBlockchainWorld);
};
```

And finally we trigger the deployment:
```bash
$> truffle deploy --reset --network=development
```
*Note: Remember that the _from_ account MUST unlock it before we run the deployment. You
can see how to do it at the top of this section.*

Output:
```bash
2_hellow_world.js
=================

   Deploying 'HelloBlockchainWorld'
   --------------------------------
   > transaction hash:    0x734944fc76af2c71bfee528c94abba2a5c71575140fede9ab26e8ee332fde3e2
   > Blocks: 0            Seconds: 0
   > contract address:    0x0f5d5bEb0766C7a26198Bf82EBF1B2df3dEA09e5
   > block number:        90
   > block timestamp:     1560868779
   > account:             0xc916Cfe5c83dD4FC3c3B0Bf2ec2d4e401782875e
   > balance:             299999995.447825
   > gas used:            104043
   > gas price:           500 gwei
   > value sent:          0 ETH
   > total cost:          0.0520215 ETH

   > Saving artifacts
   -------------------------------------
   > Total cost:           0.0520215 ETH
```

From the output above we can see that our HelloWorld smart contract was deployed
at the address _0x0f5d5bEb0766C7a26198Bf82EBF1B2df3dEA09e5_ and the deployment cost 
was _0.052 ETH_.






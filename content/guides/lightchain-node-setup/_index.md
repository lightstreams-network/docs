+++
title = "Lightchain Node"
toc = true
weight = 1
+++

In this section, we will explain the steps to install and synchronize
a Lightstreams PoA blockchain node. Moreover, as part of the functionalities
required by token exchanges, we will be proving examples of how to interact with Lightstreams blockchain in order to create accounts, transfer tokens or fetch tx receipts.

## Installation

Lightstreams has released its own [ethereum-compatible blockchain](https://github.com/lightstreams-network/lightchain)
which uses Byzantine consensus to replace the original proof-of-work (PoW) from Ethereum.

Using `lightchain` you can connect to Lightstreams blockchain and use every
functionality currently existing on Ethereum. See more in the command line [documentation](/cli-docs/lightchain/)

### Pre-compiled binaries

Lightstreams provides precompiled binaries for the most popular Unix distributions:
and macOS.

== macOS ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/lightchain/latest/lightchain-osx" -O /usr/local/bin/lightchain
```
== Linux (amd64) ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/lightchain/latest/lightchain-linux-amd64" -O /usr/local/bin/lightchain
```

After downloading the binary, you will need to set the right executable permissions to it, as follow:
```
chmod a+x /usr/local/bin/lightchain
```

### From Source code

In case you prefer to compile your own version of `lightchain` you just need to
follow the instructions at [this repository](https://github.com/lightstreams-network/lightchain).

## Run Lightchain node

Once `lightchain` is installed we can proceed with the initialization and synchronization
of a new lightstreams node.

Lightstreams implements three different networks: 
- **mainnet**: Main company network 
- **sirius**: Test network, [free tokens](/getting-started/quick-start/#get-free-testing-tokens).
- **standalone**: Isolated-local test network. 

At the minute `lightchain` is connecting by default to `mainnet`. For testing proposes we
recommend to use `sirius` or `standalone`.

### Node initialization

To initialise a new blockchain you need to run lightchain init and choose
a local path where blockchain files are going to be stored.

```
lightchain init --datadir="${HOME}/.lightchain" [--mainnet|--sirius|--standalone]
```


### Node launching

To run a lightchain node you only need to run the following command:
```
lightchain run --datadir="${HOME}/.lightchain"
```

After the above ommand is executed the Lightstreams node will proceed with the synchronization. It would take
up to several minutes, so it is time to take request your first [__free tokens__](/getting-started/quick-start/#get-free-testing-tokens)
for _Sirius_ network.

Once the node is synchronized we should leave node running in order to interact with the blockchain.

Lightstreams also provides two block explorers, one for the [MainNet](https://explorer.mainnet.lightstreams.io) 
and another for [Sirius](https://explorer.sirius.lightstreams.io), to see which is the current state of the blockchain. 
The block explorer code is [open-sourced](https://github.com/lightstreams-network/lightchain-explorer), so in case you decide to use 
_standalone_ you could also run a local instance of it.

#### Help

To see more available options for launching a lightchain node, check the
[client documentation section](/cli-docs/lightchain/run/) or execute in the terminal:
```
lightchain run -h
```

## Interact with Lightstreams node

As it was mentioned above, Lightstreams node is fully ethereum-compatible therefore
 ethereum [JSON RPC API](https://github.com/ethereum/wiki/wiki/JSON-RPC) is also available.

To enable those RPC endpoints, we need to specify the APIs we want to enable and the endpoints. At the command line argument, when Lightstreams node is launched,  we need to
include `--rpc --rpcapi eth,net,web3,personal,admin`. In case you want to enable the WebSocket endpoints you have to also use`--ws`

```
lightchain run --datadir="${HOME}/.lightchain" --rpc --rpcapi eth,net,web3,personal,admin --ws
```

By default RPC API is exposed over port _`:8545`_ and WebSocket over port _`:8546`_.
In case you want to specify a different port, you may use the following flags
`--rpcport ${RPC_PORT}` or `--wsport ${WS_PORT}` respectively.

In addition to those, IPC Unix socket is always enabled and you can find it at
`${HOME}/.lightchain/database/geth.ipc` (according to the values used on above example)

### Example

As it is explained above we can interact with Lightstreams node as we would have been
interacting with an Ethereum node. For instance, we could attach a Geth to the running
Lightstreams node and create a new account and perform a transfer.

***Start interactive Geth console***
```
geth attach http://localhost:8545
```

***Create a new account***
```
> personal.newAccount("passphrase")
"0xe7094bd66363c0442bd99ea00fccb19b0d272453"
```

***Transfer tokens***
```
> eth.sendTransaction({from:eth.accounts[0], to:"0xe7094bd66363c0442bd99ea00fccb19b0d272453", value: web3.toWei(0.05, "ether")})
"0x2ca8bce6a70566a0869a9fd2ac74743e05fe19e17ec118d7a4933f07714faeed"
```

***Read receipt***
```
> eth.getTransactionReceipt("0x2ca8bce6a70566a0869a9fd2ac74743e05fe19e17ec118d7a4933f07714faeed")
{
  blockHash: "0xc96707c294c79b7d3667a59e5f097f72375d4b7f0135e0055eabc5e70ddec717",
  blockNumber: 17793,
  contractAddress: null,
  cumulativeGasUsed: 21000,
  from: "0xc916cfe5c83dd4fc3c3b0bf2ec2d4e401782875e",
  gasUsed: 21000,
  logs: [],
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  status: "0x1",
  to: "0xe7094bd66363c0442bd99ea00fccb19b0d272453",
  transactionHash: "0x2ca8bce6a70566a0869a9fd2ac74743e05fe19e17ec118d7a4933f07714faeed",
  transactionIndex: 0
}

```

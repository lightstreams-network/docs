+++
title = "Install"
toc = true
weight = 1
+++


| Version | Release Date |
|---------|--------------|
|0.15.0-alpha|29.05.2019|


## Installation

A Lightstreams node consists of the following pieces:

- [`leth`](#leth) is a command line interface used to run, interact, and control the Lightstreams node
- [`ipfs`](#ipfs) is a decentralised file system enhanced with our award winning “Permissioned Blocks” technology
- [`lightchain`](#lightchain) is a command line interface to connect to lightstreams ethereum compatible blockchain
- [`geth`](#geth)(Optional) is the the command line interface for running a full ethereum node implemented in Go


### Leth

Leth connects to permissioned blockchain protocol (Ethereum Smart Vault) to empower
content creators to monetise their intellectual property data. It can be used a CLI or HTTP server.

#### How to install

***Pre-compiled binaries***

== macOS ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/leth/latest/leth-osx" -O /usr/local/bin/leth
```

== Linux (amd64) ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/leth/latest/leth-linux-amd64" -O /usr/local/bin/leth
```

### Lightchain

Lighstreams has released its own [ethereum-compatible blockchain](https://github.com/lightstreams-network/lightchain)
which uses byzantine consensus to replace the original proof-of-work (PoW) from Ethereum.

Using `lightchain` you can connect to Lightreams blockchain and use every
functionality currently existing on Ethereum. See more in the command line [documentation](/cli-docs/lightchain/)

#### How to install

***Source code***

Follow the instructions at [this repository](https://github.com/lightstreams-network/lightchain).

***Pre-compiled binaries***

== macOS ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/lightchain/latest/lightchain-osx" -O /usr/local/bin/lightchain
```
== Linux (amd64) ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/lightchain/latest/lightchain-linux-amd64" -O /usr/local/bin/lightchain
```

### IPFS (lightstreams version)

IPFS is a peer-to-peer distributed file system that seeks to connect all computing devices with the same system of files.

Lightstreams has enhanced original implementation of IPFS to bring a to permissioned
layer which allows users to control the access to after content is being distributed.

#### How to install

***Pre-compiled binaries***

== macOS ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/ipfs/latest/ipfs-osx" -O /usr/local/bin/ipfs
```
== Linux (amd64) ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/ipfs/latest/ipfs-linux-amd64" -O /usr/local/bin/ipfs
```

### Geth (Optional)

Only in case of using `Rinkeby` network.

***Source code***

Follow the [official instructions](https://geth.ethereum.org/downloads/)

***Pre-compiled binaries***

== macOS ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/geth/latest/geth-osx" -O /usr/local/bin/geth
```
== Linux (amd64) ==
```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/geth/latest/geth-linux-amd64" -O /usr/local/bin/geth
```

## Permissions

In case you decide to install pre-compiled versions, it will be required
another step in order to set the right executable permissions to those binaries, as follow:
```
chmod u+x /usr/local/bin/leth
chmod u+x /usr/local/bin/geth
chmod u+x /usr/local/bin/lightchain
chmod u+x /usr/local/bin/ipfs
```


## Check installation

```
> leth version
Version: 0.15.0-alpha API CORS

> ipfs version
ipfs version 0.4.16-dev

> lightchain version
Version: 1.2.0 Rock && Roll

> geth version
Geth
Version: 1.8.23-stable
Git Commit: c942700427557e3ff6de3aaf6b916e2f056c1ec2
Architecture: amd64
Protocol Versions: [63 62]
```

## Next steps
- [Quick start](/getting-started/quick-start/)
- [Create an account](/getting-started/quick-start/#create-an-account)
- [Getting free tokens](/getting-started/quick-start/#get-free-testing-tokens)

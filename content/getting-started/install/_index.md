+++
title = "Install"
toc = true
weight = 1
+++

## Install

We have compiled binaries for macOS and Linux available (Windows not yet available).

### Install from prebuilt package

#### macOS

```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/leth/leth-osx" -O /usr/local/bin/leth
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/ipfs/ipfs-osx" -O /usr/local/bin/ipfs
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/lightchain/lightchain-osx" -O /usr/local/bin/lightchain
wget -qO- https://gethstore.blob.core.windows.net/builds/geth-darwin-amd64-1.8.22-7fa3509e.tar.gz | tar xvz --strip-components=1 -C /usr/local/bin/ geth-linux-amd64-1.8.21-9dc5d1a9/geth
```

#### Linux

```
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/leth/leth-linux-amd64" -O /usr/local/bin/leth
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/ipfs/ipfs-linux-amd64" -O /usr/local/bin/ipfs
wget "https://s3.eu-central-1.amazonaws.com/lightstreams-public/lightchain/lightchain-linux-amd64" -O /usr/local/bin/lightchain
wget -qO- https://gethstore.blob.core.windows.net/builds/geth-linux-amd64-1.8.21-9dc5d1a9.tar.gz | tar xvz --strip-components=1 -C /usr/local/bin/ geth-linux-amd64-1.8.21-9dc5d1a9/geth
```

If you have any issues installing Geth, please follow the [official instructions](https://geth.ethereum.org/downloads/)

#### Windows

Not yet available.

### Set permissions

```
chmod u+x /usr/local/bin/leth
chmod u+x /usr/local/bin/ipfs
chmod u+x /usr/local/bin/geth
chmod u+x /usr/local/bin/lightchain
```

### Install with Docker

```
docker run -it -p 9091:9091 --name ls-node1 -d lightstreams/node
```

## Check installation

```
> leth version
Version: 0.7.2-alpha Meta && PoA Test Ntw

> ipfs version
ipfs version 0.4.9-rc2

> lightchain version
Version: 0.9.1-alpha Sirius-Net

> geth version
Geth
Version: 1.8.21-stable
Git Commit: 9dc5d1a915ac0e0bd8429d6ac41df50eec91de5f
Architecture: amd64
Protocol Versions: [63 62]
Network Id: 1
Go Version: go1.10.3
Operating System: linux
GOPATH=/home/ggarrido/goApps
GOROOT=/home/ggarrido/Software/go
```

## Next steps
- [Quick start](/getting-started/quick-start/)
- [Create an account](/getting-started/quick-start/#create-an-account)
- [Getting free tokens](/getting-started/quick-start/#get-free-testing-tokens)

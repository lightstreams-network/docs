+++
title = "Quick start"
toc = true
weight = 2
+++

The following assumes you have `leth` installed. Please follow [these instructions](/getting-started/install/#install) to install.

## Getting help

Run `leth help` command to display all commands you have in disposition in the current version.

```
Lightstreams CLI for interacting with a configured node.

Usage:
  leth [flags]
  leth [command]

Available Commands:
  acl         Features LethACL's pkg capabilities over CLI such as granting ACL permissions.
  auth        Features LethAuth's pkg capabilities over CLI such as token generation, verification...
  docs        Generates LETH cmd usage docs based on code into the: 'docs/cmd/auto_generated'.
  help        Help about any command
  init        Initializes new LS local node for a chosen network.
  run         Runs full Leth node by spawning blockchain and IPFS daemons.
  storage     Features LethStorage's pkg capabilities over CLI such as file upload/download, access authorization...
  version     Describes version.
  ...
  ...

Flags:
  -h, --help   help for leth

Use "leth [command] --help" for more information about a command.
```

Display current version:

```bash
leth version
Version: 0.15.0-alpha CORS API
```

Display instructions for initializing new Lightstreams Node:

```bash
leth init --help
Initializes new LS local node for a chosen network.

Usage:
  leth init [flags]

Flags:
  -h, --help             help for init
      --network string   Possible values: 'rinkeby|sirius'.
      --nodeid int       ID of the node in order to support multiple nodes on the same machine. 0 by default.
```

Go to the [command line documentation](/cli-docs/leth) to learn more about leth CLI.

## Running Lightstreams node

First, initialize new Leth node with ID 1 for Sirius network:

```bash
leth init --nodeid=1 --network=sirius

{"msg":"Initializing Leth node...","nodeID":1,"network":"sirius"}
{"msg":"IPFS: initializing IPFS node at $HOME/.lightstreams_1/ipfs"}
{"msg":"IPFS: generating 2048-bit RSA keypair...done"}
{"msg":"IPFS: peer identity: Qma1bKbQVYqHMhWzaRHAkKU5s5FsDnhR5bMzWLbjwxUaN6"}
{"msg":"IPFS successfully initialized.","dataDir":"$HOME/.lightstreams_1/ipfs"}
{"msg":"Sirius node successfully initialized.","dataDir":"$HOME/.lightstreams_1/sirius"}
{"msg":"Leth node fully initialized!!!","nodeDir":"$HOME/.lightstreams_1"}
```

Secondly, run a lightstreams node:

```bash
leth run --nodeid=1 --network=sirius

{"msg":"Starting Leth node online services (blockchain, IPFS)..."}
{"msg":"GETH: INFO [09-13|11:30:40.138] Maximum peer count ETH=25 LES=0 total=25"}
{"msg":"GETH: INFO [09-13|11:30:40.148] Starting peer-to-peer node instance=Geth/v1.8.15-stable-89451f1c/darwin-amd64/go1.10.4"}
...
```

```bash
...
{"msg":"GETH: INFO [09-13|11:31:26.189] Imported new block receipts count=906 elapsed=9.521ms   number=960 hash=413833…8d126d size=4.13kB  ignored=0"}
{"msg":"GETH: INFO [09-13|11:31:26.390] Imported new block headers count=384 elapsed=149.265ms number=1344 hash=4524ae…5d3fff ignored=0"}
{"msg":"GETH: INFO [09-13|11:31:26.406] Imported new block receipts count=384 elapsed=2.144ms   number=1344 hash=4524ae…5d3fff size=1.54kB  ignored=0"}
```

After you run the command above, the network synchronization will take several minutes.
So grab a coffee and [request some test](#get-free-testing-tokens) tokens while you wait :)


To see the current state of the lightstreams test network (Sirius) and check the status of your transactions, you can go to the [lightstreams block explorer](http://explorer.sirius.lightstreams.io)

#### Using Rinkeby network

If you prefer to run your leth over the `Rinkeby` network, just repeat the commands a using `--network=rinkeby`.

### Expose the Lighstreams HTTP API
You need to run your `leth` server again, but this time using the `--https` flag as follow:
```bash
leth run --nodeid=1 --network=sirius --https
```

Even if flag used refers to https by default is exposed over http. In case you want to use a secure protocol, follow the instructions
in the next section.

#### Running over HTTPs

To initialize `leth` over HTTPs protocol you need to follow the next steps. At first you need to use
valid SSL certificates which can be generated, for instance, by running the following bash command:

```bash
mkdir -p /etc/ssl/leth
cd /etc/ssl/leth
openssl req -x509 -out localhost.crt -keyout localhost.key \
  -newkey rsa:2048 -nodes -sha256 \
  -subj '/CN=localhost' -extensions EXT -config <( \
   printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
chmod a+r localhost.crt localhost.key
```

Once you have valid ssl certificates are allocated in your local machine, you have to edit
leth node configuration file, at `$HOME/.lightstreams_1/config.json`, and include the path
for your ssl certificates and the port where the HTTPs server is going to be exposed.

```js
{
    "https_server": {
        "port": 8080,
        "certificate_pem_filepath": "/etc/ssl/leth/localhost.crt",
        "certificate_pem_priv_key_filepath": "/etc/ssl/leth/localhost.key"
    },
....
```

At last, you need to run your `leth` server again, but this time using the `--https` flag as follow:
```bash
leth run --nodeid=1 --network=sirius --https
```

Within the first debug output shown in your terminal you will see the next one:
````
...
{"level":"debug","ts":1544091804.1871579,"caller":"http/server.go:28","msg":"Starting Leth HTTP server listening on port: 8080."}
...
````

Visit the following [link](/http-api-doc) to learn how to use leth http api.

## Get FREE Testing Tokens

### Obtaining PHT for Sirius

To get free test tokens, please signup on our community forum and [follow the instructions provided on this thread](https://discuss.lightstreams.network/t/request-test-tokens/64)


### Obtaining ETH for Rinkeby

Connect to the Lightstreams node via IPC:

```bash
geth --datadir=$HOME/.lightstreams_1/rinkeby attach ipc:$HOME/.lightstreams_1/rinkeby/geth.ipc
```

Create a new Leth node account using the attached Geth JavaScript console and check the its balance:

```javascript
geth --datadir=$HOME/.lightstreams_1/rinkeby attach ipc:$HOME/.lightstreams_1/rinkeby/geth.ipc

Welcome to the Geth JavaScript console!

Instance: Geth/v1.8.15

> personal.newAccount()
>> ...type your password...
"0xa92e3705e6d70cb45782bf055e41813060e4ce07"
> eth.accounts
["0xa92e3705e6d70cb45782bf055e41813060e4ce07"]
> eth.coinbase
"0xa92e3705e6d70cb45782bf055e41813060e4ce07"
> eth.getBalance(eth.coinbase)
0
>
```

Request FREE ETH from Rinkeby Faucet:

- Publish your Ethereum address (0xa92e3705e6d70cb45782bf055e41813060e4ce07) anywhere in a public social network
- E.g, post your address to my [Google Plus group](https://plus.google.com/u/0/communities/115209806315551990293)
- Open [https://www.rinkeby.io/#faucet](https://www.rinkeby.io/#faucet) and paste the post url
- Wait few seconds, if the blockchain is fully synced, check the balance once again `eth.getBalance(eth.coinbase)` -> 3000000000000000000

## Learn more

To learn more about how you can start sharing files using `leth`, go to the next
section, [File sharing](/guides/file-sharing/)

### Help

If in doubt, you can always run any command with a `--help` flag to show and explain to you all the possible flags and cmd usages.

```bash
leth acl --help
```

## Need human help?

We are happy to get you started! Join our [telegram channel](https://t.me/lightstreams) or ask as many questions as you want in the [lightstreams forum](http://discuss.lightstreams.network)!

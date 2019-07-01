+++
title = "Metamask Integration"
toc = true
weight = 4
+++

In this page we are going to explain how to use MetaMask to connect to Lightstreams networks
and send token to other users.

MetaMask is a bridge that allows you to connect to your ethereum blockchain using RPC protocol
in your browser. MetaMask secures your identity providing a identit y manager to sign
transaction in the blockchain.

## Installation

MetaMask can be installed as an add-on for your favorite browser Chrome, Firefox or Opera. Visit
[official website](https://metamask.io/) to know more and to install the add-on.


## Login

Log in or sign up to your MetaMask application.

![login](/img/guides/metamask_login.png)

## Create/Import Accounts

Click on “Expand View” to open in MetaMask in a new tab and manage your accounts and network in a
better interface.

![expand-view](/img/guides/metamask_expand_view.png)

You can create a new account by clicking on "Create Account" or restore your MetaMask Wallet
using the secret backup phrase you should have saved during the account creation. MetaMask
also support Ledger and Trezor hardware wallets.

![new_account](/img/guides/metamask_new_account.png)

## Networks

MetaMask engages the connection to any Ethereum compatible network using the RPC protocol. By default,
MetaMask lists the most popular Ethereum networks, such as _MainNet_, _Rinkeby_ and _Ropsten_.
But you can also connect to a local node running on port *:8545* or any other endpoint *Custom RPC*.

![new_account](/img/guides/metamask_network_list.png)

#### Connect to Lightstreams networks

Lightstreams team provides two RPC endpoints for each of its running networks, Sirius and Mainnet. To create a new connector
just click on _Custom RPC_ from the above screenshot.

**Lightstreams MainNet**

```
Network Name: Lightstreams Mainnet
New RPC URL: https://node.mainnet.lightstreams.io
ChainID: 163
Symbol: PHT
Explorer: https://explorer.lightstreams.io
```

![new_account](/img/guides/metamask_rpc_mainnet.png)


**Lightstreams Sirius (Testnet)**

```
Network Name: Lightstreams Sirius
New RPC URL: https://node.sirius.lightstreams.io
ChainID: 162
Symbol: PHT
Explorer: https://explorer.sirius.lightstreams.io
```

![new_account](/img/guides/metamask_rpc_sirius.png)

## Transfer Tokens

To be able to transfer tokens, firstly, you need to hold them. Currently our team is working in the integration
of PHT to major exchanges. In meanwhile you might request **FREE TOKENS** for Sirius by our
[*discuss forum*](https://discuss.lightstreams.network/t/request-test-tokens/64/10) or in
our [*telegram dev group*](https://t.me/LightstreamsDevelopers).

From your account dashboard click on _Send_ to start the transfer of your tokens

![new_account](/img/guides/metamask_send_step0.png)

Set a destination address in _to_, amount to be sent _Amount_ and click in _Advanced Options_
and set the amount _Gas Price_ to **500 GWEI**.

![new_account](/img/guides/metamask_send_step1.png)
![new_account](/img/guides/metamask_send_step2.png)

Click in _Save_ and _Confirm_ and wait for few seconds till you receive the confirmation as follow:

![new_account](/img/guides/metamask_send_last.png)



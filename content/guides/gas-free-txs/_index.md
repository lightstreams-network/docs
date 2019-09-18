+++
title = "Gas free transactions"
toc = true
weight = 6
+++

> Turn your dapps into apps. Free your users. No more Metamask. No more gas.

One of the biggest obstacles stopping blockchain startup applications from reaching mainstream adoption is a bad UX. Blockchain is still very technical and educating users on importance of gas fees and gas price is not working out.

Lightstreams is determined to provide all the necessary tools so developers can focus directly on their specific business use-case. For this reason we decided to implement the [EIP-1077](https://github.com/ethereum/EIPs/blob/ed621645c8f3bc5756492f327cda015f35d9f8da/EIPS/eip-1077.md) compliant [Gas Station Network](https://gsn.openzeppelin.com/) solution designed by OpenZeppelin and TabooKey directly into the Lightstreams SDK. In this getting-started guide **you will learn how to implement the GSN feature into your own Smart Contracts so your users can interact with your application without the necessary PHT tokens.**

## Take your existing Smart Contract

E.g, given you have a simple `Voter.sol` smart contract and your users can either up-vote or down-vote some arbitrary value.

```js
contract Voter {
    uint256 public count;

    function upVote() public {
        count++;
    }

    function downVote() public {
        count--;
    }
}
```

## Inherit the gas free feature

Inherit [GSN.sol](https://raw.githubusercontent.com/lightstreams-network/lightstreams-js-sdk/master/contracts/utils/GSN.sol), located in Lightstreams public JS SDK, to convert your traditional SC to a GSN compatible one.

```js
npm i --save lightstreams-js-sdk
import "@lightstreams-js-sdk/contracts/utils/GSN.sol";

contract Voter is GSN {
```

## Register your Gas Free SC in a global RelayHub

Deploy the `Voter.sol` and call the `initialize` method. As `RELAY_HUB` argument specify [0xECf278654f73000F9cB3b05858158AC49c29ed68](https://explorer.sirius.lightstreams.io/addr/0xecf278654f73000f9cb3b05858158ac49c29ed68).

This is a official RelayHub already deployed on our **Sirius** test network.

```
voter.initialize(RELAY_HUB)
```

## Pay for your users transactions

The users transactions will be free but the application still has to pay for it. This is done by pre-funding the SC you want to be gas-free in RelayHub.

Install OZ GSN Helpers:
```js
"@openzeppelin/gsn-helpers": "0.1.9",
```

Import the `fundRecipient` method:
```js
const { fundRecipient } = require('@openzeppelin/gsn-helpers');
```

Fund the `Voter.sol` with as many PHTs you are willing to pay for your users transactions gas costs:
```js
await fundRecipient(web3, {
  recipient: voter.address,
  relayHubAddress: RELAY_HUB,
  amount: web3.utils.toWei(10, "ether"),
  from: YOUR_PHT_ACCOUNT
});
```

## Let users perform FREE transactions

In order to do this, you will need a special Web3 lib decorated with HTTP Relay functionality. Why? Because the users gas-free transactions will be now submitted to a special **HTTP Relayer Server** and decorated before they are broadcasted to blockchain.

Use the [Lightstreams JS SDK](https://github.com/lightstreams-network/lightstreams-js-sdk) and your TX will be automatically routed through our Sirius Relayer Server: `https://gsn.sirius.lightstreams.io/getaddr` without any additional setup required on your side.

Require the LS modified OZ Network library:
```js
const { fromConnection } = require('@lightstreams-js-sdk/node_modules/openzeppelin/network');

// TODO: improve the require pseudo code
```

Create a new GSN powered Web3 object:
```js
gsnCtx = await fromConnection(
  web3.eth.currentProvider.host, {
    gsn: {
      dev: false,
      signKey: emptyAcc.privateKey
    }
});

web3 = gsnCtx.lib;
```

Let your users perform gas-free TXs!
```js
const voter = await new gsnCtx.lib.eth.Contract(voter.abi, voter.address);

await voter.methods.upVote().send({
  from: emptyAcc.address,
  gasPrice: 500000000000,
  gasLimit: 200000,
});
```

## Support

In case you have any question don't hesitate to ask on your [dev forum](https://discuss.lightstreams.network/)!

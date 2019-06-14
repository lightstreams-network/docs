+++
title = "Example eShop"
toc = true
weight = 3
+++

## Introduction

This example decentralized application (DApp) demonstrates how **two or more peers can connect and securely sell/purchase commercial content together without the need for a central server.**

## Source code

[Example Decentralized Peer-to-Peer eCommerce app written using ReactJS + Leth SDK](https://github.com/lightstreams-network/example-eshop)

## App

The example is only made of static js/css/html and uses ReactJS framework.

[https://example-eshop.lightstreams.io](https://example-eshop.lightstreams.io)

### 1) Configuring Node Provider
![node_provider](/img/node_provider.png)

The first step is to configure a fully synced Lightstreams Node responsible for storing files in SmartVault, managing accounts and performing the blockchain Calls/TXs.

We encourage you to run your own local node. By default, the app connects to our public gateway on the Sirius Testnet.

### 2) Configure Your Account

Create your Lightstreams account or login using an existing one. The password will be used to encrypt, lock the `keystore` file on the node's disk.

![choose_account](/img/choose_account.png)

### 3) Create a Shop

After you configure your account, you enter a general dashboard where you can see all the eShops created by our community, the content being sold and how to buy it.

![create_shop](/img/create_shop.png)

For simplicity of the demo, the metadata such as smart contract addresses of all the shops created by Lightstreams community are stored and aggregated in a real-time Firebase DB but when developing your own application, you can store them however you find appropriate. Smart contract? MySQL Database? IPFS?

For creating an eShop, you will need some PHT tokens. Request them at our [forum](https://discuss.lightstreams.network).

Creating a shop using the UI will create and deploy a new smart contract keeping track of the digital content you will be selling. This is possible thanks to the Leth SDK `shop` module booted on Lightstreams Node launch and exposed over CLI and HTTPS. For full documentation about the internals, visit our [getting started with e-commerce guide](https://docs.lightstreams.network/guides/peer-to-peer-ecommerce/).

### 4) Sell/Buy Content

Content on sale is stored in the configured node's SmartVault.

E.g, you can purchase a picture of a fountain I took in Mallorca for 15 Sirius test network PHTs. Behind the scenes, the SmartVault will grant you a permission to access this picture, securely stored in Lightstreams enhanced permissioned IPFS, the moment the Shop's Smart Contract receives the funds.

![sell_content](/img/sell_content.png)

## Conclusion

Thanks to Lightstreams SDK, Leth, creating DApps and monetizing commercial content was never easier!

[Getting started with e-commerce guide.](https://docs.lightstreams.network/guides/peer-to-peer-ecommerce/)

+++
title = "Ecommerce"
toc = true
weight = 4
+++

If you followed the [Private File Sharing](/guides/file-sharing/) tutorial you learned how to obtain free PHTs and how to distribute files in peer-to-peer manner.

In this tutorial you will learn how to sell your digital content and how other users can buy it without any intermediary!

## Selling digital content

The decentralized shopping support was added to `Leth` in version `0.12.1`. Make sure you have the latest version by running:

```bash
~ $leth version
Version: 0.12.1-alpha LethShop
```

Boot your local node connected to a `Sirius` test network. In this tutorial we will use `NodeID 101` representing the Seller's node.

```bash
leth run --nodeid=101 --network=sirius
```

Add the commercial content, you wish to sell later, to your node's storage. We will be selling a "rare" image from the **It Crowd** series.

```bash
leth storage add --nodeid=101 --network=sirius --owner=0xd119b8b038d3a67d34ca1d46e1898881626a082b --file=/Users/enchanterio/Downloads/it-crowd.jpg
```

Authorize the ACL creation protecting your commercial file:
```bash
Enter password to decrypt the account PK and store it in memory:
<type your keystore password>
```

File successfully added:
```json
{"acl":"0xEB9D37F30F406e2642E211C19Ed6F7A5FC6d8Ec4","meta":"QmNnUze4f1QfnSQJFFco2hdPWZb2iXUjcB2onAzxLQQj5f"}
```

*Note: This file is at this exact moment still private.*

Create your online **Shop**:
```bash
leth shop create --nodeid=101 --network=sirius --from=0xd119b8b038d3a67d34ca1d46e1898881626a082b
```

Output:
```json
{"shop":"0xffeF98e9de5524Eaf82A8DE88B031160f694a90A"}
```

Check the **Shop Balance** using Sirius Blockchain Explorer: https://explorer.sirius.lightstreams.io/addr/0xffef98e9de5524eaf82a8de88b031160f694a90a

![0 Shop Balance](/img/0-shop-balance.png)

**Sell the access** to your file, let's say for 1 PHT, at your newly created online, decentralized shop:
```bash
leth shop sell --nodeid=101 --network=sirius --shop=0xffeF98e9de5524Eaf82A8DE88B031160f694a90A --acl=0xEB9D37F30F406e2642E211C19Ed6F7A5FC6d8Ec4 --price_wei=1000000000000000000 --from=0xd119b8b038d3a67d34ca1d46e1898881626a082b
```

Result:
```json
{"success":"true"}
```

**From this moment, anyone can get read access to your commercial content by simply purchasing the permission to access it.**

You can announce in social media that the Read ACL Permission `0xEB9D37F30F406e2642E211C19Ed6F7A5FC6d8Ec4` to your file `QmNnUze4f1QfnSQJFFco2hdPWZb2iXUjcB2onAzxLQQj5f` is available to be purchased for `1 PHT` at your online digital shop: `0xffeF98e9de5524Eaf82A8DE88B031160f694a90A`.

## Buying digital content

All the steps below will be executed on a separate Node with ID 102.

If a malicious buyer would try to by-pass the purchasing process and download the file directly, he would run into an error:

```bash
leth storage fetch --nodeid=102 --network=sirius --account=0xf3eedaed3440614b6d9ac1ef0d910494c6bc73a8 --meta=QmNnUze4f1QfnSQJFFco2hdPWZb2iXUjcB2onAzxLQQj5f
```

Error output:
```json
{"error":{"message":"unable to fetch the file from IPFS storage. Error: ipfs cat cmd timed out","code":"ERROR_UNKNOWN"}}
```

*Note: The timeout means there is no public copy of this file. Either the file doesn't exist or all copies are protected by ACL.*

Buying the ACL Read Permission:

```bash
leth shop buy --nodeid=102 --network=sirius --shop=0xffeF98e9de5524Eaf82A8DE88B031160f694a90A --acl=0xEB9D37F30F406e2642E211C19Ed6F7A5FC6d8Ec4 --from=0xf3eedaed3440614b6d9ac1ef0d910494c6bc73a8
```

You will be prompted to authorize the purchase:
```bash
Enter password to decrypt the account PK and store it in memory:
<type your keystore password>
```

Output:
```json
{"success":"true"}
```

The buyer can now access the purchased file:
```bash
leth storage fetch --nodeid=102 --network=sirius --account=0xf3eedaed3440614b6d9ac1ef0d910494c6bc73a8 --meta=QmNnUze4f1QfnSQJFFco2hdPWZb2iXUjcB2onAzxLQQj5f
```

Output:
```json
{"output":"/var/folders/f9/11wh9x9j31d75nxgwv2qsj3r0000gn/T/it-crowd.jpg"}
```

Let's open it:
```bash
open /var/folders/f9/11wh9x9j31d75nxgwv2qsj3r0000gn/T/it-crowd.jpg
```

![Purchased File](/img/shop_bought_file.jpg)

## Shop sale earnings

https://explorer.sirius.lightstreams.io/addr/0xffef98e9de5524eaf82a8de88b031160f694a90a

Shop balance increased to 1 PHT:
![Shop balance after purchase](/img/1-shop-balance.png)

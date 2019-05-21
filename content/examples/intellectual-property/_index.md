+++
title = "Example DApp Document Authorizer Demo"
toc = true
weight = 2
+++

## What is the Intellectual Property demo dapp?

Lightstreams document authorizer demo intends to show case a real world document authorizer application where content creators could offer their intellectual property for selling in a decentralized manner using Lightstreams Smart Vault to guarantee the security and traceability of their published content.

## Nodes

Lightstreams provides two separate and independent nodes of this document authorizer demo to represent the real decentralization
of this DApp.

- [Demo Node 1](https://demo.node1.lightstreams.io)
- [Demo Node 2](https://demo.node2.lightstreams.io)

## Application

On every new session an user is automatically created and credited with 2 PHT. Below you can find a short
explanation of the functionalities you can find in this demo.

#### Lightstreams WhitePaper

On the Demo home page default there is pre-uploaded content to purchase,
 in this case it is the Lightstreams WhitePaper for the reasonable price of 0.2 PHT.

#### Upload Content

From home page click, or from the application service, on **Publish** or from the application menu.

After you agree on the term&conditions it will start deploying a new Smart Contract which will hold the
Access Control List(ACL) of the file you are about to upload. It is required to have at least 1 PHT to perform
this action.

Once the deployment of the smart contract is completed, you fill up the form include a title and description for the
new file, a cover image and the file itself. Click on _Publish_. After uploading and deployment is finished
it will display a content profile card with the public and private information of the published content.

#### Library

On the _Library_ every purchased and published content is being listed.

#### Share your Content

To purchase the content published by other users we need to _Search_ for it using the Public Content ID
provided after uploading was completed. Pasting that ID and click on _Search_ the public data regarding the published
content is displayed along with a _Purchase_ button to proceed with the purchasing of the content.

#### Purchase Content

 To purchase this content you need to click on the public link, this link loads
 the public metadata information about the content such as Title, Description, Cover image, Owner and  price.
 After you click in `Purchase` it performs a purchase tx in the blockchain which send
 to the content owner to total amount set at the price.

 Once the tx is completed the private content is loaded and downloadable. Also you can see the
 receipt of it and clicking on it you can see from Lightstreams Explorer the actual details of the transaction.



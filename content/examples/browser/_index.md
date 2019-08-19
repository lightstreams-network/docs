+++
title = "Example Browser Demo"
toc = true
weight = 1
+++

## Source code

[Example Pure Browser Application using Lightstreams](https://github.com/lightstreams-network/example-browser)

## Live Demo

[https://demo-browser.lightstreams.io/](https://demo-browser.lightstreams.io/)

## Introduction

This example decentralized application (DApp) demonstrates how two or more peers can connect together and securely share private content together without the need for a central server. You can point the application to your local Lightstreams Node (localhost:9000). By default it connects to our public gateway on the sirius testnet, [https://gateway.sirius.lightstreams.io](https://gateway.sirius.lightstreams.io).

## Browser Appplication

The example is only made of static js/css/html and uses react, redux, and styled-components under the hood. The files that you upload are stored on the Lightstreams Node and the files' metadata  are stored on browser's localStorage. If you delete your localStorage, you will no longer see what files have been uploaded to your node.

## js-ipfs

In order to discover other peers with whom to share content, the example application uses the the js-ipfs implementation of IPFS for peer-discovery. This is a bit overkill for now, but could allow for information or file-exchange before the actual sharing of private content.

## Getting started

0. Follow the steps in the [README](https://github.com/lightstreams-network/example-browser/blob/master/README.md) to install & run the application (the application should be running on http://localhost:8080 (we'll call this running app, node1)
1. Create an account with a password. This will generate a public key that you should write down somewhere, it can be used to login (with your password) and unlock your wallet on the Lightstreams Node.
2. Request Lightstreams free test tokens to the newly created address (https://discuss.lightstreams.network/t/request-test-tokens/64)
2. Upload some content
3. Copy the File Meta Hash (under the "Files" sections)
4. Paste the File Meta Hash in the "Download File" section
5. Click on the Link to download the file


## Grant access to/share content with another peer

Once you've uploaded some content, you'll probably want to grant access to someone else and share it with them.

1. In a new browser (if you use Chrome, launch Firefox or Safari), we'll launch another app (which we'll call node2). Open the same URL: http://localhost:8080
2. Create an account with password
3. In node1, go to your uploaded files and copy paste the account address from node2 into the input next to the "Grant to" button
4. In node2, copy the File Meta Hash into the "Download File" section
5. Click on the link to download the file.
6. Tada! You are allowed to download the file.
7. Try again, upload a file on node1, but this time skip Step3 (don't grant access to node2). You should not be able to download the file!

## Conclusion

This Lightstreams browser application shows how two or more peers can securely share private content between one another without the need for a central server and using blockchain smart contracts to grant access/permissions to the files.








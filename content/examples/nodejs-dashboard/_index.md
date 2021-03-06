+++
title = "Example NodeJS Smart Vault Dashboard"
toc = true
weight = 1
+++

## Source code

[Code](https://github.com/lightstreams-network/example-nodejs)

## Live Demo

Node1 -> [https://demo.nodejs.lightstreams.io](https://demo.nodejs.lightstreams.io)
Node2 -> [https://demo.nodejs-2.lightstreams.io](https://demo.nodejs-2.lightstreams.io)

## Introduction

Lightstreams Smart Vault Dashboard app showcase an example of a decentralize app (Dapp)
using [Lightstreams Smart Vault SDK](https://docs.lightstreams.network/getting-started/quick-start/)
in a NodeJS.

Using this DApp you will be able to upload your files uploaded into a Lightstreams Smart Vault
node and manage the its distribution and acceptability. In addition you will be able
to also request access to other users files and manage the pending request to your own content made by
other users.

## Features

### Create an account

![Signup](/img/nodejs/signup.png?raw=true)

### Login

![Login](/img/nodejs/login.png?raw=true)

### Your user wallet

![Signup](/img/nodejs/wallet.png?raw=true)

### Upload file

![Upload file](/img/nodejs/upload_file.png?raw=true)

### My files

You can see the list of files you uploaded and which users have access to them. By clicking
on one of the little icon you can revoke the access to the users at anytime.

![My Files](/img/nodejs/my_files.png?raw=true)

Also you can download the content of the files you uploaded.

### Grant access to file

Grant access to other users to your content without waiting for a access request.

![Grant access to file](/img/nodejs/grant_access.png?raw=true)


### Request access to other user file

Insert the username of other user and load the list of available items of this user.
By clicking on the locker icon you will send a access request to the file owner. In case
you already got access to the file it will display the download action.

![Pending request](/img/nodejs/pending_requests.png?raw=true)

### Manage pending access requests

On this section it will listed the pending access requests from other users to your files.

![Request file access](/img/nodejs/request_file_access.png?raw=true)


## Freemium Model

This project implements a simple freemium model to fund users activity within the
platform. The source for this funding come from two different sources.

The first of them is what it was called stake holder account. This account
 is linked to every instance of the server application and it is funding the creation
 of new users through its own endpoints.

 The second funding source is an Faucet smart contract [0xdf81615E44b34C7015bF148De30526A4863c0DcD](https://explorer.sirius.lightstreams.io/addr/0xdf81615e44b34c7015bf148de30526a4863c0dcd) which will fund
 the activity of users up to 10 PHTs. This smart contract can be top up by every entity
 interested in the growth of the project.

Once users exceeds the initial 10 PHTs they can request more tokens for their accounts contacting Lightstreams Dev Team
either [Telegram](https://t.me/LightstreamsDevelopers) or on the [Discuss forum](https://discuss.lightstreams.network/c/dev)







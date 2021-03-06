# Nanikore User Manual

![](https://raw.githubusercontent.com/allen880117/nanikore/main/metadata/art/nanikore.png)

## Introduction

Nanikore is a stock certificate system. This is the manual for version 0.0.1.

The main usage for Nanikore is to provides stock issuing, transacting and redemption. Features include multi-signature, SCN tracking and opensea integration.

The internal barebones of Nanikore is ERC 1155 smart contract with additional features implemented on top of it. Board of directors can rely on this to issue new stocks and allocate the total volume. Clients buy stocks through the ERC 1155 smart contract which guarantees transactions to be executed in an automatic and decentralized fashion. The system has been successfully deployed with polygon and rinkeby test network.

This system can be tested using [Remix IDE](https://remix.ethereum.org/).

## How to buy stocks (for customer)

Call *`safeTransferFrom`* with following arguments
* *`from`*: the address of seller
* *`to`*: the address of buyer
* *`id`*: should fill in `0`
* *`amount`*: the number of stock units to be transfered
* *`data`*: arbitrary binary data you would like to include in this transfer

![](https://i.imgur.com/C0hL5K4.png)


## How to issue stocks (for board of directors)

### Deploy

To deploy the smart contract, following parameters are required:
* *`_OWNERS`*: a list of owners' address
* *`_NUMCONFIRMATIONSREQUIRED`*: the minimum confirmation required for each issued request to be executed
* *`_ORIGINALSHARE`*: initial number of issued stock units

![](https://i.imgur.com/onBdyVq.png)


### Issue stocks

Customers should submit requests through *`submitIssueRequest`* with following arguments
* *`to`*: the address of the customer
* *`_value`*: the number of stock units the customer requests

![](https://i.imgur.com/PUGCejB.png)


Board of directors should confirm the request with `confirmIssueRequest`
* *`_txIndex`*: the index of transaction

![](https://i.imgur.com/MYDZAW4.png)

Once the minimum number of confirmation is fulfilled, the contract will be executed automatically, transferring the stocks to the customer.

### Adjust the volume of issued stocks

Board of directors can increase the volume of issued stocks with *`mintStock`*
* *`amount`*: the amount to increase.

They can also decrease the volume of specific address by *`burnStock`*
* *`addr`*: from which the stocks will be removed
* *`amount`*: the amount to decrease

## Opensea Screenshot

![](https://i.imgur.com/Y0UiiJ8.png)

https://testnets.opensea.io/assets/0xc3eb5e0fe72388b41b756dfa25120a077bd4f9e2/0

# Relayer

0x Relayer for v2 Scrypts implementation.

At its core the Scrypts platform is an order book of quests. Quests are objects that include a prize in escrow plus a list of completion requirements. 

There are two versions of the Scrypts implementation. V1 is a proof-of-concept design that was built before considering 0x. V2 is an improved design that uses the 0x exchange protocol as the underlying exchange mechanism. 

## V1 Technical Specification 

The V1 questing platform consists of a smart contract on Ethereum, plus a web client that allows users to interact with our contract. 

#### Questing Contract
The smart contract has multiple responsibilities and acts as the mechanism of exchange as well as the main data store.

Key Functions
-Quest creation
-Escrow functions (holding creator’s prize in escrow)
-Quest Cancelation (owner only)
-Swapping functions (swapping prize and requirements upon completion)
-Balance Checking (check if users are true owners of submitted prizes and requirements)

#### Web Client
The web client provides a portal and experience around the Scrypts contract. The client is built primarily using React, the OpenSea API, and Web3.js. 

Key Functions
-Display quests for users 
-Display live balances
-Allow users to complete quest 
-Allow users to create quests
-Allow quest creators to cancel quests

## V2 Technical Specification 

In the new (and more robust version), the Scrypts backend will be a 0x relayer instead of our own smart contract. 

#### Quest Structure
Quests will now exist as ‘maker’ orders on 0x. In most cases (except for 1-to-1 asset swaps) quests will utilize the new MultiAssetProxy support. Quest creators will submit a prize as one component of the order, and users can complete quests by submitting the appropriate bundle of assets. Prizes can be any combination of ERC20s, ERC721s, and even ERC1155s (when that support is fully integrated). Bundles can be swapped for bundles if users find a need for that as well. 

#### Web Client
The web client will remain mostly the same on a UI level, except it will use the 0x APIs and relayer tools to create, fill, and monitor transactions. (As opposed to sending transactions to our own contract on Ethereum). We will still use the OpenSea API for metadata and perhaps also for efficient balance checking. 

# Newcoin SDK documentation
Newcoin foundation

## 


## Motivation for Newcoin

Newcoin SDK enables the work with Newcoin blockchain as a unified resource, abstracting multiple services under one umbrella. 

Above that, it adds the following: 
* Based on the open source consensus SW
* Ready to use contracts to facilitate economic activity
* Top-down rather than market based resource distribution process (RAM, CPU, NET) aligned with interests of the entire ecosystem
* Community control over deployment of new contracts.

It is believed that within this model, the ecosystem will bring higher value to the participants as opposed 
to current models of economic competitions.

### Core features
Newcoin SDK abstracts the following:
* Blockchain operations: such as account creation, permissions management, token transfers, account queries etc.
* Newcoin shared contracts provided to community ("Services")
* External query services: blockchain indexing (hyperion), assets indexing (atomic assets).

### Structure 

At the top level the methods follow CQRS pattern (Command and Query Responsibility Segregation) whereby 
they are divided into State Altering methods creating transactionsn

* State Altering (command) methods return only the transaction ID in case a transaction has been successfully
broadcast. In some cases they return also details of an operatoin such as ID of a new allocated object.
* Query methods return information about the state of the blockchain.

### Shared contracts  

While anyone with an account and a key can deploy a contract to the blockchain, only contracts whitelisted with 
block producers can be executed. The list of currently ready contracts: 
* **eosio** and **eosio.token** contracts managing accounts and system currency 
* **Atomicassets** factory contract for collection creation and NFT minting
* **Main pool** (pool.nco): staking NCO for all participants of the ecosystem. Staked NCO turns into GNCO which is the internal currency of exchange.
* **Creator pools** (pools.nco) allow staking the internal GNCO currency into pools of specific creators and/or DAOs
* **DAO organization** (daos.nco) facilitates on-chain voting and collective economic decision making (buying NFTs, issuing currency, staking into other daos)
* **Farms** allowing staking of creators' currency

New services need to follow the internal review and decision making by voting. 
(NCIP - NewCoin Improvement Process). When voted in, the block produceds will be expected to whitelist the contract. 

<details>
<summary>Libraries</summary>
The pools and DAO contracts have their own libraries:
 
 * pool.nco  - https://github.com/@newcoin-foundation/newcoin.pool-js,  npm i @newcoin-foundation/newcoin.pool-js
 * pools.nco - https://github.com/@newcoin-foundation/newcoin.pools-js, npm i @newcoin-foundation/newcoin.pools-js
 * daos.nco  - https://github.com/@newcoin-foundation/newcoin.daos-js,  npm i @newcoin-foundation/newcoin.daos-js
 * farms.nco TBD
 * atomicassets
 
</details>

### Environments 

  There are three versions of the blockchain: dev, test, and main. 
  * Devnet has multiple unstable copies of contracts and is geared for development and testing of Newcoin infrastructure.
  * Testnet has stable versions of contracts which can be periodically replaced by more advanced versions, tokens have no value.
  * Mainnet 
  
  * the urls of node for transaction, hyperion and atomic assets servers.
  * the names of the specific contract instances
 
#### Lists of currently functional URLs 
<details>
https://nodeos-test.newcoin.org/ 
https://nodeos-dev.newcoin.org/

https://explorer-test.newcoin.org/
https://explorer-dev.newcoin.org/

 Others
https://atomic-test.newcoin.org/atomicassets/v1/config
https://atomic-dev.newcoin.org/atomicassets/v1/config
https://gov-test.newcoin.org/ - nw
https://gov-dev.newcoin.org/ - nw
https://hyperion-test.newcoin.org/v2/health
https://hyperion-dev.newcoin.org/v2/health
https://lightapi-test.newcoin.org/health
https://lightapi-dev.newcoin.org/health

</details> 
   
#### Contract account names
<details>
  Devnet
  Testnet
  Mainnet
</details>

## Working with Newcoin

### Pre-requisites

* A newcoin account with private key - not an application managed account 
* NCO currency 

As Newcoin blockchain is restricted from publishing illegal content, most of the accounts on it are managed, meaning 
that the private key is hidden from the user. Accounts with known private

### Initialization

Installing:
npm i @newcoin-foundation/newcoin-sdk

Newcoin constructor accepts Blockchain URLs and contract names working in this blockchain.
Ready URL and contract names as constants are provided in src/types.ts

## Services descriptions
  
### EOSIO native services
  * Accounts creation with default collection and template for NFT minting
  * Permissions management
  * Account queries

### Main (newcoin) pool 
  * GNCO tracking
  * Receive staking benefits from main DAO distributions
  * Introduce special proposals: whitelist contract, issue tokens to applicant
  
### Staking pools for creators
  * Investment pool, staking GNCO 
  * Creator Coins being dispensed into the staking account
  * Issue creator tokens
  * One pool per creator 
  
### DAOs
  * Economic entity
  * Comprises a pool and DAO voting structure (allocate discord channel automatically?)
  * Proposals divided into types: NFT purchase/sell, inflate/deflate token, offchain voting, member whitelisting  

### Data types

Data types are in @newcoin-foundation/newcoin-sdk/src/types.ts, roughly one data type per call. However, similar methods may share input data type. 

* Commonly, the input types of state altering operations contain who is performing the change ("actor", "author", "owner" etc) and her private key. 
The rest are method-specific paramaters.
* Common return type NCReturnType returns transaction IDs in named optional fields.

## New functionality (contracts) whitelisting
  * NCIP process
  * Introduction of new application originating accounts
  

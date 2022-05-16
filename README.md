# Newcoin SDK documentation
### by Newcoin foundation

## Model

Newcoin SDK enables the work with Newcoin blockchain as a unified resource, abstracting multiple services under one umbrella. 
<p>
Newcoin is based on the EOSIO open source software. developers.eos.io
  
  Above that, it adds the following: 
* Ready commonly used contracts to facilitate economic activity
* Pre-meditated resource distribution process (RAM, CPU, NET) aligned with interests of the entire ecosystem
* Community control over deployment of new contracts.

It is believed that within this model, the ecosystem will bring higher value to the participants as opposed 
to current models of economic competitions.

### Features and goals

Newcoin SDK abstracts the following:
* EOS operations: such as account creation, permissions management, token transfers, account queries etc.
* Newcoin shared contracts provided to community ("Services")
* External query services: blockchain indexing (hyperion), marketplaces indexing (atomic assets).

### Structure
AT the top level the methods follow CQRS pattern (Command and Query Responsibility Segregation) whereby 
they are divided into State Altering methods creating transactionsn

* State Altering (command) methods return only the transaction ID in case a transaction has been successfully
broadcast. In some cases they return also details of an operatoin such as ID of a new allocated object.
* Query methods return information about the state of the blockchain.

### Data types 

Data types are in @newcoin-foundation/newcoin-sdk/src/types.ts, roughly one data type per call. However, similar methods may share input data type. 
  
* Commonly, the input types of state altering operations contain who is performing the change ("actor", "author", "owner" etc) and her private key. 
The rest are method-specific paramaters.
* Common return type NCReturnType returns transaction IDs in named optional fields.

### Services (shared contracts) 

Built in services: 
* **eosio** and **eosio.token** contracts managing accounts and system currency 
* **Atomicassets** factory contract for collection creation and NFT minting
* **Main pool** (pool.nco): staking NCO for all participants of the ecosystem. Staked NCO turns into GNCO which is the internal currency of exchange.
* **Creator pools** (pools.nco) allow staking the internal GNCO currency into pools of specific creators and/or DAOs
* **DAO organization** (daos.nco) facilitates on-chain voting and collective economic decision making (buying NFTs, issuing currency, staking into other daos)
* **Farms** allowing staking of creators' currency

New services need to follow the internal review and discussion process 
(NCIP - NewCoin Improvement Process). When voted in, the block produceds will be expected to whitelist the contract. 

<details><summary>#### Libraries</summary>
<p>
The pools and DAO contracts have their own libraries:
  * pool.nco  - https://github.com/@newcoin-foundation/newcoin.pool-js, npm i @newcoin-foundation/newcoin.pool-js
  * pools.nco - https://github.com/@newcoin-foundation/newcoin.pool-js, npm i @newcoin-foundation/newcoin.pool-js
  * daos.nco  - https://github.com/@newcoin-foundation/newcoin.daos-js, npm i @newcoin-foundation/newcoin.daos-js
  * farms.nco TBD
  * atomicassets
</p>
</details>

### Testnets and the Mainnet

  There are three versions of the blockchain: dev, test, and main. As of writing this documentation most of the work is done in devnet.
  Each of the chains are defined by
  * the urls of node for transaction, hyperion and atomic assets servers.
  * the names of the specific contract instances
  
  #### Lists of URLs 
  <details>Devnet: 
  * 
  Testnet:
  * 
  Mainnet
  * 
  </details> 
   
  #### Contract account names
  <details>
  Devnet
  Testnet
  Mainnet
  </details>
    
## Working with Newcoin

### Pre-requisites

* An account with private key in order to send state altering transactions into blockchain
* Currency on that account

### Initialization

Newcoin constructor accepts Blockchain URLs and contract names working in this blockchain. 
Ready URL and contract names as constants are provided in src/types.ts
  
### Devnet / Testnet / Mainnet environments
  
  
  
 ## Service descriptions
  
 ### EOSIO blockchain services
  * Accounts management 
  * Permissions management
  * transaction queries
  
  ### Main pool (GNCO token)
  * GNCO tracking
  * Receive staking benefits from main DAO distributions
  
  ### Creator pools
  * Issue creator tokens
  * One pool per creator 
  
  ### DAOs
  * Economic entity 
  * Comprises a pool and DAO voting structure (allocate discord channel automatically?)

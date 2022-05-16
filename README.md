# Newcoin Blockchain Software Development Kit
### Newcoin foundation

## Model

Newcoin-sdk is an umbrella abstracting package simplifying the work with Newcoin blockchain.

Main features include:

* Abstraction of EOS operations such as account creation, token transfers, permissions etc.
* Abstraction of ready to use contracts ("Blockchain Services")
* Abstraction of external query services such as indexing (hyperion) and marketplaces (atomic assets).

Important principles: 
The methods are divided into State Altering and Query methods. State Altering methods usually 
return only the transaction ID in case a transaction has been successfully broadcast. 
In some cases they return also details of an operatoin such as ID of a new allocated object.

Data types 

Data types are in src/types.ts, roughly one data type per call however similar methods may share input data type.
Input types of state altering operations must contain the actor ( could also be called "owner", "author", "proposer" -
the account requesting the action, and its private key. 
The rest of parameters are method-specific.

Common return type NCReturnType returns transaction IDs in fields. 


Services 

Built in: 
* system token contract eosio.token manages 
* Main pool staking system currency NCO for rewards, using internally GNCO currency to stake.
* Creator pools for staking
* DAO organization including on-chain voting and collective economic decision making (staking into others, buying NFTs, issuing currency)
* Local NFT Marketplace


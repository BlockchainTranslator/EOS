- [1. Wallets](#1-wallets)
- [2. Accounts](#2-accounts)
- [3. Authorities and Permissions](#3-authorities-and-permissions)
- [4. Putting it all Together](#4-putting-it-all-together)
  * [4.1 Default Account Configuration (Single-Sig)](#41-default-account-configuration-single-sig)
  * [4.2 Multi-sig Account & Custom Permissions](#42-multi-sig-account--custom-permissions)

An **account** is human readable identifier that is stored on the blockchain. Every transaction has it's permissions evaluated under the configured authority of an account. Each named permission has a threshold that must be met for a transactions signed under that authority to be considered valid. Transactions are signed by utilizing a **client** that has a loaded and unlocked wallet. A wallet is software that protects and makes use of your keys. These keys may or maybe not be permissioned to an account authority on the blockchain.

## 1. Wallets

Wallets are clients that store keys that may or may not be associated to the permissions of one or more accounts. Ideally a wallet has a locked (encrypted) and unlocked (decrypted) state that is protected by a highly entropied password. The EOSIO/eos repository comes bundled with a command line interface client called `eosc` that includes a wallet as part of its functionality. 

## 2. Accounts

An account is a human readable name that is stored on the blockchain. It can be owned by an individual or group of individuals depending on permissions configuration. An account is required to transfer or otherwise push a transaction to the blockchain. 

## 3. Authorities and Permissions

Authorities determine whether or not any given message is properly authorized. 

Every account has two _native_ named permissions

- `owner` authority symbolizes ownership of an account. There are only a few transactions that require this authority, but most notably, are messages that make any kind of change to the owner authority. Generally, it is suggested that owner is kept in cold storage and not shared with anyone. `owner` can be used to recover another permission that may have been compromised.
- `active` authority is used for transferring funds, voting for producers and making other high level account changes. 

In addition to the _native_ permissions, an account can possess custom named permissions that are available to further extend account management. Custom permissions are incredibly flexible and address numerous possible use cases when implemented. Much of this is up to the developer community in how they are employed, and what conventions if any, are adopted.

Permission for any given authority can be assigned to one or multiple `public keys` or a valid `account name`. 

## 4. Putting it all Together

Below is the combination of all the above concepts and some loose examples of how they might be practically employed. 

### 4.1 Default Account Configuration (Single-Sig)

This is how an account is configured after it has been created, it has a single key for both the **owner** and **active** permissions, both keys with a weight of **1** and permissions both with a threshold of **1**. The default configuration requires a single signature to authorize a message for the native permissions.

#### __*@bob account authorities*__

| Permission | Account                                               | Weight | Threshold |
|------------|-------------------------------------------------------|--------|-----------|
| owner      |                                                       |        | 1         |
|            | EOS5EzTZZQQxdrDaJAPD9pDzGJZ5bj34HaAb8yuvjFHGWzqV25Dch | 1      |           |
| active     |                                                       |        | 1         |
|            | EOS61chK8GbH4ukWcbom8HgK95AeUfP8MBPn7XRq8FeMBYYTgwmcX | 1      |           |

In the `@bob` account example, this table shows that @bob's owner key has a permissioned weight of 1, and the required threshold to push a transaction under that authority is 1. 

To push a transaction under the owner authority, only **@bob** needs to sign the transaction with his owner key for the transaction to be eligible for validation. This key would be stored in a _wallet_, and then processed using `eosc`.

### 4.2 Multi-sig Account & Custom Permissions

The below example are authorities for a fictional account named `@multisig`. In this scenario, two users are authoritized to both the `owner` and `active` permissions of a fictional `@multisig` account, with three users permissioned to a custom `publish` permission with varying weight. 

#### __*@multisig account authorities*__

| Permission | Account                                               | Weight | Threshold |
|------------|-------------------------------------------------------|--------|-----------|
| owner      |                                                       |        | 2         |
|            | @bob                                                  | 1      |           |
|            | @stacy 	                                              | 1      |           |
| active     |                                                       |        | 1         |
|            | @bob                                                  | 1      |           |
|            | @stacy 	                                              | 1      |           |
| publish    |                                                       |        | 2         |
|            | @bob                                                  | 2      |           |
|            | @stacy 	                                              | 2      |           |
|            | EOS7Hnv4iBWo1pcEpP8JyFYCJLRUzYcXSqtQBcEnysYDFTEbUpi6y | 1      |           |

In this scenario, a weight threshold of 2 is required to make changes to the `owner` permission level, which means that because all parties have a weight of **1**, all users are required to sign the transaction for it to be fully authorized. 

To send a transaction which requires the *active* authority, the threshold is set to **1**. This implies that only 1 signature is required authorize a message from the *active* authority of the account. 

There's also a third *custom named permission* called *publish*. For the sake of this example, the *publish* permission is used to publish posts to the @multisig's blog using a theoretical blog dApp. The *publish* permission has a threshold of **2**, *@bob@** and **@stacy** both have a weight of *2*, and a **public key** has a weight of **1**. This implies that both **@bob** and **@stacy** can publish without an additional signature, whereas the **public key** requires an additional signature in order for a message under the public permission to be authorized. 

Thus the above permissions table implies that **@bob** and **@stacy**, as owners of the account, have _elevated priviledges_ similar to a moderator or editor. While this primitive example has limitations particularly with scalability and is not necessarily a good design, it does adequately demonstrate the flexible nature of the EOS permissions system.

Also notice in the above table, we've permissions using both an **account name** and a **key**. At first glance this may seem trivial, however it does suggest some added dimensions of flexibility. 

**Observations**

- @bob and @stacy can be explicitly identified as the owners of this account
- A third party can remained relatively anonymous in the context of the example **@multisig** account, assuming this key is not permissioned to any another account on the blockchain.
- @bob and @stacy have elevated priviledges for the the **publish** permissions. 


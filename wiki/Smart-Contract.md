# EOS Smart Contract

 * [1 Introduction to EOS Smart Contract](#1-introduction-to-eos-smart-contract)
    + [1.1 Required Background Knowledge](#11-required-background-knowledge)
    + [1.2 Basics of EOS Smart Contract](#12-basics-of-eos-smart-contract)
    + [1.3 Technical Limitation](#13-technical-limitation)
 * [2 Smart Contract Files](#2-smart-contract-files)
     + [2.1 HPP](#21-hpp)
     + [2.2 CPP](#22-cpp)
     + [2.3 WAST](#23-wast)
     + [2.4 ABI](#24-abi)
 * [3 Checklist](#3-checklist)
 * [4 Interacting with Smart Contract Examples](#4-interacting-with-smart-contract-examples)
    + [4.1 The Currency Contract](#41-the-currency-contract)
    + [4.2 Tie-Tac-Toe](#42-tic-tac-toe)
 * [5 Writing your first EOS Smart Contract](#5-writing-your-first-eos-smart-contract)
 * [6 Deploy and update Smart Contract](#6-deploy-and-update-smart-contract)
 * [7 Command Summary](#7-command-summary)
 * [8 Debugging Smart Contract](#8-debugging-smart-contract)
     + [8.1 Method](#81-method)
     + [8.2 Print](#82-print)
     + [8.3 Example](#83-example)
 

## 1. Introduction to EOS Smart Contract

### 1.1. Required Background Knowledge

**C / C++ Experience**

EOS.IO based blockchains execute user generated applications and code using [Web Assembly](http://webassembly.org/) (WASM). WASM is an emerging web standard with widespread support of Google, Microsoft, Apple, and others. At the moment the most mature toolchain for building applications that compile to WASM is clang/llvm with their C/C++ compiler.

Other toolchains in development by 3rd parties include: Rust, Python, and Solidiity. While these other languages may appear simpler, their performance will likely impact the scale of application you can build. We expect that C++ will be the best language for developing high-performance and secure smart contacts.

**Linux / Mac OS Experience**

The EOS.IO software only officially supports the following environment
- Ubuntu 16.10 or above, or 
- MacOS Sierra or above

**Command Line Knowledge**

There are a varity of tools provided along with EOS.IO which requires you to have basic command line knowledge in order to interact with.


### 1.2. Basics of EOS Smart Contract

**Communication Model**

EOS Smart Contract communicate with each other in form of messages and shared memory database access, e.g. a contract can read the state of another contract's database as long as it is included within the read scope of the transaction with an async vibe. The async communication may result in spam which the resource limiting algorithm will resolve.
There are two communication modes that can be defined within a contract:

- **Inline**. Inline is guaranteed to execute with the current transaction or unwind; no notification will be communicated regardless of success or failure. Inline operates with the same scopes and authorities with the same scopes and authorities the original transaction had.

- **Deferred**. Defer will get scheduled later at producer's discretion; it's possible to communicate the result of the communication or can simply timeout. Deferred can reach out to different scopes and carry the authority of contract that sends them.
*This feature is not available in STAT

**Message vs Transaction**

A message represents a single operation, whereas a transaction is a collection of one or more messages. A contract and an account communicate in the form of messages. Messages can be sent individually, or in combined form if they are intended to be executed as a whole. 

*Transaction with 1 message*.

```base
{
  "ref_block_num": "100",
  "ref_block_prefix": "137469861",
  "expiration": "2017-09-25T06:28:49",
  "scope": ["initb","initc"],
  "messages": [
    {
      "code": "eos",
      "type": "transfer",
      "authorization": [
        {
          "account": "initb",
          "permission": "active"
        }
      ],
      "data": "000000000041934b000000008041934be803000000000000"
    }
  ],
  "signatures": [],
  "authorizations": []
}
```

*Transaction with multiple messages*, these message should either all be successed or all failed.
```base
{
  "ref_block_num": "100",
  "ref_block_prefix": "137469861",
  "expiration": "2017-09-25T06:28:49",
  "scope": [...],
  "messages": [{
      "code": "...",
      "type": "...",
      "authorization": [...],
      "data": "..."
    }, {
      "code": "...",
      "type": "...",
      "authorization": [...],
      "data": "..."
    }, ...
  ],
  "signatures": [],
  "authorizations": []
}
```

**Message Name Restrictions**

Message types are actually **base32 encoded 64 bit integers**. This means they are limited to the characters a-z, 1-5, and '.' for the first 12 charcters. If there is a 13th character then it is restricted to the first 16 characters ('.' and a-p).

**Transaction Confirmation**

Receiving a transaction hash does not mean that the transaction has been confirmed, it only means that the node accepted it without error, which also means that there is a high probability of other producers will accept it.

By means of confirmation, you should see the transaction in transaction history with the block number of which it is included.


### 1.3. Technical Limitation

- **No floating point.** Contracts will not accept floating point operation since it is a non-deterministic behavior at CPU level which could lead to unintended forks.
- **Transaction to be executed within 1 ms**. Execution time of a transaciton needs to be **less than or equal to 1 ms** or the transction will fail.
- **Maximum 30 tps**. The public testnet at the moment is setup in the way that each account is limited to publish maximum 30 transactions per second. 


## 2 Smart Contract Files 

To keep things simple we have created a tool called **[eoscpp](https://github.com/EOSIO/eos/wiki/Programs-&-Tools#eoscpp)**  which can be used to bootstrap a new contract. The eoscpp too will create the 3 smart contract files with the basic skeleton for you to get started.

```base
$ eoscpp -n ${contract}
```

The above will create a new empty project in the './${project}' folder with three files:
```base
${contract}.abi ${contract}.hpp ${contract}.cpp
```

### 2.1. HPP

HPP is the header file that contain the variables, constants and functions referenced by the CPP file.

### 2.2. CPP

The CPP file is the source file that contains the functions of the contract. 

If you generate the CPP file using the eoscpp tool, the generated cpp file would looks similar to the following:
```base
#include <${contract}.hpp>

/**
 *  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
 *  call these methods.
 */
extern "C" {

    /**
     *  This method is called once when the contract is published or updated.
     */
    void init()  {
       eosio::print( "Init World!\n" ); // Replace with actual code
    }

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" ); 
    }

} // extern "C"
```

In there you can see there are 2 functions being created, `init` and `apply`. All they do are log the messages delivered and makes no other checks. Anyone can deliver any message at any time provided the block producers allow it. Absent any required signatures, the contract will be billed for the bandwidth consumed.

**init**

The `init` function will only be executed once at initial deployment. It is used for initialize contract variables, e.g. the number of token supply for a currency contract.

**apply**

`apply` is the message handler, it listens to all incoming messages and reacts according to the specifications within the function.
The `apply` function requires two input parameters, `code` and `action`.

**code filter**

In order to response to a particular message, you can structure your `apply` function as the following, you may also construct response to general messages by omitting the code filter.
```base
if (code == N(${contract_name}) {
    //your handler to response to particular message
}
```

Within that you can also define response to respective actions.

**action filter**

To response to particular action, you can structure your `apply` function as the following as the following. This is normally used in conjuction with the code filter.
```base
if (action == N(${action_name}) {
    //your handler to response to particular action
}
```

### 2.3. WAST

Any program that wants to deploy to the EOS.IO blockchain must first compile into WASM format. This is the only format the blockchain accepts.

Once you have the CPP file ready, you can compile it into a text version of WASM (.wast) using the `eoscpp` tool.
```base
$ eoscpp -o ${contract}.wast ${contract}.cpp
```


### 2.4. ABI

The  Application Binary Interface (ABI) is a JSON-based description on how to convert user actions between their JSON and Binary representations. The ABI also describes how to convert the database state to/from JSON. Once you have described your contract via an ABI then developers and users will be able to interact with your contract seemlessly via JSON.

The ABI file can be generated from the HPP files using the `eoscpp` tool:
```base
$ eoscpp -g ${contract}.abi ${contract}.hpp
```

Here is an example of what the skeleton contract ABI looks like:
```base
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
      }
    },{
      "name": "account",
      "base": "",
      "fields": {
        "account": "name",
        "balance": "uint64"
      }
    }
  ],
  "actions": [{
      "action": "transfer",
      "type": "transfer"
    }
  ],
  "tables": [{
      "table": "account",
      "type": "account",
      "index_type": "i64",
      "key_names" : ["account"],
      "key_types" : ["name"]
    }
  ]
}
```
You will notice that this ABI defines an action `transfer` of type `transfer`. This tells EOS.IO that when `${account}->transfer` message is seen that the payload is of type `transfer`. The type `transfer` is defined in the `structs` array in the object with `name` set to `transfer`.

```base
...
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
      }
    },{
...
```
It has several fields, including `from`, `to` and `quantity`. These fields have the coresponding types `account_name`, and `uint64`. `account_name` is a built in type used to represent base32 string as uint64. To see more about what built in types are available check [here](https://github.com/EOSIO/eos/blob/b2af4daa8acb64bbb341fd85f7e8a2cd54fa4de4/libraries/types/abi_serializer.cpp).
```base
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
...
```
Inside the above `types` array we define list of alias for existing type. Here, we define `name` as alias of `account_name`.


## 3. Checklist

Before getting started with an EOS Smart Contract be sure to do all the following:

**Build the latest built**

Make sure you have the latest built in your enviornment, you will need that in order to access `eoscpp` and `eosc`, the tools that are necessary for you to get started. Instructions on getting the latest built can be found in the [Environment](https://github.com/EOSIO/eos/wiki/Local-Environment) section.

Once you have the latest eosio/eos code installed, make sure that ${CMAKE_INSTALL_PREFIX}/bin is in your path, or you will have to install it by running the following command.

```base
cd build 
make install
```

**Connect to the EOS.IO blockchain**

You can connect to a node using the command

```base
$ eosc -H ${node_ip} -p ${port_num}
```

*node_ip* can be a private node's IP of you can connect to the public testnet using public nodes ip [here](Testnet%3A%20Public#nodes).

*port_num* is either 8888 or 8889, depending on the configuration.

**Create a wallet and have access to an account**

In order to deploy a contract to the blockchain you will need an account created on the EOS.IO blockchain. Every contract requires an associated account. 

If you hold EOS Tokens already you should have an account on the public testnet. If you need to create a new account for testing, please follow the instructions below:

- [Create a wallet](Tutorials#11-creating-and-managing-wallets)
- [Create an account](Tutorials#14-creating-an-account)
- [Import your account in the wallet created](Tutorials#12-generating-and-importing-eos-keys)


## 4. Interacting with Smart Contract Examples

Before deep diving into building a smart contract, there are smart contract examples which you can reference so to understand how EOS smart contract functions. 

In order to interact with these sample contracts, you will need to first complete all items on the [checklist](#3-checklist) above and deploy the sample contracts to the EOS.IO blockchain.


### 4.1. The Currency Contract 

**Deploying the sample contract**

The example currency contracts can be found [here](https://github.com/EOSIO/eos/tree/master/contracts/currency), if you have downloaded the EOSIO repository, you should be able to find it in your local drive.

The folder contains the .abi, .cpp and .hpp files, you will need to generate the .wast file before you can deploy the contract.
```base
$ eoscpp -o currency.wast currency.cpp
```

Once you have successfully generated the .wast file, you can use the `set contract` command to deploy.
```base
$ eosc set contract ${contract_account_name} ../contracts/currency.wast ../contracts/currency.abi
Reading WAST...
Assembling WASM...
Publishing contract...
{
  "transaction_id": "1abb46f1b69feb9a88dbff881ea421fd4f39914df769ae09f66bd684436443d5",
  "processed": {
    "ref_block_num": 144,
    "ref_block_prefix": 2192682225,
    "expiration": "2017-09-14T05:39:15",
    "scope": [
      "eos",
      "${account}"
    ],  
    ...
}
```
Ensure that your wallet is unlocked and you have active key for ${contract_account_name} imported

**Understanding the contract**

Now that we have deployed the contract, anybody can use the `eosc`'s `get code` to retrieve the .abi of the contract and understand what interface is available for this contract.
```base
$ eosc get code currency -a currency.abi
code hash: 86968a9091ce32255777e2017fccaede8cea2d4978b30f25b41ee97b9d77bed0
saving abi to currency.abi
$ cat currency.abi
{
  "types": [{
      "newTypeName": "account_name",
      "type": "Name"
    }
  ],
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
      }
    },{
      "name": "account",
      "base": "",
      "fields": {
        "account": "name",
        "balance": "uint64"
      }
    }
  ],
  "actions": [{
      "action": "transfer",
      "type": "transfer"
    }
  ],
  "tables": [{
      "table": "account",
      "indextype": "i64",
      "keynames": [
        "account"
      ],
      "keytype": [],
      "type": "account"
    }
  ]
}
```

**Observations**
- The contract accepts an action called `transfer` that accepts message with fields `from`, `to`, and `quantity`
- There is a table `account`, that stores the data

Now that we have find out there are the transfer action and the account table that we can use to check the balance, we can use `eosc` to interact with them.

**Read account balance**

To query data from a table, simply use the `get table` command with the syntax `eosc get table ${account} ${contract} ${table}`.
```bash
$ eosc get table ${account} currency account
{
  "rows": [{
     "key": "account",
     "balance": 1000000000
     }
  ],
  "more": false
}
```

**Transfer funds**

Anyone can send any message to any contract at any time but the contracts may reject messages which are not given necessary permission. Messages are not sent "from" anyone, they are sent "with permission of" one or more accounts and permission levels. 

The following command would transfer 50 *token* from account_a to account_b within the currency contract.
```base
$ eosc push message currency transfer '{"from":"${account_a}","to":"${account_b}","quantity":50}' --scope ${account_a},${account_b} --permission ${account_a}@active
```

We specify the `--scope` argument to give the currency contract read/write permission to those users so it can modify their balances. In a future release scope will be automatically determined.

As a confirmation of a successfully submitted transaction you will receive json output that includes a `transaction_id` field.
```base
1589302ms thread-0   currency.cpp:271  operator()  ] Converting argument to binary...
1589304ms thread-0   currency.cpp:290  operator()  ] Transaction result:
{
  "transaction_id": "1c4911c0b277566dce4217edbbca0f688f7bdef761ed445ff31b31f286720057",
  "processed": {
    "refBlockNum": 1173,
    "refBlockPrefix": 2184027244,
    "expiration": "2017-08-24T18:28:07",
    "scope": [...],
    "signatures": [],
    "messages": [...]
  }
}
```

Once you received the success result, you can check the state of the account by reading the account balance from the account table as you did previously.


### 4.2. Tic-Tac-Toe

The tic-tac-toe contract is a paper-and-pencil game for two players, X and O, who take turns marking the spaces in a 3×3 grid. The player who succeeds in placing three of their marks in a horizontal, vertical, or diagonal row wins the game.

**Game rules**
  - Each player pair can have up to 2 unique games, one where player_1 becomes host and player_2 become challenger and vice versa
  - The game data is stored inside games table of "host" scope with "challenger" as the key
  
**Example**
 
|Coordinate|0|1|2|
|:-:|:-:|:-:|:-:|
|0|-|o|x|
|1|-|x|-|
|2|x|o|o|

Board is represented with number:
  - 0 represents empty cell
  - 1 represents cell filled by host 
  - 2 represents cell filled by challenger

Therefore, assuming x is host, o is challenger, the above board will have the following representation: [0, 2, 1, 0, 1, 0, 1, 2, 2] inside the game object.

  
**Deploying the sample contract**

The example tic_tac_toe contracts can be found [here](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe), if you have downloaded the EOSIO repository, you should be able to find it in your local drive.

The folder contains the .abi, .cpp and .hpp files, you will need to generate the .wast file before you can deploy the contract. 
```base
$ eoscpp -o tic_tac_toe.wast tic_tac_toe.cpp
```

Once you have successfully generated the .wast file, you can use the `set contract` command to deploy. For this example, we are going to deploy it on account `tic.tac.toe`. Note that the EOS.IO blockchain only support base32 char for the account name that's why, underscore is replaced with '.'. If you are going to deploy it to other account beside `tic.tac.toe`, replace any occurence of `tic.tac.toe` in the .hpp, .cpp, and .abi with your account name.
```base
$ eosc set contract tic.tac.toe tic_tac_toe.wast tic_tac_toe.abi
Reading WAST...
Assembling WASM...
Publishing contract...
{
  "transaction_id": "1abb46f1b69feb9a88dbff881ea421fd4f39914df769ae09f66bd684436443d5",
  "processed": {
    "ref_block_num": 144,
    "ref_block_prefix": 2192682225,
    "expiration": "2017-09-14T05:39:15",
    "scope": [
      "eos",
      "tic.tac.toe"
    ],  
    ...
}
```

**Understanding the contract**

Now that we have deployed the contract, anybody can use the `eosc`'s `get code` to retrieve the .abi of the contract and understand what interface is available for this contract.
```base
$ eosc get code tic.tac.toe. -a tic_tac_toe.abi
code hash: c78d16396a5a63b1be47fd570633084cb5fe2eaa9980ca87ec25061d68299294
saving abi to tic_tac_toe.abi
$ cat tic_tac_toe.abi
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
  "structs": [{
      "name": "game",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name",
        "turn": "account_name",
        "winner": "account_name",
        "board": "uint8[]"
      }
    },{
      "name": "create",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name"
      }
    },{
      "name": "restart",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name",
        "by": "account_name"
      }
    },{
      "name": "close",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name"
      }
    },{
      "name": "movement",
      "base": "",
      "fields": {
        "row": "uint32",
        "column": "uint32"
      }
    },{
      "name": "move",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name",
        "by": "account_name",
        "movement": "movement"
      }
    }
  ],
  "actions": [{
      "action_name": "create",
      "type": "create"
    },{
      "action_name": "restart",
      "type": "restart"
    },{
      "action_name": "close",
      "type": "close"
    },{
      "action_name": "move",
      "type": "move"
    }
  ],
  "tables": [{
        "table_name": "games",
        "type": "game",
        "index_type": "i64",
        "key_names" : ["challenger"],
        "key_types" : ["account_name"]
      }
  ]
}
```

**Observations**
- The contract accepts actions called `create`, `restart`, `close` and `move` where each actions accept message with different fields  
- There is a table called `games`, that stores the data


**How to play the game:**

- Create a game using `create` action, with you as the host and other account as the challenger.

```bash
$ eosc push message tic.tac.toe create '{"challenger":"${challenger_account_name}","host":"${your_account_name}"}' --permission ${your_account}@active
```

- The first move needs to be done by the host, use the `move` action to make a move by specifying which row and column to fill.
```bash
$ eosc push message tic.tac.toe move '{"challenger":"${challenger_account_name}","host":"${your_account_name}","by":"${your_account_name}","''{"row":0,"column":1}"}' --permission ${your_account}@active
```

- Then ask the challenger to make a move, after that it's the host's turn again. Repeat until the winner is determined.
```bash
$ eosc push message tic.tac.toe move '{"challenger":"${challenger_account_name}","host":"${your_account_name}","by":"${your_account_name}","''{"row":1,"column":1}"}' --permission ${challenger_account}@active
```

- To restart the game, use the `restart` action
```bash
$ eosc push message tic.tac.toe restart '{"challenger":"${challenger_account_name}","host":"${your_account_name}","by":"${your_account_name}"}' --permission ${your_account}@active
```
- To clear the game from the database, use the `close` action. This will free up space after the game has concluded.
```bash
$ eosc push message tic.tac.toe close '{"challenger":"${challenger_account_name}","host":"${your_account_name}"}' --permission ${your_account}@active
```



## 5. Writing your first EOS smart contract 

**Hello World**

In this section, we will be building a **hello world** contract step by step. 

Before you begin, you will need to first complete all items on the [checklist](#3-checklist) above.

**Lets begin**
First, we use `eoscpp` to generate the skeleton of the smart contract. This will create a new empty project in the **hello** folder with the abi, hpp and cpp file.

```base
$ eoscpp -n hello
```

The CPP file should contain a sample code which will print the text **Hello World: ${account}->${action}** when it receives a message.

```base
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
    }
```

We should now generate the .wast from this cpp file.
```base
$ eoscpp -o hello.wast hello.cpp
```

Now that you have the .wast and .abi files, you can deply your contract to the blockchain.

Assuming your wallet is unlocked and has keys for `${account}`, you can now upload this contract to the blockchain with the following command:

```base
$ eosc set contract ${account} hello.wast hello.abi
Reading WAST...
Assembling WASM...
Publishing contract...
{
  "transaction_id": "1abb46f1b69feb9a88dbff881ea421fd4f39914df769ae09f66bd684436443d5",
  "processed": {
    "ref_block_num": 144,
    "ref_block_prefix": 2192682225,
    "expiration": "2017-09-14T05:39:15",
    "scope": [
      "eos",
      "${account}"
    ],
    "signatures": [
      "2064610856c773423d239a388d22cd30b7ba98f6a9fbabfa621e42cec5dd03c3b87afdcbd68a3a82df020b78126366227674dfbdd33de7d488f2d010ada914b438"
    ],
    "messages": [{
        "code": "eos",
        "type": "setcode",
        "authorization": [{
            "account": "${account}",
            "permission": "active"
          }
        ],
        "data": "0000000080c758410000f1010061736d0100000001110460017f0060017e0060000060027e7e00021b0203656e76067072696e746e000103656e76067072696e7473000003030202030404017000000503010001071903066d656d6f7279020004696e69740002056170706c7900030a20020600411010010b17004120100120001000413010012001100041c00010010b0b3f050041040b04504000000041100b0d496e697420576f726c64210a000041200b0e48656c6c6f20576f726c643a20000041300b032d3e000041c0000b020a000029046e616d6504067072696e746e0100067072696e7473010004696e697400056170706c790201300131010b4163636f756e744e616d65044e616d6502087472616e7366657200030466726f6d0b4163636f756e744e616d6502746f0b4163636f756e744e616d6506616d6f756e740655496e743634076163636f756e740002076163636f756e74044e616d650762616c616e63650655496e74363401000000b298e982a4087472616e736665720100000080bafac6080369363401076163636f756e7400076163636f756e74"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```

If you are monitoring the output of your eosd process you should see:
```base
...] initt generated block #188249 @ 2017-09-13T22:00:24 with 0 trxs  0 pending
Init World!
Init World!
Init World!
```
You will notice the lines "Init World!" are executed 3 times. This isn't a mistake. When the blockchain is processing transactions the following happens:

1st : eosd receives a new transaction (validating transaction)
- creates a temporary session
- attempts to apply the transaction
- succeeds and prints "Init World!"
- or fails undoes the changes (potentially failing after printing "Init World!")

2nd : eosd starts to produce a block
- undoes all pending state
- pushes all transactions as it builds the block
- prints "Init World!" a second time
- finishes building the block
- undoes all of the temporary changes while creating block

3rd : eosd pushes the generated block as if it is received it from the network
- prints "Init World!" a third time

At this point your contract is ready to start receiving messages. Since the default message handler accepts all messages we can send it anything we want. Let's try sending it an empty message:
```base
$ eosc push message ${account} hello '"abcd"' --scope ${account}
```

This command will send the message "hello" with binary data represented by the hex string "abcd". Note, in a bit we will show how to define the ABI so that you can replace the hex string with a pretty, easy-to-read, JSON object. For now we merely want to demonstrate how the message type "hello" is dispatched to account.

The result is:
```base
{
  "transaction_id": "69d66204ebeeee68c91efef6f8a7f229c22f47bcccd70459e0be833a303956bb",
  "processed": {
    "ref_block_num": 57477,
    "ref_block_prefix": 1051897037,
    "expiration": "2017-09-13T22:17:04",
    "scope": [
      "${account}"
    ],
    "signatures": [],
    "messages": [{
        "code": "${account}",
        "type": "hello",
        "authorization": [],
        "data": "abcd"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```
If you are following along in eosd then you should have seen the following scroll by the screen:
```base
Hello World: ${account}->hello
Hello World: ${account}->hello
Hello World: ${account}->hello
```
Once again your contract was executed and undone twice before being applied the 3rd time as part of a generated block.

If we look into the ABI file, you will notice it defines an action `transfer` of type `transfer`. This tells EOS.IO that when `${account}->transfer` message is seen that the payload is of type `transfer`. The type `transfer` is defined in the `structs` array in the object with `name` set to `"transfer"`.

```base
...
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
      }
    },{
...
```

Now that we have reviewed the ABI defined by the skeleton, we can construct a message call for transfer:
```base
eosc push message ${account} transfer '{"from":"currency","to":"inita","quantity":50}' --scope initc
2570494ms thread-0   main.cpp:797                  operator()           ] Converting argument to binary...
{
  "transaction_id": "b191eb8bff3002757839f204ffc310f1bfe5ba1872a64dda3fc42bfc2c8ed688",
  "processed": {
    "ref_block_num": 253,
    "ref_block_prefix": 3297765944,
    "expiration": "2017-09-14T00:44:28",
    "scope": [
      "initc"
    ],
    "signatures": [],
    "messages": [{
        "code": "initc",
        "type": "transfer",
        "authorization": [],
        "data": {
          "from": "currency",
          "to": "inita",
          "quantity": 50
        },
        "hex_data": "00000079b822651d000000008040934b3200000000000000"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```
If you observe the output of eosd you should see:
```base
Hello World: ${account}->transfer
Hello World: ${account}->transfer
Hello World: ${account}->transfer
```

According to the ABI the transfer message has the format:
```base
  "fields": {
    "from": "account_name",
    "to": "account_name",
	"quantity": "uint64"
  }
```
We also know that account_name -> uint64 which means that the binary representation of the message is the same as:
```base
struct transfer {
    uint64_t from;
    uint64_t to;
    uint64_t quantity;
};
```
The EOS.IO C API provides access to the message payload via the Message API:
```base
uint32_t message_size();
uint32_t read_message( void* msg, uint32_t msglen );
```
Let's modify hello.cpp to print out the content of the message:
```base
#include <hello.hpp>

/**
 *  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
 *  call these methods.
 */
extern "C" {

    /**
     *  This method is called once when the contract is published or updated.
     */
    void init()  {
       eosio::print( "Init World!\n" );
    }

    struct transfer {
       uint64_t from;
       uint64_t to;
       uint64_t quantity;
    };

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          transfer message;
          static_assert( sizeof(message) == 3*sizeof(uint64_t), "unexpected padding" );
          auto read = read_message( &message, sizeof(message) );
          assert( read == sizeof(message), "message too short" );
          eosio::print( "Transfer ", message.quantity, " from ", eosio::name(message.from), " to ", eosio::name(message.to), "\n" );
       }
    }

} // extern "C"
```

Then we can recompile and deploy it with:

```base
eoscpp -o hello.wast hello.cpp 
eosc set contract ${account} hello.wast hello.abi
```
eosd will call init() again because of the redeploy
```base
Init World!
Init World!
Init World!
```
Then we can execute transfer:
```base
$ eosc push message ${account} transfer '{"from":"currency","to":"inita","quantity":50}' --scope ${account}
{
  "transaction_id": "a777539b7d5f752fb40e6f2d019b65b5401be8bf91c8036440661506875ba1c0",
  "processed": {
    "ref_block_num": 20,
    "ref_block_prefix": 463381070,
    "expiration": "2017-09-14T01:05:49",
    "scope": [
      "${account}"
    ],
    "signatures": [],
    "messages": [{
        "code": "${account}",
        "type": "transfer",
        "authorization": [],
        "data": {
          "from": "currency",
          "to": "inita",
          "quantity": 50
        },
        "hex_data": "00000079b822651d000000008040934b3200000000000000"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```
And on eosd we should see the following output:
```base
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
```
**Using C++ API to Read Messages**

So far we used the C API because it is the lowest level API that is directly exposed by EOS.IO to the WASM virtual machine. Fortunately, eoslib provides a higher level API that removes much of the boiler plate.
```base
/// eoslib/message.hpp
namespace eosio {
	 template<typename T>
	 T current_message();
}
```
We can update hello.cpp to be more concise as follows:
```base
#include <hello.hpp>

/**
 *  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
 *  call these methods.
 */
extern "C" {

    /**
     *  This method is called once when the contract is published or updated.
     */
    void init()  {
       eosio::print( "Init World!\n" );
    }

    struct transfer {
       eosio::name from;
       eosio::name to;
       uint64_t quantity;
    };

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::current_message<transfer>();
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }

} // extern "C"
```
You will notice that we updated the `transfer` struct to use the `eosio::name` type directly, and then condensed the checks around `read_message` to a single call to `current-Message`.

After compiling and uploading it you should get the same results as the C version.

**Requiring Sender Authority to Transfer**

One of the most common requirements of any contract is to define who is allowed to perform the action. In the case of a curency transfer, we want require that the account defined by the `from` parameter signs off on the message.

The EOS.IO software will take care of enforcing and validating the signatures, all you need to do is require the necessary authority.
```base
    ...
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::current_message<transfer>();
          eosio::require_auth( message.from );
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }
    ...
```
After building and deploying we can attempt to transfer again:
```base
 $ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account}
 1881603ms thread-0   main.cpp:797                  operator()           ] Converting argument to binary...
 1881630ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
 status_code == 200: Error
 : 3030001 tx_missing_auth: missing required authority
 Transaction is missing required authorization from initb
     {"acct":"initb"}
         thread-0  message_handling_contexts.cpp:19 require_authorization
...
```
If you look on `eosd` you will see this:

```base
Hello World: initc->transfer
1881629ms thread-0   chain_api_plugin.cpp:60       operator()           ] Exception encountered while processing chain.push_transaction:
...
```
This shows that it attempted to apply your transaction, printed the initial "Hello World" and then aborted when `eosio::require_auth` failed to find authorization of account `initb`.

We can fix that by telling eosc to add the required permission:
```base
$ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account} --permission initb@active
```
The `--permission` command defines the account and permission level, in this case we use the active authority which is the default.

This time the transfer should have worked like we saw before.

**Aborting a Message on Error**

A large part of contract development is verifying preconditions, such that the quantity transferred is greater than 0. If a user attempts to execute an invalid action, then the contract must abort and any changes made get automatically reverted.
```base
    ...
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::currentMessage<transfer>();
          assert( message.quantity > 0, "Must transfer a quantity greater than 0" );
          eosio::requireAuth( message.from );
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }
    ...
```
We can now compile, deploy, and attempt to execute a transfer of 0:
```base
 $ eoscpp -o hello.wast hello.cpp
 $ eosc set contract ${account} hello.wast hello.abi
 $ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":0}' --scope initc --permission initb@active
 3071182ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
 status_code == 200: Error
 : 10 assert_exception: Assert Exception
 test: assertion failed: Must transfer a quantity greater than 0
```

Now that you have completed the Hello World tutorial, you are ready to write your first Smart Contract.

## 6. Deploy and update Smart Contract

As mentioned in the tutorial above, deploying a contract onto the blockchain can simply be done by using the `set contract` command, where the `set contract` command do not only upload but also update an existing contract, but only if you have permission to do so. 

Use the following command to:
- deploy a new contract, and
- update an existing contract 
```base
$ eosc set contract ${account} ${contract}.wast ${contract}.abi
```


## 7. Command Summary

Download and build the latest EOS.IO software `$ build.sh ${architecture} ${build_mode}`

Writing smart contract
- Create the skeleton using the eoscpp tool `$ eoscpp -n ${contract}`
- Program your smart contract in the .cpp & .hpp file
- Generate the .abi file `$ eoscpp -g ${contract}.abi ${contract}.hpp`
- Generate the .wast file `$ eoscpp -o ${contract}.wast ${contract}.cpp`

Deploy smart contract
- Connect to a node `$ eosc -H ${node_ip} -p ${port_num}`
- Create a wallet `$ eosc wallet create`
- [Create an account] if you do not already hold an EOS keys
- Import your account key `$ eosc wallet import ${private_key}`
- Unlock your wallet `$ eosc wallet unlock ${wallet} `
- Deploy the contract `$ eosc set contract ${account} ${contract}.wast ${contract}.abi`

## 8. Debugging Smart Contract

In order to be able to debug your smart contract, you will need to setup local eosd node. This local eosd node can be run as separate private testnet or as an extension of public testnet (or the official testnet).

When you are creating your smart contract for the first time, it is recommended to test and debug your smart contract on a private testnet first, since you have full control of the whole blockchain. This enables you to have unlimited amount of eos needed and you can just reset the state of the blockchain whenever you want. When it is ready for production, debugging  on the public testnet (or official testnet) can be done by connecting your local eosd to the public testnet (or official testnet) so you can see the log of the testnet in your local eosd.

The concept is the same, so for the following guide, debugging on the private testnet will be covered.


If you haven't set up your own local eosd, please follow the [setup guide](https://github.com/EOSIO/eos/wiki/Local-Environment). By default, your local eosd will just run in a private testnet unless you modify the config.ini file to connect with public testnet (or official testnet) nodes as described in the following [guide](Testnet%3A%20Public).

### 8.1. Method
The main method used to debug smart contract is **Caveman Debugging**, where we utilize the printing functionality to inspect the value of a variable and check the flow of the contract. Printing in smart contract can be done through the Print API ([C](https://github.com/EOSIO/eos/blob/master/contracts/eoslib/print.h) and [C++](https://github.com/EOSIO/eos/blob/master/contracts/eoslib/print.hpp)). The C++ API is the wrapper for C API, so most often we will just use the C++ API.

### 8.2. Print
Print C API supports the following data type that you can print:
- prints - a null terminated char array (string)
- prints_l - any char array (string) with given size
- printi - 64 bit unsigned integer
- printi128 - 128 bit unsigned integer
- printd - double encoded as 64 bit unsigned integer
- printn - base32 string encoded as 64 bit unsigned integer
- printhex - hex given binary of data and its size 

While Print C++ API wraps some of the above C API by overriding the print() function so user doesn't need to determine which specific print function he needs to use. Print C++ API supports
- a null terminated char array (string)
- integer (128 bit unsigned, 64 bit unsigned, 32 bit unsigned, signed, unsigned)
- base32 string encoded as 64 bit unsigned integer
- struct that has print() method

### 8.3. Example
Let's write a new contract as example for debugging
- debug.hpp
```cpp
#include <eoslib/eos.hpp>
#include <eoslib/db.hpp>

namespace debug {
    struct foo {
        account_name from;
        account_name to;
        uint64_t amount;
        void print() const {
            eosio::print("Foo from ", eosio::name(from), " to ",eosio::name(to), " with amount ", amount, "\n");
        }
    };
}
```
- debug.cpp
```cpp
#include <debug.hpp>

extern "C" {

    void init()  {
    }

    void apply( uint64_t code, uint64_t action ) {
        if (code == N(debug)) {
            eosio::print("Code is debug\n");
            if (action == N(foo)) {
                 eosio::print("Action is foo\n");
                debug::foo f = eosio::current_message<debug::foo>();
                if (f.amount >= 100) {
                    eosio::print("Amount is larger or equal than 100\n");
                } else {
                    eosio::print("Amount is smaller than 100\n");
                    eosio::print("Increase amount by 10\n");
                    f.amount += 10;
                    eosio::print(f);
                }
            }
        }
    }
} // extern "C"
```
- debug.hpp
```cpp
{
  "structs": [{
      "name": "foo",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "amount": "uint64"
      }
    }
  ],
  "actions": [{
      "action_name": "foo",
      "type": "foo"
    }
  ]
}

```

Let's deploy it and send a message to it. Assume that you have `debug` account created and have its key in your wallet.
```bash
$ eoscpp -o debug.wast debug.cpp
$ eosc set contract debug debug.wast debug.abi
$ eosc push message debug foo '{"from":"inita", "to":"initb", "amount":10}' --scope debug
```

When you check your local eosd node log, you will see the following lines after the above message is sent.
```
Code is debug
Action is foo
Amount is smaller than 100
Increase amount by 10
Foo from inita to initb with amount 20
```
There, you can confirm that your message is going to the right control flow and the amount is updated correctly. You might see the above message at least 2 times and that's normal because each transaction is being applied during verification, block generation, and block application.


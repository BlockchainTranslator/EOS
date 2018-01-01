- [1. Accounts & Wallets](#1-accounts--wallets)
  * [1.1 Creating and Managing Wallets](#11-creating-and-managing-wallets)
  * [1.2 Generating and Importing EOS Keys](#12-generating-and-importing-eos-keys)
  * [1.3 Backing up your Wallet](#13-backing-up-your-wallet)
  * [1.4 Creating an Account](#14-creating-an-account)
- [2. Currency Contract Walkthrough](#2-currency-contract-walkthrough)
- [3. Smart Contract "Hello World"](#3-smart-contract-hello-world)
- [4. Tic-Tac-Toe](#4-tic-tac-toe)

## 1. Accounts & Wallets

**Notice** This tutorial is geared towards use on a **private testnet**, but will work on public testnet with minor modifications. 

#### What you'll learn

You'll learn how to create and manage wallets, their keys and then use this wallet to interact with the blockchain through `eosc`.

#### Who this Tutorial is For

This tutorial is for users who want to learn about wallet and account management. It will attempt to teach you as much about `eosc` and how wallets and accounts on EOS interact with each other. Advanced users may be better suited to check out the **[Command Reference](Command%20Reference)**

#### Prerequisites

- Built and running copy of `eosc` and `eos-walletd` on your system.
- Basic understanding of command line interface. 

**Note:** Instructions require slight modification when applied to a docker installation. 

### 1.1 Creating and Managing Wallets

#### Open your terminal and change to the directory where EOS was built

This will make it easier for us to interact with `eosc`, which is a command line interface for interacting with `eosd` and `eos-walletd`. 

```bash
$ cd /path_to_eos/build/programs/eosc
```

The first thing you'll need to do is create a wallet; use the `wallet create` command of `eosc`

```bash
$ eosc wallet create
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"A MASTER PASSWORD"
```

A wallet called _default_ is now inside `eos-walletd` and has returned the **master password** for this wallet. Be sure to save this password somewhere safe. This password is used to unlock (decrypt) your wallet file. 

The file for this wallet is named `default.wallet` and is located in the `data-dir` directory of your EOS directory (or the directory you specified with the `--data-dir` argument when launching `eos-walletd`)

#### Managing Multiple Wallets and Wallet Names

`eosc` is capable of managing multiple wallets. Each individual wallet is protected by different wallet master passwords. The example below creates another wallet and demonstrates how to name it by using the `-n` argument.

```bash
$ eosc wallet create -n periwinkle
Creating wallet: periwinkle
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"A MASTER PASSWORD"
```

Now confirm that the wallet was created with your chosen name.

```bash
$ eosc wallet list
Wallets:
[
  "default *",
  "periwinkle *"
]
```

It's important to notice the asterisk (*) after each listed wallet, which means that the respective wallet is unlocked. When using `create wallet` the resulting wallet is unlocked by default for your convenience.

Lock that second wallet using `wallet lock`

```bash
$ eosc wallet lock -n periwinkle
Locked: 'periwinkle'
```

Upon running `wallet list` again, you will see that the asterisk is gone, meaning that the wallet is now locked.

```bash
$ eosc wallet list
Wallets:
[
  "default *",
  "periwinkle"
]
```

Unlocking a named wallet entails calling `wallet unlock` with an `-n` parameter followed by the name of the wallet and then entering the wallet's master password in the password prompt (yes, you can paste the password). Go ahead and grab the master key for the second wallet you created, execute the command below and when the _password_ prompt appears, paste and press _enter_. You'll be presented with a confirmation.

```bash
$ eosc wallet unlock -n periwinkle
```

eosc will let you know that the wallet was unlocked

```bash
Unlocked: 'periwinkle'
```

_**Note:** You can also use a `--password` argument followed by the master password to skip the prompt, but this results in your master password being visible in the console history_

Now check your progress

```bash
$ eosc wallet list
Wallets:
[
  "default *",
  "periwinkle *"
]
```

Wonderful, the _periwinkle_ wallet is followed by an asterisk, so it is now unlocked. 

_**Note:** Interacting with the 'default' wallet using the wallet command does not require the `-n` parameter_

Restart `eos-walletd` now, and then go back to where you were calling `eosc` and run the following command

```bash
$ eosc wallet list
Wallets:
[]
```

Interesting, where did the wallet go?

Wallets first need to be opened, and because you shut down `eos-walletd`, the wallet wasn't open. Run the following commands.

```bash
$ eosc wallet open
$ eosc wallet list
Wallets:
[
  "default"
]
```

That's better. 

_**Note:** If you wanted to open a named wallet, you would run `$ eosc wallet open -n periwinkle`, see a pattern forming? ;)_

You'll notice in the last response that the default wallet is locked by default. Unlock it now, you'll need it in the subsequent steps. 

Run the `wallet unlock` command and paste your _default_ wallet's master password when the password prompt appears.

```bash
$ eosc wallet unlock
Unlocked: 'default'
```
Go ahead and check that the wallet is unlocked

```bash
$ eosc wallet list
Wallets:
[
  "default *"
]
```
The wallet is accompanied by an asterisk, so it's unlocked. Excellent. 

You've learned how to create multiple wallets, and interact with them in `eosc`. But an empty wallet doesn't do you much good, time to import some keys. 

### 1.2 Generating and Importing EOS Keys

There are several ways to generate an EOS key pair, but this tutorial will focus on `create key` command in `eosc`

Generate two keypairs

```bash
$ eosc create key
Private key:###
Public key: ###
$ eosc create key
Private key:###
Public key: ###
```

You now have two EOS keypairs. At this point, these are just arbitrary keypairs and by themselves have no authority.

If you followed all of the previous steps, your _default_ wallet should be open and unlocked.

In this next step, we execute `wallet import` twice, one for each *private key* that were generated earlier. You now need to import these to your `default` wallet.

```bash
$ eosc wallet import ${private_key_1}
```
And then again with the second private key

```bash
$ eosc wallet import ${private_key_2}
```

If successful, each time `wallet import` command responds with the public key corresponding to your private key, your console should look something like..

```bash
$ eosc wallet import ${private_key_1}
imported private key for: ${public_key_1}
$ eosc wallet import ${private_key_2}
imported private key for: ${public_key_2}
```

We can check which keys are loaded by calling `wallet keys`

```bash
$ eosc wallet keys
[[
    "EOS6....",
    "5KQwr..."
  ],
  [
    "EOS3....",
    "5Ks0e..."
  ]
]
```

The wallet will protect these keys when it's locked. Accessing the keys in a locked wallet requires the master password that was provided to you during wallet creation. Because the wallet file itself is encrypted, it's not _required_ to backup your keypairs, but backing up your wallet file in a safe place is highly recommended. 

### 1.3 Backing up your wallet

Now that your wallet contains keys, it's good to get into the habit of a backup, in case some unspeakable event results in the loss of this file. One example may be a flash drive. Without the password, the wallet file is encrypted with high entropy, and the keys inside are incredibly difficult (improbable by all reasonable measures) to access.

You can find your wallet files in the `data-dir`. If you did not specify a `--data-dir` parameter when launching eos, you can file this in `/path/to/eos/build/programs/eosd` (the exact path to eos will differ from system to system).

```bash
$ cd /path_to_eos/build/programs/eosd && ls
blockchain   blocks   config.ini   default.wallet   periwinkle.wallet
```

Once in the directory you will the two files, `default.wallet` and `periwinkle.wallet`. Go ahead and save them somewhere (practice makes perfect!)

### 1.4 Creating an Account

**If you're working with the public testnet, to proceed you will either need to have a genesis allocation or apply for an account from the faucet. And make necessary adjustments below (hint: inita should be replaced with your account)**

First let's *examine* the `create account` command and its positional arguments.

```bash
$ eosc create account inita ${desired_account_name} ${public_key_1} ${public_key_2}
```

**Breakdown of the positional arguments for `create account` command**

- `inita` is the name of the **account name** that will fund the account creation, and subsequently the new account.
- `desired_account_name` is the name of the account you would like to create
- `public_key_1` and `public_key_2` are public keys, the first one will be permissioned as the owner authority of your account, and the second one will be permissioned for the active authority of your account. 

You generated two keypairs previously, you can either scroll up in your console, as you executed this command only moments ago, or execute `wallet keys` if you disdain scrolling or have cleared your screen

```bash
$ eosc wallet keys
[[
    "EOS6....",
    "5KQwr..."
  ],
  [
    "EOS3....",
    "5Ks0e..."
  ]
]
```

As a reminder, your public keys start with `EOS...`. The keys above are arbitrary until you have added them to an authority, which one you decide to user for active and owner are inconsequential until you have created your account.

_Reminder,_ your owner key equates to full control of your account, whereas your active key equates to full access over funds in your account. 

With all you've just learned, replace the placeholders in the following command and press enter. 

```bash
$ eosc create account inita ${desired_account_name} ${public_key_1} ${public_key_2}
```
Did you recieve an error mentioning "authorities" somewhere? Don't fret, I put you through that intentionally. The reason you got an error, is that you do not have the **@inita**  account keys loaded. Sorry about that, couldn't resist. 

**inita's** keys are included in `config.ini` but for your convenience I've went ahead and grabbed the key and provided it below. Just execute the provided command, maybe that makes up for forcing you through an error?

```bash
$ eosc wallet import 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```
it will respond with 

```bash
imported private key for: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```

Now that the **@inita** account's keys are loaded, execute the `create account` command you crafted before I baited you into a trap, and press enter. 

If all goes well, `eosc` will return a json object with a transaction ID, similar to the following

```
{
  "transaction_id": "6acd2ece68c4b86c1fa209c3989235063384020781f2c67bbb80bc8d540ca120",
  "processed": {
    "refBlockNum": "25217",
    "refBlockPrefix": "2095475630",
    "expiration": "2017-07-25T17:54:55",
    "scope": [
      "eos"...
```

Great! You now have an account and it is on a blockchain. 

Go ahead and pat yourself on the back, you've created a wallet, learned a bit about how wallets work, generated keys, imported them into your wallet and created an account. 

## 2. Currency Contract Walkthrough

### Objective

The following tutorial will guide the user through the sample currency
contract which can be found in the public github repository
[here](https://github.com/EOSIO/eos/tree/master/contracts/currency).

### Overview

The currency contract handles the transfer of a currency from one
account to another, whereas the different account balances are saved for
every user local in their scope.

### Action

Currently there is only one action exposed by the contract, which is:  
currency_transfer: Transfers an amount of currency from one account to
another.

### Start!

The smart contract is divided in three files:

| currency.hpp | header file where the declarations and structures of the contract are defined |
|--------------|-------------------------------------------------------------------------------|
| currency.cpp | Contract logic and implementation                                             |
| currency.abi | Interface definition for the user to interact                                 |

### Header File: currency.hpp

First import all the necessary libraries and define your own namespace
such as:

~~~~
// Import necessary libraries

#include <eoslib/eos.hpp>   // Generic eos library, i.e. print, type, math, etc
#include <eoslib/token.hpp> // Token usage
#include <eoslib/db.hpp>    // Database access

namespace currency {
    // Your code here
}
~~~~

Next add a currency token; It’s in fact a uin64_t wrapper which checks
for proper types and under/overflows for standard-compatible token
messages

~~~~
typedef eosio::token<uint64_t,N(currency)> currency_tokens;
~~~~

A structure for our action, which looks as follows:
~~~~
struct transfer {
    account_name from;          //transfer source account
    account_name to;            //transfer destination account
    currency_tokens quantity;   //amount to be transferred
};
~~~~
Additionally, we need to store the balance in a table. The table is
defined as follows:

~~~~
using accounts = eosio::table<N(defaultscope),N(currency),N(account),account,uint64_t>;
~~~~
-   First template parameter defines the default scope of the
    table, i.e. when a data is stored to this table without specifying
    the scope, it will fall back to this account

-   Second template parameter defines the owner of the table (i.e.
    contract's name)

-   Third template parameter defines the name of the table

-   Fourth template parameter defines the structure that it stores (will
    be defined in the next section)

-   Fifth template parameter defines the data type of the table's key

Once the table is defined the structure that needs to be stored (in our
case “account”) needs to be defined as well. This is done in another
struct:
~~~~
struct account {
    //Constructor
    account( currency_tokens b = currency_tokens() ):balance(b){}

    //The key is constant because there is only one record per
    //scope/currency/accounts
    const uint64_t key = N(account);

    //Number of tokens in account
    currency_tokens balance;

    // Method to check if account is empty.
    // returns true if the account balance is zero.
    bool is_empty()const { return balance.quantity == 0; }
};
~~~~
The structure contains both a constructor and a standard function for
comparison against an empty account.

It’s important to note, that the key is the first variable who’s type
matches the type defined in the table definition above (as fifth
template parameter).

To round things up, we add an accessor function to access the owners
account information, which returns information stored here:
owner/TOKEN_NAME/account/account. This function goes in the header to
provide 3<sup>rd</sup> party access to a user’s balance:
~~~~
inline account get_account( account_name owner ) {
    account owned_account;
    accounts::get( owned_account, owner );
    return owned_account;
}
~~~~
Note: The function accounts:get returns the account owner. In case the
account does not exist, it returns a default constructed account.

### Source File: currency.cpp
~~~~
#include <currency/currency.hpp>

// The init() and apply() methods must have C calling convention

extern "C" {
    // Only called once
    void init() {
    }

    // The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action_name ) {
        // Put your message handler here
    }
} // extern "C"
~~~~
All contracts have the above skeleton in common. Every contract must
have the above functions:

Init() is being called once at the beginning of the lifetime of a
contract. It can be used to setup the environment in order for the
contract to function properly.

Apply( uint64_t code, uint64_t action_name) is being used a message
sink. Whenever a message is being sent to the contract, this function is
the entry point; The two parameters have the following meaning:

-   code: This is the name of the contract
-   action_name: This is the name of the action

In the case of the currency contract, the init() function looks as
follows:
~~~~
void init() {
    account owned_account;

    //Initialize currency account only if it does not exist
    if ( !accounts::get( owned_account, N(currency) )) {
        store_account( N(currency),
        account( currency_tokens(1000ll\*1000ll\*1000ll) ) );
    }
}
~~~~
The first time this contract runs, it checks, if the currency account
already has a table. In the table the currency balance is recorded. In
case there is no table a new table is being generated and an initial
amount of 1000,000,000, which makes the currency contract the initial
owner of 1000,000,000 currency units.

The message sink looks as follows:
~~~~
void apply( uint64_t code, uint64_t action ) {
    if( code == N(currency) ) {
        if( action == N(transfer) )
            account::apply_currency_transfer( current_message<account::transfer >() );
    }
}
~~~~
It is best practice to implement filters as in the above code sample in
order to make sure that only the correct messages are being processed
and then call the atual message handler after filtering.

Notice that current_message<T>() is used before passing it to
specific handler, current_message<T>() is converting the message
that the contract receives to struct T.

### Actual Message Handler

The actual transfer of currency is performed in:
~~~~
void apply_currency_transfer( const account::transfer& transfer_msg )
{
    require_notice( transfer_msg.to, transfer_msg.from );
    require_auth( transfer_msg.from );

    auto from = get_account( transfer_msg.from );
    auto to = get_account( transfer_msg.to );

    from.balance -= transfer_msg.quantity;
    to.balance += transfer_msg.quantity;

    store_account( transfer_msg.from, from );
    store_account( transfer_msg.to, to );
}
~~~~
The code is straight forward, subtracting currency from the source
account and adding it to the destination account.

The require_notice function is an inline action which makes it possible
to forward the received message to another account. In this case the
transfer message is forwarded to the source and destination account.
This is an extremely useful feature as it enables these “notified
accounts” to chain in their own functionality.

The require_auth function makes sure that the message is signed in the
correct way. In this case the holder of the source account needs to sign
the transaction for the transfer to be handled as expected.

Observe that we are using the get_account function that is provided in
the header in order to retrieve the correct account object.

Since we are using tokens, automatic over and underflow assertions are
being backed into the actual subtraction and addition operations.

Finally the amounts are updated via the store_account function.

### Store_account

This function handles the actual storage of the balance:
~~~~
void store_account( account_name current_account, const account& value ) {
    if( a.is_empty() ) {
        accounts::remove( value, current_account);
    } else {
        accounts::store( value, current_account);
    }
}
~~~~
The interesting fact about this is, that the account (meaning the table
saved under the scope of current_account gets removed if empty. Since
whenever money is transferred onto a non-existing account the table gets
created.

As such removing unnecessary tables is a resource saving mechanism that
should be applied as best practice when writing any smart contract.

NOTE: When comparing the above code samples with the actual code in the
repository, please be aware of the usage of TOKEN_NAME as a #define in
order to make renaming the account name more easy. In the above code,
TOKEN_NAME has been replaced by account for easier legibility.

### ABI File: currency.abi

Abi (a.k.a Application Binary Interface) acts as an interface between
the sent message and the binary version of the smart contract. Let's
start with a generic version which includes the following objects:

-   struct: list of data structure used by the action/ table in the
    contract

-   actions: list of actions available in the contract

-   tables: list of tables available in the contract
~~~~
{
    "structs": \[{
        "name": "...",
        "base": "...",  
        "fields": { ... }
    }, ...\],
    "actions": \[{
        "action_name": "...",
        "type": "..."
    }, ...\],
    "tables": \[{
        "table_name": "...",
        "type": "...",
        "key_names" : \[...\],
        "key_types" : \[...\]
    }, ...\]
}
~~~~
### struct Objects

From the information in the header file most of the ABI can be created.
As such we start with the structures; There are two structures in the
header file:
~~~~
struct transfer {
    account_name from;
    account_name to;
    currency_tokens quantity;
};

struct account {
    account( currency_tokens b = currency_tokens() ):balance(b){}
    const uint64_t key = N(account);
    currency_tokens balance;
    bool is_empty()const { return balance.quantity == 0; }
};
~~~~
These structures turn into the following ABI information:
~~~~
"structs": \[{
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
        "key": "name",
        "balance": "uint64"
    }
}\]
~~~~
### action Object

Action Objects correspond similarly. As such, we have one action named
“transfer” in the currency contract which looks as follows in the ABI
file:
~~~~
"actions": \[{
    "action_name": "transfer",
    "type": "transfer"
}\]
~~~~
### table Object

In the header file a single index called “account” table is being
defined:
~~~~
eosio::table<N(defaultscope),N(currency),N(account),account,uint64_t>;
~~~~
This table turns into the following ABI object:
~~~~
"tables": \[{
    "table_name": "account",
    "type": "account",
    "index_type": "i64",
    "key_names" : \["key"\],
    "key_types" : \["name"\]
}\]
~~~~
rounding up the ABI file.

### Deploy and run

Now all the three files (currency.hpp, currency.cpp, currency.abi) can
be deployed from command line:
~~~~
$ eosc set contract currency currency.wast currency.abi
~~~~
Make sure that the wallet is unlocked and contains the currency key.
After the deployment the contracts action can be triggered from command
line in the following way:
~~~~
$ eosc push message currency transfer ‘{“from”:“currency”,“to”:“tester”,“quantity”:50}’ -S currency -S tester -p currency@active
~~~~

## 3. Smart Contract “Hello World”
To keep things simple we have created a tool called `eoscpp` which can be used to bootstrap a new contract. For this
to work we assume you have installed the eosio/eos code installed and that ${CMAKE_INSTALL_PREFIX}/bin is in your path.


```bash
$ eoscpp -n hello
$ cd hello
$ ls
```

The above will create a new empty project in the './hello' folder with three files:

```bash
hello.abi hello.hpp hello.cpp
```

Let's take a look at the simplest possible contract:

```bash
$ cat hello.cpp

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

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
    }

} // extern "C"
```

This contract implements the two entry points, `init` and `apply`. All it does is log the messages delivered and makes no other checks. Anyone can deliver any message at any time provided the block producers allow it.  Absent any required signatures, the contract will be billed for the bandwidth consumed.

You can compile this contract into a text version of WASM (.wast) like so:

```bash
$ eoscpp -o hello.wast hello.cpp
```

#### Deploying your Contract

Now that you have compiled your application it is time to deploy it. This will require you to do the following first:

1. start eosd with wallet plugin enabled
2. create a wallet & import keys for at least one account
3. keep your wallet unlocked

Assuming your wallet is unlocked and has keys for `${account}`, you can now upload this contract to the blockchain with the following command:

```bash
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

```bash
...] initt generated block #188249 @ 2017-09-13T22:00:24 with 0 trxs  0 pending
Init World!
Init World!
Init World!
```

You will notice the lines "Init World!" are executed 3 times, this isn't a mistake.  When the blockchain is processing transactions the following happens:

1. eosd receives a new transaction
  * creates a temporary session
  * attempts to apply the transaction
  * **succeeds and prints "Init World!"**
  * or fails undoes the changes (potentially failing after printing "Init World!")
2. eosd starts to produce a block
  * undoes all pending state
  * pushes all transactions as it builds the block
  * **prints "Init World!" a second time**
  * finishes building the block
  * undoes all of the temporary changes while creating block
3. eosd pushes the generated block as if it received it from the network
  * **prints "Init World!" a third time**

At this point your contract is ready to start receiving messages. Since the default message handler accepts all messages we can send it
anything we want. Let's try sending it an empty message:

```bash
$ eosc push message ${account} hello '"abcd"' --scope ${account}
```

This command will send the message "hello" with binary data represented by the hex string "abcd". Note, in a bit we will show how to define the ABI so that
you can replace the hex string with a pretty, easy-to-read, JSON object. For now we merely want to demonstrate how the message type "hello" is dispatched to
account.


The result is:
```bash
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

If you are following along in `eosd` then you should have seen the following scroll by the screen:

```bash
Hello World: ${account}->hello
Hello World: ${account}->hello
Hello World: ${account}->hello
```

Once again your contract was executed and undone twice before being applied the 3rd time as part of a generated block.  

#### Message name Restrictions

Message types (eg. "hello") are actually base32 encoded 64 bit integers. This means they are limited to the charcters a-z, 1-5, and '.' for the first
12 charcters and if there is a 13th character then it is restricted to the first 16 characters ('.' and a-p).


#### ABI - Application Binary Interface

The ABI is a JSON-based description on how to convert user actions between their JSON and Binary representations. The ABI also
describes how to convert the database state to/from JSON. Once you have described your contract via an ABI then developers and
users will be able to interact with your contract seemlessly via JSON.

We are working on tools that will automate the generation of the ABI from the C++ source code, but for the time being you may have
to generate it manually. 

Here is an example of what the skeleton contract ABI looks like:

```json
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

You will notice that this ABI defines an action `transfer` of type `transfer`.  This tells EOS.IO that when `${account}->transfer` message is seen that the payload is of type
`transfer`.  The type `transfer` is defined in the `structs` array in the object with `name` set to `"transfer"`.  

```json
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

It has several fields, including `from`, `to` and `quantity`.  These fields have the coresponding types `account_name`, `account_name`, and `uint64`.  `account_name` is defined as a typedef in
the `types` array to `name`, which is a built in type used to encode a uint64_t as base32 (eg account names).

```json
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
...
```

Now that we have reviewed the ABI defined by the skeleton, we can construct a message call for `transfer`:

```bash
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

If you observe the output of `eosd` you should see:

```
Hello World: ${account}->transfer
Hello World: ${account}->transfer
Hello World: ${account}->transfer
```

### Processing Arguments of Transfer Message

According to the ABI the transfer message has the format: 

```json
	 "fields": {
		 "from": "account_name",
		 "to": "account_name",
		 "quantity": "uint64"
	 }
```

We also know that account_name -> name -> uint64 which means that the binary representation of the message is the same as:

```c
struct transfer {
    uint64_t from;
    uint64_t to;
    uint64_t quantity;
};
```

The EOS.IO C API provides access to the message payload via the Message API:

```
uint32_t message_size();
uint32_t read_message( void* msg, uint32_t msglen );
```

Let's modify `hello.cpp` to print out the content of the message:

```c
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
          auto read = readMessage( &message, sizeof(message) );
          assert( read == sizeof(message), "message too short" );
          eosio::print( "Transfer ", message.quantity, " from ", eosio::name(message.from), " to ", eosio::name(message.to), "\n" );
       }
    }

} // extern "C"
```

Then we can recompile and deploy it with:

```bash
eoscpp -o hello.wast hello.cpp 
eosc set contract ${account} hello.wast hello.abi
```

`eosd` will call init() again because of the redeploy

```bash
Init World!
Init World!
Init World!
```

Then we can execute transfer:

```bash
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

And on `eosd` we should see the following output:

```bash
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
```

#### Using C++ API to Read Messages
So far we used the C API because it is the lowest level API that is directly exposed by EOS.IO to the WASM virtual machine. Fortunately, eoslib provides a higher level API that
removes much of the boiler plate. 

```c
/// eoslib/message.hpp
namespace eosio {
	 template<typename T>
	 T current_message();
}
```

We can update `hello.cpp` to be more concise as follows:

```c
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

You will notice that we updated the `transfer` struct to use the `eosio::name` type directly, and then condenced the checks around `read_message` to a single call to `current_message`.

After compiling and uploading it you should get the same results as the C version.

### Requiring Sender Authority to Transfer

One of the most common requirements of any contract is to define who is allowed to perform the action. In the case of a curency transfer, we want require that the account defined by the `from` parameter signs off on the message. 

The EOS.IO software will take care of enforcing and validating the signatures, all you need to do is require the necessary authority.

```c
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

```bash
 eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account}
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
```
Hello World: initc->transfer
1881629ms thread-0   chain_api_plugin.cpp:60       operator()           ] Exception encountered while processing chain.push_transaction:
...
```

This shows that it attempted to apply your transaction, printed the initial "Hello World" and then aborted when `eosio::require_auth` failed to find authorization of account `initb`.

We can fix that by telling `eosc` to add the required permission:

```bash
 eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account} --permission initb@active
```

The `--permission` command defines the account and permission level, in this case we use the `active` authority which is the default.

This time the transfer should have worked like we saw before.

### Aborting a Message on Error

A large part of contract development is verifying preconditions, such that the quantity transferred is greater than 0. If a user attempts to execute an invalid action, then
the contract must abort and any changes made get automatically reverted.

```c
    ...
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::current_message<transfer>();
          assert( message.quantity > 0, "Must transfer a quantity greater than 0" );
          eosio::require_auth( message.from );
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }
    ...
```
We can now compile, deploy, and attempt to execute a transfer of 0:

```bash
 $ eoscpp -o hello.wast hello.cpp
 $ eosc set contract ${account} hello.wast hello.abi
 $ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":0}' --scope initc --permission initb@active
 3071182ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
 status_code == 200: Error
 : 10 assert_exception: Assert Exception
 test: assertion failed: Must transfer a quantity greater than 0
```

## 4. Tic-Tac-Toe

### Objective

The following tutorial will guide the user to build a sample Player vs Player game contract. We will use tic tac toe game to demonstrate this. Final result of this tutorial can be found [here](https://github.com/EOSIO/eos/tree/master/contracts/tic_tac_toe).

### Assumption
For this game, we are using a standard 3x3 tic tac toe board. Players are divided into two roles: **host** and **challenger**. Host always makes the first move. Each pair of players can **ONLY** have up to two games at the same time, one where the first player become the host and the other one where the second player become the host. 


#### Board
Instead of using `o` and `x` as in the traditional tic tac toe game. We use `1` to denote movement by host, `2` to denote movement by challenger, and `0` to denote empty cell. Furthermore, we will use one dimensional array to store the board. Hence:

|           | (0,0) | (1,0) | (2,0) |
| :-------: | :---: | :---: | :---: |
| **(0,0)** | -     | o     | x     |
| **(0,1)** | -     | x     | -     |
| **(0,2)** | x     | o     | o     |

Assuming x is host, the above board is equal to `[0, 2, 1, 0, 1, 0, 1, 2, 2]`

#### Action
User will have the following actions to interact with this contract:
- create: create a new game
- restart: restart an existing game, host/ challenger is allowed to do this
- close: close an existing game, which frees up the storage used to store the game, only host is allowed to do this 
- move: make a movement

#### Contract account
For the following guide, we are going to push the contract to an account called `tic.tac.toe`. In case `tic.tac.toe` account name is already taken, you can also use another account by replacing any occurence of `tic.tac.toe` in the code with your account name. If you haven't create the account, please create the account first.
```bash
$ eosc create account ${creator_name} ${contract_account_name} ${contract_pub_owner_key} ${contract_pub_active_key} --permission ${creator_name}@active
# e.g. $ eosc create account inita tic.tac.toe  EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA --permission inita@active
```
Ensure that you have your wallet unlocked and the creator's private active key in the wallet imported, otherwise the above command will fail.

### Start!
We are going to create three files here:
- tic_tac_toe.hpp => header file where the structure of the contract is defined
- tic_tac_toe.cpp => main logic of the contract
- tic_tac_toe.abi => interface for user to interact with the contract

### Defining Structure
Let's first start with the header file and define the structure of the contract. Open **tic_tac_toe.hpp** and start with the following boilerplate
```cpp
// Import necessary library
#include <eoslib/eos.hpp> // Generic eos library, i.e. print, type, math, etc
#include <eoslib/db.hpp> // Database access

using namespace eosio;
namespace tic_tac_toe {
    // Your code here
}
```

#### Games Table
For this contract, we will need to have a table that store list of games. Let's define it:
```cpp
...
namespace tic_tac_toe {
    ...
    using Games = eosio::table<N(tic.tac.toe),N(tic.tac.toe),N(games),game,uint64_t>;
}
  
```
NB: In case you upload the contract to other account `tic.tac.toe`, replace `tic.tac.toe` with your account name
- First template parameter  defines the default scope of the table, i.e. when a data is stored to this table without specifying the scope, it will fallback to this account
- Second template parameter defines the account that has write access to this table, in this case it's the contract account name
- Third template parameter defines the name of the table
- Fourth template parameter defines the structure that it stores (will be defined in the next section)
- Fifth template parameter defines the data type of the table's key

#### Game Structure
Let's define structure for the game. Ensure that this struct definition appears before the table definition in the code.
```cpp
...
namespace tic_tac_toe {
    struct PACKED(game) {
        // Default constructor
        game() {};
        // Constructor
        game(account_name challenger, account_name host):challenger(challenger), host(host), turn(host) {
            // Initialize board
            initialize_board();
        };
        // Account name of the challenger, this also acts as key of the table
        account_name     challenger;
        // Account name of the host
        account_name     host;
        // Whose turn it is, = account name of host/ challenger
        account_name     turn; // = account name of host/ challenger
        // Winner of the game, = none or draw or account name of host/ challenger
        account_name     winner = N(none); 
        // Length of the board array, this need to be placed immediately before the board array. It is needed so the abiserializer can pack/ unpack the array properly from/ to the database
        uint8_t          board_len = 9;
        // Board array
        uint8_t          board[9]; 

        // Initialize board with empty cell
        void initialize_board() {
            for (uint8_t i = 0; i < board_len ; i++) {
            board[i] = 0;
            }
        }

        // Reset game
        void reset_game() {
            initialize_board();
            turn = host;
            winner = N(none);
        }
    };
    ...
}
```
Remember that in the previous table definition, we declare `uint64_t` as the data type of the table's key. Hence, for the above game structure, the first `sizeof(uint64_t)` bytes of the structure will be treated as the table's key. By the way, `account_name` is just an alias for `uint64_t`.

#### Action Structure
##### Create
To create the game, we need host account name and challenger's account name
```cpp
...
namespace tic_tac_toe {
    ...
    struct create {
        account_name   challenger;
        account_name   host;
    };
    ...
}
```
##### Restart
To restart the game, we need host account name and challenger's account name to identify the game. Furthermore, we need to specify who want to restart the game, so we can verify the correct signature is provided.
```cpp
...
namespace tic_tac_toe {
    ...
    struct restart {
        account_name   challenger;
        account_name   host;
        account_name   by;
    };
    ...
}
```
##### Close
To close the game, we need host account name and challenger's account name to identify the game.
```cpp
...
namespace tic_tac_toe {
    ...
    struct close {
        account_name   challenger;
        account_name   host;
    };
    ...
}
```
##### Move
To make a move, we need host account name and challenger's account name to identify the game. Furthermore, we need to specify who makes this move and the movement he is making.
```cpp
...
namespace tic_tac_toe {
    ...
    struct movement {
        uint32_t    row;
        uint32_t    column;
    };

    struct Move {
        account_name   challenger;
        account_name   host;
        account_name   by; // the account who wants to make the move
        movement       m;
    };
    ...
}
```
You can see the final tic_tac_toe.hpp [here](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe/tic_tac_toe.hpp)

### Main
Let's open tic_tac_toe.cpp and setup the boilerplate
```cpp
#include <tic_tac_toe.hpp>
using namespace eosio;
/**
*  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
*  call these methods.
*/
extern "C" {

  // Only called once
  void init()  {
  }

  /// The apply method implements the dispatch of events to this contract
  void apply( uint64_t code, uint64_t action_name ) {
      // Put your message handler here
  }

} // extern "C"
```

#### Message handler
We want tic_tac_toe contract to only react to message send to `tic.tac.toe` account and react differently according to the type of the action. Let's set the message filter inside the apply function:
```cpp
  ...
  void apply( uint64_t code, uint64_t action_name ) {
        if (code == N(tic.tac.toe)) {
            if (action_name == N(create)) {
                tic_tac_toe::apply_create(current_message<tic_tac_toe::create>());
            } else if (action_name == N(restart)) {
                tic_tac_toe::apply_restart(current_message<tic_tac_toe::restart>());
            } else if (action_name == N(close)) {
                tic_tac_toe::apply_close(current_message<tic_tac_toe::close>());
            } else if (action_name == N(move)) {
                tic_tac_toe::apply_move(current_message<tic_tac_toe::move>());
            }
        }
  }
  ...
```

Notice that we use `current_message<T>()` before passing it to specific handler, `current_message<T>()` is converting the message that the contract receives to `struct T`. 

NB: if you are deploying this contract to an account other than `tic.tac.toe`, replace `tic.tac.toe` with your account name.


To make things tidy, we will encapsulate the message handler inside `namespace tic_tac_toe`:
```cpp
namespace tic_tac_toe {
  
  void apply_create(const create& c) {
    // Put code for create action here
  }

  void apply_restart(const restart& r) {
    // Put code for restart action here
  }

 
  void apply_close(const close& c) {
    // Put code for close action here
  }

  void apply_move(const move& m) {
    // Put code for move action here
  }
  ...
}

```

#### Create Message Handler
For the create message handler, we want to:
1. Ensure that the message has signature from the host
2. Ensure that the game is not played by the same player
3. Ensure that there is no existing game
4. Store the newly created game into the db
```cpp
namespace tic_tac_toe {
    ...
    void apply_create(const create& c) {
        require_auth(c.host);
        assert(c.challenger != c.host, "challenger shouldn't be the same as host");

        // Check if game already exists
        game existing_game;
        bool game_exists = Games::get(c.challenger, existing_game, c.host);
        assert(game_exists == false, "game already exists");

        game game_to_create(c.challenger, c.host);
        Games::store(game_to_create, c.host);
    }
    ...
}

```

#### Restart Message Handler
For the create message handler, we want to:
1. Ensure that the message has signature from the host/ challenger
2. Ensure that the game exists
3. Ensure that the restart action is done by host/ challenger
4. Reset the game
5. Store the updated game to the db
```cpp
namespace tic_tac_toe {
    ...
    void apply_restart(const restart& r) {
        require_auth(r.by);

        // Check if game exists
        game game_to_restart;
        bool game_exists = Games::get(r.challenger, game_to_restart, r.host);
        assert(game_exists == true, "game doesn't exist!");

        // Check if this game belongs to the message sender
        assert(r.by == game_to_restart.host || r.by == game_to_restart.challenger, "this is not your game!");

        // Reset game
        game_to_restart.reset_game();

        Games::update(game_to_restart, game_to_restart.host);
    }
    ...
}

```

#### Close Message Handler
For the create message handler, we want to:
1. Ensure that the message has signature from the host
2. Ensure that the game exists
3. Remove the game from the db
```cpp
namespace tic_tac_toe {
    ...
    void apply_close(const close& c) {
        require_auth(c.host);

        // Check if game exists
        game game_to_close;
        bool game_exists = Games::get(c.challenger, game_to_close, c.host);
        assert(game_exists == true, "game doesn't exist!");

        Games::remove(game_to_close, game_to_close.host);
    }
    ...
}

```

#### Move Message Handler
For the move message handler, we want to:
1. Ensure that the message has signature from the host/ challenger
2. Ensure that the game exists
3. Ensure that the game is not finished yet
4. Ensure that the move action is done by host/ challenger
5. Ensure that this is the right user's turn
6. Verify movement is valid
7. Update board with the new move
8. Change the move_turn to the other player
9. Find the winner
10. Store the updated game to the db
```cpp
namespace tic_tac_toe {
    ...
    bool is_valid_movement(const movement& mvt, const game& game_for_movement) {
    // Put code here
    }

    account_name get_winner(const game& current_game) {
        // Put code here
    }

    void apply_move(const move& m) {
        require_auth(m.by);

        // Check if game exists
        game game_to_move;
        bool game_exists = Games::get(m.challenger, game_to_move, m.host);
        assert(game_exists == true, "game doesn't exist!");

        // Check if this game hasn't ended yet
        assert(game_to_move.winner == N(none), "the game has ended!");
        // Check if this game belongs to the message sender
        assert(m.by == game_to_move.host || m.by == game_to_move.challenger, "this is not your game!");
        // Check if this is the  message sender's turn
        assert(m.by == game_to_move.turn, "it's not your turn yet!");


        // Check if user makes a valid movement
        assert(is_valid_movement(m.mvt, game_to_move), "not a valid movement!");

        // Fill the cell, 1 for host, 2 for challenger
        bool is_movement_by_host = m.by == game_to_move.host;
        if (is_movement_by_host) {
        game_to_move.board[m.mvt.row * 3 + m.mvt.column] = 1;
        game_to_move.turn = game_to_move.challenger;
        } else {
        game_to_move.board[m.mvt.row * 3 + m.mvt.column] = 2;
        game_to_move.turn = game_to_move.host;
        }
        // Update winner
        game_to_move.winner = get_winner(game_to_move);
        Games::update(game_to_move, game_to_move.host);
    }
    ...
}

```
#### Movement Validation
Valid movement is defined as movement done inside the board on an empty cell:
```cpp
namespace tic_tac_toe {
    ...
        bool is_empty_cell(const uint8_t& cell) {
            return cell == 0;
        }
        bool is_valid_movement(const movement& mvt, const game& game_for_movement) {
            uint32_t movement_location = mvt.row * 3 + mvt.column;
            bool is_valid = movement_location < game_for_movement.board_len && is_empty_cell(game_for_movement.board[movement_location]);
            return is_valid;
        }
    ...
}
```
#### Get Winner
Winner is defined as the first player who succeeds in placing three of their marks in a horizontal, vertical, or diagonal row.
```cpp
namespace tic_tac_toe {
    ...
    account_name get_winner(const game& current_game) {
        if((current_game.board[0] == current_game.board[4] && current_game.board[4] == current_game.board[8]) ||
        (current_game.board[1] == current_game.board[4] && current_game.board[4] == current_game.board[7]) ||
        (current_game.board[2] == current_game.board[4] && current_game.board[4] == current_game.board[6]) ||
        (current_game.board[3] == current_game.board[4] && current_game.board[4] == current_game.board[5])) {
            //  - | - | x    x | - | -    - | - | -    - | x | -
            //  - | x | -    - | x | -    x | x | x    - | x | -
            //  x | - | -    - | - | x    - | - | -    - | x | -
            if (current_game.board[4] == 1) {
                return current_game.host;
            } else if (current_game.board[4] == 2) {
                return current_game.challenger;
            }
        } else if ((current_game.board[0] == current_game.board[1] && current_game.board[1] == current_game.board[2]) ||
                (current_game.board[0] == current_game.board[3] && current_game.board[3] == current_game.board[6])) {
            //  x | x | x       x | - | -
            //  - | - | -       x | - | -
            //  - | - | -       x | - | -
            if (current_game.board[0] == 1) {
                return current_game.host;
            } else if (current_game.board[0] == 2) {
                return current_game.challenger;
            }
        } else if ((current_game.board[2] == current_game.board[5] && current_game.board[5] == current_game.board[8]) ||
                (current_game.board[6] == current_game.board[7] && current_game.board[7] == current_game.board[8])) {
            //  - | - | -       - | - | x
            //  - | - | -       - | - | x
            //  x | x | x       - | - | x
            if (current_game.board[8] == 1) {
                return current_game.host;
            } else if (current_game.board[8] == 2) {
                return current_game.challenger;
            }
        } else {
            bool is_board_full = true;
            for (uint8_t i = 0; i < current_game.board_len; i++) {
                if (is_empty_cell(current_game.board[i])) {
                    is_board_full = false;
                    break;
                }
            }
            if (is_board_full) {
                return N(draw);
            }
        }
        return N(none);
    }
    ...
}
```
You can see the final tic_tac_toe.cpp [here](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe/tic_tac_toe.cpp)
### Creating ABI
Abi (a.k.a Application Binary Interface) is needed here, so the contract can understand the message that you send as binary.
Let's open tic_tac_toe.abi and defines the boilerplate here:
```json
{
  "structs": [{
      "name": "...",
      "base": "...",
      "fields": { ... }
  }, ...],
  "actions": [{
      "action_name": "...",
      "type": "..."
  }, ...],
  "tables": [{
      "table_name": "...",
      "type": "...",
      "key_names" : [...],
      "key_types" : [...]
  }, ...]
```
- struct: list of data structure used by the action/ table in the contract
- actions: list of actions available in the contract
- tables: list of tables available in the contract

#### Table ABI
Remember that in tic_tac_toe.hpp, we create an single index i64 table called games. It stores `game` structure and use `challenger` as the key, which data type is `account_name`. Hence, the abi will be:
```json
{
    ...
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
    }],
    "tables": [{
            "table_name": "games",
            "type": "game",
            "index_type": "i64",
            "key_names" : ["challenger"],
            "key_types" : ["account_name"]
        }
    ]
    ...
}
```

#### Actions ABI
For the actions, we define the actions inside `actions` and the structure of the actions inside `structs`.
```json
{
    ...
    "structs": [{
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
    }],
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
  ]
    ...
}
```

### Deploy!
Now all the three files (tic_tac_toe.hpp, tic_tac_toe.cpp, tic_tac_toe.abi) are ready. Time to deploy!
```bash
$ eosc set contract tic.tac.toe tic_tac_toe.wast tic_tac_toe.abi
```
Ensure that your wallet is unlocked and you have `tic.tac.toe` key imported. If you are going to upload the contract to another account beside `tic.tac.toe`, replace `tic.tac.toe` with your account name and ensure you have the key for that account in your wallet

### Play!
After the deployment and the transaction is confirmed, the contract is already available in the blockchain. You can play with it now!

#### Create
```bash
$ eosc push message tic.tac.toe create '{"challenger":"inita", "host":"initb"}' -S initb -S tic.tac.toe -p initb@active 
```
#### Move
```bash
$ eosc push message tic.tac.toe move '{"challenger":"inita", "host":"initb", "by":"initb", "movement":{"row":0, "column":0} }' -S initb -S tic.tac.toe -p initb@active 
$ eosc push message tic.tac.toe move '{"challenger":"inita", "host":"initb", "by":"inita", "movement":{"row":1, "column":1} }' -S initb -S tic.tac.toe -p inita@active 
```
#### Restart
```bash
$ eosc push message tic.tac.toe restart '{"challenger":"inita", "host":"initb", "by":"initb"}' -S initb -S tic.tac.toe -p initb@active 
```
#### Close
```bash
$ eosc push message tic.tac.toe close '{"challenger":"inita", "host":"initb"}' -S initb -S tic.tac.toe -p initb@active
```
#### See the game status
```
$ eosc get table initb tic.tac.toe games
{
  "rows": [{
      "challenger": "inita",
      "host": "initb",
      "turn": "inita",
      "winner": "none",
      "board": [
        1,
        0,
        0,
        0,
        2,
        0,
        0,
        0,
        0
      ]
    }
  ],
  "more": false
}
```


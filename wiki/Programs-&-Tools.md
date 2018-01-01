* [Programs](#programs)
    * [eosd](#eosd)
    * [eosc](#eosc)
    * [eos-walletd](#eos-walletd)
    * [launcher](#launcher)
    * [snapshot](#snapshot)
* [Tools](#tools)
    * [eoscpp](#eoscpp)

## Programs

### eosd

The core EOS daemon that can be configured with plugins to run a node. Example uses are block production, dedicated API endpoints and local development. 

### eosc

`eosc` is a command line tool that interfaces with the REST api exposed by `eosd`. In order to use `eosc` you will need to have the end point (IP address and port number) to an `eosd` instance and also configure `eosc` to load the 'eosio::chain_api_plugin'. eosc contains documentation for all of its commands. For a list of all commands known to eosc, simply run it with no arguments:

```base
$ eosc
ERROR: RequiredError: Subcommand required
Command Line Interface to Eos Client
Usage: ./eosc [OPTIONS] SUBCOMMAND

Options:
  -h,--help                   Print this help message and exit
  -H,--host TEXT=localhost    the host where eosd is running
  -p,--port UINT=8888         the port where eosd is running
  --wallet-host TEXT=localhost
                              the host where eos-walletd is running
  --wallet-port UINT=8888     the port where eos-walletd is running
  -v,--verbose                output verbose messages on error

Subcommands:
  version                     Retrieve version information
  create                      Create various items, on and off the blockchain
  get                         Retrieve various items and information from the blockchain
  set                         Set or update blockchain state
  transfer                    Transfer EOS from account to account
  net                         Interact with local p2p network connections
  wallet                      Interact with local wallet
  benchmark                   Configure and execute benchmarks
  push                        Push arbitrary transactions to the blockchain
```

To get help with any particular subcommand, run it with no arguments as well:
```base
$ eosc create
ERROR: RequiredError: Subcommand required
Create various items, on and off the blockchain
Usage: ./eosc create SUBCOMMAND

Subcommands:
  key                         Create a new keypair and print the public and private keys
  account                     Create a new account on the blockchain
  producer                    Create a new producer on the blockchain

$ eosc create account
ERROR: RequiredError: creator
Create a new account on the blockchain
Usage: ./eosc create account [OPTIONS] creator name OwnerKey ActiveKey

Positionals:
  creator TEXT                The name of the account creating the new account
  name TEXT                   The name of the new account
  OwnerKey TEXT               The owner public key for the account
  ActiveKey TEXT              The active public key for the account

Options:
  -s,--skip-signature         Specify that unlocked wallet keys should not be used to sign transaction
  -x,--expiration             set the time in seconds before a transaction expires, defaults to 30s
  -f,--force-unique           force the transaction to be unique. this will consume extra bandwidth and remove any protections against accidently issuing the same transaction multiple times
  ```

### eos-walletd

An EOS wallet daemon that loads wallet related plugins, such as the HTTP interface and RPC API

### launcher

The launcher application simplifies the distribution of multiple eosd nodes across a LAN or a wider network. It can be configured via CLI to compose per-node configuration files, distribute these files securely amongst the peer hosts and then start up the multiple instances of eosd.

### snapshot

A submodule referencing `EOSIO/genesis` repository that contains a nodejs application for generating a snapshot from crowdsale contract, a web GUI for configuring a genesis block and other genesis related tools. 

## Tools

### eoscpp

#### Using eoscpp to generate the ABI specification file

**eoscpp** can generate the ABI specification file by inspecting the content of types declared in the contract source code.

To indicate that a type must be exported to the ABI (as an action or a table), the **@abi** annotation must be used in the **comment attached to the type declaration**.

The syntax for the annotation is as following.

- @abi action [name name2 ... nameN]
- @abi table [index_type name]
To generate the ABI file, **eoscpp** must be called with the **-g** option.

```base
➜ eoscpp -g abi.json types.hpp
Generated abi.json ...
```

**eoscpp** can also be used to generate helper functions that serialize/deserialize the types defined in the ABI spec.
```base
➜ eoscpp -g abi.json -gs types.hpp
Generated abi.json ...
Generated types.gen.hpp ...
```

#### Examples

#### Declaring an action
```base
#include <eoslib/types.hpp>
#include <eoslib/string.hpp>

//@abi action
struct action_name {
  uint64_t    param1;
  uint64_t    param2;
  eosio::string param3;
};
{
  "types": [],
  "structs": [{
      "name": "action_name",
      "base": "",
      "fields": {
        "param1": "uint64",
        "param2": "uint64",
        "param3": "string"
      }
    }
  ],
  "actions": [{
      "action_name": "actionname",
      "type": "action_name"
    }
  ],
  "tables": []
}
```

### Declaring multiple actions using the same interface.

```
#include <eoslib/types.hpp>
#include <eoslib/string.hpp>

//@abi action action1 action2
struct action_name {
  uint64_t param1;
  uint64_t param2;
  eosio::string   param3;
};
{
  "types": [],
  "structs": [{
      "name": "action_name",
      "base": "",
      "fields": {
        "param1": "uint64",
        "param2": "uint64",
        "param3": "string"
      }
    }
  ],
  "actions": [{
      "action_name": "action1",
      "type": "action_name"
    },{
      "action_name": "action2",
      "type": "action_name"
    }
  ],
  "tables": []
}
```

### Declaring a table

```base
#include <eoslib/types.hpp>
#include <eoslib/string.hpp>

//@abi table
struct my_table {
  uint64_t key;
};
{
  "types": [],
  "structs": [{
      "name": "my_table",
      "base": "",
      "fields": {
        "key": "uint64"
      }
    }
  ],
  "actions": [],
  "tables": [{
      "table_name": "mytable",
      "index_type": "i64",
      "key_names": [
        "key"
      ],
      "key_types": [
        "uint64"
      ],
      "type": "my_table"
    }
  ]
}
```
### Declaring a table with explicit index type

*a struct with 3 uint64_t can be both i64 or i64i64i64
```base
#include <eoslib/types.hpp>

//@abi table i64
struct my_new_table {
  uint64_t key;
  uint64_t name;
  uint64_t age;
};
{
  "types": [],
  "structs": [{
      "name": "my_new_table",
      "base": "",
      "fields": {
        "key": "uint64",
        "name": "uint64",
        "age": "uint64"
      }
    }
  ],
  "actions": [],
  "tables": [{
      "table_name": "mynewtable",
      "index_type": "i64",
      "key_names": [
        "key"
      ],
      "key_types": [
        "uint64"
      ],
      "type": "my_new_table"
    }
  ]
}
```

#### Declaring a table and an action that use the same struct.
```base
#include <eoslib/types.hpp>
#include <eoslib/string.hpp>

/*
 * @abi table
 * @abi action
 */ 
struct my_type {
  eosio::string key;
  eosio::name value;
};
{
  "types": [],
  "structs": [{
      "name": "my_type",
      "base": "",
      "fields": {
        "key": "string",
        "value": "name"
      }
    }
  ],
  "actions": [{
      "action_name": "mytype",
      "type": "my_type"
    }
  ],
  "tables": [{
      "table_name": "mytype",
      "index_type": "str",
      "key_names": [
        "key"
      ],
      "key_types": [
        "string"
      ],
      "type": "my_type"
    }
  ]
}
```

### Example of typedef exporting
```base
#include <eoslib/types.hpp>
struct simple {
  uint64_t u64;
};

typedef simple simple_alias;
typedef eosio::name name_alias;

//@abi action
struct action_one : simple_alias {
  uint32_t u32;
  name_alias name;
};
{
  "types": [{
      "new_type_name": "simple_alias",
      "type": "simple"
    },{
      "new_type_name": "name_alias",
      "type": "name"
    }
  ],
  "structs": [{
      "name": "simple",
      "base": "",
      "fields": {
        "u64": "uint64"
      }
    },{
      "name": "action_one",
      "base": "simple_alias",
      "fields": {
        "u32": "uint32",
        "name": "name_alias"
      }
    }
  ],
  "actions": [{
      "action_name": "actionone",
      "type": "action_one"
    }
  ],
  "tables": []
}
```

#### Using the generated serialization/deserialization functions
```base
#include <eoslib/types.hpp>
#include <eoslib/string.hpp>

struct simple {
  uint32_t u32;
  fixed_string16 s16;
};

struct my_complex_type {
  uint64_t u64;
  eosio::string str;
  simple simple;
  bytes bytes;
  public_key pub;
};

typedef my_complex_type complex;

//@abi action
struct test_action {
  uint32_t u32;
  complex cplx;
};
void apply( uint64_t code, uint64_t action ) {
   if( code == N(mycontract) ) {
      if( action == N(testaction) ) {
        auto msg = eosio::current_message<test_action>();
        eosio::print("test_action content\n");
        eosio::dump(msg);
         
        bytes b = eosio::raw::pack(msg);
        printhex(b.data, b.len);
     }
  }
}
```
### NOTE: table names and action names cannot use an underscore ("_").
### Calling contract with test values
```base
eosc push message mycontract testaction '{"u32":"1000", "cplx":{"u64":"472", "str":"hello", "bytes":"B0CA", "pub":"EOS8CY2pCW5THmzvPTgEh5WLEAxgpVFXaPogPvgvVpVWCYMRdzmwx", "simple":{"u32":"164","s16":"small-string"}}}' -S mycontract
```

#### Will produce the following output in eosd console
```base
test_action content
u32:[1000]
cplx:[
  u64:[472]
  str:[hello]
  simple:[
    u32:[164]
    s16:[small-string]
  ]
  bytes:[b0ca]
  pub:[03b41078f445628882fe8c1e629909cbbd67ff4b592b832264dac187ac730177f1]
]
e8030000d8010000000000000568656c6c6fa40000000c736d616c6c2d737472696e6702b0ca03b41078f445628882fe8c1e629909cbbd67ff4b592b832264dac187ac730177f1
```

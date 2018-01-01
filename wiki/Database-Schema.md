- [1. Primary Schema Relationships](#1-primary-schema-relationships)
- [2. Blocks](#2-blocks)
- [3. Transactions](#3-transaction)
- [4. Messages](#4-message)
- [5. Accounts](#5-accounts-collection)

## 1. Primary Schema Relationships

The following diagram shows the primary schemas for each collection in the database: [Block](#2-blocks), [Transaction](#3-transaction), [Message](#4-message), and [Account](#5-accounts-collection).  To increase performance of reads/queries and reduce overall storage requirements, we have chosen to not denormalize and nest these different entities to show relationships.  This shows the primary key for each collection document and any foreign keys as well.

![EOS Database Schema Diagram (Dawn 2.0)](assets/database_schema-diagram.png?raw=true)

**Conventions**

- Primary and Foreign key fields should end with `_id`, unless it’s a list of keys, in which case the field name should be the plural of the schema type of the referenced object.

## 2. Blocks

| Field                   | Type                       | Ref ID | Description                                        |
|-------------------------|----------------------------|--------|----------------------------------------------------|
| id                      | _String_                   | PK     | System unique id                                   |
| block_num               | _Integer_                  |        | Ordinal numeric identifier                         |
| previous                | _String_                   | FK     | SHA256 of previous block                           |
| timestamp               | _MongoDB Date (timestamp)_ |        | Scheduled time                                     |
| transaction_merkle_root | _String_                   |        | checksum (SHA256) of block when generated          |
| producer                | _String_                   | FK     | Account name of block producer                     |
| producer_signature      | _String_                   |        |                                                    |
| transactions            | _[ObjectId,...]_           |        | List of transaction ids associated with this block |
| ref_block_prefix        | _Integer_                  |        |                                                    |
| producer_changes        | _Array_                    |        | Changes to list of producers                       |


### Example
```
{
  "previous": "000000099271295c7e73dcf268802491f8d7e715608a6ec8182f0d4c4d6921bf",
  "timestamp": "2017-12-04T03:09:10",
  "transaction_merkle_root": "0000000000000000000000000000000000000000000000000000000000000000",
  "producer": "inita",
  "producer_changes": [],
  "producer_signature": "20621b7582a272a8ef15e0caa2590c279b706b851e9007ba558855c0b2844e0bb975481417ecbe7f3b5ffb488ec733f508c6455743bc26604d5f220bcd25e4f731",
  "cycles": [],
  "id": "0000000abf6baeb841293e7b6423f47e98517206595bbae4eb69281ca0501a57",
  "block_num": 10,
  "ref_block_prefix": 2067671361
}

```

## 3. Transaction

| Field                   | Type                       | Ref ID | Description                                        |
|-------------------------|----------------------------|--------|----------------------------------------------------|
| transaction_id          | _ObjectId_                 | **PK** | System unique id                                   |
| ref_block_num           | _Integer_                  |        | Reference block number                             |
| ref_block_prefix        | _Integer_                  |        | Reference block header                             |
| expiration              | _String_                   |        | Expiration time of transaction                     |
| scope                   | _Array_                    |        | Account scopes                                     |
| transaction_merkle_root | _String_                   |        | checksum (SHA256) of block when generated          |
| producer_account_id     | _String_                   | FK     | Account nmae of block producer                     |
| signatures              | _Array_                    |        | Array of signatures                                |


### Example
```
{
  "transaction_id": "f989025b959026f4d1e97346c0808b0fa316f7426384ce4ded83d52fde0404bf",
  "transaction": {
    "ref_block_num": 7284,
    "ref_block_prefix": 1294303748,
    "expiration": "2017-12-04T07:31:48",
    "scope": [
      "benchmark...3",
      "benchmark...i"
    ],
    "signatures": [
      "1f58d30c249bebfca299d485636b1bf6836df9df4a362221648f433897170fb70f1dc8933f70936d82266534883d187ba39f6fa7a448e881803c8c7530ff3afb18"
    ]
```

## 4. Message

| Field                   | Type                       | Ref ID | Description                                        |
|-------------------------|----------------------------|--------|----------------------------------------------------|
| code                 | _String_                |            | Name of contract                                           |
| type                 | _String_                |            | Name of action                                             |
| authorization        | _Nested_Document_       |            | Authorizing account and permission                         |  
| data                 | _Nested document_       |            | A nested document, any format, specific to message in use  |
| hex_data             | _String_                |            | Hexadecimal representation of data                         |


### Example
```
    "messages": [{
        "code": "eos",
        "type": "transfer",
        "authorization": [{
            "account": "benchmark...i",
            "permission": "active"
          }
        ],
        "data": {
          "from": "benchmark...i",
          "to": "benchmark...3",
          "amount": 1,
          "memo": "2017-12-04T07:31:19 1512372679244267"
        },
        "hex_data": "0e0080d7c886a63a030080d7c886a63a010000000000000024323031372d31322d30345430373a33313a31392031353132333732363739323434323637"
      }
    ]
```

### Authorization Nested Document

| Field                | Type                    | Ref ID     | Description                                                |
|----------------------|-------------------------|------------|------------------------------------------------------------|
| account              | _String_                | FK         | Authorizing account name                                   |
| permission           | _Permission_            |            | Permission used to authorize transaction                   |


### Example
```
        "authorization": [{
            "account": "benchmark...i",
            "permission": "active"
          }
        ]
```


## 5. Accounts (Collection)

| Field                | Type                    | Ref ID | Description                          |
|----------------------|-------------------------|--------|--------------------------------------|
| name                 | _String_                | **PK** | Account Name                         |
| eos_balance          | _String_                |        | Balance                              |
| staked_balance       | _String_                |        | Staked balance                       |
| unstaking_balance    | _String_                |        | Unstaking balance                    |
| last_unstaking_time  | _Date (timestamp)_)     |        | Timestamp of last modified date/time |
| permissions          | _[Nested document,...]_ |        | Nested permission structure          |


### Example

```
{
  "account_name": "inita",
  "eos_balance": "999977.9995 EOS",
  "staked_balance": "0.0000 EOS",
  "unstaking_balance": "0.0000 EOS",
  "last_unstaking_time": "1969-12-31T23:59:59",
  "permissions": [{
      "perm_name": "active",
      "parent": "owner",
      "required_auth": {
        "threshold": 1,
        "keys": [{
            "key": "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
            "weight": 1
          }
        ],
        "accounts": []
      }
    },{
      "perm_name": "owner",
      "parent": "",
      "required_auth": {
        "threshold": 1,
        "keys": [{
            "key": "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
            "weight": 1
          }
        ],
        "accounts": []
      }
    }
  ]
}
```

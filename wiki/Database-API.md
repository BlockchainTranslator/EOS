APIs that store and retrieve data on the blockchain EOS.IO

![enter image description here](https://eosio.github.io/eos/group__database.png)

**Table of Contents**

- [1. Overview](#1-overview)
- [2. Modules](#2-modules)
  * [2.1 Database C API](#21-database-c-api)
    + [2.1.1 Single String Index Table](#211-single-string-index-table)
    + [2.1.2 Single 64 bit Index Table](#212-single-64-bit-index-table)
    + [2.1.3 Dual 128 bit Index Table](#213-dual-128-bit-index-table)
    + [2.1.4 Triple 64 bit Index Table](#214-triple-64-bit-index-table)
  * [2.2 Database C++ API](#22-database-c-api)
    + [2.2.1 Single Index Table](#221-single-index-table)
    + [2.2.2 Dual Index Table](#222-dual-index-table)
- [3. Indexes](#3-indexes)
  * [3.1 Primary Index](#31-primary-index)
    + [3.1.1 Description](#311-description)
    + [3.1.2 Static Public Member Functions](#312-static-public-member-functions)
  * [3.2 Secondary Index](#32-secondary-index)
    + [3.2.1 Description](#321-description)
    + [3.2.2 Static Public Member Functions](#322-static-public-member-functions)

## **1. Overview**
The data are organized according to the following broad structure:

 - Scope - an account where the data is stored
 - Code - the account name which has write permission
 - Table - a name for the table that is being stored
 - Record - a row in the table

Every transaction specifies the set of valid scopes that may be read and/or written to. The code that is running determines what can be written to; therefore, write operations do not allow you to specify/configure the code.

> **Note:**
Attempts to read and/or write outside the valid scope and/or code sections will cause your transaction to fail.

The database APIs assume that the first bytes of each record represent the primary and/or secondary keys followed by an arbitrary amount of data.

## **2. Modules**

### **2.1 Database C API**
C APIs for interfacing with the database.

![enter image description here](https://eosio.github.io/eos/group__database_c.png)

#### **2.1.1 Single String Index Table**
These methods interface with a simple table with String unique primary key and arbitrary binary data value. 

![enter image description here](https://eosio.github.io/eos/group__dbstr.png)

##### **2.1.1.1 Function Documentation**

###### **store_str**

    int32_t store_str (account_name scope, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Parameters*

 - scope - the account scope that will be read, must exist in the transaction scopes list
 - table	- the ID/name of the table within the current scope/code context to modify

*Returns*

1 if a new record was created, 0 if an existing record was updated

*Precondition*

datalen >= sizeof(uint64_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((Name*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

a record is either created or updated with the given scope and table.

*Exceptions*

if	called with an invalid precondition execution will be aborted

###### **update_str**

    int32_t update_str (account_name scope, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Returns*

1 if the record was updated, 0 if no record with key was found

###### **load_str**

    int32_t load_str (account_name scope, account_name code, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Parameters*

 - scope - the account scope that will be read, must exist in the transaction scopes list
 - code - identifies the code that controls write-access to the data
 - table - the ID/name of the table within the scope/code context to query
 - data - location to copy the stored record, should be initialized with the key to get
 - datalen - the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if key was not found

###### **front_str**

    int32_t front_str (account_name scope, account_name code, table_name table, char *value, uint32_t valuelen)

###### **back_str**

    int32_t back_str (account_name scope, account_name code, table_name table, char *value, uint32_t valuelen)

###### **next_str**

    int32_t next_str (account_name scope, account_name code, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

###### **previous_str**

    int32_t previous_str (account_name scope, account_name code, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

###### **lower_bound_str**

    int32_t lower_bound_str (account_name scope, account_name code, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

###### **upper_bound_str**

    int32_t upper_bound_str (account_name scope, account_name code, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Returns*

1 if the record was updated, 0 if no record with key was found

###### **remove_str**

    int32_t remove_str (account_name scope, table_name table, char *key, uint32_t keylen)

*Parameters*

 - data	- must point to at least 8 bytes containing primary key

*Returns*

1 if a record was removed, and 0 if no record with key was found

#### **2.1.2 Single 64 bit Index Table**
These methods interface with a simple table with 64 bit unique primary key and arbitrary binary data value. 

![enter image description here](https://eosio.github.io/eos/group__dbi64.png)

##### **2.1.2.1 Example**

```
#pragma pack(push, 1)
struct test_model {
   account_name   name;
   unsigned char age;
   uint64_t      phone;
};

test_model alice{ N(alice), 20, 4234622};
test_model bob  { N(bob),   15, 11932435};
test_model carol{ N(carol), 30, 545342453};
test_model dave { N(dave),  46, 6535354};

int32_t res = store_i64(currentCode(),  N(test_table), &dave,  sizeof(test_model));
res = store_i64(currentCode(), N(test_table), &carol, sizeof(test_model));
res = store_i64(currentCode(), N(test_table), &bob, sizeof(test_model));
res = store_i64(currentCode(), N(test_table), &alice, sizeof(test_model));

test_model alice;
alice.name = N(alice);

res = load_i64( currentCode(), currentCode(), N(test_table), &alice, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && tmp.name == N(alice) && tmp.age == 20 && tmp.phone == 4234622, "load_i64");

res = front_i64( currentCode(), currentCode(), N(test_table), &tmp, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && tmp.name == N(alice) && tmp.age == 20 && tmp.phone == 4234622, "front_i64 1");

res = back_i64( currentCode(), currentCode(), N(test_table), &tmp, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && tmp.name == N(dave) && tmp.age == 46 && tmp.phone == 6535354, "back_i64 2");

res = previous_i64( currentCode(), currentCode(), N(test_table), &tmp, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && tmp.name == N(carol) && tmp.age == 30 && tmp.phone == 545342453, "carol previous");

res = next_i64( currentCode(), currentCode(), N(test_table), &tmp, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && tmp.name == N(dave) && tmp.age == 46 && tmp.phone == 6535354, "back_i64 2");

uint64_t key = N(alice);
res = remove_i64(currentCode(), N(test_table), &key);
ASSERT(res == 1, "remove alice");

test_model lb;
lb.name = N(bob);

res = lower_bound_i64( currentCode(), currentCode(), N(test_table), &lb, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && lb.name == N(bob), "lower_bound_i64 bob" );

test_model ub;
ub.name = N(alice);

res = upper_bound_i64( currentCode(), currentCode(), N(test_table), &ub, sizeof(test_model) );
ASSERT(res == sizeof(test_model) && ub.age == 15 && ub.name == N(bob), "upper_bound_i64 bob" );
```

##### **2.1.2.2 Function Documentation**

###### **store_i64**

    int32_t store_i64 (account_name scope, table_name table, const void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the current scope/code context to modify

*Returns*

1 if a new record was created, 0 if an existing record was updated

*Precondition*

datalen >= sizeof(uint64_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint64_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

a record is either created or updated with the given scope and table.

*Exceptions*
if	called with an invalid precondition execution will be aborted

###### **update_i64**

    int32_t update_i64 (account_name scope, table_name table, const void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the current scope/code context to modify

*Returns*

1 if the record was updated, 0 if no record with key was found

*Precondition*

datalen >= sizeof(uint64_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint64_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

a record is either created or updated with the given scope and table.

*Exceptions*

if	called with an invalid precondition execution will be aborted


###### **load_i64**

    int32_t load_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the stored record, should be initialized with the key to get
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if key was not found

###### **front_i64**

    int32_t front_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **back_i64**

    int32_t back_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

- the number of bytes read or -1 if no record found

###### **next_i64**

    int32_t next_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record. Should be initialized with the key to get next record.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if key was not found

###### **previous_i64**

    int32_t previous_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record. Should be initialized with the key to get previous record.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if key was not found

###### **lower_bound_i64**

    int32_t lower_bound_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound. Should be initialized with the key to find lower bound of.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if key was not found

###### **upper_bound_i64**

    int32_t upper_bound_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound. Should be initialized with the key to find upper bound of.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if key was not found

###### **remove_bound_i64**

    int32_t remove_i64 (account_name scope, table_name table, void *data)

*Parameters*

- scope	- the account socpe that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table withing the scope/code context to query
- data	- must point to at lest 8 bytes containing primary key

*Returns*

1 if a record was removed, and 0 if no record with key was found

#### **2.1.3 Dual 128 bit Index Table**
Interface to a database table with 128 bit primary and secondary keys and arbitary binary data value. 

![enter image description here](https://eosio.github.io/eos/group__dbi128i128.png)

##### **2.1.3.1 Description**

*Parameters*

- scope	- the account where table data will be found
- code	- the code which owns the table
- table	- the name of the table where record is stored
- data	- a pointer to memory that is at least 32 bytes long
- len	- the length of data, must be greater than or equal to 32 bytes

*Returns*

the total number of bytes read or -1 for "not found" or "end" where bytes read includes 32 bytes of the key
These methods assume a database table with records of the form:

> struct record {
   uint128  primary;
   uint128  secondary;
   ... arbitrary data ...
};

You can iterate over these indicies with primary index sorting records by { primary, secondary } and the secondary index sorting records by { secondary, primary }. This means that duplicates of the primary or secondary values are allowed so long as there are no duplicates of the combination {primary, secondary}.

##### **2.1.3.2 Example**

```
struct test_model128x2 {
    uint128_t number;
    uint128_t price;
    uint64_t  extra;
    uint64_t  table_name;
};
 
test_model128x2 alice{0, 500, N(alice), N(table_name)};
test_model128x2 bob{1, 1000, N(bob), N(table_name)};
test_model128x2 carol{2, 1500, N(carol), N(table_name)};
test_model128x2 dave{3, 2000, N(dave), N(table_name)};
 
int32_t res = store_i128i128(CurrentCode(), N(table_name), &alice, sizeof(test_model128x2));
res = store_i128i128(CurrentCode(), N(table_name), &bob, sizeof(test_model128x2));
ASSERT(res == 1, "db store failed");
res = store_i128i128(CurrentCode(), N(table_name), &carol, sizeof(test_model128x2));
ASSERT(res == 1, "db store failed");
res = store_i128i128(CurrentCode(), N(table_name), &dave, sizeof(test_model128x2));
ASSERT(res == 1, "db store failed");
 
test_model128x2 query;
query.number = 0;
 
res = load_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 0 && query.price == 500 && query.extra == N(alice), "load");
 
res = front_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 3 && query.price = 2000 && query.extra == N(dave), "front");
 
res = next_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), & query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 2 && query.price == 1500 && query.extra == N(carol), "next");
 
res = back_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 0 && query.price == 500 && query.extra == N(alice), "back");
 
res = previous_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 1 && query.price == 1000 && query.extra == N(bob), "previous");
 
query.number = 0;
res = lower_bound_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 0 && query.price == 500 && query.extra == N(alice), "lower");
 
res = upper_bound_primary_i128i128(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 1 && query.price == 1000 && query.extra == N(bob), "upper");

query.extra = N(bobby);
res = update_i128128(CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == sizeof(test_model128x2) && query.number == 1 & query.price == 1000 && query.extra == N(bobby), "update");

res = remove_i128128(CurrentCode(), N(table_name), &query, sizeof(test_model128x2));
ASSERT(res == 1, "remove")
```

##### **2.1.3.3 Function Documentation**

###### **load_primary_i128i128**

    int32_t 	load_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the primary key to load
- len	- length of record to copy

*Returns*

the number of bytes read, -1 if key was not found

*Precondition*

len >= sizeof(uint128_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint128_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

data will be initialized with the len bytes of record matching the key.

*Exceptions*

if	called with an invalid precondition execution will be aborted

###### **front_primary_i128i128**

    int32_t front_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **back_primary_i128i128**

    int32_t back_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **next_primary_i128i128**

    int32_t next_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record of primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **previous_primary_i128i128**

    int32_t previous_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)
 
*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record of primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **upper_bound_primary_i128i128**

    int32_t upper_bound_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of a primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **lower_bound_primary_i128i128**

    int32_t lower_bound_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of a primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **load_secondary_i128i128**

    int32_t load_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the secondary key to load
- len	- length of record to copy

*Returns*

the number of bytes read, -1 if key was not found

*Precondition*

len >= sizeof(uint128_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint128_t*)data) stores the secondary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

data will be initialized with the len bytes of record matching the key.

*Exceptions*

if	called with an invalid precondition execution will be aborted

###### **front_secondary_i128i128**

    int32_t front_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **back_secondary_i128i128**

    int32_t back_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **next_secondary_i128i128**

    int32_t next_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record of secondary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **previous_secondary_i128i128**

    int32_t previous_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record of secondary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **upper_bound_secondary_i128i128**

    int32_t upper_bound_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of a primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **lower_bound_secondary_i128i128**

    int32_t lower_bound_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of given secondary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found

###### **remove_i128i128**

    int32_t remove_i128i128 (account_name scope, table_name table, const void *data)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the scope/code context to query
- data	- must point to at lest 32 bytes containing {primary,secondary}

*Returns*

1 if a record was removed, and 0 if no record with key was found

###### **store_i128i128**

    int32_t store_i128i128 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the scope/code context to query
- data	- must point to a at least 32 bytes containing (primary, secondary)
- len	- the length of the data

*Returns*

1 if a new record was created, 0 if an existing record was updated 

###### **update_i128i128**

    int32_t update_i128i128 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the scope/code context to query
- data	- must to a at least 32 bytes containing (primary, secondary)
- len	- the length of the data

*Returns*

1 if the record was updated, 0 if no record with key was found

#### **2.1.4 Triple 64 bit Index Table**
Interface to a database table with 64 bit primary, secondary and tertiary keys and arbitrary binary data value. 

![enter image description here](https://eosio.github.io/eos/group__dbi64i64i64.png)

##### **2.1.4.1 Description**

*Parameters*

- scope	- the account where table data will be found
- code	- the code which owns the table
- table	- the name of the table where record is stored
- data	- a pointer to memory that is at least 32 bytes long
- len	- the length of data, must be greater than or equal to 32 bytes

*Returns*

the total number of bytes read or -1 for "not found" or "end" where bytes read includes 24 bytes of the key
These methods assume a database table with records of the form:

> struct record {
   uint64  primary;
   uint64  secondary;
   uint64  tertiary;
   ... arbitrary data ...
};

You can iterate over these indices with primary index sorting records by { primary, secondary, tertiary }, the secondary index sorting records by { secondary, tertiary } and the tertiary index sorting records by { tertiary }.

##### **2.1.4.2 Example**

```
struct test_model3xi64 {
       uint64_t a;
       uint64_t b;
       uint64_t c;
       uint64_t name;
};

test_model3xi64 alice{ 0, 0, 0, N(alice) };
test_model3xi64 bob{ 1, 1, 1, N(bob) };
test_model3xi64 carol{ 2, 2, 2, N(carol) };
test_model3xi64 dave{ 3, 3, 3, N(dave) };

int32_t res = store_i64i64i64(CurrentCode(), N(table_name), &alice, sizeof(test_model3xi64));
res = store_i64i64i64(CurrentCode(), N(table_name), &bob, sizeof(test_model3xi64));
res = store_i64i64i64(CurrentCode(), N(table_name), &carol, sizeof(test_model3xi64));
res = store_i64i64i64(CurrentCode(), N(table_name), &dave, sizeof(test_model3xi64));

test_model3xi64 query;
query.a = 0;
res = load_primary_i64i64i64(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model3xi64));
ASSERT(res == sizeof(test_model3xi64) && query.name == N(alice), "load");

res = front_primary_i64i64i64(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model3xi64));
ASSERT(res == sizeof(test_model3xi64) && query.name == N(dave), "front");

res = back_primary_i64i64i64(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model3xi64));
ASSERT(res == sizeof(test_model3xi64) && query.name == N(alice), "back");

res = previous_primary_i64i64i64(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model3xi64));
ASSERT(res == sizeof(test_model3xi64) && query.name == N(bob), "previous");

res = next_primary_i64i64i64(CurrentCode(), CurrentCode(), N(table_name), &query, sizeof(test_model3xi64));
ASSERT(res == sizeof(test_model3xi64) && query.name == N(alice), "next");*
```

##### **2.1.4.3 Function Documentation**

###### **load_primary_i64i64i64**
    int32_t load_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the (primary,secondary,tertiary) to load
- len	- length of record to copy

*Returns*

the number of bytes read, -1 if key was not found

*Precondition*

data is a valid pointer to a range of memory at least len bytes long
*((uint64_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

data will be initialized with the len bytes of record matching the key.

*Exceptions*

if	called with an invalid precondition execution will be aborted
 
###### **front_primary_i64i64i64**
    int32_t front_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **back_primary_i64i64i64**
    int32_t back_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **next_primary_i64i64i64**
    int32_t next_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record of primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **previous_primary_i64i64i64**
    int32_t previous_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record of primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **upper_bound_primary_i64i64i64**
    int32_t upper_bound_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of a primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **lower_bound_primary_i64i64i64**
    int32_t lower_bound_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **load_secondary_i64i64i64**
    int32_t load_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the (secondary,tertiary) to load
- len	- length of record to copy

*Returns*

the number of bytes read, -1 if key was not found

*Precondition*

data is a valid pointer to a range of memory at least len bytes long
*((uint64_t*)data) stores the secondary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

data will be initialized with the len bytes of record matching the key.

*Exceptions*

if	called with an invalid precondition execution will be aborted
 
###### **front_secondary_i64i64i64**
    int32_t front_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of a secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **back_secondary_i64i64i64**
    int32_t back_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **next_secondary_i64i64i64**
    int32_t next_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **previous_secondary_i64i64i64**
    int32_t previous_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **upper_bound_secondary_i64i64i64**
    int32_t upper_bound_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of tertiary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **lower_bound_secondary_i64i64i64**
    int32_t lower_bound_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of secondary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **load_tertiary_i64i64i64**
    int32_t load_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the (tertiary) to load
- len	- length of record to copy

*Returns*

the number of bytes read, -1 if key was not found

*Precondition*

data is a valid pointer to a range of memory at least len bytes long
*((uint64_t*)data) stores the tertiary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*Postcondition*

data will be initialized with the len bytes of record matching the key.

*Exceptions*

if	called with an invalid precondition execution will be aborted
 
###### **front_tertiary_i64i64i64**
    int32_t front_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of a tertiary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **back_tertiary_i64i64i64**
    int32_t back_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of a tertiary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **next_tertiary_i64i64i64**
    int32_t next_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **previous_tertiary_i64i64i64**
    int32_t previous_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **upper_bound_tertiary_i64i64i64**
    int32_t upper_bound_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

scope	- the account scope that will be read, must exist in the transaction scopes list
code	- identifies the code that controls write-access to the data
table	- the ID/name of the table within the scope/code context to query
data	- location to copy the upper bound of tertiary key; must be initialized with a key value
len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **lower_bound_tertiary_i64i64i64**
    int32_t lower_bound_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of tertiary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*Returns*

the number of bytes read or -1 if no record found
 
###### **remove_i64i64i64**
    int32_t remove_i64i64i64 (account_name scope, table_name table, const void *data)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the name of table where record is stored
- data	- must point to at least 24 bytes containing {primary,secondary,tertiary}

*Returns*

1 if a record was removed, and 0 if no record with key was found
 
###### **store_i64i64i64**
    int32_t store_i64i64i64 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the name of table where record is stored
- data	- must point to at least 24 bytes containing (primary,secondary,tertiary)
- len	- length of the data

*Returns*
1 if a new record was created, 0 if an existing record was updated
 
###### **update_i64i64i64**
    int32_t update_i64i64i64 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the name of table where record is stored
- data	- must point to at least 24 bytes containing (primary,secondary,tertiary)
- len	- length of the data

*Returns*
1 if the record was updated, 0 if no record with key was found

### **2.2 Database C++ API**
C++ APIs for interfacing with the database, it provides a simple interface for storing any fixed-size struct as a database row.

![enter image description here](https://eosio.github.io/eos/group__database_cpp.png)

#### **2.2.1 Single Index Table**

This specialization of Table is for single-index tables

![enter image description here](https://eosio.github.io/eos/group___singleindextable.png)

##### **2.2.1.1 Description**

###### **Classes**

> struct  	table < scope, code, table, Record, PrimaryType, void >

> struct  	[primary_index](#31-primary-index)

###### **Public Types**
Primary

> typedef PrimaryType 	primary

> typedef PrimaryType 	table < scope, code, table, Record, PrimaryType, void >::Primary

###### **Parameters**

- scope	- the default account name scope that this table is located within
- code	- the code account name which has write permission to this table
- table	- a unique identifier (name) for this table
- Record	- the type of data stored in each row
- PrimaryType	- the type of the first field stored in Record

##### **2.2.1.2 Example**

```
struct MyModel {
   uint128_t number;
   uint64_t  name;
};

typedef table <N(myscope), N(mycode), N(mytable), MyModel, uint128_t> MyTable;

MyModel a { 1, N(one) };
MyModel b { 2, N(two) };
MyModel c { 3, N(three) };
MyModel d { 4, N(four) };

bool res = MyTable::store(a);
ASSERT(res, "store");

res = MyTable::store(b);
ASSERT(res, "store");

res = MyTable::store(c);
ASSERT(res, "store");

res = MyTable::store(d);
ASSERT(res, "store");

MyModel query;
res = MyTable::front(query);
ASSERT(res && query.number == 4 && query.name == N(four), "front");

res = MyTable::back(query);
ASSERT(res && query.number == 1 && query.name == N(one), "back");

res = MyTable::primary_index::previous(query);
ASSERT(res && query.number == 2 && query.name == N(two), "previous");

res = MyTable::primary_index::next(query);
ASSERT(res && query.number == 1 && query.name == N(one), "next");

query.number = 4;
res = MyTable::get(query);
ASSERT(res && query.number == 4 && query.name = N(four), "get");

query.name = N(Four);
res = MyTable.update(query);
ASSERT(res && query.number == 4 && query.name == N(Four), "update");

res = MyTable.remove(query);
ASSERT(res, "remove");

res = MyTable.get(query);
ASSERT(!res, "get of removed record");
```

##### **2.2.1.3 Static Public Member Functions**

###### **front (Record &r)**
    static bool front (Record &r)

    static bool table< scope, code, table, Record, PrimaryType, void >::front (Record & r)	

fetches the front of the table

*Parameters*

- r	- reference to hold the value

*Returns*

true if successfully retrieved the front

###### **back (Record &r)**
    static bool back (Record &r)

    static bool table< scope, code, table, Record, PrimaryType, void >::back (Record & r)	

fetches the back of the table

*Parameters*

r	- reference to hold the value

*Returns*

true if successfully retrieved the back

###### **get (const PrimaryType &p, Record &r, uint64_t s=scope)**
    static bool get (const PrimaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::get	(const PrimaryType &p, Record &r, uint64_t s=scope)

retrieves the record for the specified primary key

*Parameters*

- p	- the primary key of the record to fetch
- r	- reference of record to hold return value
- s	- scope; defaults to scope of the class.

*Returns*

true if get succeeds.

###### **get (Record &r, uint64_t s=scope)**

    static bool get (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::get	(Record & 	r, uint64_t s = scope)	

retrieves a record based on initialized primary key value

*Parameters*

r	- reference of a record to hold return value; must be initialized to the primary key to be fetched.
s	- scope; defaults to scope of the class.

*Returns*

true if get succeeds.
 
###### **store (const Record &r, uint64_t s=scope)**

    static bool store (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::store (const Record & r, uint64_t s = scope)	

store a record to the table

*Parameters*

- r	- the record to be stored.
- s	- scope; defaults to scope of the class.

*Returns*

true if store succeeds.

###### **update (const Record &r, uint64_t s=scope)**

    static bool update (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::store (const Record & r, uint64_t s = scope)

store a record to the table

*Parameters*

- r	- the record to be stored.
- s	- scope; defaults to scope of the class.

*Returns*

true if store succeeds.

###### **static bool remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::remove (const Record & r, uint64_t 	s = scope)	

remove a record from the table.

*Parameters*

- r	- the record to be removed.
- s	- scope; defaults to scope of the class.

*Returns*

true if remove succeeds.

#### **2.2.2 Dual Index Table**
defines a type-safe C++ wrapper around the Database C API

![enter image description here](https://eosio.github.io/eos/group__dual_index_table.png)

##### **2.2.2.1 Description**

###### **Classes**

> class  	table< scope, code, table, Record, PrimaryType, SecondaryType >

> struct  	[primary_index](#31-primary-index)

> struct  	[secondary_index](#32-secondary-index)

###### **Public Type**
Primary
> typedef PrimaryType 	primary

> typedef PrimaryType table< scope, code, table, Record, PrimaryType, SecondaryType >::Primary

Secondary
> typedef SecondaryType 	secondary

> typedef SecondaryType table< scope, code, table, Record, PrimaryType, SecondaryType >::Secondary


###### **Parameters**

- scope	- the default account name/scope that this table is located within
- code	- the code account name which has write permission to this table
- table	- a unique identifier (name) for this table
- Record	- the type of data stored in each row
- PrimaryType	- the type of the first field stored in Record
- SecondaryType	- the type of the second field stored in Record

The primary and secondary indices are sorted as N-bit unsigned integers from lowest to highest.

##### **2.2.2.2 Example**

```
struct Model {
    uint64_t primary;
    uint64_t secondary;
    uint64_t value;
};

typedef table <N(myscope), N(mycode), N(mytable), Model, uint64_t, uint64_t> MyTable;
Model a { 1, 11, N(first) };
Model b { 2, 22, N(second) };
Model c { 3, 33, N(third) };
Model d { 4, 44, N(fourth) };

bool res = MyTable::store(a);
ASSERT(res, "store");

res = MyTable::store(b);
ASSERT(res, "store");

res = MyTable::store(c);
ASSERT(res, "store");

res = MyTable::store(d);
ASSERT(res, "store");

Model query;
res = MyTable::primary_index::get(1, query);
ASSERT(res && query.primary == 1 && query.value == N(first), "first");

res = MyTable::primary_index::front(query);
ASSERT(res && query.primary == 4 && query.value == N(fourth), "front");

res = MyTable::primary_index::back(query);
ASSERT(res && query.primary == 1 && query.value == N(first), "back");

res = MyTable::primary_index::previous(query);
ASSERT(res && query.primary == 2 && query.value == N(second), "previous");

res = MyTable::primary_index::next(query);
ASSERT(res && query.primary == 1 && query.value == N(first), "first");

res = MyTable::secondary_index::get(11, query);
ASSERT(res && query.primary == 11 && query.value == N(first), "first");

res = MyTable::secondary_index::front(query);
ASSERT(res && query.secondary == 44 && query.value == N(fourth), "front");

res = MyTable::secondary_index::back(query);
ASSERT(res && query.secondary == 11 && query.value == N(first), "back");

res = MyTable::secondary_index::previous(query);
ASSERT(res && query.secondary == 22 && query.value == N(second), "previous");

res = MyTable::secondary_index::next(query);
ASSERT(res && query.secondary == 11 && query.value == N(first), "first");

res = MyTable::remove(query);
ASSERT(res, "remove");

res = MyTable::get(query);
ASSERT(!res, "not found already removed");
```

##### **2.2.2.3 Static Public Member Functions**

###### **get (const PrimaryType &p, Record &r, uint64_t s=scope)**

    static bool get (const PrimaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::get(const PrimaryType & p, Record & r, uint64_t s = scope)	

*Parameters*

- p	- reference to primary key to retrieve
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

###### **store (const Record &r, uint64_t s=scope)**

    static bool store (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::store (const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store.
- s	- account scope. default is current scope of the class

*Returns*

true if successful store.

###### **update (const Record &r, uint64_t s=scope)**

    static bool update (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::update	(const Record & r, uint64_t s = scope)	

*Parameters*

- r	- reference to a record to update.
- s	- account scope. default is current scope of the class

*Returns*

true if successful update.

###### **remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::remove	(const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to remove.
- s	- account scope. default is current scope of the class

*Returns*

true if successful remove.

## **3. Indexes**

### **3.1 Primary Index**

#### **3.1.1 Description**
The Primary Index

    table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index Struct Reference

#### **3.1.2 Static Public Member Functions**

##### **front (Record &r, uint64_t s=scope)**

    static bool front (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::front (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store the front record based on primary index.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **back (Record &r, uint64_t s=scope)**

    static bool back (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::back (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store the back record based on primary index.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **next (Record &r, uint64_t s=scope)**

    static bool next (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::next (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store next value; must be initialized with current.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **previous (Record &r, uint64_t s=scope)**

    static bool previous (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::previous (Record & r, uint64_t s = scope)	

*Parameters*

- r	- reference to a record to store previous value; must be initialized with current.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **get (const PrimaryType &p, Record &r, uint64_t s=scope)**

    static bool get (const PrimaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::get (const PrimaryType & p, Record & r, uint64_t s = scope)	

*Parameters*

- p	- reference to primary key to load; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **lower_bound (const PrimaryType &p, Record &r)**

    static bool lower_bound (const PrimaryType &p, Record &r)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::lower_bound (const PrimaryType & p, Record & r )

*Parameters*

- p	- reference to primary key to get the lower bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **upper_bound (const PrimaryType &p, Record &r)**

    static bool upper_bound (const PrimaryType &p, Record &r)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::upper_bound (const PrimaryType & p, Record & r )	

*Parameters*

- p	- reference to primary key to get the upper bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::remove	(const Record & r, uint64_t s = scope)	

*Parameters*

- r	- reference to a record to remove from table;
- s	- account scope. default is current scope of the class

*Returns*

true if successfully removed;

### **3.2 Secondary Index**

#### **3.2.1 Description**
The Secondary Index.

    table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index Struct Reference

#### **3.2.2 Static Public Member Functions**

##### **front (Record &r, uint64_t s=scope)**

    static bool front (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::front (Record & r, uint64_t s = scope)

*Parameters*

r	- reference to a record to store the front record based on secondary index.
s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **back (Record &r, uint64_t s=scope)**

    static bool back (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::back	(Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store the back record based on secondary index.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **next (Record &r, uint64_t s=scope)**

    static bool next (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::next	(Record & r, uint64_t s = scope)	

*Parameters*

- r	- reference to a record to return the next record .
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **previous (Record &r, uint64_t s=scope)**

    static bool previous (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::previous	(Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to return the next record.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **get (const SecondaryType &p, Record &r, uint64_t s=scope)**

    static bool get (const SecondaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::get (const SecondaryType & p, Record & r, uint64_t s = scope)	

*Parameters*

- p	- reference to secondary index key
- r	- reference to record to hold the value
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **lower_bound (const SecondaryType &p, Record &r, uint64_t s=scope)**

    static bool lower_bound (const SecondaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::lower_bound (const SecondaryType & p, Record & r, uint64_t s = scope)
 
*Parameters*

- p	- reference to secondary key to get the lower bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **upper_bound (const SecondaryType &p, Record &r, uint64_t s=scope)**

    static bool upper_bound (const SecondaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::upper_bound (const SecondaryType & p, Record & r, uint64_t s = scope)

*Parameters*

- p	- reference to secondary key to get the upper bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*Returns*

true if successful read.

##### **remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::remove (const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to be removed.
- s	- account scope. default is current scope of the class

*Returns*

true if successfully removed.



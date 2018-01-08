APIs that store and retrieve data on the blockchain EOS.IO

![enter image description here](https://eosio.github.io/eos/group__database.png)

**Table of Contents**

- [1. Overview | 概观](#1-overview)
- [2. Modules | 模块](#2-modules)
  * [2.1 Database C API | 数据库 C API](#21-database-c-api)
    + [2.1.1 Single String Index Table | 单字符串索引表](#211-single-string-index-table)
    + [2.1.2 Single 64 bit Index Table | 单64位索引表](#212-single-64-bit-index-table)
    + [2.1.3 Dual 128 bit Index Table | 双128位索引表](#213-dual-128-bit-index-table)
    + [2.1.4 Triple 64 bit Index Table |三重64位索引表](#214-triple-64-bit-index-table)
  * [2.2 Database C++ API　| 数据库　C++ API](#22-database-c-api)
    + [2.2.1 Single Index Table | 单索引表](#221-single-index-table)
    + [2.2.2 Dual Index Table | 双索引表](#222-dual-index-table)
- [3. Indexes | 索引](#3-indexes)
  * [3.1 Primary Index | 主索引](#31-primary-index)
    + [3.1.1 Description　| 描述](#311-description)
    + [3.1.2 Static Public Member Functions | 静态公有成员函数](#312-static-public-member-functions)
  * [3.2 Secondary Index | 次级索引](#32-secondary-index)
    + [3.2.1 Description | 描述](#321-description)
    + [3.2.2 Static Public Member Functions | 静态公有成员函数](#322-static-public-member-functions)

## **1. Overview**
## **1. 概观**
The data are organized according to the following broad structure:

 - Scope - an account where the data is stored
 - Code - the account name which has write permission
 - Table - a name for the table that is being stored
 - Record - a row in the table

 数据是按照以下广泛的结构进行组织：

   - 范围 - 存储数据的帐户
   - 代码 - 具有写入权限的帐户名称
   - 表格 - 正在存储的表格的名称
   - 记录 - 表中的一行

Every transaction specifies the set of valid scopes that may be read and/or written to. The code that is running determines what can be written to; therefore, write operations do not allow you to specify/configure the code.

每个事务都需指定可以读取和/或写入的有效范围集合。正在运行的代码决定了可以写入的内容; 因此，写入操作不允许您指定/配置代码。

> **Note:**
Attempts to read and/or write outside the valid scope and/or code sections will cause your transaction to fail.
> **注意：**
尝试在有效的作用域和/或代码段之外进行读取和/或写入将导致事务失败。


The database APIs assume that the first bytes of each record represent the primary and/or secondary keys followed by an arbitrary amount of data.

数据库API假设每个记录的第一个字节代表主键和/或辅助键，后面跟随着任意数量的数据。

## **2. Modules**
## **2. 模块**

### **2.1 Database C API**
### **2.1 数据库 C API**

C APIs for interfacing with the database.
与数据库交互的C API。

![enter image description here](https://eosio.github.io/eos/group__database_c.png)

#### **2.1.1 Single String Index Table**
#### **2.1.1　单字符串索引表**

These methods interface with a simple table with String unique primary key and arbitrary binary data value.
这些方法与一个带有String类型的唯一主键和任意二进制数据值的简单表格交互。

![enter image description here](https://eosio.github.io/eos/group__dbstr.png)

##### **2.1.1.1 Function Documentation**
##### **2.1.1.1 功能文档**

###### **store_str**

    int32_t store_str (account_name scope, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Parameters*
*参数*

 - scope - the account scope that will be read, must exist in the transaction scopes list
 - table	- the ID/name of the table within the current scope/code context to modify

 - scope - 将要读取的帐户范围必须存在于事务范围列表中
 - table - 当前范围/代码上下文中要修改的表的ID /名称

*Returns*
*返回*

1 if a new record was created, 0 if an existing record was updated
如果创建了新记录则返回１，如果现有记录被跟新了则返回0

*Precondition*
*前提*

datalen >= sizeof(uint64_t)　
data is a valid pointer to a range of memory at least datalen bytes long
*((Name*)data) stores the primary key　scope is declared by the current transaction　
this method is being called from an apply context (not validate or precondition)

datalen >= sizeof(uint64_t)
数据是一个有效的指针，指向一个至少有datalen字节长度的内存
*((Name*)data)存储主键作用域被当前事务声明
这个方法是从一个应用上下文被调用（不验证或先决条件）

*Postcondition*
*后置条件*

a record is either created or updated with the given scope and table.
一个记录是创建或更新与给定的范围和表。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止


###### **update_str**

    int32_t update_str (account_name scope, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Returns*
*返回*

1 if the record was updated, 0 if no record with key was found
如果记录已更新，则返回1;如果没有找到具有密钥的记录，则返回0

###### **load_str**

    int32_t load_str (account_name scope, account_name code, table_name table, char *key, uint32_t keylen, char *value, uint32_t valuelen)

*Parameters*
*参数*

 - scope - the account scope that will be read, must exist in the transaction scopes list
 - code - identifies the code that controls write-access to the data
 - table - the ID/name of the table within the scope/code context to query
 - data - location to copy the stored record, should be initialized with the key to get
 - datalen - the maximum length of data to read, must be greater than sizeof(uint64_t)

 - scope - 将要读取的帐户范围必须存在于事务范围列表中
 - code - 标识控制对数据的写入访问的代码
 - table - 要查询的范围或者代码上下文中的表的ID或名称
 - data - 要复制存储的记录的位置，应该用key初始化来获取
 - datalen - 要读取的最大数据长度，必须大于sizeof(uint64_t)

*Returns*
*返回*

the number of bytes read or -1 if key was not found
读取的字节数，如果没有找到密钥，则返回-1

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
*返回*

1 if the record was updated, 0 if no record with key was found
如果记录已更新，则返回1;如果没有找到具有密钥的记录，则返回0

###### **remove_str**

    int32_t remove_str (account_name scope, table_name table, char *key, uint32_t keylen)

*Parameters*
*参数*

 - data	- must point to at least 8 bytes containing primary key
 - data - 必须指向包含主键的至少8个字节

*Returns*
*返回*

1 if a record was removed, and 0 if no record with key was found
如果记录被删除，则为1;如果没有找到记录，则记录为0

#### **2.1.2 Single 64 bit Index Table**
#### **2.1.2 单64位索引表**

These methods interface with a simple table with 64 bit unique primary key and arbitrary binary data value.
这些方法与具有64位唯一主键和任意二进制数据值的简单表格进行交互。

![enter image description here](https://eosio.github.io/eos/group__dbi64.png)

##### **2.1.2.1 Example**
##### **2.1.2.1 例子**
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
##### **2.1.2.2 函数文档**

###### **store_i64**

    int32_t store_i64 (account_name scope, table_name table, const void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the current scope/code context to modify

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 当前范围/代码上下文中要修改的表的ID/名称

*Returns*
*返回*

1 if a new record was created, 0 if an existing record was updated
如果创建了新记录则返回１，则在更新已有记录时则返回0

*Precondition*
*前提*

datalen >= sizeof(uint64_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint64_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

datalen >= sizeof(uint64_t)
数据是一个有效的指针，指向一个至少有datalen字节长度的内存
*((uint64_t*)data)存储主键作用域被当前事务声明
范围是被当前交易声明的
这个方法是从一个应用上下文被调用（不验证或先决条件）

*Postcondition*
*前提条件*

a record is either created or updated with the given scope and table.
一个记录是创建或更新与给定的范围和表。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **update_i64**

    int32_t update_i64 (account_name scope, table_name table, const void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the current scope/code context to modify

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 当前范围/代码上下文中要修改的表的ID /名称

*Returns*
*返回*

1 if the record was updated, 0 if no record with key was found
如果记录已更新，则为1;如果没有找到具有密钥的记录，则为0

*Precondition*
*前提条件*

datalen >= sizeof(uint64_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint64_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

datalen >= sizeof(uint64_t)
数据是一个有效的指针，指向一个至少有datalen字节长度的内存
*((uint64_t*)data)存储主键作用域被当前事务声明
范围是被当前交易声明的
这个方法是从一个应用上下文被调用（不验证或先决条件）

*Postcondition*
*后置条件*

a record is either created or updated with the given scope and table.
一个记录是创建或更新与给定的范围和表。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **load_i64**

    int32_t load_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the stored record, should be initialized with the key to get
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制存储的记录的位置，应该用key来初始化来获取
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if key was not found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **front_i64**

    int32_t front_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制前面记录的位置
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **back_i64**

    int32_t back_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制后面记录的位置
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

- the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **next_i64**

    int32_t next_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record. Should be initialized with the key to get next record.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制下一条记录的位置。应该用key初始化以获得下一条记录。
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if key was not found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **previous_i64**

    int32_t previous_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record. Should be initialized with the key to get previous record.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制上一条记录的位置。应该用key初始化以获得下一条记录。
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if key was not found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **lower_bound_i64**

    int32_t lower_bound_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound. Should be initialized with the key to find lower bound of.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制下界的位置。应该用key来初始化找到下界。
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if key was not found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **upper_bound_i64**

    int32_t upper_bound_i64 (account_name scope, account_name code, table_name table, void *data, uint32_t datalen)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound. Should be initialized with the key to find upper bound of.
- datalen	- the maximum length of data to read, must be greater than sizeof(uint64_t)

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制上界的位置。应该用key来初始化找到上界。
- datalen - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if key was not found
返回读取的字节数，如果没有找到密钥，则返回-1

###### **remove_bound_i64**

    int32_t remove_i64 (account_name scope, table_name table, void *data)

*Parameters*
*参数*

- scope	- the account socpe that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table withing the scope/code context to query
- data	- must point to at lest 8 bytes containing primary key

- scope - 将被读取的帐户社会必须存在于事务范围列表中
- table - 带查询范围/代码上下文的表的ID/名称
- data - 必须指向至少包含主键的8个字节

*Returns*
*返回*

1 if a record was removed, and 0 if no record with key was found
如果记录被删除，则为1;如果没有找到记录，则记录为0

#### **2.1.3 Dual 128 bit Index Table**
#### **2.1.3 双128位索引表**
Interface to a database table with 128 bit primary and secondary keys and arbitary binary data value.
与128位主键和次级键以及任意二进制数据值的数据库表交互。

![enter image description here](https://eosio.github.io/eos/group__dbi128i128.png)

##### **2.1.3.1 Description**
##### **2.1.3.1 描述**

*Parameters*
*参数*

- scope	- the account where table data will be found
- code	- the code which owns the table
- table	- the name of the table where record is stored
- data	- a pointer to memory that is at least 32 bytes long
- len	- the length of data, must be greater than or equal to 32 bytes

- scope - 表数据将被查到的帐户
- code - 拥有该表的代码
- table - 存储记录的表的名称
- data - 指向至少32字节长的内存的指针
- len - 数据的长度必须大于或等于32个字节

*Returns*
*返回*

the total number of bytes read or -1 for "not found" or "end" where bytes read includes 32 bytes of the key
读取的总字节数，或-1表示“not found”，或“end”，其中字节读取包括32个字节的密钥

These methods assume a database table with records of the form:
这些方法假设一个数据库表格，其格式为：

> struct record {
   uint128  primary;
   uint128  secondary;
   ... arbitrary data ...
};

You can iterate over these indicies with primary index sorting records by { primary, secondary } and the secondary index sorting records by { secondary, primary }. This means that duplicates of the primary or secondary values are allowed so long as there are no duplicates of the combination {primary, secondary}.

你可以迭代记录用{primary，secondary}排序的主索引记录和用{secondary，primary}排序的辅助索引记录。这意味着只要没有重复的{primary，secondary}组合，就允许重复的单独主键或单独辅键。

##### **2.1.3.2 Example**
##### **2.1.3.2 例子**

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
##### **2.1.3.3 函数文档**

###### **load_primary_i128i128**

    int32_t 	load_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
*参数*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the primary key to load
- len	- length of record to copy

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 拥有该表的代码
- table - 当前范围/代码上下文中要修改的表的ID /名称
- data - 复制记录的位置，必须用主键进行初始化加载
- len - 要复制的记录的长度

*Returns*
*返回*

the number of bytes read, -1 if key was not found
返回读取的字节数，如果没有找到密钥，则返回-1

*Precondition*
*前置条件*

len >= sizeof(uint128_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint128_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

datalen >= sizeof(uint64_t)
数据是一个有效的指针，指向一个至少有datalen字节长度的内存
*((uint128_t*)data)存储主键作用域被当前事务声明
范围是被当前交易声明的
这个方法是从一个应用上下文被调用（不验证或先决条件）

*Postcondition*
*前提条件*

data will be initialized with the len bytes of record matching the key.
数据将用与键匹配的记录的len个字节进行初始化。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **front_primary_i128i128**

    int32_t front_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*
- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 位置复制主键的前面记录
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **back_primary_i128i128**

    int32_t back_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*
 - scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 位置来复制主键的后面记录
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **next_primary_i128i128**

    int32_t next_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record of primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*
- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制主键的下一个记录的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **previous_primary_i128i128**

    int32_t previous_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record of primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*
- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制主键的前一个记录的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **upper_bound_primary_i128i128**

    int32_t upper_bound_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of a primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*
- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制一个主键的上界的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **lower_bound_primary_i128i128**

    int32_t lower_bound_primary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of a primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*
- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制一个主键的下界的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **load_secondary_i128i128**

    int32_t load_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the secondary key to load
- len	- length of record to copy

*参数*
- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 拥有该表的代码
- table - 当前范围/代码上下文中要修改的表的ID /名称
- data - 复制记录的位置，必须用辅助键初始化才能加载
- len - 要复制的记录的长度

*Returns*
*返回*

the number of bytes read, -1 if key was not found
返回读取的字节数，-1如果没有找到密钥

*Precondition*

len >= sizeof(uint128_t)
data is a valid pointer to a range of memory at least datalen bytes long
*((uint128_t*)data) stores the secondary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

*前提*

len>=sizeof(uint128_t)
数据是指向至少datalen字节长的内存范围的有效指针
*((uint128_t *)data)存储二级密钥
范围由当前事务声明
这个方法是从一个应用的上下文（不验证或先决条件）

*Postcondition*
*后置条件*

data will be initialized with the len bytes of record matching the key.
数据将用与键匹配的记录的len字节进行初始化。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **front_secondary_i128i128**

    int32_t front_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制副键的前面记录的位置
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **back_secondary_i128i128**

    int32_t back_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*
- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)
*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制副键的后面记录的位置
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **next_secondary_i128i128**

    int32_t next_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record of secondary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制次级秘钥对应的下一个记录的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **previous_secondary_i128i128**

    int32_t previous_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record of secondary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制次级秘钥对应的上一个记录的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **upper_bound_secondary_i128i128**

    int32_t upper_bound_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of a primary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data -复制主键的上界的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **lower_bound_secondary_i128i128**

    int32_t lower_bound_secondary_i128i128 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of given secondary key; must be initialized with a key.
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data -复制主键的下界的位置; 必须用键来初始化。
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
返回读取的字节数，如果没有找到记录，则返回-1

###### **remove_i128i128**

    int32_t remove_i128i128 (account_name scope, table_name table, const void *data)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the scope/code context to query
- data	- must point to at lest 32 bytes containing {primary,secondary}

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 必须指向至少32个字节，包含{primary，secondary}

*Returns*
*返回*

1 if a record was removed, and 0 if no record with key was found
如果记录被删除，则为1;如果没有找到记录，则记录为0

###### **store_i128i128**

    int32_t store_i128i128 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the scope/code context to query
- data	- must point to a at least 32 bytes containing (primary, secondary)
- len	- the length of the data

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 必须指向至少32个字节，包含（主要，次要）
- len - 数据的长度

*Returns*
*返回*

1 if a new record was created, 0 if an existing record was updated
如果创建了新记录,则为１，已有记录被跟新时，则为0

###### **update_i128i128**

    int32_t update_i128i128 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the ID/name of the table within the scope/code context to query
- data	- must to a at least 32 bytes containing (primary, secondary)
- len	- the length of the data

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 必须指向至少32个字节，包含（主要，次要）
- len - 数据的长度


*Returns*
*返回*

1 if the record was updated, 0 if no record with key was found
如果记录已更新，则为1;如果没有找到具有密钥的记录，则为0

#### **2.1.4 Triple 64 bit Index Table**
#### **2.1.4 三重64位索引表**

Interface to a database table with 64 bit primary, secondary and tertiary keys and arbitrary binary data value.
与64位主键，次级键和三级键以及任意二进制数据值的数据库表交互。

![enter image description here](https://eosio.github.io/eos/group__dbi64i64i64.png)

##### **2.1.4.1 Description**
##### **2.1.4.1 描述**

*Parameters*

- scope	- the account where table data will be found
- code	- the code which owns the table
- table	- the name of the table where record is stored
- data	- a pointer to memory that is at least 32 bytes long
- len	- the length of data, must be greater than or equal to 32 bytes

*参数*

- scope - 将查找表数据的帐户
- code - 拥有该表的代码
- table - 存储记录的表的名称
- data - 指向至少32字节长的内存的指针
- len - 数据的长度必须大于或等于32个字节

*Returns*
*返回*

the total number of bytes read or -1 for "not found" or "end" where bytes read includes 24 bytes of the key
读取的字节总数, 或-1表示“not found”或“end”，其中读取的字节包括24个字节的密钥

These methods assume a database table with records of the form:
这些方法假设一个数据库表格，其格式为：

> struct record {
   uint64  primary;
   uint64  secondary;
   uint64  tertiary;
   ... arbitrary data ...
};

You can iterate over these indices with primary index sorting records by { primary, secondary, tertiary }, the secondary index sorting records by { secondary, tertiary } and the tertiary index sorting records by { tertiary }.
您可以使用{primary，secondary，tertiary}的主索引排序记录，{secondary，tertiary}的次索引排序记录和{tertiary}的三级索引排序记录遍历这些索引。

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

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 拥有该表的代码
- table - 当前范围/代码上下文中要修改的表的ID /名称
- data - 要复制记录的位置，必须用（primary，secondary，tertiary）加载进行初始化
- len - 要复制的记录的长度

*Returns*
*返回*

the number of bytes read, -1 if key was not found
读取的字节数，如果没有找到密钥，则为-1

*Precondition*
*前提条件*

data is a valid pointer to a range of memory at least len bytes long
*((uint64_t*)data) stores the primary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)
数据是一个有效指针，指向一个至少为len字节长的内存区域
*((uint64_t *)data)存储主键
范围由当前事务声明
这个方法是从一个应用的上下文（不验证或先决条件）

*Postcondition*
*后置条件*

data will be initialized with the len bytes of record matching the key.
数据将用与键匹配的记录的len字节进行初始化。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **front_primary_i64i64i64**
    int32_t front_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 位置复制主键的前面记录
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）


*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **back_primary_i64i64i64**
    int32_t back_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of primary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 位置来复制主键的后面记录
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **next_primary_i64i64i64**
    int32_t next_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record of primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制主键的下一个记录的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **previous_primary_i64i64i64**
    int32_t previous_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record of primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制主键的上一个记录的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **upper_bound_primary_i64i64i64**
    int32_t upper_bound_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of a primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制主键的上界的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **lower_bound_primary_i64i64i64**
    int32_t lower_bound_primary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of primary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制主键的下界的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **load_secondary_i64i64i64**
    int32_t load_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the (secondary,tertiary) to load
- len	- length of record to copy

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 拥有该表的代码
- table - 当前范围/代码上下文中要修改的表的ID /名称
- data - 复制记录的位置，必须用（二级，三级）加载进行初始化
- len - 要复制的记录的长度

*Returns*
*返回*

the number of bytes read, -1 if key was not found
读取的字节数，如果没有找到密钥，则返回-1

*Precondition*
*前提条件*

data is a valid pointer to a range of memory at least len bytes long
*((uint64_t*)data) stores the secondary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

数据是一个有效指针，指向一个至少为len字节长的内存区域
*((uint64_t *)data)存储二级密钥
范围由当前事务声明
这个方法是从一个应用的上下文（不验证或先决条件）

*Postcondition*
*后置条件*

data will be initialized with the len bytes of record matching the key.
数据将用与键匹配的记录的len字节进行初始化。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **front_secondary_i64i64i64**
    int32_t front_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of a secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制次级键的前面记录的位置
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **back_secondary_i64i64i64**
    int32_t back_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of secondary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制次级键的后面记录的位置
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **next_secondary_i64i64i64**
    int32_t next_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制下一条记录的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **previous_secondary_i64i64i64**
    int32_t previous_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制上一条记录的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **upper_bound_secondary_i64i64i64**
    int32_t upper_bound_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of tertiary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制第三级键上界的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **lower_bound_secondary_i64i64i64**
    int32_t lower_bound_secondary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of secondary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制第三级键下界的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **load_tertiary_i64i64i64**
    int32_t load_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- the code which owns the table
- table	- the ID/name of the table within the current scope/code context to modify
- data	- location to copy the record, must be initialized with the (tertiary) to load
- len	- length of record to copy

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 拥有该表的代码
- table - 当前范围/代码上下文中要修改的表的ID /名称
- data - 要复制记录的位置，必须用（tertiary）进行初始化才能加载
- len - 要复制的记录的长度

*Returns*
*返回*

the number of bytes read, -1 if key was not found
读取的字节数，如果没有找到密钥，则返回-1

*Precondition*
*前提条件*

data is a valid pointer to a range of memory at least len bytes long
*((uint64_t*)data) stores the tertiary key
scope is declared by the current transaction
this method is being called from an apply context (not validate or precondition)

数据是一个有效指针，指向一个至少为len字节长的内存区域
*((uint64_t *)data)存储第三级键
范围由当前事务声明
这个方法是从一个应用的上下文（不验证或先决条件）

*Postcondition*
*后置条件*

data will be initialized with the len bytes of record matching the key.
数据将用与键匹配的记录的len字节进行初始化。

*Exceptions*
*异常*

if	called with an invalid precondition execution will be aborted
如果调用无效的前提条件执行将被中止

###### **front_tertiary_i64i64i64**
    int32_t front_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the front record of a tertiary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制第三级键的前面记录的位置
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **back_tertiary_i64i64i64**
    int32_t back_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the back record of a tertiary key
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制第三级键的后面记录的位置
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **next_tertiary_i64i64i64**
    int32_t next_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the next record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制下一条记录的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **previous_tertiary_i64i64i64**
    int32_t previous_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the previous record; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中表的ID /名称
- data - 复制上一条记录的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **upper_bound_tertiary_i64i64i64**
    int32_t upper_bound_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the upper bound of tertiary key; must be initialized with a key value-
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)


*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中的表的ID /名称
- data - 复制第三级键的上界的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **lower_bound_tertiary_i64i64i64**
    int32_t lower_bound_tertiary_i64i64i64 (account_name scope, account_name code, table_name table, void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- code	- identifies the code that controls write-access to the data
- table	- the ID/name of the table within the scope/code context to query
- data	- location to copy the lower bound of tertiary key; must be initialized with a key value
- len	- the maximum length of data to read, must be greater than sizeof(uint64_t)

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- code - 标识控制对数据的写入访问的代码
- table - 要查询的范围/代码上下文中的表的ID /名称
- data - 复制第三级键的下界的位置; 必须用关键值初始化
- len - 要读取的最大数据长度必须大于sizeof（uint64_t）

*Returns*
*返回*

the number of bytes read or -1 if no record found
读取的字节数，如果没有找到记录，则返回-1

###### **remove_i64i64i64**
    int32_t remove_i64i64i64 (account_name scope, table_name table, const void *data)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the name of table where record is stored
- data	- must point to at least 24 bytes containing {primary,secondary,tertiary}

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 存储记录的表格的名称
- data - 必须指向至少24个字节，包含{primary，secondary，tertiary}

*Returns*
*返回*

1 if a record was removed, and 0 if no record with key was found
如果记录被删除，则为1;如果没有找到记录，则记录为0

###### **store_i64i64i64**
    int32_t store_i64i64i64 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the name of table where record is stored
- data	- must point to at least 24 bytes containing (primary,secondary,tertiary)
- len	- length of the data

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 存储记录的表格的名称
- data - 必须指向至少24个字节，包含（主要，次要，第三级）
- len - 数据的长度

*Returns*
*返回*

1 if a new record was created, 0 if an existing record was updated
如果创建了新记录，则为１，如果已有记录跟新了，则为０。

###### **update_i64i64i64**
    int32_t update_i64i64i64 (account_name scope, table_name table, const void *data, uint32_t len)

*Parameters*

- scope	- the account scope that will be read, must exist in the transaction scopes list
- table	- the name of table where record is stored
- data	- must point to at least 24 bytes containing (primary,secondary,tertiary)
- len	- length of the data

*参数*

- scope - 将要读取的帐户范围必须存在于事务范围列表中
- table - 存储记录的表格的名称
- data - 必须指向至少24个字节，包含（主要，次要，第三级）
- len - 数据的长度

*Returns*
*返回*

1 if the record was updated, 0 if no record with key was found
如果记录已更新，则为1;如果没有找到具有密钥的记录，则为0

### **2.2 Database C++ API**
### **2.2　数据库　C++ API **
C++ APIs for interfacing with the database, it provides a simple interface for storing any fixed-size struct as a database row.
用于连接数据库的C++ API，它提供了一个简单的接口，用于将任何固定大小的结构存储为数据库行。

![enter image description here](https://eosio.github.io/eos/group__database_cpp.png)

#### **2.2.1 Single Index Table**
#### **2.2.1　单一索引表**
This specialization of Table is for single-index tables
表的这种专门化是针对单索引表的

![enter image description here](https://eosio.github.io/eos/group___singleindextable.png)

##### **2.2.1.1 Description**
##### **2.2.1.1　描述**

###### **Classes**
###### **类**

> struct  	table < scope, code, table, Record, PrimaryType, void >

> struct  	[primary_index](#31-primary-index)

###### **Public Types**
###### **公有类型**
Primary

> typedef PrimaryType 	primary

> typedef PrimaryType 	table < scope, code, table, Record, PrimaryType, void >::Primary

###### **Parameters**

- scope	- the default account name scope that this table is located within
- code	- the code account name which has write permission to this table
- table	- a unique identifier (name) for this table
- Record	- the type of data stored in each row
- PrimaryType	- the type of the first field stored in Record

- scope - 此表所在的默认帐户名称范围
- code - 对此表具有写入权限的代码帐户名称
- table - 此表的唯一标识符（名称）
- Record - 每行存储的数据类型
- PrimaryType - 记录中存储的第一个字段的类型

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
##### **2.2.1.3 静态公有成员函数**

###### **front (Record &r)**
    static bool front (Record &r)

    static bool table< scope, code, table, Record, PrimaryType, void >::front (Record & r)

fetches the front of the table
拿到表格的前几行

*Parameters*

- r	- reference to hold the value
- r	- 保存这个值的引用

*Returns*
*返回*

true if successfully retrieved the front
如果成功检索到前几行，则为true

###### **back (Record &r)**
    static bool back (Record &r)

    static bool table< scope, code, table, Record, PrimaryType, void >::back (Record & r)

fetches the back of the table
拿到表格的后几行

*Parameters*

- r	- reference to hold the value
- r	- 保存这个值的引用

*Returns*
*返回*

true if successfully retrieved the back
如果成功检索到前几行，则为true

###### **get (const PrimaryType &p, Record &r, uint64_t s=scope)**
    static bool get (const PrimaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::get	(const PrimaryType &p, Record &r, uint64_t s=scope)

retrieves the record for the specified primary key
检索指定主键的记录

*Parameters*

- p	- the primary key of the record to fetch
- r	- reference of record to hold return value
- s	- scope; defaults to scope of the class.

*参数*

- p - 要获取的记录的主键
- r - 保存返回值的记录参考
- s - 默认为该类的范围。

*Returns*
*返回*

true if get succeeds.
如果成功获取，则为true

###### **get (Record &r, uint64_t s=scope)**

    static bool get (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::get	(Record & 	r, uint64_t s = scope)

retrieves a record based on initialized primary key value
基于初始化的主键值检索记录

*Parameters*

- r	- reference of a record to hold return value; must be initialized to the primary key to be fetched.
- s	- scope; defaults to scope of the class.

*参数*

- r - 保持返回值的记录的引用; 必须初始化为要获取的主键。
- s - 默认为该类的范围。

*Returns*
*返回*

true if get succeeds.
如果成功获取，则为true

###### **store (const Record &r, uint64_t s=scope)**

    static bool store (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::store (const Record & r, uint64_t s = scope)

store a record to the table
将记录存储在表格中

*Parameters*

- r	- the record to be stored.
- s	- scope; defaults to scope of the class.

*参数*

- r - 要存储的记录。
- s - 默认为该类的范围。

*Returns*
*返回*

true if store succeeds.
如果成功存储，则为true

###### **update (const Record &r, uint64_t s=scope)**

    static bool update (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::store (const Record & r, uint64_t s = scope)

store a record to the table
将记录存储在表格中

*Parameters*

- r	- the record to be stored.
- s	- scope; defaults to scope of the class.

*参数*

- r - 要存储的记录。
- s - 范围; 默认为该类的范围。


*Returns*
*返回*

true if store succeeds.
如果成功存储，则为true

###### **static bool remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, void >::remove (const Record & r, uint64_t 	s = scope)

remove a record from the table.
从表中删除一条记录。

*Parameters*

- r	- the record to be removed.
- s	- scope; defaults to scope of the class.

*参数*

- r - 要删除的记录。
- s - 范围; 默认为该类的范围。

*Returns*
*返回*

true if remove succeeds.
如果成功删除，则为true

#### **2.2.2 Dual Index Table**
#### ** 2.2.2双重索引表**
defines a type-safe C++ wrapper around the Database C API
定义一个对数据库C　API的类型安全的C ++包装器

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

###### **参数**

- scope - 此表所在的默认帐户名称/范围
- code - 对此表具有写入权限的代码帐户名称
- table - 此表的唯一标识符（名称）
- Record - 每行存储的数据类型
- PrimaryType - 记录中存储的第一个字段的类型
- SecondaryType - 记录中存储的第二个字段的类型

主索引和次索引按从低到高的N位无符号整数排序

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

*参数*

- p - 要检索的主键的引用
- r - 引用一个记录来加载值。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

###### **store (const Record &r, uint64_t s=scope)**

    static bool store (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::store (const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用要存储的记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful store.

*返回*

如果成功存储则返回true

###### **update (const Record &r, uint64_t s=scope)**

    static bool update (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::update	(const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to update.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用要更新的记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful update.

*返回*

如果成功跟新则返回true

###### **remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::remove	(const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to remove.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用要删除的记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful remove.

*返回*

如果成功删除则返回true

## **3. Indexes**
## **3. 索引**

### **3.1 Primary Index**
### **3.1 主索引**

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

*参数*

- r - 引用记录来存储基于主索引的前端记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **back (Record &r, uint64_t s=scope)**

    static bool back (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::back (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store the back record based on primary index.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用记录来存储基于主索引的后备记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **next (Record &r, uint64_t s=scope)**

    static bool next (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::next (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store next value; must be initialized with current.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用记录来存储下一个值; 必须在当前初始化。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true


##### **previous (Record &r, uint64_t s=scope)**

    static bool previous (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::previous (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store previous value; must be initialized with current.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用记录来存储上一个值; 必须在当前初始化。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **get (const PrimaryType &p, Record &r, uint64_t s=scope)**

    static bool get (const PrimaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::get (const PrimaryType & p, Record & r, uint64_t s = scope)

*Parameters*

- p	- reference to primary key to load; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*参数*

- p - 加载主键的引用; 必须用值来初始化;
- r - 引用一个记录来加载值。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **lower_bound (const PrimaryType &p, Record &r)**

    static bool lower_bound (const PrimaryType &p, Record &r)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::lower_bound (const PrimaryType & p, Record & r )

*Parameters*

- p	- reference to primary key to get the lower bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*参数*

- p - 主键获取下界的参考; 必须用值来初始化;
- r - 引用一个记录来加载值。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **upper_bound (const PrimaryType &p, Record &r)**

    static bool upper_bound (const PrimaryType &p, Record &r)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::upper_bound (const PrimaryType & p, Record & r )

*Parameters*

- p	- reference to primary key to get the upper bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*参数*

- p - 主键获取上限的引用; 必须用值来初始化;
- r - 引用一个记录来加载值。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::primary_index::remove	(const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to remove from table;
- s	- account scope. default is current scope of the class

*参数*

- r - 引用要从表中删除的记录;
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successfully removed;

*返回*

如果成功删除则为true;

### **3.2 Secondary Index**
### **3.2　次级索引**

#### **3.2.1 Description**
The Secondary Index.

    table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index Struct Reference

#### **3.2.2 Static Public Member Functions**

##### **front (Record &r, uint64_t s=scope)**

    static bool front (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::front (Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store the front record based on secondary index.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用记录来存储基于二级索引的前端记录。
- s - 账户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **back (Record &r, uint64_t s=scope)**

    static bool back (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::back	(Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to store the back record based on secondary index.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用一条记录来存储基于二级索引的后退记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **next (Record &r, uint64_t s=scope)**

    static bool next (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::next	(Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to return the next record .
- s	- account scope. default is current scope of the class

*参数*

- r - 引用一条记录来返回下一条记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **previous (Record &r, uint64_t s=scope)**

    static bool previous (Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::previous	(Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to return the previous record.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用一条记录来返回上一条记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **get (const SecondaryType &p, Record &r, uint64_t s=scope)**

    static bool get (const SecondaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::get (const SecondaryType & p, Record & r, uint64_t s = scope)

*Parameters*

- p	- reference to secondary index key
- r	- reference to record to hold the value
- s	- account scope. default is current scope of the class

*参数*

- p - 二级索引键的引用
- r - 引用记录来保存值
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **lower_bound (const SecondaryType &p, Record &r, uint64_t s=scope)**

    static bool lower_bound (const SecondaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::lower_bound (const SecondaryType & p, Record & r, uint64_t s = scope)

*Parameters*

- p	- reference to secondary key to get the lower bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*参数*

- p - 引用次级键得到下界; 必须用值来初始化;
- r - 引用一个记录来加载值。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **upper_bound (const SecondaryType &p, Record &r, uint64_t s=scope)**

    static bool upper_bound (const SecondaryType &p, Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::upper_bound (const SecondaryType & p, Record & r, uint64_t s = scope)

*Parameters*

- p	- reference to secondary key to get the upper bound of; must be initialized with a value;
- r	- reference to a record to load the value to.
- s	- account scope. default is current scope of the class

*参数*

- p - 引用次级键来获得上界; 必须用值来初始化;
- r - 引用一个记录来加载值。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successful read.

*返回*

如果成功读取则返回true

##### **remove (const Record &r, uint64_t s=scope)**

    static bool remove (const Record &r, uint64_t s=scope)

    static bool table< scope, code, table, Record, PrimaryType, SecondaryType >::secondary_index::remove (const Record & r, uint64_t s = scope)

*Parameters*

- r	- reference to a record to be removed.
- s	- account scope. default is current scope of the class

*参数*

- r - 引用要删除的记录。
- s - 帐户范围。 默认是该类的当前范围

*Returns*

true if successfully removed.

*返回*

如果成功删除则返回true

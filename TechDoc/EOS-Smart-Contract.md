>原文链接：<https://github.com/EOSIO/eos/wiki/Smart%20Contract>
>
>翻译：区块链中文字幕组 - [张奎](https://github.com/byzhangkui)
>
> 翻译时间：2018-01-22

# EOS Smart Contract
# EOS 智能合约

*   [1 Introduction to EOS Smart Contract](https://github.com/EOSIO/eos/wiki/Smart%20Contract#1-introduction-to-eos-smart-contract)
    *   [1.1 Required Background Knowledge](https://github.com/EOSIO/eos/wiki/Smart%20Contract#11-required-background-knowledge)
    *   [1.2 Basics of EOS Smart Contract](https://github.com/EOSIO/eos/wiki/Smart%20Contract#12-basics-of-eos-smart-contract)
    *   [1.3 Technical Limitation](https://github.com/EOSIO/eos/wiki/Smart%20Contract#13-technical-limitation)
*   [2 Smart Contract Files](https://github.com/EOSIO/eos/wiki/Smart%20Contract#2-smart-contract-files)
    *   [2.1 HPP](https://github.com/EOSIO/eos/wiki/Smart%20Contract#21-hpp)
    *   [2.2 CPP](https://github.com/EOSIO/eos/wiki/Smart%20Contract#22-cpp)
    *   [2.3 WAST](https://github.com/EOSIO/eos/wiki/Smart%20Contract#23-wast)
    *   [2.4 ABI](https://github.com/EOSIO/eos/wiki/Smart%20Contract#24-abi)
*   [3 Checklist](https://github.com/EOSIO/eos/wiki/Smart%20Contract#3-checklist)
*   [4 Interacting with Smart Contract Examples](https://github.com/EOSIO/eos/wiki/Smart%20Contract#4-interacting-with-smart-contract-examples)
    *   [4.1 The Currency Contract](https://github.com/EOSIO/eos/wiki/Smart%20Contract#41-the-currency-contract)
    *   [4.2 Tie-Tac-Toe](https://github.com/EOSIO/eos/wiki/Smart%20Contract#42-tic-tac-toe)
*   [5 Writing your first EOS Smart Contract](https://github.com/EOSIO/eos/wiki/Smart%20Contract#5-writing-your-first-eos-smart-contract)
*   [6 Deploy and update Smart Contract](https://github.com/EOSIO/eos/wiki/Smart%20Contract#6-deploy-and-update-smart-contract)
*   [7 Command Summary](https://github.com/EOSIO/eos/wiki/Smart%20Contract#7-command-summary)
*   [8 Debugging Smart Contract](https://github.com/EOSIO/eos/wiki/Smart%20Contract#8-debugging-smart-contract)
    *   [8.1 Method](https://github.com/EOSIO/eos/wiki/Smart%20Contract#81-method)
    *   [8.2 Print](https://github.com/EOSIO/eos/wiki/Smart%20Contract#82-print)
    *   [8.3 Example](https://github.com/EOSIO/eos/wiki/Smart%20Contract#83-example)


*   [1 EOS智能合约介绍](https://github.com/EOSIO/eos/wiki/Smart%20Contract#1-introduction-to-eos-smart-contract)
      *   [1.1 所需要的背景知识](https://github.com/EOSIO/eos/wiki/Smart%20Contract#11-required-background-knowledge)
      *   [1.2 EOS智能合约基础](https://github.com/EOSIO/eos/wiki/Smart%20Contract#12-basics-of-eos-smart-contract)
      *   [1.3 技术限制](https://github.com/EOSIO/eos/wiki/Smart%20Contract#13-technical-limitation)
*   [2 智能合约文件](https://github.com/EOSIO/eos/wiki/Smart%20Contract#2-smart-contract-files)
      *   [2.1 HPP](https://github.com/EOSIO/eos/wiki/Smart%20Contract#21-hpp)
      *   [2.2 CPP](https://github.com/EOSIO/eos/wiki/Smart%20Contract#22-cpp)
      *   [2.3 WAST](https://github.com/EOSIO/eos/wiki/Smart%20Contract#23-wast)
      *   [2.4 ABI](https://github.com/EOSIO/eos/wiki/Smart%20Contract#24-abi)
*   [3 检查清单](https://github.com/EOSIO/eos/wiki/Smart%20Contract#3-checklist)
*   [4 同智能合约样例交互](https://github.com/EOSIO/eos/wiki/Smart%20Contract#4-interacting-with-smart-contract-examples)
      *   [4.1 现金合约](https://github.com/EOSIO/eos/wiki/Smart%20Contract#41-the-currency-contract)
      *   [4.2 井字棋游戏](https://github.com/EOSIO/eos/wiki/Smart%20Contract#42-tic-tac-toe)
*   [5 编写你的第一个智能合约](https://github.com/EOSIO/eos/wiki/Smart%20Contract#5-writing-your-first-eos-smart-contract)
*   [6 部署和更新智能合约](https://github.com/EOSIO/eos/wiki/Smart%20Contract#6-deploy-and-update-smart-contract)
*   [7 命令汇总](https://github.com/EOSIO/eos/wiki/Smart%20Contract#7-command-summary)
*   [8 调试智能合约](https://github.com/EOSIO/eos/wiki/Smart%20Contract#8-debugging-smart-contract)
      *   [8.1 方法](https://github.com/EOSIO/eos/wiki/Smart%20Contract#81-method)
      *   [8.2 打印](https://github.com/EOSIO/eos/wiki/Smart%20Contract#82-print)
      *   [8.3 样例](https://github.com/EOSIO/eos/wiki/Smart%20Contract#83-example)


## 1. Introduction to EOS Smart Contract  
## 1. EOS智能合约介绍  

### 1.1. Required Background Knowledge  
### 1.1. 所需要的背景知识  
#### C / C++ Experience  
#### C / C++ 经验  

EOS.IO based blockchains execute user-generated applications and code using [Web Assembly](http://webassembly.org/) (WASM). WASM is an emerging web standard with widespread support of Google, Microsoft, Apple, and others. At the moment the most mature toolchain for building applications that compile to WASM is clang/llvm with their C/C++ compiler.  

基于EOS.IO的区块链使用 [Web Assembly](http://webassembly.org/)（WASM）执行用户生成的应用程序和代码。WASM 是一个被谷歌、微软、苹果等公司广泛支持的web标准。当前最成熟的将应用程序编译成WASM的工具是使用 C/C++ 编译器的 clang/llvm。  

Other toolchains in development by 3rd parties include: Rust, Python, and Solidity. While these other languages may appear simpler, their performance will likely impact the scale of application you can build. We expect that C++ will be the best language for developing high-performance and secure smart contracts.  

其他第三方的工具包括：Rust，Python 和 Solidiity。虽然这些其他语言可能看起来更简单，但是他们的性能可能会影响你构建的应用程序的规模。我们相信 C++ 是开发高性能和安全智能合约最好的语言。  

#### Linux / Mac OS Experience  
#### Linux / Mac OS经验

The EOS.IO software only officially supports the following environment  
EOS.IO软件官方只支持以下的环境：  
- Ubuntu 16.10 or above, or  
- Ubuntu 16.0版本及以上，或
- MacOS Sierra or above  
- MacOS Sierra 版本及以上

#### Command Line Knowledge
#### 命令行知识

There are a variety of tools provided along with EOS.IO which requires you to have basic command line knowledge in order to interact with.  

EOS.IO 提供了一系列的工具，你需要有基本的命令行知识才能与之交互。  


### 1.2. Basics of EOS Smart Contract
### 1.2. EOS智能合约基础

#### Communication Model
#### 通讯模式

EOS Smart Contract communicate with each other in form of messages and shared memory database access, e.g. a contract can read the state of another contract's database as long as it is included within the read scope of the transaction with an async vibe. The async communication may result in spam which the resource limiting algorithm will resolve. There are two communication modes that can be defined within a contract:

EOS 智能合约通过消息和访问共享内存数据库的形式进行通信。例如，一个合约可以读取另外一个合约的数据库状态，只要它被包含在一个异步事务读取范围内。异步通信可能造成垃圾消息，但是资源限制算法将解决这个问题。在一个合约中可以定义两种通信模型：

- **Inline**. Inline is guaranteed to execute with the current transaction or unwind; no notification will be communicated regardless of success or failure. Inline operates with the same scopes and authorities with the same scopes and authorities the original transaction had.  

- **内联**。内联被保证在当前事务中被执行，不管通信成功或者失败都没有通知。内联操作与原始的事务拥有相同的作用域和权限。  

- **Deferred**. Defer will get scheduled later at producer's discretion; it's possible to communicate the result of the communication or can simply timeout. Deferred can reach out to different scopes and carry the authority of contract that sends them. *This feature is not available in STAT

- **延期**。延期将根据生产者的预期来安排，它可以传达通信的结果或者简单的超时。延期可以访问不同的作用域，并且可以传递合约的权限。*这个特性在 STAT 中不可用。

#### Message vs Transaction
#### 消息 vs 事务

A message represents a single operation, whereas a transaction is a collection of one or more messages. A contract and an account communicate in the form of messages. Messages can be sent individually, or in combined form if they are intended to be executed as a whole.  

一个消息代表一个简单的操作，然而事务是一个或者多个消息的集合。一个合约和一个帐号以消息的形式通信。消息可以被单独发送，也可以以组合的形式发送，以便它们被当成一个整体来执行。

Transaction with 1 message.  

包含1个消息的事务  

``` JSON
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

Transaction with multiple messages, these message should either all be successed or all failed.  

包含多个消息的事务，这些消息要么全部成功要么全部失败。

``` JSON
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

#### Message Name Restrictions
#### 消息名字限制

Message types are actually **base32 encoded 64-bit** integers. This means they are limited to the characters a-z, 1-5, and '.' for the first 12 characters. If there is a 13th character then it is restricted to the first 16 characters ('.' and a-p).

消息类型是base32编码的64位整数。这意味着开头12个字符的范围被限制在a-z, 1-5, 和'.'这些字符中。如果有第13个字符，它就被限制在最初16个字符（'.' 和 a-p）的范围内。

#### Transaction Confirmation
#### 交易确认  
Receiving a transaction hash does not mean that the transaction has been confirmed, it only means that the node accepted it without error, which also means that there is a high probability of other producers will accept it.  
收到一个交易的哈希并不意味着这个交易已经被确认，这仅仅意味着节点在没有产生错误的情况下接受了它，同时也意味其他生产者也更有可能接受它。  
By means of confirmation, you should see the transaction in transaction history with the block number of which it is included.  
确认的意思是，你可以通过包含这笔交易的区块的区块号在交易历史记录中查看到这笔交易。

### 1.3. Technical Limitation
### 1.3. 技术限制  
- **No floating point**. Contracts will not accept floating point operation since it is a non-deterministic behavior at CPU level which could lead to unintended forks.

- **没有浮点数**。合约不接受浮点运算，因为这在 CPU 层存在不确定的行为，可能会导致意外的分叉。

- **Transaction to be executed within 1 ms**. Execution time of a transaction needs to be less than or equal to 1 ms or the transaction will fail.

- **交易必须在1ms内执行**。交易的执行时间需要小于或等于 1 毫秒，否则交易将失败。

- **Maximum 30 tps**. The public testnet at the moment is set up in the way that each account is limited to publish maximum 30 transactions per second.

- **最大每秒30笔交易**。 目前公测网络的设置了每个账户每秒最多发布 30 笔交易的限制。

## 2 Smart Contract Files
## 2 智能合约文件

To keep things simple we have created a tool called [eoscpp](https://github.com/EOSIO/eos/wiki/Programs-&-Tools#eoscpp) which can be used to bootstrap a new contract. The eoscpp tool will create the 3 smart contract files with the basic skeleton for you to get started.  

简单起见，我们提供了一个叫做 [eoscpp](https://github.com/EOSIO/eos/wiki/Programs-&-Tools#eoscpp) 的工具，可以被用来创建一个新的合约。eoscpp 工具将创建包含基本框架的3个智能合约文件，以方便你开始。  

``` Command
$ eoscpp -n ${contract}
```

The above will create a new empty project in the './${project}' folder with three files:

上面的命令在文件夹 './${project}'中创建了一个新的空项目，包含以下三个文件：

``` file
${contract}.abi ${contract}.hpp ${contract}.cpp
```

### 2.1. HPP
HPP is the header file that contain the variables, constants, and functions referenced by the CPP file.

HPP是包含变量、常量和函数的头文件，它被cpp文件引用。

### 2.2. CPP

The CPP file is the source file that contains the functions of the contract.

CPP文件是包含合约函数的源文件。

If you generate the CPP file using the eoscpp tool, the generated cpp file would look similar to the following:

如果是用eoscpp工具生成这个CPP文件，这个生成的cpp文件类似如下形式：

``` C
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

``` C
#include <${contract}.hpp>

/**
 *  init() 和 apply() 函数必须符合C调用约定，
 *  保证区块链可以查找和调用到这两个方法。
 */
extern "C" {

    /**
     *  这个函数在合约被发布或者更新时被调用一次。
     */
    void init()  {
       eosio::print( "Init World!\n" ); // 用真实代码替换
    }

    /// apply 函数实现这个合约事件的分发
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
    }

} // extern "C"
```

In there you can see there are 2 functions being created, `init` and `apply`. All they do are log the messages delivered and makes no other checks. Anyone can deliver any message at any time provided the block producers allow it. Absent any required signatures, the contract will be billed for the bandwidth consumed.

这里你可以看到有2个函数被创建，`init`和`apply`。他们做的事只是记录传递的信息，并且没有进行其他的检查。任何人都可以在任何时间传递任何消息，只要区块的生产者允许。在没有所需的签名的情况下，合约将被按照所消耗的带宽收费。

#### init

The init function will only be executed once at initial deployment. It is used for initializing contract variables, e.g. the number of token supply for a currency contract.

init函数只会在初始化部署的时候被执行一次。它被用来初始化合约变量。例如货币合约的代币数量。

#### apply

apply is the message handler, it listens to all incoming messages and reacts according to the specifications within the function. The apply function requires two input parameters, code and action.

apple函数是消息处理器，它建提供所有进入的消息，然后根据函数内部的定义进行处理。apply函数需要两个输入参数，code和action。

#### code filter

In order to respond to a particular message, you can structure your apply function as the following. You may also construct response to general messages by omitting the code filter.

为了响应一个特定的消息，你可以用以下的方式构造你的apply函数，你也可以通过省略代码过滤器来构造对一般消息的响应。

``` C
if (code == N(${contract_name}) {
    //your handler to response to particular message
}
```

``` C
if (code == N(${contract_name}) {
    //你响应特定消息的响应函数
}
```

Within that you can also define response to respective actions.

通过这种形式你可以定义不同动作的响应方式。

#### action filter
#### 动作过滤器

To respond to a particular action, you can structure your apply function as the following. This is normally used in conjuction with the code filter.

为了响应特定的操作，你可以用下面的方式构造你的apply函数。 这通常与代码过滤器结合使用。

``` C
if (action == N(${action_name}) {
    //your handler to respond to a particular action
}
```

``` C
if (action == N(${action_name}) {
    //你响应特定事件的响应函数
}
```

### 2.3. WAST
Any program that wants to deploy to the EOS.IO blockchain must first compile into WASM format. This is the only format the blockchain accepts.

任何想要部署到EOS.IO区块链的程序都必须先编译成WASM格式。 这是区块链接受的唯一格式。

Once you have the CPP file ready, you can compile it into a text version of WASM (.wast) using the `eoscpp` tool.

``` C
$ eoscpp -o ${contract}.wast ${contract}.cpp
```

### 2.4. ABI
The Application Binary Interface (ABI) is a JSON-based description on how to convert user actions between their JSON and Binary representations. The ABI also describes how to convert the database state to/from JSON. Once you have described your contract via an ABI then developers and users will be able to interact with your contract seamlessly via JSON.

应用程序二进制接口（ABI）是一个基于JSON的描述，介绍如何在JSON和二进制形式之间转换用户行为。 ABI还介绍了如何在JSON之间转换数据库状态。 一旦通过ABI描述了合约，开发人员和用户就可以通过JSON无缝地与您的合约进行交互。

The ABI file can be generated from the HPP files using the eoscpp tool:

ABI文件可以使用`eoscpp`工具从HPP文件生成：

``` C
$ eoscpp -g ${contract}.abi ${contract}.hpp
```

Here is an example of what the skeleton contract ABI looks like:

下面是一个骨架合约ABI的样子：

``` C
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

你可以看到这个ABI定义了一个类型为`transfer`的动作`transfer`。这告诉EOS.IO当`${account}->transfer`消息出现时，有效负载就是`transfer`类型。类型`transfer`定义在这个对象中`name`为`transfer`的`structs`数组中。

``` C
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

It has several fields, including `from`, `to` and `quantity`. These fields have the corresponding types `account_name`, and `uint64`. `account_name` is a built-in type used to represent base32 string as uint64. To see more about what built-in types are available, check [here](https://github.com/EOSIO/eos/blob/b2af4daa8acb64bbb341fd85f7e8a2cd54fa4de4/libraries/types/abi_serializer.cpp).

它包含一些字段，包括`from`，`to`和`quantity`。这些字段都包含相关的类型`account_name`和`uint64`。`account_name`是一个内置类型通常代表base32编码的64位整数。点击[这里](https://github.com/EOSIO/eos/blob/b2af4daa8acb64bbb341fd85f7e8a2cd54fa4de4/libraries/types/abi_serializer.cpp)查看更多的内置类型。

``` C
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
...
```

Inside the above `types` array we define a list of alias for existing type. Here, we define `name` as an alias of `account_name`.

在上面`types`数组中，我们定义了当前存在类型的别名，我们定义`name`作为`account_name`的别名。

# 3. Checklist
# 3. 检查清单

Before getting started with an EOS Smart Contract be sure to do all the following:

在开始EOS智能合约之前，确保完成以下的事情：

#### Build the latest build
#### 编译最新版本

Make sure you have the latest build in your environment, you will need that in order to access `eoscpp` and `eosc,`` the tools that are necessary for you to get started. Instructions on getting the latest built can be found in the [Environment](https://github.com/EOSIO/eos/wiki/Local-Environment) section.

确保在你的环境中是最新的构建版本，以便可以获取`eoscpp`和`eosc`。你必须利用这些工具来开始创建合约。获取最新的构建方式的指导可以在[环境](https://github.com/EOSIO/eos/wiki/Local-Environment)这部分找到。

Once you have the latest eosio/eos code installed, make sure that ${CMAKE_INSTALL_PREFIX}/bin is in your path, or you will have to install it by running the following command.

一旦你有最新的eosid/eos代码，确保${CMAKE_INSTALL_PREFIX}/bin在你的环境变量中，否则你需要按照以下的命令来安装它。

``` Command
cd build
make install
```

#### Connect to the EOS.IO blockchain
#### 连接到EOS.IO 区块链

You can connect to a node using the command  
你可以通过下面的命令连接到一个节点  

``` command
$ eosc -H ${node_ip} -p ${port_num}
```

node_ip can be a private node's IP of you can connect to the public testnet using public nodes ip [here](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public#nodes).  
node_ip可以是私有的节点IP，如果你可以连接到公共测试网络可以用[这里](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public#nodes)的公共节点IP。

port_num is either 8888 or 8889, depending on the configuration.  
port_num 是8888或8889，依赖你的配置。

#### Create a wallet and have access to an account
#### 创建一个钱包并且授权给一个账户

In order to deploy a contract to the blockchain, you will need an account created on the EOS.IO blockchain. Every contract requires an associated account.

为了部署一个合约到区块链上，你需要在EOS.IO区块链上创建一个帐号。每一个合约都需要一个关联帐号。

If you hold EOS Tokens already you should have an account on the public testnet. If you need to create a new account for testing, please follow the instructions below:

如果你已经拥有EOS代币，你应该已经在公测网络上拥有一个帐号。如果你需要创建一个新的帐号来做测试，请依照以下步骤执行：

- [Create a wallet](https://github.com/EOSIO/eos/wiki/Tutorials#11-creating-and-managing-wallets)
- [Create an account](https://github.com/EOSIO/eos/wiki/Tutorials#14-creating-an-account)
- [Import your account in the wallet created](https://github.com/EOSIO/eos/wiki/Tutorials#12-generating-and-importing-eos-keys)

- [创建一个钱包](https://github.com/EOSIO/eos/wiki/Tutorials#11-creating-and-managing-wallets)
- [创建一个帐号](https://github.com/EOSIO/eos/wiki/Tutorials#14-creating-an-account)
- [在钱包中导入帐号](https://github.com/EOSIO/eos/wiki/Tutorials#12-generating-and-importing-eos-keys)


# 4. Interacting with Smart Contract Examples
# 4. 与智能合约样例交互

Before deep diving into building a smart contract, there are smart contract examples which you can reference so to understand how EOS smart contract functions.

在深入构建一个智能合约之前，这里有一些智能合约的样例，让你来理解EOS智能合约是如何起作用的。

In order to interact with these sample contracts, you will need to first complete all items on the [checklist](https://github.com/EOSIO/eos/wiki/Smart%20Contract#3-checklist) above and deploy the sample contracts to the EOS.IO blockchain.

为了同这些样例合约交互，你需要首先完成以上的[检查列表](https://github.com/EOSIO/eos/wiki/Smart%20Contract#3-checklist)，并且部署样例合约到EOS.IO区块链。

## 4.1. The Currency Contract
## 4.1. 现金合约

#### Deploying the sample contract
#### 部署样例合约

The example currency contracts can be found [here](https://github.com/EOSIO/eos/tree/master/contracts/currency), if you have downloaded the EOSIO repository, you should be able to find it on your local drive.

样例现金合约可以在[这里](https://github.com/EOSIO/eos/tree/master/contracts/currency)被找到。如果你已经下载了EOSIO仓库，你应该可以在你本地驱动器中找到他。

The folder contains the .abi, .cpp and .hpp files, you will need to generate the .wast file before you can deploy the contract.

这个文件夹包含.abi,.cpp和.hpp文件，在部署合约之前你需要生成.wast文件。

``` Command
$ eoscpp -o currency.wast currency.cpp
```

Once you have successfully generated the .wast file, you can use the `set contract` command to deploy.

一旦你成功生成这个.wast文件，你可以用`set contract`命令去部署。

``` Command
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

确保你的钱包没有被锁定，并且${contract_account_name}被导入。

#### Understanding the contract
#### 理解合约

Now that we have deployed the contract, anybody can use the `eosc`'s `get code` to retrieve the .abi of the contract and understand what interface is available for this contract.

现在我们已经部署了合约，任何人可以利用`eosc`的 `get code`来检索合约的.abi文件，并且理解这个合约有哪些接口可利用。

``` Command
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

#### Observations
#### 观察

- The contract accepts an action called `transfer` that accepts a message with fields `from`, `to`, and `quantity`
- 这个合约接受`transfer`的动作，可接受包含`from`，`to`和`quantity`参数的消息。

- There is a table named `account`, that stores the data
- 这里有一个名为`account`的表格来存储数据

Now that we have found a transfer action and the account table that we can use to check the balance, we can use `eosc` to interact with them.

现在我们已经找出有一个transfer动作和一个名为account的表格，这样我们可以检查账户余额，利用`eosc`来和他们交互。

#### Read account balance
#### 读取账户余额

To query data from a table, simply use the `get table` command with the syntax `eosc get table ${account} ${contract} ${table}`.

从表格中查询数据，可简单的使用`get table`命令完成，例如`eosc get table ${account}`

``` Command
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

### Transfer funds
### 转移资金

Anyone can send any message to any contract at any time but the contracts may reject messages which are not given necessary permission. Messages are not sent "from" anyone, they are sent "with permission of" one or more accounts and permission levels.

任何人都可以在任何时间给发送任意消息给任意的合约，但是在没有足够的权限的情况下，合约可能会拒绝接收消息。消息并不是从某人发出，而是被有用权限的一个或者多个账户发送。

The following command would transfer 50 token from account_a to account_b within the currency contract.

以下的命令将利用现金合约从account_a转移50个代币到account_b。

``` Command
$ eosc push message currency transfer '{"from":"${account_a}","to":"${account_b}","quantity":50}' --scope ${account_a},${account_b} --permission ${account_a}@active
```

We specify the `--scope` argument to give the currency contract read/write permission to those users so it can modify their balances. In a future release scope will be automatically determined.

我们使用`--scope`参数将现金合约读写权限授权给这些用户，以便它可以修改账户余额。将来的发布版中，scope 将会被自动确定。

As a confirmation of a successfully submitted transaction, you will receive JSON output that includes a `transaction_id` field.

作为一个成功提交的交易的确认，你将收到包含`transaction_id`的JSON字符串输出。

``` Command
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

一旦你收到成功的结果，你可以通过帐号表来读取这个帐号余额，检查这个帐号的状态，就像你之前做的一样。

## 4.2. Tic-Tac-Toe
## 4.2. 井字棋

The tic-tac-toe contract is a paper-and-pencil game for two players, X and O, who take turns marking the spaces in a 3×3 grid. The player who succeeds in placing three of their marks in a horizontal, vertical, or diagonal row wins the game.

这个井字棋合约是一个两人玩的纸笔游戏，轮流在3×3点表格中做X和O的标记。成功在表格里标记3个水平，垂直或者对角线的人赢得比赛。

#### Game rules

- Each player pair can have up to 2 unique games, one where player_1 becomes host and player_2 become challenger and vice versa
- 每对玩家可以有最多2个角色，player_1作为擂主， player_2作为挑战者，反之亦然。

- The game data is stored inside games table of "host" scope with "challenger" as the key
- 这个游戏的数据被存储在游戏表里的“host”字段，"challenger"作为键。

#### Example
| Coordinate | 0 | 1 | 2 |
| ---- |--  |-- |--  |
| 0 | - | o  | x |
| 1 | - | x | - |
| 2 | x | o | o |


Board is represented with number:  
棋牌用数字表示  
- 0 represents empty cell  
- 0表示空单元格  
- 1 represents cell filled by host  
- 1表示由擂主填充的单元格
- 2 represents cell filled by challenger  
- 2表示由挑战者填充的单元格

Therefore, assuming x is host, o is challenger, the above board will have the following representation: [0, 2, 1, 0, 1, 0, 1, 2, 2] inside the game object.

所以，假设X是擂主，o是挑战者。上面的棋盘用游戏对象描述如下[0, 2, 1, 0, 1, 0, 1, 2, 2]

#### Deploying the sample contract
#### 部署样例条约

The example tic_tac_toe contracts can be found [here](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe), if you have downloaded the EOSIO repository, you should be able to find it in your local drive.

井字棋的合约可以在[这里](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe)被找到。如果你已经下载了EOSIO仓库，你可以在你的本地磁盘中找到。

The folder contains the .abi, .cpp and .hpp files, you will need to generate the .wast file before you can deploy the contract.

这个文件夹包含.abi,.cpp和.hpp文件，在部署合约之前你需要生成.wast文件。

``` Command
$ eoscpp -o tic_tac_toe.wast tic_tac_toe.cpp
```

Once you have successfully generated the .wast file, you can use the set contract command to deploy. For this example, we are going to deploy it on account tic.tac.toe. Note that the EOS.IO blockchain only supports base32 char for the account name that's why, underscore is replaced with '.'. If you are going to deploy it to other account beside tic.tac.toe, replace any occurrence of tic.tac.toe in the .hpp, .cpp, and .abi with your account name.

一旦你成功生成.wast文件，你可以利用set contract命令去部署。在这个例子中，我们可以把它部署在帐号tic.tac.toe中。注意EOS.IO区块链的帐号名只支持base32字符，这是为什么下划线被替换成'.'。如果你准备部署它到其他帐号而不是tic.tac.toe，请在.hpp, .cpp和.abi文件里把tic.tac.toe替换成你的帐号名。

``` Command
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

#### Understanding the contract
#### 理解合约

Now that we have deployed the contract, anybody can use the eosc's get code to retrieve the .abi of the contract and understand what interface is available for this contract.

现在我们已经部署了合约，任何人可以用`eosc`'s `get code`去获取合约的.abi和得到这个合约所暴露的接口。

``` Command
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

#### Observations
#### 观察

- The contract accepts actions called `create`, `restart`, `close` and `move` where each actions accept message with different fields
- 这个合约接受`create`, `restart`, `close` 和 `move` 事件，每个事件都接受不同的消息。
- There is a table called `games`, that stores the data
- 这里有一个叫做`games`的表来存储数据

#### How to play the game:
#### 如何玩这个游戏

- Create a game using `create` action, with you as the host and other account as the challenger.
- 使用`create`动作来创建游戏，你是擂主，其他帐号是挑战者。

``` command
$ eosc push message tic.tac.toe create '{"challenger":"${challenger_account_name}","host":"${your_account_name}"}' --permission ${your_account}@active
```

- The first move needs to be done by the host, use the `move` action to make a move by specifying which row and column to fill.
- 必须由擂主进行第一步，使用`move`动作来指定填充哪一个格子。

``` Command
$ eosc push message tic.tac.toe move '{"challenger":"${challenger_account_name}","host":"${your_account_name}","by":"${your_account_name}","''{"row":0,"column":1}"}' --permission ${your_account}@active
```

- Then ask the challenger to make a move, after that it's the host's turn again. Repeat until the winner is determined.
- 然后让挑战者走下一步，接着又轮到擂主。就此反复，直到分出胜负。

``` Command
$ eosc push message tic.tac.toe move '{"challenger":"${challenger_account_name}","host":"${your_account_name}","by":"${your_account_name}","''{"row":1,"column":1}"}' --permission ${challenger_account}@active
```

- To restart the game, use the `restart` action
- 使用`restart`方法重新开始游戏

``` Command
$ eosc push message tic.tac.toe restart '{"challenger":"${challenger_account_name}","host":"${your_account_name}","by":"${your_account_name}"}' --permission ${your_account}@active
```

- To clear the game from the database, use the `close` action. This will free up space after the game has concluded.
- 使用`close`动作可以将游戏从数据库中清除。在游戏结束后可以清除空间。

``` Command
$ eosc push message tic.tac.toe close '{"challenger":"${challenger_account_name}","host":"${your_account_name}"}' --permission ${your_account}@active
```

# 5. Writing your first EOS smart contract
# 5. 编写你的第一个EOS智能合约

#### Hello World

In this section, we will be building a **hello world** contract step by step.

这一节里，我们将一步一步构建一个**hello world**合约

Before you begin, you will need to first complete all items on the [checklist](https://github.com/EOSIO/eos/wiki/Smart%20Contract#3-checklist) above.  

在你开始之前，你需要先完成检查清单里所有的项目。

**Let's begin** First, we use `eoscpp` to generate the skeleton of the smart contract. This will create a new empty project in the **hello** folder with the abi, hpp and cpp file.   

**让我们开始** 首先，我们使用 `eoscpp` 来生成智能合约框架。这将在**hello**文件夹中创建一个空的项目，包含abi,hpp和cpp文件。

``` Command
$ eoscpp -n hello
```

The CPP file should contain a sample code which will print the text **Hello World: ${account}->${action}** when it receives a message.

当它收到消息时，CPP文件应该包含一个简单的代码来打印出文本**Hello World: ${account}->${action}**

``` command
void apply( uint64_t code, uint64_t action ) {
   eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
}
```

We should now generate the .wast from this cpp file.

我们现在应该从这个cpp文件中生成.wast

``` Command
$ eoscpp -o hello.wast hello.cpp
```

Now that you have the .wast and .abi files, you can deploy your contract to the blockchain.

现在你获得来.wast和.abi文件，你可以将你的合约部署到区块链上了。

Assuming your wallet is unlocked and has keys for `${account}`, you can now upload this contract to the blockchain with the following command:

假设你的钱包没有被锁定并且有`${account}`的键值，你现在可以用以下的命令上传这个合约到区块链上。

``` Command
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

如你你在监视你的eosd进程，你可以看到：

``` Command
...] initt generated block #188249 @ 2017-09-13T22:00:24 with 0 trxs  0 pending
Init World!
Init World!
Init World!
```

You will notice the lines "Init World!" are executed 3 times. This isn't a mistake. When the blockchain is processing transactions the following happens:

你会注意到，"Init World!"这行被执行了3次。这不是错误。当区块链在处理事物时，会发生下面的事情：

1st : eosd receives a new transaction (validating transaction)

第一 ： eosd收到一个新的事务（校验事务）
- creates a temporary session
- 创建一个临时会话
- attempts to apply the transaction
- 试图应用这个事务
- succeeds and prints "Init World!"
- 成功打出"Init World!"
- or fails undoes the changes (potentially failing after printing "Init World!")
- 或者失败取消改变（在打印出"Init World!"后潜在的失败）

2nd : eosd starts to produce a block
第二 ： eosd 开始生产一个区块
- undoes all pending state
- 取消所有挂起状态
- pushes all transactions as it builds the block
- 将所有的事务构建入区块
- prints "Init World!" a second time
- 第二次输出"Init World!"
- finishes building the block
- 结束构建区块
- undoes all of the temporary changes while creating block
- 当创建区块时取消所有临时修改

3rd : eosd pushes the generated block as if it is received it from the network

第三 ： eosd 推送生成的区块，好像它被从网络上接收一样。

- prints "Init World!" a third time
- 第三次输出"Init World!"

At this point, your contract is ready to start receiving messages. Since the default message handler accepts all messages we can send it anything we want. Let's try sending it an empty message:

这时，你的合约已经准备好接收消息了。因为默认的消息处理器可以接收所有的消息，所以我们可以给它发我们想发的。让我们尝试发送一个空消息：

``` command
$ eosc push message ${account} hello '"abcd"' --scope ${account}
```

This command will send the message "hello" with binary data represented by the hex string "abcd". Note, in a bit, we will show how to define the ABI so that you can replace the hex string with a pretty, easy-to-read, JSON object. For now, we merely want to demonstrate how the message type "hello" is dispatched to account.

这个命令将发送"hello"消息，参数是十六进制字符串"abcd"代表的二进制数据。注意，过一会，我们将展示如何定义ABI，以便你可以使用一个优雅，可读的JSON对象来替代十六进制字符串。目前，我们只是想示范"hello"消息被分发给帐号。

结果是：

``` Command
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

If you are following along in eosd, then you should have seen the following scroll by the screen:

如果你跟随eosd，你会看到屏幕会滚动显示以下内容：

``` Command
Hello World: ${account}->hello
Hello World: ${account}->hello
Hello World: ${account}->hello
```

Once again your contract was executed and undone twice before being applied the 3rd time as part of a generated block.

你的合约被执行，并且被撤销两次，第3次作为生成块的一部分。

If we look into the ABI file, you will notice it defines an action `transfer` of type `transfer`. This tells EOS.IO that when `${account}->transfer` message is seen that the payload is of type `transfer`. The type `transfer` is defined in the `structs` array in the object with `name` set to `"transfer`".

如果我们打开ABI文件，你会注意到它定义了一个类型为`transfer`的动作`transfer`。这告诉EOS.IO当`${account}->transfer`消息出现时，有效负载就是`transfer`类型。类型`transfer`定义在这个对象中`name`为`transfer`的`structs`数组中。

``` Command
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

现在我们已经看到

``` Command
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

如果你检查eosd的输出窗口，你会看到：

``` command
Hello World: ${account}->transfer
Hello World: ${account}->transfer
Hello World: ${account}->transfer
```

According to the ABI the transfer message has the format:

根据ABI，transfer消息有着以下的格式：

``` command
"fields": {
    "from": "account_name",
    "to": "account_name",
	"quantity": "uint64"
  }
```

We also know that account_name -> uint64 which means that the binary representation of the message is the same as:

我们都知道 account_name -> uint64 意味着消息的二进制表示和以下一样：

``` Command
struct transfer {
    uint64_t from;
    uint64_t to;
    uint64_t quantity;
};
```

The EOS.IO C API provides access to the message payload via the Message API:

EOS.IO C语言API提供消息API来访问消息的负载内容。

``` Command
uint32_t message_size();
uint32_t read_message( void* msg, uint32_t msglen );
```

Let's modify hello.cpp to print out the content of the message:

让我们修改 hello.cpp 来打印消息的内容：

``` Command
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

我们可以重新编译和部署：

``` command
eoscpp -o hello.wast hello.cpp
eosc set contract ${account} hello.wast hello.abi
```

eosd will call init() again because of the redeploy

重新部署后eosd会再次调用 init() 函数

``` command
Init World!
Init World!
Init World!
```

Then we can execute transfer:

然后我们可以执行转移：

``` Command
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

我们可以在eosd窗口中看到如下的输出：

``` command
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
```

#### Using C++ API to Read Messages
#### 使用C++ API来读取消息

So far we used the C API because it is the lowest level API that is directly exposed by EOS.IO to the WASM virtual machine. Fortunately, eoslib provides a higher level API that removes much of the boilerplate.

到此位置，我们使用来C API，因为它是EOS.IO直接暴露给WASM虚拟机最底层的API。幸运的是，eoslib提供来一个更高层的API，移除了大量的样板。

``` command
/// eoslib/message.hpp
namespace eosio {
	 template<typename T>
	 T current_message();
}
```

We can update hello.cpp to be more concise as follows:

我们可以用以下简洁的方式更新hello.cpp

``` Command
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

你会注意到我们使用`eosio::name`类型来直接替代`transfer`结构，并且将`read_message`相关的代码简化成`current-Message`。

After compiling and uploading it you should get the same results as the C version.

在编译和上传之后，你会得到和C语言版本一样的结果。

#### Requiring Sender Authority to Transfer
#### 转账时请求发送方权限

One of the most common requirements of any contract is to define who is allowed to perform the action. In the case of a currency transfer, we want to require that the account defined by the from parameter signs off on the message.

对于合约来说，一个最重要的需求就是定义谁可以执行这个动作。在货币转移的例子当中，我们需要有from参数的帐号来签名这个消息。

The EOS.IO software will take care of enforcing and validating the signatures, all you need to do is require the necessary authority.

EOS.IO 软件将强制执行和验证签名，你所要做的就是请求必要的权限。

``` C
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

在编译和部署完成后，我们可以再次尝试转账：

``` command
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

在eosd窗口你会看到这些：

``` Command
Hello World: initc->transfer
1881629ms thread-0   chain_api_plugin.cpp:60       operator()           ] Exception encountered while processing chain.push_transaction:
...
```

This shows that it attempted to apply your transaction, printed the initial "Hello World" and then aborted when eosio::require_auth failed to find authorization of account initb.

上面输出展示它试图应用你的转账，打印出初始的"Hello World"，然后当eosio::require_auth没有正确获取到账户initb的授权后，取消了这笔交易。

We can fix that by telling eosc to add the required permission:

我们可以通过告诉eosc添加所需要的权限：

``` Command
$ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account} --permission initb@active
```

The `--permission` command defines the account and permission level, in this case we use the active authority which is the default.

`--permission` 命令定义这个账户以及它的权限，这个例子中，我们使用默认的活动权限。

This time the transfer should have worked like we saw before.

这次，转账会想我们之前看到那样执行。

#### Aborting a Message on Error
#### 在遇到错误时终止消息执行

A large part of contract development is verifying preconditions, such that the quantity transferred is greater than 0. If a user attempts to execute an invalid action, then the contract must abort and any changes made get automatically reverted.

合约开发中一大部分的工作在于校验先决条件，例如转账金额是否大于0。如果一个用户试图执行一个无效动作，合约必须要终止这个动作，并且自动的回滚任何改变。

``` C
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

我们现在可以编译，部署，尝试执行一个0金额的转账：

``` Command
$ eoscpp -o hello.wast hello.cpp
$ eosc set contract ${account} hello.wast hello.abi
$ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":0}' --scope initc --permission initb@active
3071182ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
status_code == 200: Error
: 10 assert_exception: Assert Exception
test: assertion failed: Must transfer a quantity greater than 0
```

Now that you have completed the Hello World tutorial, you are ready to write your first Smart Contract.
现在你已经完成了Hello World的指导课程，你已经可以编写你的第一个智能合约。

# 6. Deploy and update Smart Contract
# 6. 部署和更新智能合约

As mentioned in the tutorial above, deploying a contract onto the blockchain can simply be done by using the `set contract` command. In addition, the `set contract` command will also update an existing contract, if you have permission to do so.

就像在刚才指导课程中提到的一样，可以简单的使用`set contract`部署一个合约到区块链上。另外， `set contract`命令在你有权限的时候，还可以更新一个已经发布的合约。

Use the following command to:
利用下面的命令可以：

- deploy a new contract, and  
- 部署一个新合约，以及  
- update an existing contract  
- 更新一个已存在的合约  

``` Command
$ eosc set contract ${account} ${contract}.wast ${contract}.abi
```

# 7. Command Summary
# 7. 命令汇总

Download and build the latest EOS.IO software `$ build.sh ${architecture} ${build_mode}`
下载编译最新的EOS.IO 程序`$ build.sh ${architecture} ${build_mode}`

Writing smart contract
编写智能合约

- Create the skeleton using the eoscpp tool `$ eoscpp -n ${contract}`
- 使用eoscpp工具`$ eoscpp -n ${contract}`创建合约框架
- Program your smart contract in the .cpp & .hpp file
- 在.cpp和.hpp文件中编写你的智能合约
- Generate the .abi file `$ eoscpp -g ${contract}.abi ${contract}.hpp`
- 使用`$ eoscpp -g ${contract}.abi ${contract}.hpp`命令生成.abi文件
- Generate the .wast file `$ eoscpp -o ${contract}.wast ${contract}.cpp`
- 使用`$ eoscpp -o ${contract}.wast ${contract}.cpp`命令来生成.wast文件

Deploy smart contract
部署智能合约

- Connect to a node `$ eosc -H ${node_ip} -p ${port_num}`
- 使用`$ eosc -H ${node_ip} -p ${port_num}`创建一个节点
- Create a wallet `$ eosc wallet create`
- 使用`$ eosc wallet create`创建一个钱包
- [Create an account] if you do not already hold an EOS keys
- 【创建一个帐号】如果你没有EOS密钥
- Import your account key `$ eosc wallet import ${private_key}`
- 使用`$ eosc wallet import ${private_key}`导入你的帐号密钥
- Unlock your wallet `$ eosc wallet unlock ${wallet}`
- 使用`$ eosc wallet unlock ${wallet}`解锁你的钱包
- Deploy the contract `$ eosc set contract ${account} ${contract}.wast ${contract}.abi`
- 使用 `$ eosc set contract ${account} ${contract}.wast ${contract}.abi` 部署合约

# 8. Debugging Smart Contract
# 8. 调试智能合约

In order to be able to debug your smart contract, you will need to setup local eosd node. This local eosd node can be run as separate private testnet or as an extension of public testnet (or the official testnet).

你需要设置本地的eosd节点来调试你的智能合约。这个本地的eosd节点可以被运行为独立的私有测试网络，或者作为公有测试网络（或官方测试网络）的扩展。

When you are creating your smart contract for the first time, it is recommended to test and debug your smart contract on a private testnet first, since you have full control of the whole blockchain. This enables you to have unlimited amount of eos needed and you can just reset the state of the blockchain whenever you want. When it is ready for production, debugging on the public testnet (or official testnet) can be done by connecting your local eosd to the public testnet (or official testnet) so you can see the log of the testnet in your local eosd.

因为你拥有整个区块链的控制权，所以在当你第一次创建智能合约时，建议你先在私有测试网络上进行测试和调试。这可以让你用户无限数量的EOS，而且你可以随时重置区块链状态。当你的合约可以发布时，可以通过你本地的eosd连接到公有测试网络（或官方测试网络）上进行测试，这样你可以在你本地的eosd控制台上看到测试网络的日志。

The concept is the same, so for the following guide, debugging on the private testnet will be covered.

这个概念是相同的，对于一下的指南，你可以在私有测试网络中进行。

If you haven't set up your own local eosd, please follow the [setup guide](https://github.com/EOSIO/eos/wiki/Local-Environment). By default, your local eosd will just run in a private testnet unless you modify the config.ini file to connect with public testnet (or official testnet) nodes as described in the following [guide](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public).

如果你海没有设置你自己的本地eosd，请按照[设置指导](https://github.com/EOSIO/eos/wiki/Local-Environment)进行。默认的，你的eosd本地测试网络将运行一个私有测试网络，除非你按照一下的[指导](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public)修改config.ini文件来连接到公有测试网络（或官方测试网络）。

## 8.1. Method
## 8.1. 方法

The main method used to debug smart contract is **Caveman Debugging**, where we utilize the printing functionality to inspect the value of a variable and check the flow of the contract. Printing in smart contract can be done through the Print API ([C](https://github.com/EOSIO/eos/blob/master/contracts/eoslib/print.h) and [C++](https://github.com/EOSIO/eos/blob/master/contracts/eoslib/print.hpp)). The C++ API is the wrapper for C API, so most often we will just use the C++ API.

用于调试智能合约的主要方法是**野蛮人调试**，利用打印功能来检查变量的值以及检查合约的流程。可以利用打印接口（([C](https://github.com/EOSIO/eos/blob/master/contracts/eoslib/print.h) 和 [C++](https://github.com/EOSIO/eos/blob/master/contracts/eoslib/print.hpp))）在智能合约中进行输出。C++ 接口是 C 接口的封装，所以我们经常只用C++接口。


## 8.2. Print
Print C API supports the following data type that you can print:
C 打印接口支持一下的数据类型：

- prints - a null terminated char array (string)
- prints - 空字符结尾的字符数组（字符串）
- prints_l - any char array (string) with given size
- prints_l - 戈丁大小的字符数组（字符串）
- printi - 64-bit unsigned integer
- printi - 64位无符号整型
- printi128 - 128-bit unsigned integer
- printi128 - 128位无符号整型
- printd - double encoded as 64-bit unsigned integer
- printd - 双编码64位无符号整型
- printn - base32 string encoded as 64-bit unsigned integer
- printn - base32编码的64位无符号整数
- printhex - hex given binary of data and its size
- printhex - 给定的二进制数据和大小的16进制数据

While Print C++ API wraps some of the above C API by overriding the print() function so user doesn't need to determine which specific print function he needs to use. Print C++ API supports

而 C++ 打印函数通过 print() 封装了以上的一些 C 接口，所以使用者不需要决定使用哪一个打印函数。C++ 打印接口支持：

- a null terminated char array (string)
- 空字符结尾的字符数组（字符串）
- integer (128-bit unsigned, 64-bit unsigned, 32-bit unsigned, signed, unsigned)
- 整型（128位无符号，64位无符号，32位无符号，有符号，无符号）
- base32 string encoded as 64-bit unsigned integer
- base32编码的64位无符号整数
- struct that has print() method
- 包含有 print() 函数的结构体

# 8.3. Example
# 8.3. 示例

Let's write a new contract as example for debugging

让我们写一个新的合约作为示例来调试

- debug.hpp

``` C++
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

``` C++
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

``` C
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

Let's deploy it and send a message to it. Assume that you have debug account created and have its key in your wallet.

让我们部署并且给他发送一条消息。假设你已经有一个调试账户，并且在你的钱包中有密钥。

``` Command
$ eoscpp -o debug.wast debug.cpp
$ eosc set contract debug debug.wast debug.abi
$ eosc push message debug foo '{"from":"inita", "to":"initb", "amount":10}' --scope debug
```

When you check your local eosd node log, you will see the following lines after the above message is sent.

当你检查你本地的eosd节点日志，在上面消息被发送后你会看到以下的信息：

``` Command
Code is debug
Action is foo
Amount is smaller than 100
Increase amount by 10
Foo from inita to initb with amount 20
```

There, you can confirm that your message is going to the right control flow and the amount is updated correctly. You might see the above message at least 2 times and that's normal because each transaction is being applied during verification, block generation, and block application.

然后，你可以确定你的消息在正确的控制流中，并且数量被正确的更新。你可能看到至少2次上面的消息，这是正常的。因为每个交易被验证、块生成、块应用后被应用。


----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

张奎 区块链技术爱好者，热衷于区块链相关技术研究，欢迎加微信号:mazeboy

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

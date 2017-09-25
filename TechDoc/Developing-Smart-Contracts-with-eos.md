# Developing Smart Contracts / Decentralized Applications with EOS.IO 使用eos开发智能合约（分布式应用程序）

> 本文翻译自：https://eosio.github.io/eos/md_contracts_eoslib_tutorial.html
> 
> 译者：[区块链中文字幕组 胡亮](https://github.com/gumoon)
> 
> 翻译时间：2017-09-20

This tutorial is targeted toward those who would like to get started building decentralized applications or smart contracts using the EOS.IO software development kit. It will cover writing contracts/applications in C++ and uploading them to the blockchain. It will not cover how to build or deploy interactive web interfaces.

本教程的目标用户：想使用 eos sdk 来构建分布式应用程序或智能合约的人。包括两部分内容：如何使用 C++ 语言编写智能合约以及上传智能合约到区块链。它不涉及怎么编译eos和部署交互式web接口。

For the rest of this tutorial we will use the term "contract" to refer to the code that powers decentralized applications.

在后面的文章中，我们将使用术语”contract“表示分布式应用程序。

## Required Background Knowledge 需要的背景知识

This tutorial assumes that you have basic understanding of how to use 'eosd' and 'eosc' to setup a node and deploy the example contracts. If you have not yet successfully followed that tutorial, then do that first and come back.

本教程假定你已经基本知道如何使用 `eosd` 和 `eosc` 来搭建一个节点和部署例子合约。如果你没有按照那个教程做成功，请先去完成它，然后再回来这里。

### C / C++ Experience Required 需要有 C/C++ 编程经验

EOS.IO based blockchains execute user generated applications and code using Web Assembly (WASM). WASM is an emerging web standard with widespread support of Google, Microsoft, Apple, and others. At the moment the most mature toolchain for building applications that compile to WASM is clang/llvm with their C/C++ compiler.

EOS.IO 底层区块链使用 WASM 执行用户应用程序。WASM 是一个正被 Google、微软、苹果和其他公司广泛支持的web标准。当前构建应用程序最成熟的工具链是：使用带有c/c++编译器的 clang/llvm来编译应用程序为WASM。

Other toolchains in development by 3rd parties include: Rust, Python, and Solidiity. While these other languages may appear simpler, their performance will likely impact the scale of application you can build. We expect that C++ will be the best language for developing high-performance and secure smart contacts.


第三方的其他工具链包括：Rust，Python，和 Solidiity。这些语言看起来更简单，但是，性能可能会影响到应用程序的扩展。我们认为，C++ 是最好的用于开发高性能、安全智能合约的编程语言。

If you are not experienced with C/C++, then you should learn the basics first and then come back.

如果你对C/C++不熟，你应该先去学习一下C++基础知识，然后再回来这里。

### Linux / Mac OS X Command Line Linux 或 Mac OSX 命令行

The EOS.IO software only officially supports unix environments and building with clang.

EOS.IO 软件，官方仅支持 Unix 环境，并且使用 clang 来构建。

## Basics of Smart Contracts / Decentralized Applications 智能合约/分布式应用程序基础

Fundamentally every contract is a state machine that responds to signed user actions. These contracts are uploaded to the blockchain as pre-compiled Web Assembly (WASM) files with an ABI (Application Binary Interface).

本质上，每一个智能合约都是一个状态机。它响应签名的用户行为。智能合约以 WASM 和 ABI 的形式被上传到区块链。

To keep things simple we have created a tool called eoscpp which can be used to bootstrap a new contract. For this to work we assume you have installed the eosio/eos code installed and that ${CMAKE_INSTALL_PREFIX}/bin is in your path.

简化起见，我们已经创建了 `eoscpp` 工具来生成一个新的智能合约。该工具正常工作的前提是，你已经安装了 eosio/eos 代码，并且 `${CMAKE_INSTALL_PREFIX}/bin` 在你的 `PATH` 路径了。

> 译者说：
> `eoscpp` 工具在你 make 完eos项目之后，在 `/path/to/build/tools` 文件夹中。你需要执行 ``make install`` 来安装它。

```
$ eoscpp -n hello
$ cd hello
$ ls
```

The above will create a new empty project in the './hello' folder with three files:

以上命令执行完后，将在 `./hello` 目录下生成一个新的空项目。`hello`文件夹包括三个文件：

```
hello.abi hello.hpp hello.cpp
```

Let's take a look at the simplest possible contract:

让我们来看一下最简单可用的智能合约：

```
cat hello.cpp
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
       eos::print( "Init World!\n" );
    }
    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eos::print( "Hello World: ", eos::Name(code), "->", eos::Name(action), "\n" );
    }
} // extern "C"
```

This contract implements the two entry points, init and apply. All it does is log the messages delivered and makes no other checks. Anyone can deliver any message at any time provided the block producers allow it. Absent any required signatures, the contract will be billed for the bandwidth consumed.

这个合约实现两个入口点：init 和 apply。他们都仅仅是打印了日志，而没有做其他的校验。所以，任何人都可以在任何时间发生任何消息，只要区块生产者允许。不带任何签名的合约将会产生带宽消费的账单。

You can compile this contract into a text version of WASM (.wast) like so:

你可以像这样编译合约为文本格式的 WASM：

```
$ eoscpp -o hello.wast hello.cpp
```

### Deploying your Contract 部署合约

Now that you have compiled your application it is time to deploy it. This will require you to do the following first:

既然你已经编译完了，下面就来部署它。部署之前，需要先完成以下步骤：

1. start eosd with wallet plugin enabled 带着钱包插件启动 `eosd` 
2. create a wallet & import keys for at least one account 创建一个钱包，并且为至少一个账户导入私钥
3. keep your wallet unlocked 确保钱包没有锁定

Assuming your wallet is unlocked and has keys for ${account}, you can now upload this contract to the blockchain with the following command:

假设你的钱包没有锁定，并且有 ${account} 账户的key，你可以使用以下命令上传合约到区块链：

```
$ eosc set contract ${account} hello.wast hello.abi
Reading WAST...
Assembling WASM...
Publishing contract...
{
  "transaction_id": "1abb46f1b69feb9a88dbff881ea421fd4f39914df769ae09f66bd684436443d5",
  "processed": {
    "refBlockNum": 144,
    "refBlockPrefix": 2192682225,
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

如果你正在监控 `eosd` 的输出，你应该能看到：

```
...] initt generated block #188249 @ 2017-09-13T22:00:24 with 0 trxs  0 pending
Init World!
Init World!
Init World!
```

You will notice the lines "Init World!" are executed 3 times, this isn't a mistake. When the blockchain is processing transactions the following happens:

你已经注意到了 "Init World!" 被执行了3次，这不是错误。区块链处理交易的流程是这样的：

1. eosd receives a new transaction eosd收到一个新的交易
    * creates a temporary session 创建一个临时会话
    * attempts to apply the transaction 尝试去 apply 这个交易
    * succeeds and prints "Init World!" 成功的话并且打印： "Init World!"
    * or fails undoes the changes (potentially failing after printing "Init World!") 失败的话，撤销改动
2. eosd starts to produce a block eosd 开始生产一个区块
    * undoes all pending state 撤销所有 pending 状态
    * pushes all transactions as it builds the block  把所有的交易推送过来生产区块
    * prints "Init World!" a second time 第二次打印 ”Init World!"
    * finishes building the block 完成区块生产
    * undoes all of the temporary changes while creating block 撤销生产区块时的所有临时改变
3. eosd pushes the generated block as if it received it from the network eosd 推送生成的区块到区块链网络
    * prints "Init World!" a third time 第三次打印 "Init World"

At this point your contract is ready to start receiving messages. Since the default message handler accepts all messages we can send it anything we want. Let's try sending it an empty message:

现在，你的合约准备好开始接受消息了。因为默认的消息处理器接收任意的消息，所以，我们可以发送我们想发送的任何消息。我们来尝试发送一个空消息。

```
$ eosc push message ${account} hello '"abcd"' --scope ${account}
```

This command will send the message "hello" with binary data represented by the hex string "abcd". Note, in a bit we will show how to define the ABI so that you can replace the hex string with a pretty, easy-to-read, JSON object. For now we merely want to demonstrate how the message type "hello" is dispatched to account.

这个命令将发送以十六进制字符串“abcd”表示的二进制数据为消息内容的消息“hello”。注意：现在我们将展示如何定义 ABI，以便你可以使用一个美观的，易读的JSON对象来替换十六进制字符串。现在，我们只不过想举例说明，“hello”类型的消息是如何被分发给某个账号的。

The result is:

结果是：

```
{
  "transaction_id": "69d66204ebeeee68c91efef6f8a7f229c22f47bcccd70459e0be833a303956bb",
  "processed": {
    "refBlockNum": 57477,
    "refBlockPrefix": 1051897037,
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

如果你正盯着 `eosd` 的输出，你应该已经看到下面的内容滚动在屏幕上。

```
Hello World: ${account}->hello
Hello World: ${account}->hello
Hello World: ${account}->hello
```

Once again your contract was executed and undone twice before being applied the 3rd time as part of a generated block.

再一次看到，合约被执行和撤销了两次，第三次作为一个生成的区块被应用。

### Message Name Restrictions 消息名约束

Message types (eg. "hello") are actually base32 encoded 64 bit integers. This means they are limited to the charcters a-z, 1-5, and '.' for the first 12 charcters and if there is a 13th character then it is restricted to the first 16 characters ('.' and a-p).

消息类型（像：“hello”）实际上是经 base32 算法编码的64位整数。这意味着，消息名开头的12个字符被限制为:字符a-z,1-5和'.'。超过13个字符则消息名开头的16个字符限制为：'.'和 a-p。

### ABI - Application Binary Interface 应用程序二进制接口

The ABI is a JSON-based description on how to convert user actions between their JSON and Binary representations. The ABI also describes how to convert the database state to/from JSON. Once you have described your contract via an ABI then developers and users will be able to interact with your contract seemlessly via JSON.

ABI是基于JSON格式来描述在JSON格式与二进制格式之间怎么转换用户动作。ABI也描述怎么让数据库状态和JSON格式互转。一旦你通过ABI来描述你的合约，其他开发者和用户将能够通过JSON跟你的合约进行交互。

We are working on tools that will automate the generation of the ABI from the C++ source code, but for the time being you may have to generate it manually.

我们的工具将从C++源码自动生成ABI。但是，某些时候你可能不得不手动生成它。

Here is an example of what the skeleton contract ABI looks like:

这是一个骨架合约ABI的例子，看起来像这样：

```
{
  "types": [{
      "newTypeName": "AccountName",
      "type": "Name"
    }
  ],
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "AccountName",
        "to": "AccountName",
        "amount": "UInt64"
      }
    },{
      "name": "account",
      "base": "",
      "fields": {
        "account": "Name",
        "balance": "UInt64"
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
      "indextype": "i64",
      "keynames" : ["account"],
      "keytypes" : ["Name"]
    }
  ]
}
```

You will notice that this ABI defines an action transfer of type transfer. This tells EOS.IO that when ${account}->transfer message is seen that the payload is of type transfer. The type transfer is defined in the structs array in the object with name set to "transfer".

你肯定注意到这个ABI定义了一个 transfer 类型的 transfer 行为。它告诉 EOS.IO ，当向账户发送 transfer 消息，消息体为 transfer 类型。transfer 类型定义在对象的结构体数组中，名字叫 transfer。

```
...
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "AccountName",
        "to": "AccountName",
        "amount": "UInt64"
      }
    },{
...
```

It has several fields, including from, to and amount. These fields have the coresponding types AccountName, AccountName, and UInt64. AccountName is defined as a typedef in the types array to Name, which is a built in type used to encode a uint64_t as base32 (eg account names).

它包括几个字段：from, to 和 amount。这些字段对应的类型为： AccountName, AccountName 和 UInt64。AccountName 类型是 类型数组中 Name 类型的别名。Name 类型是一个內建类型，用于使用 base32 算法编码一个 uint64_t 类型值。（如：账户名）

```
{
  "types": [{
      "newTypeName": "AccountName",
      "type": "Name"
    }
  ],
...
```

Now that we have reviewed the ABI defined by the skeleton, we can construct a message call for transfer:

既然我们已经看过了 skeleton 中 ABI 的定义，现在我们来构造一个 transfer 消息调用。

```
eosc push message ${account} transfer '{"from":"currency","to":"inita","amount":50}' --scope initc
2570494ms thread-0   main.cpp:797                  operator()           ] Converting argument to binary...
{
  "transaction_id": "b191eb8bff3002757839f204ffc310f1bfe5ba1872a64dda3fc42bfc2c8ed688",
  "processed": {
    "refBlockNum": 253,
    "refBlockPrefix": 3297765944,
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
          "amount": 50
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

如果你观察 eosd 的输出，你应该看到了：

```
Hello World: ${account}->transfer
Hello World: ${account}->transfer
Hello World: ${account}->transfer
```

## Processing Arguments of Transfer Message 处理 transfer 消息参数

According to the ABI the transfer message has the format:

根据 ABI 中，transfer 消息的格式：

```
"fields": {
    "from": "AccountName",
    "to": "AccountName",
    "amount": "UInt64"
}
```

We also know that AccountName -> Name -> UInt64 which means that the binary representation of the message is the same as:

我们知道 `AccountName->Name->UInt64` ，这个转换意味着，消息的二进制格式跟下面的表示一样：

```
struct transfer {
    uint64_t from;
    uint64_t to;
    uint64_t amount;
};
```

The EOS.IO C API provides access to the message payload via the Message API:

EOS.IO 接口提供消息API来访问消息体内容。

```
uint32_t messageSize();
uint32_t readMessage( void* msg, uint32_t msglen );
```

Let's modify hello.cpp to print out the content of the message:

我们来修改 `hello.cpp` ，打印消息体的内容：

```
#include <hello.hpp>
extern "C" {
    void init()  {
       eos::print( "Init World!\n" );
    }
    struct transfer {
       uint64_t from;
       uint64_t to;
       uint64_t amount;
    };
    void apply( uint64_t code, uint64_t action ) {
       eos::print( "Hello World: ", eos::Name(code), "->", eos::Name(action), "\n" );
       if( action == N(transfer) ) {
          transfer message;
          static_assert( sizeof(message) == 3*sizeof(uint64_t), "unexpected padding" );
          auto read = readMessage( &message, sizeof(message) );
          assert( read == sizeof(message), "message too short" );
          eos::print( "Transfer ", message.amount, " from ", eos::Name(message.from), " to ", eos::Name(message.to), "\n" );
       }
    }
} // extern "C"
```

Then we can recompile and deploy it with:

接着，我们使用以下命令重新编译和部署该合约：

```
eoscpp -o hello.wast hello.cpp 
eosc set contract ${account} hello.wast hello.abi
```

eosd will call init() again because of the redeploy

因为重新部署，eosd 将再次调用 `init()` 

```
Init World!
Init World!
Init World!
```

Then we can execute transfer:

然后，我们执行 transfer 行为:

```
$ eosc push message ${account} transfer '{"from":"currency","to":"inita","amount":50}' --scope ${account}
{
  "transaction_id": "a777539b7d5f752fb40e6f2d019b65b5401be8bf91c8036440661506875ba1c0",
  "processed": {
    "refBlockNum": 20,
    "refBlockPrefix": 463381070,
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
          "amount": 50
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

在 eosd 中，我们应该能看到以下输出：

```
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
```

### Using C++ API to Read Messages 使用 C++ API来读消息

So far we used the C API because it is the lowest level API that is directly exposed by EOS.IO to the WASM virtual machine. Fortunately, eoslib provides a higher level API that removes much of the boiler plate.

到此为止，我们已经使用 C 语言接口实现了读消息。C语言接口是 EOS.IO 暴露给 WASM 虚拟机的最低级别接口。幸运的是， `eoslib` 提供更高级别的接口，来帮助我们屏蔽很多底层细节。

```
namespace eos {
     template<typename T>
     T currentMessage();
}
```

We can update hello.cpp to be more concise as follows:

我们可以像下面这样来更新 `hello.cpp`，`hello.cpp` 文件变得更加简洁了。

```
#include <hello.hpp>
extern "C" {
    void init()  {
       eos::print( "Init World!\n" );
    }
    struct transfer {
       eos::Name from;
       eos::Name to;
       uint64_t amount;
    };
    void apply( uint64_t code, uint64_t action ) {
       eos::print( "Hello World: ", eos::Name(code), "->", eos::Name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eos::currentMessage<transfer>();
          eos::print( "Transfer ", message.amount, " from ", message.from, " to ", message.to, "\n" );
       }
    }
} // extern "C"
```

You will notice that we updated the transfer struct to use the eos::Name type directly, and then condenced the checks around readMessage to a single call to currentMessage.

你肯定注意到，我们修改 transfer 结构为直接使用 `eos::Name` 类型。`readMessage`相关的代码替换为一次调用 `currentMessage`。

After compiling and uploading it you should get the same results as the C version.

重新编译并且上传到区块链后，你应该看到跟 C 版本的代码相同的结果。

## Requiring Sender Authority to Transfer

One of the most common requirements of any contract is to define who is allowed to perform the action. In the case of a curency transfer, we want require that the account defined by the from parameter signs off on the message.

一个通用的合约需求是定义谁被允许执行某个 action 。在金融交易的案例中，我们要求转出账户的消息带签名。

The EOS.IO software will take care of enforcing and validating the signatures, all you need to do is require the necessary authority.

EOS.IO 软件将强制验证签名。你只需要请求必要的授权。

```
...
void apply( uint64_t code, uint64_t action ) {
   eos::print( "Hello World: ", eos::Name(code), "->", eos::Name(action), "\n" );
   if( action == N(transfer) ) {
      auto message = eos::currentMessage<transfer>();
      eos::requireAuth( message.from );
      eos::print( "Transfer ", message.amount, " from ", message.from, " to ", message.to, "\n" );
   }
}
...
```

After building and deploying we can attempt to transfer again:

重新编译和部署后，我们再次尝试 transfer ：

```
 eosc push message ${account} transfer '{"from":"initb","to":"inita","amount":50}' --scope ${account}
 1881603ms thread-0   main.cpp:797                  operator()           ] Converting argument to binary...
 1881630ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
 status_code == 200: Error
 : 3030001 tx_missing_auth: missing required authority
 Transaction is missing required authorization from initb
     {"acct":"initb"}
         thread-0  message_handling_contexts.cpp:19 require_authorization
...
```

If you look on eosd you will see this:

在 eosd 输出里，你会看到这些：

```
Hello World: initc->transfer
1881629ms thread-0   chain_api_plugin.cpp:60       operator()           ] Exception encountered while processing chain.push_transaction:
...
```

This shows that it attempted to apply your transaction, printed the initial "Hello World" and then aborted when eos::requireAuth failed to find authorization of account initb.

这显示区块链尝试去执行你的交易，打印了初始化“Hello,World"文本，然后调用 `eos::requireAuth` 时，因找不到 initb 账户的授权信息而失败，从而，交易中断了。

We can fix that by telling eosc to add the required permission:

我们可以修复这个问题：通过添加 permission 参数来调用 `eosc`。

```
eosc push message ${account} transfer '{"from":"initb","to":"inita","amount":50}' --scope ${account} --permission initb@active
```

The --permission command defines the account and permission level, in this case we use the active authority which is the default.

`--permission` 命令选项定义了账户和权限级别。针对授权失败的情况，我们使用默认的 active 权限。

This time the transfer should have worked like we saw before.

这一次，transfer 应该像之前那样正常执行。

## Aborting a Message on Error

A large part of contract development is verifying preconditions, such that the amount transferred is greater than 0. If a user attempts to execute an invalid action, then the contract must abort and any changes made get automatically reverted.

合约开发的大部分工作是验证先决条件，如：转移的金额要大于0。如果用户尝试执行一个非法动作，合约必须中断并且自动回滚所有的更改。

```
...
void apply( uint64_t code, uint64_t action ) {
   eos::print( "Hello World: ", eos::Name(code), "->", eos::Name(action), "\n" );
   if( action == N(transfer) ) {
      auto message = eos::currentMessage<transfer>();
      assert( message.amount > 0, "Must transfer an amount greater than 0" );
      eos::requireAuth( message.from );
      eos::print( "Transfer ", message.amount, " from ", message.from, " to ", message.to, "\n" );
   }
}
...
```

We can now compile, deploy, and attempt to execute a transfer of 0:

我们编译、部署，并且尝试执行一个转移金额为0的动作：

```
$ eoscpp -o hello.wast hello.cpp
$ eosc set contract ${account} hello.wast hello.abi
$ eosc push message ${account} transfer '{"from":"initb","to":"inita","amount":0}' --scope initc --permission initb@active
3071182ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
status_code == 200: Error
: 10 assert_exception: Assert Exception
test: assertion failed: Must transfer an amount greater than 0
```




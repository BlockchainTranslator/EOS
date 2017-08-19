>原文链接：<https://eosio.github.io/eos/group__contractdev.html>
>
>翻译：区块链中文字幕组 - [张奎](https://github.com/byzhangkui) [胡亮](https://github.com/gumoon)
>
>审核：区块链中文字幕组 - [梓岑](https://yoyow.org/)

# How To Write Contracts EOS 如何为 EOS.IO 编写智能合约

Introduction to writing contracts for EOS.IO.  

EOS.IO 合约编写简介。

## Modules  模块

[Database API](#)

APIs that store and retreive data on the blockchain

在区块链上存储和检索数据的接口。

[Math API](#)

Defines common math functions.

定义常用数学函数。  

[Message API](#)

Define API for querying message properties.

定义消息属性查询接口。

[Console API](#)

Enables applications to log/print text messages.

支持应用程序记录/打印文本消息。

[Token API](#)

Defines the ABI for interfacing with standard-compatible token messages and database tables.

定义ABI（应用系统二进制接口），实现与标准兼容的 token 消息及数据库表之间的交互

[Builtin Types](#)

Specifies typedefs and aliases.

指定类型定义和别名。    

## Detailed Description 详细说明
### Background 背景
EOS.IO contracts (aka applications) are deployed to a blockchain as pre-compiled Web Assembly (aka WASM). WASM is compiled from C/C++ using LLVM and clang, which means that you will require knowledge of C/C++ in order to develop your blockchain applications. While it is possible to develop in C, we strongly recommend that all developers use the EOS.IO C++ API which provides much stronger type safety and is generally easier to read.

EOS.IO 合约（应用程序）以预编译的 Web Assembly（WASM）形式部署在区块链上。WASM 使用 C/C++ 编写，通过 LLVM 和 clang 编译，这意味着，开发 EOS.IO 智能合约首先需要具备 C/C++ 基础。不过，虽然可以用 C 语言来开发，但我们强烈推荐使用C++ 接口。C++ 接口是强类型安全性的 ，并且也更容易阅读。

### Application Structure 应用程序结构

EOS.IO applications are designed around event (aka message) handlers that respond to user actions. For example, a user might transfer tokens to another user. This event can be processed and potentially rejected by the sender, the receiver, and the currency application itself.

EOS.IO 应用程序是围绕响应用户行为的事件（消息）处理来设计的。如用户间的代币转账交易会触发一个事件。这个事件可以被发送方，接收方或者当前应用程序本身进行处理或者拒绝。

As an application developer you get to decide what actions users can take and which handlers may or must be called in response to those events.  

开发者需要决定用户可以触发哪些行为，以及哪些处理函数应该或者必须被调用，用以作为对这些事件的响应。

#### Entry Points 入口点
EOS.IO applications have a apply which is like main in traditional applications:  

EOS.IO 应用程序提供 apply 方法作为入口点，类似传统应用程序的 main 方法：

```C
extern "C" {
   void init();
   void apply( uint64_t code, uint64_t action );
}
```

main is give the arguments code and action which uniquely identify every event in the system. For example, code could be a currency contract and action could be transfer. This event (code,action) may be passed to several contracts including the sender and receiver. It is up to your application to figure out what to do in response to such an event.  

apply 方法包含 code 和 action 两个参数，在系统内通过这两个参数可唯一标识每个事件。例如，code 可以是一个现金合约，而 action 就是转移的行为。这个事件（code，action）可以被传递到包括发送者和接收者的多个合约中。如何响应一个事件, 由应用程序确定。 

init is another entry point that is called once immediately after loading the code. It is where you should perform one-time initialization of state.

init 是另外一个程序入口点，在加载代码后会被立即调用，且只被调用一次的。在这里你可以实现一次性的状态初始化。

#### Example Apply Entry Handler 入口处理函数的示例

Generally speaking, you should use your entry handler to dispatch events to functions that implement the majority of your logic and optionally reject events that your contract is unable or unwilling to accept.  

一般来说，你应该使用入口处理函数去分发事件到对应的方法。这些方法实现主要的处理逻辑，或者选择性地拒绝合约不识别或者不应该接受的事件。

```C
extern "C" {
   void apply( uint64_t code, uint64_t action ) {
      if( code == N(currency) ) {
         if( action == N(transfer) )
            currency::apply_currency_transfer( currentMessage< currency::Transfer >() );
      } else {
         assert( false, "rejecting unexpected event" );
      }
   }
}
```

>**Note  说明**
>
>When defining your entry points it is required that they are placed in an extern "C" code block so that c++ name mangling[^footnote] does not get applied to the function.

>当你定义入口点时，需要将代码放在 extern "C" 代码块中，使得 C++ 名字修饰[^footnote]不会应用到该方法上。

[^footnote]: *name mangling* 名字修饰，又译做名字粉碎、名字重整，是编译器在函数、结构体、类或其它的数据类型的名字中编码附加信息一种方法，以消除二义性。应用场景如区分重载函数，标识调用约定等。

https://eosio.github.io/eos/group__contractdev.html
# How To Write Contracts
# 如何编写合约
Introduction to writing contracts for EOS.IO.  
介绍如何为 EOS.IO 编写合约。

## Detailed Description
## 详细说明  
### Background
### 背景
(1.1)EOS.IO contracts (aka applications) are deployed to a blockchain as pre-compiled Web Assembly (aka WASM). (1.2)WASM is compiled from C/C++ using LLVM and clang, which means that you will require knowledge of C/C++ in order to develop your blockchain applications.(1.3) While it is possible to develop in C, we strongly recommend that all developers use the EOS.IO C++ API which provides much stronger type safety and is generally easier to read.  
(1.1)EOS.IO 合约（应用程序）以预编译的 Web Assembly（WASM）的形式部署在区块链上。(1.2)WASM 使用 C/C++ 编写，通过 LLVM 和 clang 编译，这意味着你需要 C/C++ 的知识才能开发你的区块链应用。(1.3)虽然可以用 C 语言来开发，但是我们强烈推荐所有开发者使用 EOS.IO 的 C++ API，它是强类型安全的，而且通常更容易阅读。

| 第一段审核结果        | 张奎           | 胡亮  |
| ------------- |:-------------| :-----|
| (1.1)      |  |  |
| (1.2)      |       |    |
| (1.3) |       |    |

讨论区：
(1.1)  
(1.2)  
(1.3)  

### Application Structure
### 应用程序结构
(2.1)EOS.IO applications are designed around event (aka message) handlers that respond to user actions.(2.2) For example, a user might transfer tokens to another user. (2.3)This event can be processed and potentially rejected by the sender, the receiver, and the currency application itself.  
(2.1)EOS.IO 应用程序是围绕响应用户行为的事件（消息）处理来设计的。(2.2)例如，一个用户转移 tokens 给另外一个用户。(2.3)这个事件可以被发送方，接收方或者当前应用程序本身进行处理或者拒绝。  
(3.1)As an application developer you get to decide what actions users can take and which handlers may or must be called in response to those events.  
(3.1)作为应用程序的开发者，你需要决定用户可以触发什么行为，以及哪些事件处理函数应该或者必须被调用以响应这些事件。
### Entry Points
### 入口点

(4.1)EOS.IO applications have a apply which is like main in traditional applications:  
(4.1)EOS.IO 应用程序提供类似传统应用程序的 main 方法相同作用的 apply 方法作为入口点：

```C
extern "C" {
   void init();
   void apply( uint64_t code, uint64_t action );
}
```

(5.1)main is give the arguments code and action which uniquely identify every event in the system. (5.2)For example, code could be a currency contract and action could be transfer. (5.3)This event (code,action) may be passed to several contracts including the sender and receiver. (5.4)It is up to your application to figure out what to do in response to such an event.  
(5.1)main 方法包含 code 和 action 两个参数，在系统内通过这两个参数可唯一标识每个事件。(5.2)例如，code 可以是一个现金合约，而 action 就是转移的行为。(5.3)这个事件（code，action）可以被传递到包括发送者和接收者的多个合约中。(5.4)你的应用程序就需要明确如何响应这个事件。
(6.1)init is another entry point that is called once immediately after loading the code. (6.2)It is where you should perform one-time initialization of state.
(6.1)init 是加载代码后会被立即调用，且只被调用一次的另外一个入口点。(6.2)在这里你可以实现一次性的状态初始化。

### Example Apply Entry Handler
### apply 入口处理函数的示例
(7.1)Generally speaking, you should use your entry handler to dispatch events to functions that implement the majority of your logic and optionally reject events that your contract is unable or unwilling to accept.  
(7.1)一般来说，你应该使用入口处理函数去分发事件到对应的方法，这些方法实现主要的逻辑，以及拒绝合约不识别或者不应该接受的事件。

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
#### Note
#### 说明
(8.1)When defining your entry points it is required that they are placed in an extern "C" code block so that c++ name mangling does not get applied to the function.  
(8.1)当你定义入口点时，需要将代码放在 extern "C" 代码块中使得 C++ 名字改编不会应用到该方法上。

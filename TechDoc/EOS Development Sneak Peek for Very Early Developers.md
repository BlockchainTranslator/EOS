> [EOS Development Sneak Peek for Very Early Developers](https://steemit.com/eosdev/@dan/eos-development-sneak-peek-for-very-early-developers)

# EOS Development Sneak Peek for Very Early Developers -- EOS开发早鸟指南

Although the official test network is still in preparation, anyone can create their own test environment on a local node. Please understand things are likely to change; however, not drastically so.

虽然官方测试网络仍在准备中，但任何人都可以在本地节点上创建自己的测试环境。请了解这些内容很可能会发生改动，但不会很大。

We have started to put together documentation for developers. This documentation often lags behind development and is currently far below the standard of what we plan to deliver along with the official test network.

[https://eosio.github.io/eos/](https://eosio.github.io/eos/)

我们已经开始为开发人员做了汇总的文档。但该文档经常会落后于开发进度，目前水准也远低于计划和官方测试网络一并提供的文档的水准。

[https://eosio.github.io/eos/](https://eosio.github.io/eos/)

## Starting a Local Node -- 启动一个本地节点

Anyone can start a local node by following the build instructions here:

[How to Build EOS.IO (eosd)](https://eosio.github.io/eos/group__howtobuild.html)  

任何人都可以通过以下的生成指令来启动一个本地节点：

[如何生成 EOS.IO (eosd) ](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/How%20To%20Build%20EOS.md)

## Interfacing with Local Node via RPC -- 通过 RPC 与本地节点交互

The `eosd` executable can be configured to expose a REST/JSON interface over HTTP. The existing APIs are quite limited but will be dramatically expanded over time. For information on how to interface with this RPC interface directly please see this documentation:

[eosd RPC Interface](https://eosio.github.io/eos/group__eosiorpc.html)

可以将可执行文件 `eosd` 配置为通过 HTTP 来暴露 REST/JSON 接口。现有的 API 还非常有限，但随着时间的推移会急剧扩展。有关如何直接与此 RPC 接口进行交互的信息，请参阅以下文档：

[eosd RPC 接口](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/eosd%20RPC%20Interface.md)  

## Interfacing with Local Node via CLI (eosc) -- 通过 CLI（eosc） 与本地节点交互

`eosc` is a tool that wraps the RPC interface and makes it easy for users to query `eosd`. This tool will eventually become the primary way to interact with `eosd` for developers wishing to publish contracts to the blockchain.

`eosc` 是包装了 RPC 接口的一个工具，以方便用户来查询 `eosd` 。对于希望将合约发布到区块链的开发人员，这个工具将成为与 `eosd` 进行交互的主要方式。

For a quick tutorial on how to create accounts, transfer funds, upload contracts, and interface with those contracts via `eosc` and `eosd` please see this:

[eosc - command line client](https://eosio.github.io/eos/group__eosc.html)

关于如何创建帐户，转移资产，上传合约以及通过 `eosc` 和 `eosd` 与这些合约进行交互的快速教程，请参阅：

[eosc - 命令行客户端](https://github.com/BlockchainTranslator/EOS/blob/master/TechDoc/EOS%20Command%20Line%20Client.md)  

## Current Development Status -- 开发现状

As things currently stand the blockchain is doing no signature validation. This means any account can trigger any action. This makes things very easy to test the logic of your applications. It also means that it is not currently necessary to maintain a wallet with private keys to use the network to test your applications.

按现状来看，区块链是在没有签名验证的情况下运行的。这意味着任何帐户都可以触发任何操作。这可以很容易地测试应用程序的逻辑。这同时也意味着目前无需维护一个带有私钥的钱包来使用网络对应用程序进行测试。

Over the next few weeks we will be building a CLI wallet and enabling developers to turn on signature validation and permission checking.

在接下来的几个星期内，我们将构建一个 CLI 钱包，使开发人员能够启用签名验证和权限检查。

Also note that the current RPC API makes it very difficult to query the state of your contract. This will be remedied next week.

另请注意，当前的 RPC API 使您很难查询合约的状态。这将在下周得到改进。

## Getting Started with Development -- 开发入门

We have several [example contracts](https://github.com/EOSIO/eos/tree/master/contracts) that you can use as a starting point:

我们提供了几个 [合约示例](https://github.com/EOSIO/eos/tree/master/contracts) ，可以作为开发的起点：

For information about the available APIs please see:

[How to Write Contracts](https://eosio.github.io/eos/group__contractdev.html)

关于可用 API 的信息，请参阅：

[如何编写合约](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/How%20To%20Write%20Contracts.md)  

There is also a helpful index of [all documentation](https://eosio.github.io/eos/modules.html).

这还有一个链接了 [所有文档](https://eosio.github.io/eos/modules.html) 的索引，非常有用。

## Developer Channel -- 开发者频道

We have also created a new developer channel on Telegram ( tg://join?invite=EaEnSUPktgfoI-XPfMYtcQ ). This channel is heavily moderated to keep the topic focused on developers helping developers. If you have questions this is the best place to get real-time support from the community. Our developers will also monitor this chat and attempt to help as time permits.

我们还在 Telegram 上创建了一个新的开发者频道 Telegram ( tg://join?invite=EaEnSUPktgfoI-XPfMYtcQ ) 。这个频道做了比较严格的限制，以保持主题聚焦在开发人员的互助上。如果您有疑问，这是获得社区实时支持的最佳途径。我们的开发人员也会监控该频道上的讨论，并会在时间允许的情况下提供协助。

We would also like to establish the [#eosdev](https://steemit.com/trending/eosdev) tag here on steemit. If you have developer questions and/or answers please post under this tag. I will attempt to follow it and turn it into our own stack exchange. Quality questions, answers, and tutorials will receive up votes.

我们也在 steemit 上建立了 [#eosdev](https://steemit.com/trending/eosdev) 标签。如果您有开发者的问题和（或）答案，请在该标签下发布。我会试着跟进它，并将它变成我们自己的 stack exchange 。高质量的问题、答案及教程将会获得投票。

## This is just the beginning -- 这仅仅是个开始

This information is provided for information purposes only based upon community demand. We would appreciate any feedback you can give as it will help us refine how we develop EOS.IO to serve the needs of developers. All documentation and designs are still subject to change, but with your feedback they can change for the better!

这些信息是依据社区需求而提供的，以供参考。我们将非常感谢您的任何反馈意见，因为这将有助于我们改进 EOS.IO 的开发，以满足开发者们的需求。所有的文档和设计仍然会有变化，但随着您的反馈，它们可以变地更好！

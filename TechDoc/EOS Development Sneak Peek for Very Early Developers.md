# EOS开发早鸟指南
原文链接：[EOS Development Sneak Peek for Very Early Developers](https://steemit.com/eosdev/@dan/eos-development-sneak-peek-for-very-early-developers)

虽然官方测试网络仍在准备中，但任何人都可以在本地节点上创建自己的测试环境。请了解这些内容很可能会发生改动，但不会很大。

我们已经开始为开发人员做了汇总的文档。但该文档经常会落后于开发进度，目前水准也远低于计划和官方测试网络一并提供的文档的水准。

[https://eosio.github.io/eos/](https://eosio.github.io/eos/)

## 启动一个本地节点
任何人都可以通过以下的生成指令来启动一个本地节点：

[如何生成 EOS.IO (eosd) ](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/How%20To%20Build%20EOS.md)  
原文链接：[How to Build EOS.IO (eosd)](https://eosio.github.io/eos/group__howtobuild.html)

## 通过 RPC 与本地节点交互

可以将可执行文件 `eosd` 配置为通过 HTTP 来暴露 REST/JSON 接口。现有的 API 还非常有限，但随着时间的推移会急剧扩展。有关如何直接与此 RPC 接口进行交互的信息，请参阅以下文档：

[eosd RPC 接口](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/eosd%20RPC%20Interface.md)  
原文链接：[eosd RPC Interface](https://eosio.github.io/eos/group__eosiorpc.html)

## 通过 CLI（eosc） 与本地节点交互

`eosc` 是包装了 RPC 接口的一个工具，以方便用户来查询 `eosd` 。对于希望将合约发布到区块链的开发人员，这个工具将成为与 `eosd` 进行交互的主要方式。

关于如何创建帐户，转移资产，上传合约以及通过 `eosc` 和 `eosd` 与这些合约进行交互的快速教程，请参阅：

[eosc - 命令行客户端](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/EOS%20Command%20Line%20Client.md)  
原文链接：[eosc - command line client](https://eosio.github.io/eos/group__eosc.html)

## 开发现状
按现状来看，区块链是在没有签名验证的情况下运行的。这意味着任何帐户都可以触发任何操作。这可以很容易地测试应用程序的逻辑。这同时也意味着目前无需维护一个带有私钥的钱包来使用网络对应用程序进行测试。

在接下来的几个星期内，我们将构建一个 CLI 钱包，使开发人员能够启用签名验证和权限检查。

另请注意，当前的 RPC API 使您很难查询合约的状态。这将在下周得到改进。

## 开发入门
我们提供了几个 [合约示例](https://github.com/EOSIO/eos/tree/master/contracts) ，可以作为开发的起点：

关于可用 API 的信息，请参阅：

[如何撰写合同](https://github.com/BlockChainTranslator/EOS/blob/master/TechDoc/How%20To%20Write%20Contracts.md)  
原文链接：[How to Write Contracts](https://eosio.github.io/eos/group__contractdev.html)

这还有一个链接了 [所有文档](https://eosio.github.io/eos/modules.html) 的索引，非常有用。

## 开发者频道

我们还在 Telegram 上创建了一个新的开发者频道 [Telegram](tg://join?invite=EaEnSUPktgfoI-XPfMYtcQ) 。这个频道做了比较严格的限制，以保持主题聚焦在开发人员的互助上。如果您有疑问，这是获得社区实时支持的最佳途径。我们的开发人员也会监控该频道上的讨论，并会在时间允许的情况下提供协助。

我们也在 steemit 上建立了 [#eosdev](https://steemit.com/trending/eosdev) 标签。如果您有开发者的问题和（或）答案，请在该标签下发布。我会试着跟进它，并将它变成我们自己的 stack exchange 。高质量的问题、答案及教程将会获得投票。

## 这仅仅是个开始
这些信息是依据社区需求而提供的，以供参考。我们将非常感谢您的任何反馈意见，因为这将有助于我们改进 EOS.IO 的开发，以满足开发者们的需求。所有的文档和设计仍然会有变化，但随着您的反馈，它们可以变地更好！
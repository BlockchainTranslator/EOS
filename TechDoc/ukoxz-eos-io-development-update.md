> 本文翻译自：https://steemit.com/eos/@dan/ukoxz-eos-io-development-update?from=singlemessage&isappinstalled=0#eos
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator) [鱼](https://github.com/oscnet)
>
> 翻译时间：2018-2-4
>

 本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

## EOS.IO Development Update | EOS.IO 开发更新

![](https://steemitimages.com/DQmUnysCE7zTHRLYUpFfqJ9C4G84qVzY2iZCSu6ZVJ1rdzG/image.png)

Our team has been working around the clock to make our EOS.IO software the best it can be. Those following along on GitHub should see some substantial improvements in the structure of the code as we implement many of the things we discussed in the last update.

为了将 EOS.IO 软件做得最好，我们的团队一直在夜以继日地工作。在 GitHub 上 follow 我们项目的应该看到了我们代码结构的一些实质性的改进。因为我们实现了上次更新中讨论的许多事情。

EOSIO BIOS
----------

A computer's BIOS is built into the hardware and is the first thing a computer loads prior to starting the operating system. This week we continue with the operating system metaphor to make the EOSIO blockchain bootstrap process as simple as possible, like a computer BIOS. The blockchain now starts up with a very simple initial state:

1.  a single account (eosio.system)
2.  a single private key
3.  a single block producer

EOSIO BIOS
----------
计算机的 BIOS 内置于硬件中，启动操作系统之前计算机首先加载 BIOS。本周，通过借鉴操作系统的启动过程，我们继续使 EOSIO 区块链的启动过程尽可能简单，就像电脑的 BIOS 一样。区块链现在以一个非常简单的初始状态启动：

1. 一个帐户（eosio.system）
2. 一个私钥
3. 一个单一的块生产者

This initial account is like the root account on linux systems, it has unlimited power until it yields this power to a higher level operating system smart contract. From this initial state, the [@eosio.system](/@eosio.system) account will upload the operating system smart contract that implements the following:

1.  staking for voting, network bandwidth, cpu bandwidth, ram, and storage.
2.  producer and proxy vote creation

这个初始帐户就像 linux 系统上的 root 帐户一样，在授权给更高级别的操作系统智能合约之前，它拥有无限的权力。这个初始状态后，[@eosio.system](/@eosio.system) 帐户将上传运行操作系统智能合约，该合约执行以下操作：

1. 设置投票、网络带宽、CPU带宽、内存和存储标准。
2. 创建生产者和代理投票

You can view this initial state as an embryonic stem cell capable of adapting an EOSIO based blockchain to any number of use cases and governance structures all of which can be updated and tweaked without requiring any hard forks.

We gain many benefits from this approach because it makes the core EOSIO software simpler and easier to test.

您可以将此初始状态视为胚胎干细胞，能够将基于 EOSIO 的区块链调整为任意数量的用例和治理结构，所有这些都可以在不需要任何硬分叉的情况下进行更新和调整。

我们从这种方法中获得了许多好处，它使得 EOSIO 核心软件更简单、更容易测试。

Dynamic Number of Block Producers
---------------------------------

The primary outcome of this is that EOSIO blockchains now support a dynamic number of block producers which can be changed with a simple update to the [@eosio.system](/@eosio.system) smart contract. We will still default this to 21 producers, but this is no longer hard coded.

The primary reason for making it dynamic is because for many private blockchains, 21 producers is beyond overkill. Enterprise use of private blockchains may prefer to have just a couple of producers and test networks might want only a single producer.

动态调整块生产者数量
-------------
这样做的主要结果是 EOSIO 区块链现在支持动态数量的区块生产者，通过对
[@eosio.system](/@eosio.system)智能合约的简单更新就可以更改区块生产者数量。默认我们仍然使用 21 个块生产者，但这不再是硬编码。

可以动态调整块生产者数量的主要原因是因为对于许多私有区块链来说，21 个生产者有点太多了。使用私有区块链的企业可能更倾向于仅使用几个块生产者，并且测试网络可能只需要一个生产者。

Metering
--------

Historically we have indicated that each transaction would have at most 1ms of runtime as measured subjectively by the block producer. We realized there is a demand for some transactions which could take up to 50ms to run and also want to incentivize efficiency by encouraging developers to design transactions that take less than 50us to run. Under our original model all transactions utilized the same CPU whether 50us or 1ms meaning there is no incentive to optimize below 1ms.

Because runtime is subjective and can vary depending upon other activities running on the same computer, it is not possible to generate an objective and reproducible measure of runtime.

计量
----
从历史上看，我们已经指出由块生产者主观地测量出每个交易最多只能有 1ms 的运行时间。但我们意识到一些交易有可能需要 50ms 运行时，同时为提高效率也希望通过鼓励开发者设计运行时间小于 50us 的交易。在我们的原始模型中，不论是 50us 还是 1ms，所有交易都使用了相同的 CPU ，这意味着将没有动力对 1ms 以下的交易进行优化。

因为运行时间是主观的，并且可能根据在同一台计算机上同时运行的其他程序的活动而变化，计算出客观和可再现的运行时间是不可能的。

We realized that at no additional cost, we could modify our existing time-based rate limiter to a limiter that would calculate an objective estimate of the number of WASM instructions executed. This is similar to how Ethereum measures gas consumption. With this new objective measure we can rate limit CPU just like we rate limit bandwidth.

The block producers will use the same "dynamic oversubscription" algorithm for CPU usage that they use with network bandwidth. This means that while the network has spare CPU capacity users can get more CPU-per-staked token than they would be guaranteed to get during full congestion.

The block producers would still implement a subjective runtime limit in addition to the CPU instruction counting. This subjective limit would protect the network from those who would abuse the metering algorithm by using the most time-expensive operations more than the less time-expensive operations.

我们意识到，在不增加成本的情况下，我们可以将现有的基于时间的费率限制器替换为基于客观的所执行 WASM 指令数目的限制器。这与以太坊计算 gas 消耗量相似。有了这个新的客观测量仪，我们就可以像限制带宽一样对 CPU 进行限制。

块生产者对 CPU 的使用计算与网络带宽使用率采用相同的“动态超额认购”算法。这意味着，当网络有空闲 CPU 容量时，用户可以获得比在拥挤期间所保证能得到的更多的每单位代币权益的 CPU 算力。

除了 CPU 指令计数之外，块生产者仍将实行主观运行时间限制。这种主观限制可以保护网络免受那些使用最耗时的指令操作多于花费时间较少的指令操作的滥用计量算法的人员的影响。

Separation of CPU and Network Bandwidth
---------------------------------------

In previous updates we indicated that we would separate out RAM, Storage, and Bandwidth where CPU/Network were both considered part of bandwidth. We realized that some applications, like Steem, might have high network bandwidth (for posts) and low CPU bandwidth, whereas other applications might have low network bandwidth (exchange orders), but higher CPU bandwidth (order matching). This means that one-size-fits-all pricing and/or staking does not make sense.

To keep things simple, the user interface can still bundle these things together for normal users; however, power users now have more price flexibility.

分离 CPU 和网络带宽
--------------
在之前的更新中，我们表示要将RAM，存储和带宽分开， CPU/网络 也视为带宽的一部分。我们意识到，像 Steem 这样的一些应用程序可能具有较高的网络带宽（用于发布文章）和较低的 CPU 带宽，而其他应用程序可能具有较低的网络带宽（如交换订单），但较高的 CPU 带宽（如订单匹配）。这意味着一刀切的定价和/或股份是没有意义的。

为了简单起见，对于普通用户，用户界面仍然可以将这些东西捆绑在一起; 然而，对高级用户现在有更多的价格灵活性。

Transaction Compression
-----------------------

In the process of adding support for the c++ STL library we noticed that smart contracts could get quite large (50kb) and would therefore consume significant network bandwidth. It is conceivable that more complex contracts might grow to be over 200kb. We also realized that many applications, such as Steem, bundle very compressible content into transactions.

We added support for zlib compression of transactions which can provide a 60% or more reduction in bandwidth usage for smart contract uploads and potentially higher for Steem-like content.

事务压缩
-------
在为 c++ STL 库添加支持的过程中，我们注意到智能合约可能会变得相当大（50kb），因此会消耗大量的网络带宽。可以想象，更复杂的合约可能会超过200kb。我们也意识到许多应用程序（如Steem）将非常具有可压缩性的内容捆绑到事务中。

我们增加了对 zlib 压缩交易的支持，可以为上传智能合约节省 60％ 或更多的带宽，对于类似 Steem 的内容则可能有更高的压缩率。

Network Updates
---------------

The P2P network team has been busy updating the code to enhance performance and stability. This week they made significant progress on the following:

1.  block summary - when a block is broadcast only the transaction IDs are included rather than retransmitting all the transactions in the block. This will reduce bandwidth usage by almost 50%.

2.  large message support - broadcasting large messages (like 50kb smart contracts) needs a different network protocol than small messages (like 200 byte transfers).

网络更新
-------
P2P网络团队一直忙于更新代码以提高性能和稳定性。本周他们在以下方面取得了重大进展：

区块摘要 - 区块广播时只包含交易 ID 而不是重新传输块中的所有交易。这将使带宽使用减少近 50％。

大容量消息支持 - 在广播大容量消息（如 50kb 智能合约）与小容量消息（如 200 字节传输）时使用不同的网络协议。


Conclusion
==========

Our development team is working to make EOSIO the most efficient, general purpose, and flexible platform to date.

结论
====
我们的开发团队正在努力使 EOSIO 成为迄今为止最高效、最通用和最灵活的平台。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

鱼 区块链技术爱好者，欢迎加微信号交流：**oscnet**

本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

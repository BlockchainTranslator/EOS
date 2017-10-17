
# Why Decentralized Exchange Protocols Matter 为什么去中心化的交易协议是至关重要

> 本文翻译自：https://medium.com/@FEhrsam/why-decentralized-exchange-protocols-matter-58fb5e08b320

>译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [茶猫](https://github.com/BlockchainTranslator/EOS)

>翻译时间：2017-10-14
>

Decentralized exchange is early today but feels like it will be essential in a few years.

去中心化的交易在今天看来为时尚早，但我觉得在未来的几年里将会是至关重要的。

First, the difference between a decentralized exchange and a decentralized exchange protocol:

首先，去中心化的交易所和去中心化的交易协议是有所不同的：
![enter image description here](https://cdn-images-1.medium.com/max/800/1*DzPME3bv3EU71EKpDT6FDA.png)

EtherDelta, an early decentralized exchange（以德，早期的去中心化交易所）

A decentralized exchange has some combination of decentralized properties. At the moment this most likely means some mix of 1) on-blockchain trade clearing, 2) ability for users to retain control of their funds, and 3) hosting an orderbook in some decentralized manner (this is currently inefficient with current levels of blockchain scaling). They are mostly frontend apps for now. They may run on a decentralized exchange protocol (see below). In the future they may not be a frontend, but rather nodes in a p2p network which relay orders to others, and have only programmatic interfaces. Early examples of decentralized exchanges with frontends include EtherDeltaand OasisDEX. Neither currently use an underlying decentralized exchange protocol. They are small at the moment— EtherDelta does about 2% of the largest centralized exchange’s volume per day.

一个去中心化的交易所有一些去中心化的特性。目前这些特性表现在：1、链上的交易结算。2、用户能够保留对其资金的控制能力。3、用某种去中心化的方式来委托订单（以目前的区块链规模，效率还比较低下）。他们这些（去中心化交易所）目前订单平台多以app的形式。他们或许运行在去中心化的交易协议上（见下文）。在未来他们不仅是一个订单平台，而是成为用来广播订单给其他人的P2P网络中的节点，还具有编程接口。早期的去中心化交易所有EtherDelta和OasisDEX。这两者目前都没有使用底层的去中心化交易协议。他们目前的规模还很小——EtherDelta 每天的交易规模仅仅是最大的中心化交易所的2%。

A decentralized exchange protocol defines some combination of: a common trade order format, a way to reward those who spread orders, and a way to complete a trade when a match is found. Examples include Kyber, 0x, Swap, and OmiseGO.

一个去中心化的交易协议定义了如下的一组特性 ：一个通用的交易订单格式，对传播订单的人有奖励，找到一个匹配来完成交易。类似的例子有Kyber，0x，Swap和Omise GO

#### Benefits of decentralized exchanges

There are a few obvious benefits to decentralized exchanges. First, they allow you to remain in control of your funds. So no risk of the exchange being hacked or going insolvent. This can lead to higher liquidity, as users may be willing to leave orders open on the orderbook for longer when counterparty risk is gone.

### 去中心化交易的益处

去中心化交易所有一些明显的益处。首先，它能够让你完全保留对自己资产的掌控，就不会有交易所被攻击和无法偿还的风险。这可以产生更高的流动性，因为当相应的风险消失后，用户更愿意将自己的订单公开在订单表上更长的时间。

Second, they create global orderbooks. Decentralized exchanges are borderless and can serve anyone from any country.

第二，它将产生全球的订单表。去中心化的交易所是无国界的，可以服务来自任何一个国家的用户。

Third, they are low friction. No signup required, just trade.

第三，更少的阻力。无需注册，直接交易。


### Benefits of decentralized exchange protocols

Decentralized exchange protocols bring the benefits of decentralized exchanges and add a few more.

### 去中心化交易协议的益处

去中心化的交易协议除了具有去中心化交易所的益处外，还具有更多的益处：

First, extending the idea of global orderbooks, decentralized exchange protocols create even more global pools of liquidity. Orders share the same format and can be matched by anyone in any venue, from a p2p relay network to a decentralized exchange app to a text message. If you want to try a demo, check out the 0x order generator. It lets you create a link to a trustless trade you can send to anyone to complete.

首先，扩大全球订单表的概念，去中心化交易协议创造更多的全球流动性池。通过去中心化的APP发布信息在P2P网络里广播订单，因为该订单使用同一种格式可以让任何人在任何地点被匹配到。如果你像试一些去中心化交易协议的原型，可以点击 https://0xproject.com/portal。 可以用此来创建一个含有无需信任的交易需求的链接，发送此链接给任何人来完成交易匹配。

Second, decentralized exchange protocols significantly lower the friction of running a decentralized application (dapp). Most decentralized apps will require multiple tokens to work in concert to power them. For example, an app might use a combination of Ether to commit transactions to the blockchain, Filecoin to store and retrieve data, something like Golem to perform more heavy computation, and a token native to the application itself. When launching an app, it’s unlikely a user will have all of these tokens in the right ratios at the right time to seamlessly run it. So a just-in-time mechanism for acquiring tokens is needed. So if you’re designing a dapp or wallet like Metamask, this means you’d be likely to integrate a decentralized exchange protocol, where no third party API or account setup is required.

第二，去中心化的交易协议可以显著降低运行去中心化应用（dapp）的阻力。大多数的去中心化应用需要多种代币协同运行来支持。例如，一个app可能需要使用不同的以太坊代币来提交交易记录给区块链，Filecoin用来存储和检索数据，有些像Golem用来运行更多的计算，而且一个代币内置属于一个应用。当你安装了一个app，用户不大可能将这些所有代币按正确的比例和正确的时间无缝地运行在这个app上。所以需要一个即时获取代币的机制。如果你设计一个例如Metamask的dapp或者钱包，这就意味着你需要内置一个去中心化的交易协议，而无需第三方的API或者账户设置。

Further, there’s a category of behaviors which decentralized exchange protocols uniquely enable. This is where things really get interesting.

此外，还有一些去中心化交易协议特有的特性。这才是真正有趣的地方。

Consider the case of a smart contract which needs to acquire different tokens to operate. Smart contracts can’t make web-based API calls, so they can’t directly access web-based centralized exchanges. But they can call other smart contracts, so they can directly access decentralized exchanges. As smart contracts become more autonomous and complex, this feels like a must have. As a result, blockchain native dapps and scripts will prefer and often need to use decentralized exchanges. While there aren’t many dapps now so volume is low, there will be lots of “real” (vs. speculative) volume when dapps become plentiful.

考虑到一个智能合约需要不同的代币来运行的情况。智能合约不能调用基于web的API，所以他们无法直接访问基于web端的中心化交易所。但他们可以访问调用其他智能合约，所以他们可以直接访问去中心化的交易所。当智能合约变得越来越自治且复杂，这将会是必然的趋势。结果是，区块链原生dapp和脚本将经常运行和使用去中心化的交易协议。现在还没有那么多的dapp所以（去中心化交易协议）容量还比较低，当dapp越来越多的时候，将会有很多「真实」（相比于投机）的容量。
![enter image description here](https://cdn-images-1.medium.com/max/1000/1*UBN7UOT8yG2yFcRHkaq33w.png)


dApps accessing a global liquidity pool thanks to a shared decentralized exchange protocol, from 0x whitepaper
通过共享的去中心化交易协议，dapp获得全球范围的流动性池——来自0x白皮书

Decentralized exchange protocols are also open standards that are easy for anyone to build on and customize. For example, dYdX, a protocol for decentralized derivatives, is being built on 0x. People can create any sort of custom product they want using these protocols which is then freely available for anyone else to trade, use, or modify.

去中心化交易协议是开放标准的，易于任何人建立和订制协议。比如，dYdX，一个去中心化的金融衍生协议，就是创建在0x上。人们可以使用这些协议创建任何类型的定制化产品，然后免费给其他用户去交易、使用或者修改。

Finally, decentralized exchange protocols can automatically support new tokens immediately. For applications creating and supporting thousands of tokens this will be a requirement. Imagine millions of single day prediction markets with tokens representing each outcome. The same requirement applies when we get thousands of tokenized information feeds around different topics. If you believe we are headed to a world of thousands of tokens, supporting them all natively is critical. And if you are dealing with thousands of tokens, you are likely to want to do it through code rather than manually, which is where the programmatic interface of decentralized exchange protocols is also important.

最后，去中心化的交易协议可以自动立刻支持新发行的代币。对那些创建和支持数千种代币的应用来说，这点是十分需要的。想象单日展示有数以百万计代币（价格）结果的预测市场。当我们获得关于不同主题的数千个代币化信息源时，也有同样的需求。如果你相信我们正走向一个有着数千万代币的世界，支持其代币是至关重要的。而且如果你正在处理着数千个代币，那么你更可能希望通过代码而不是手工去处理，这就是为什么去中心化交易协议的编程接口是如此重要。

### Drawbacks

There are some drawbacks. Decentralized exchange requires users to manage security of their own funds and tools for that are immature. They currently have low throughput and face the same scalability challenges as their underlying blockchains, so those wanting low latency and high throughput will prefer centralized exchanges for quite a while. They currently offer little to no support for fiat currencies. They are probably challenging to deal with for regulated entities like traditional financial institutions. Finally, the lack of a block reward-like incentive supercharger in decentralized exchange protocols may make their network effects harder to get off the ground than in some other tokens. But most of these drawbacks can be overcome with time.

### 缺点

也有一些缺点。去中心化的交易需要用户自己管理资产的安全，而目前此类工具的安全性还不够成熟。（中心化交易）目前有着低并发和面对着如底层区块链一样的可扩展性的挑战，所以有些人在相当长的时间里，希望使用低延迟和高并发的中心化交易所。（去中心化交易）目前也不支持法币。这可能对类似传统金融机构的组织来说是一个挑战。最后，在去中心化交易协议里，对大的承兑商缺乏区块奖励激励可能会让其网络效率相比于其他代币更难提高。但是大多数的缺点都会随着时间推移被克服。

Zooming out a bit, the future of decentralized exchange is mind boggling. The number and scope of assets that become tokenized will exceed what we see in current financial markets by orders of magnitude. Thanks to decentralized exchange protocols, those tokens will be tradable on unified global markets. And tokens, unlike most assets, allow programmatic interaction with their corresponding systems, so the ability for interplay between the asset, its native system, and other assets is higher than ever. Buckle up.

说远一些，去中心化交易的未来令人难以执行。未来代币化的资产规模上会超过目前的金融市场。由于去中心化交易协议的存在，这些代币可以在不统一的国际市场上可交易。而代币不同于其他资产，允许相应的系统调用编程接口，因此他们有能力在不同的资产之间调配操作，它的内在的系统和其他资产比以往任何时候都要优异。系好安全带（我们坐在区块链的快速列车上）

作者：Fred Ehrsam 

#### 区块链中文字幕组
致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。
如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号：w1791520555
本文由币乎社区（bihu.com）内容支持计划赞助。

#### 本文译者简介
茶猫 产品经理，区块链技术爱好者，致力于区块链产品分析，欢迎添加微信公众号：bitzhidao

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

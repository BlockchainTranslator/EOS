# EOS is nailing it (almost 100%) | EOS 正迈向成功 (几乎100%)

> 本文翻译自：https://medium.com/@yobanjo/eos-is-nailing-it-almost-100-aafa3f6410f5
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [oscnet](https://github.com/oscnet)
>
> 翻译时间：2017-11-5

Dan Larimer surprised a lot of people with a brand new cryptoproject. The BitShares and Steemit founder presented EOS; a blockchain-system to “decentralize everything”. That’s something we’ve heard before isn’t it?

作为 BitShares 和 Steemit 项目的创始人 Dan Larimer 提出的 EOS 这个全新的区块链项目让很多人感到兴奋和惊讶。一个 "去中心化一切" 的区块链系统。我们以前听说过类似的说法吗？

## The claims | 声明

As I remember reading about Bitshares and DACs in the early beginnings of crypto I decided to give EOS (and Dan) a fair chance. I read their whitepaper and watched a presentation to see what the fuzz was all about. And boy, did we got some claims! EOS claims to support millions of transactions per second so it can become the operating system for the blockchain world. There’s no need for users to pay anything (!) and even social networks like Facebook could run on EOS. Dan even got as far as saying that each Facebook-like could be a blockchain interaction on EOS.

我记得早期我就读到过有关 Bitshares 和 DAC 的文章，所以我决定给EOS（和 Dan）一个公平的机会。我阅读他们的白皮书，观看了演示文稿，想了解 EOS 到底是什么东东。特别的，我们在其中看到了一些技术声明！EOS声称每秒能支持数百万次交易，因此它可以成为区块链世界的操作系统。使用时用户不需要支付任何费用！甚至像 Facebook 这样的社交网络也可以在 EOS 上运行。Dan 甚至还说，类似 Facebook 的程序都可以成为跟 EOS 交互的区块链应用。

## The idea |想法

Are you still here? I’m actually surprised I am. I criticized Ethereum and all their similar claims (infinite sharding!) in quite a number of posts. But Dan Larimer is even beyond the Ethereum claims with his lack of transaction costs and “likes” on a blockchain. Time to look at his magic ingredients on how to make a network like that even possible.

你还在阅读吗？我真的对这些感到很惊讶。我在很多帖子中批评过以太坊和所有类似（无限分片！）的声称。但 Dan Larimer 声称 EOS 远远超越了以太坊，它没有交易成本，一切“运行”在区块链上。现在让我们看看，他是如何神奇的将实现这样的网络成为可能。

Dan is the inventor of Delegated Proof Of Stake (DPOS) and this is quite different from miners fighting to solve a hash contest. In short you have several miners that mine certain blocks if they’re allowed to by stakeholders. So instead of getting trust from hashpower you gain trust by nodes in the network that own coins. But wait a second; in EOS things are even different than that. In EOS; App-devs can actually pick certain miners to make their blocks… How can that ever be secure?

Dan 是委托权益证明（DPOS）的发明者，这与矿工们为解决 hash (哈希)竞赛而奋斗是截然不同的。简而言之，DPOS 就是在利益相关者允许下，你可以用矿工来挖掘某些区块。通过拥有金钱（coin） 的网络节点而不是算力获得信任。但是等一下，在EOS中，情况甚至更为不同，EOS 应用程序开发人员实际上可以挑选某些矿工来创建自己的区块......(这种情况下)如何才能保证网络安全？

## The whole network | 整个网络

Let’s take a little step back here. The whole EOS-network is filled with blockchains where most of the Apps will have their own blockchain to interact with their users. The chains are also linked to each other so you can transfer EOS-tokens from one chain to the other. Let’s assume the whole network has 1000 miners. Now each miner is active in several blockchains but never on 2 chains at once. So a miner (called a Block producer in EOS) could make a block in a social network App, and several seconds later in a financial App. That way miners have their attention all over the place and a bunch of rules apply to make things more secure. But what if several evil miners join? And take people’s tokens?? Well, this is the smart part about EOS. Here’s a certain rule from their whitepaper:

> The EOS.IO software requires every transaction to include the hash of a recent block header. This hash serves two purposes:
- prevents a replay of a transaction on forks that do not include the referenced block; and
- signals the network that a particular user and their stake are on a specific fork.

让我们退后一步看，整个 EOS 网络充满了区块链，大多数应用程序将通过自己的区块链与用户进行交互。链与链之间也互相连接，因此您可以将 EOS 代币从一个链转移到另一个链。假设整个网络有1000名矿工。现在每个矿工都活跃在几个区块链中，但却不能同时出现在两个链上。所以一个矿工（EOS 中称为块生产商）可以在社交网络应用程序中创建一个区块，几秒钟后在又可在一个金融应用程序中创建一个区块。这样一来，矿工们就会把注意力全部放在这里，一系列规则可以使事情变得更加安全。但如果有几个邪恶的矿工加入呢？并且它们拿了其它人的代币？那么，这就是 EOS 聪明的地方。他们的白皮书中有一个特定的规则：

> EOS.IO软件要求每个事务都包含最近块头的散列值。这个散列值有两个目的：
- 防止在不包括引用块的分叉上重放交易; 和
- 向网络声明特定用户和他们的权益在特定分支上。

This is something really new in the blockchain world. Users “confirm” blocks by including a pointer to another recent valid block. That way miners can’t fool the system as they would be caught quite fast by the users in the network. And there’s more. App-devs could easily vote out evil miners as they have the right to choose them in the first place. Next to that good miners can kick out the bad ones as well. So there are actually 3 different ways to protect the blockchains in the network.

这个规则在区块链领域非常新颖。用户通过包含指向另一个最近有效块的指针来“确认”块。这样，矿工就不能欺骗这个系统，因为这样的话会很快被网络中的其它用户发现。而且，应用程序开发者因为有权在第一时间选出邪恶的矿工，所以可以很容易地通过投票筛除出来。甚而，好矿工也可以剔除那些不好的矿工。所以实际上有三种不同的方法来保护网络中的区块链安全。

## Decentralized | 去中心化

But how can Delegated Proof Of Stake be decentralized? Well let’s assume we have 1000 miners on the EOS-network. How does that compare to hashpower in a Proof Of Work-system?? It all depends on the algorithms that come with DPOS but if we assume equal distribution of blocks to the delegates the calculation is as follows:

100% capacity / 1000 miners = 0.1% “hashpower” per miner

但是如何证明授权权益证明(DPOS)是去中心化的？那么让我们假设 EOS 网络上有1000名矿工。这与工作量证明(POW)系统中的哈希算力相比如何？这一切都取决于 DPOS 算法，但如果我们假设区块平均分发给矿工，计算如下：

100％ 算力 / 1000名矿工 = 0.1％的算力/每个矿工

Dan was making this point (not this calculation) in a reply to Vitalik Buterin as well. Vitalik still has the view that Ethereum is decentralized although all hashpower is controled by just several mining-pools:

Dan 在 Vitalik Buterin 的回复中也提到了这一点（不是这个算式）。Vitalik 仍然认为以太坊是去中心化的，尽管所有的算力都是由几个矿池来控制的：
![Completely centralized mining on Ethereum](https://cdn-images-1.medium.com/max/1600/1*nxPvyqkknt3UBLbToSCQ7Q.png)<center>以太坊完全中心化的挖矿组织</center>


What would you prefer? A network where 48,4% of the hashpower is controlled by one group or a DPOS-system where the biggest miner has only 0.1% of all capacity in the network?

你喜欢哪个？网络上48.4％的哈希算力由一个组织来控制
，还是一个 DPOS 系统控制的，其中最大的矿工只占网络中所有算力的0.1％？

## Millions of transactions? | 数百万的交易量

This is always a tricky part isn’t it? Things work in theory but what about a live network? Well, Dan comes up with quite an idea here. They want to use Web Assembly to run contracts on “close to native” speeds inside their virtual machines. This means that miners can use about 80% of their CPU-speeds which is way more than the slow Ethereum Virtual Machine for example. And that without the need to calculate billions of hashes before a block is found. This might indeed bring extraordinary speeds to run contract on EOS where a 1000-fold improvement to current systems is likely. Add the idea of dedicated blockchains for each App and things might work out quite well.

这是不是总是一个棘手的部分？理论上有效，但是在实际网络中表现如何呢？Dan 在这里提出了一个很有意思的想法。他们希望使用Web Assembly在虚拟机内以“接近本机”的速度运行合约。这意味着矿工可以使用大约80％的CPU速度，这比缓慢的以太坊虚拟机快得多。而且，在找到块之前，不需要计算数十亿个哈希值。这确实可以带来非凡的速度运行 EOS 上的合约，对现有系统可能会有1000倍的提升。为每个应用程序添加专门的区块链的想法，可能会让事情做得更好。

If EOS brings us crowdfunds where 5000 users can join an ICO wihtin seconds then that’s a big improvement. And if these same users can buy/sell their coins later on, on a decentralized exchange on EOS then that’s even better. A system like Etherdelta is works quite nicely but putting out an order sometimes takes minutes, minutes where the price of a token might already have changed dramatically. No wonder Bitfinex is already partnering with EOS as they might bring the first secure exchange where orders are finalized in seconds instead of minutes. It would save the crypto community quite some wallet and exchange headaches.

如果使用 EOS 网络进行众筹，5000个用户可以在几秒钟内加入 ICO，那么这是一个巨大的进步。
日后如果这些用户可以在 EOS 的去中心化交易所上买入/卖出他们的代币，那就更完美了。
像 Etherdelta 以德这样的去中心化交易系统工作得非常好，但是它下个订单需要几分钟的时间，在这期间代币的价格可能已经发生了巨大的变化。Bitfinex 已经与 EOS 合作，通过这样的合作，可能实现第一个安全的去中心化的交易所，并且能在几秒钟内完成订单，而不是原来的几分钟。这样加密社区将节省相当多的费用和减轻交易的难度。

## Critical notes… | 重要说明

No, I’m not a fanboy yet! (ok, maybe just a bit). I got myself some EOS-tokens even while I dislike the idea of a year long ICO. MaidSafe for example, is a humble Scottish company with around 20 people (lot of engineers) working for them. That’s while their ICO in 2014 “only” brought them 8 million dollars. They did sell a bit of their company last year on BankToTheFuture but overall I think they’re still running under a total cashburn of 10 million so far. And that’s since 2014. I guess EOS can build the whole thing with 30 tot 50 million dollar. No need for a long, high valued ICO.

现在，我还不是一个 EOS 的粉丝！（好吧，也许我得承认只是有一点点的粉）。虽然我不喜欢 EOS 长达一年的 ICO，我还是持有一些 EOS。例如，MaidSafe 是一个谦虚的苏格兰公司，大约有20人（很多工程师）为他们工作。2014年他们的 ICO 只融了800万美元。去年他们在 BankToTheFuture 上卖掉了一些，但总的来说，我认为他们到目前为止还是有一千万的现金。这是自2014年以来，我认为 EOS 可以达到3000万到5000万美元市值。但却不需要一个长期、高估值的ICO。

## Conclusion |结论

Dan Larimer has already showed his skills with several cryptoprojects. He invented the completely undervalued Delegated Proof Of Stake and was the first to come up with the idea of a Decentralized Autonomous Company (DAC) which was later copied by others into the DAO. It seems he is on to some amazing scalable project right now which might free us from all the ‘waiting for confirmation’ terror. The world is ready for a fast new blockchain system and it’s a big win if decentralized exchanges become the norm.

Dan Larimer 在几个区块链项目中已经显示了他的能力。他发明了完全被低估的授权权益证明（DPOS），并且首先提出了去中心化自治公司（DAC）的想法，后来被其他人复制到 DAO 项目中。现在看来他正在进行一个惊人的可扩展项目，这可能使我们摆脱所有“等待交易确认”的恐慌。世界正在为快速的新型区块链系统做好准备，如果去中化交易成为常态，这无疑将是一个巨大的胜利。


In a next post I will write some more about EOS and I’ll explain their idea of “zero transactions costs” which is quite a nice one as well.

在下一篇文章中，我将会详细介绍一下EOS，我将解释他们的“零交易成本”的想法，这也是个相当不错的想法。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

鱼 区块链技术爱好者， 欢迎加微信号 oscnet 交流。

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

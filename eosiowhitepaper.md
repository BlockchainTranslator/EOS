

#### Background背景

Blockchain technology was introduced in 2008 with the launch of the Bitcoin currency, and since then entrepreneurs and developers have attempted to generalize the technology to support a wider range of applications on a single blockchain platform.

区块链技术在2008年伴随着比特币的问世而被人所知，自那以后，企业家和开发人员都试图让这一项技术普及化，来支持在单一区块链平台上的更大范围的应用。

While a number of blockchain platforms have struggled to support functional decentralized applications, application specific blockchains such as the BitShares decentralized exchange (2014) and Steem social media platform (2016) have become heavily used blockchains with tens of thousands of daily active users. They have achieved this by increasing performance to thousands of transactions per second, reducing latency to 1.5 seconds, eliminating per-transaction fees, and providing a user experience similar to those currently provided by existing centralized services.

虽然一些区块链平台在努力设法支持可用的去中心化应用，但一些特定的区块链应用，如比特股去中心化交易所（2014）和Steem社交媒体平台（2016）已经大量地使用了区块链技术，并且每天活跃用户数达到上万。它们做到这一点在于：提高性能至每秒上千条交易，降低确认延迟时间至1.5秒，取消预交易费，提供类似于现有的中心化服务那样的用户体验。

Existing blockchain platforms are burdened by large fees and limited computational capacity that prevent widespread blockchain adoption.

目前的区块链平台最大的瓶颈在于手续费太高和运算能力有限，这阻碍了区块链技术的广泛使用。

#### Requirements for Blockchain Applications区块链应用必须具备的条件

In order to gain widespread use, applications on the blockchain require a platform that is flexible enough to meet the following requirements:

为了获得更广泛的使用，区块链上的应用需要平台足够灵活，能够满足以下条件：

##### Support Millions of Users支持百万级用户数

Competing with businesses such as eBay, Uber, AirBnB, and Facebook, require blockchain technology capable of handling tens of millions of active daily users. In certain cases, an application may not work unless a critical mass of users is reached and therefore a platform that can handle very large numbers of users is paramount.

和eBay, Uber, AirBnB和Facebook这样的企业竞争，需要区块链技术能够处理上千万的日活跃用户数。在某些情况下，一个应用也许不能正常运行，如果用户数不够多的话，因此一个能够处理非常多用户数的平台就至关重要。

##### Free Usage免费使用

Application developers need the flexibility to offer users free services; users should not have to pay in order to use the platform or benefit from its services. A blockchain platform that is free to use for users will likely gain more widespread adoption. Developers and businesses can then create effective monetization strategies.

应用开发人员需要灵活地来为用户提供免费服务；用户不应该为使用这个平台或从平台的服务中获益而要付费。一个用户可以自由使用的区块链平台将可能获得更广泛的采用。然后，开发人员和企业能够创建有效的盈利策略。

##### Easy Upgrades and Bug Recovery易于升级和修复漏洞

Businesses building blockchain based applications need the flexibility to enhance their applications with new features. The platform must support software and smart contract upgrades.

在区块链上搭建应用的企业需要灵活地使用新的特性来增强他们的应用程序。这个平台必须支持软件和智能合约的升级。

All non-trivial software is subject to bugs, even with the most rigorous of formal verification. The platform must be robust enough to fix bugs when they inevitably occur.

所有重大的软件注定会有漏洞的，甚至在经过最严格的形式验证。这个平台必须足够健壮来修复不可避免的漏洞。

##### Low Latency低延迟性

A good user experience demands reliable feedback with a delay of no more than a few seconds. Longer delays frustrate users and make applications built on a blockchain less competitive with existing non-blockchain alternatives. The platform should support low latency of transactions.

好的用户体验需要可靠的反馈，这种反馈的延迟最多只能几秒钟。更长的延迟时间令用户烦躁，使得搭建在区块链上的应用缺乏与现有的非区块链应用的竞争力。这个平台必须支持交易的低延迟性。

##### Sequential Performance连续处理能力

There are some applications that just cannot be implemented with parallel algorithms due to sequentially dependent steps. Applications such as exchanges need enough sequential performance to handle high volumes. Therefore, the platform should support fast sequential performance.

有一些应用程序不能通过并行算法执行，由于对前后步骤的依赖。像交易所这样的应用程序需要足够强的连续处理能力来完成大规模的交易量。因此，这个平台必须支持快速的连续处理能力。

##### Parallel Performance并行能力

Large scale applications need to divide the workload across multiple CPUs and computers.

大规模的应用程序需要将负载分配到多个CPU和计算机上。

#### Consensus Algorithm (BFT-DPOS)共识算法(BFT-DPOS)

EOS.IO software utilizes the only known decentralized consensus algorithm proven capable of meeting the performance requirements of applications on the blockchain, Delegated Proof of Stake (DPOS). Under this algorithm, those who hold tokens on a blockchain adopting the EOS.IO software may select block producers through a continuous approval voting system. Anyone may choose to participate in block production and will be given an opportunity to produce blocks, provided they can persuade token holders to vote for them.

EOS.IO软件利用已知的去中心化共识算法 - 委任权益证明(DPOS)，这个算法被证实能够满足区块链上搭建应用的所需条件。在这个算法设计中，那些持有采用EOS.IO软件搭建的区块链应用的通证的人也许通过一个持续的投票系统来选择节点生产者。任何人都可以选择参与到区块生长中，并能够获得产生区块的机会，假如他们能够说服代币持有者为他们投票的话。

The EOS.IO software enables blocks to be produced exactly every 0.5 second and exactly one producer is authorized to produce a block at any given point in time. If the block is not produced at the scheduled time, then the block for that time slot is skipped. When one or more blocks are skipped, there is a 0.5 or more second gap in the blockchain.

EOS.IO软件能够做到每0.5秒出块的性能，并且一个生产者被授权在任何给定的时间点产生一个块。如果这个块没有按照既定的时间产生，那么对于这个时间段来说，这个块就被跳过。当一个或多个块被跳过时，区块链里就存在一个0.5秒以上的间隔。

Using the EOS.IO software, blocks are produced in rounds of 126 (6 blocks each, times 21 producers). At the start of each round 21 unique block producers are chosen by preference of votes cast by token holders. The selected producers are scheduled in an order agreed upon by 15 or more producers.

使用EOS.IO软件，区块按照每轮126个产生（每次6个，一次21个生产者）。每一轮开始的时候，21个区块生产者被代币持有者投票选出。被选中的生产者将按照一种被15个以上的生产者认同的顺序执行。

If a producer misses a block and has not produced any block within the last 24 hours they are removed from consideration until they notify the blockchain of their intention to start producing blocks again. This ensures the network operates smoothly by minimizing the number of blocks missed by not scheduling producers who are proven to be unreliable.

如果一个生产者丢失一个块，在过去的24小时内没有产生一个块，那么他们就被考虑从21个节点中被淘汰出去，直到他们再次让区块链知道他们开始产生块的意向。通过不安排那些被证实不可靠的生产者，把丢失的块数降到最少，来保证网络的平稳运行。

Under normal conditions a DPOS blockchain does not experience any forks because, rather than compete, the block producers cooperate to produce blocks. In the event there is a fork, consensus will automatically switch to the longest chain. This method works because the rate at which blocks are added to a blockchain fork is directly correlated to the percentage of block producers that share the same consensus. In other words, a blockchain fork with more producers on it will grow in length faster than one with fewer producers, because the fork with more producers will experience fewer missed blocks.

在一般条件下，采用DPOS的区块链并不会分叉，因为区块的生产者并不是竞争，而是通过合作的方式来产生块。如果有分叉，那么共识算法将自动地切换到最长的链。这种方法行得通的原因在于：区块被添加到一个分叉上的速度直接和采用相同共识算法的区块生产者的比例相关联。换句话说，一个分叉上有更多的区块生产者将比有更少的区块生产者的分叉在长度上增长地更快，因为有更多生产者的分叉会经历更少丢失的块。

Furthermore, no block producer should be producing blocks on two forks at the same time. A block producer caught doing this will likely be voted out. Cryptographic evidence of such double-production may also be used to automatically remove abusers.

此外，区块生产者不应该同时在两个分叉上产生块。被抓住这样做的区块生产者就被投票淘汰出去。双花这样的密码学证据也可能用来自动地把作恶者移除出去。

Byzantine Fault Tolerance is added to traditional DPOS by allowing all producers to sign all blocks so long as no producer signs two blocks with the same timestamp or the same block height. Once 15 producers have signed a block the block is deemed irreversible. Any byzantine producer would have to generate cryptographic evidence of their treason by signing two blocks with the same timestamp or blockheight. Under this model a irreversible consensus should be reachable within 1 second.

只要没有生产者用相同的时间戳或在相同的区块高度对两个块签名，通过允许所有的生产者对区块签名，拜占庭容错被添加到传统的DPOS算法中。一旦15个生产者对一个块签名，这个块就注定不可撤销。任一个拜占庭生产者将不得不通过用相同的时间戳或区块高度来对两个块签名，制造他们作恶的密码学证据。在这种模型下，一个不可逆转的共识应该在1秒内达成。

##### Transaction Confirmation交易确认

Typical DPOS blockchains have 100% block producer participation. A transaction can be considered confirmed with 99.9% certainty after an average of 0.25 seconds from time of broadcast.

典型的DPOS区块链拥有100%的区块生产者的参与。一个交易从广播后在平均0.25秒的时间内被确认的概率达到99.9%。

In addition to DPOS, EOS.IO adds asynchronous Byzantine Fault Tolerance (aBFT) for faster achievement of irreversibility. The aBFT algorithm provides 100% confirmation of irreversibility within 1 second.

除了DPOS，EOS.IO加入了异步拜占庭容错(aBFT)来更快地实现交易的不可逆转性。aBFT 算法实现1秒时间内100%的不可逆转的确认。

##### Transaction as Proof of Stake (TaPoS)作为权益证明的交易

The EOS.IO software requires every transaction to include part of the hash of a recent block header. This hash serves two purposes:

EOS.IO软件要求每个交易包含最近一个区块头的部分哈希值。这个哈希值有两个目的：

1.prevents a replay of a transaction on forks that do not include the referenced block; and

1.防止没有把被引用的块打包进来的分叉区块链上出现重复事务；

signals the network that a particular user and their stake are on a specific fork.

2.使得网络能知道用户和他们的权益是否在分叉出来的区块链上。

Over time all users end up directly confirming the blockchain which makes it difficult to forge counterfeit chains as the counterfeit would not be able to migrate transactions from the legitimate chain.

久而久之，所有用户最终直接确认区块链，这使得伪造假链变得困难，因为假链无法从合法链中迁移交易。

------

**区块链中文字幕组**
致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号：w1791520555。
[点击查看 GITHUB 及更多的译文](https://github.com/BlockchainTranslator/EOS)

**本文译者介绍**
Chuan，区块链技术爱好者。欢迎加我的微信：youyuxiaochuan
译文版权所有，转载需完整注明以上内容。


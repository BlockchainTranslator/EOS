# Dan Larimer, Creator Of The Fastest Blockchains, Now Targeting Sub-second Latency In EOS  最快的区块链创始人，Dan Larimer， 现在的目标是在EOS上实现半秒延迟

> 本文翻译自：https://www.cryptocoin.news/news/ethereum/dan-larimer-creator-of-the-fastest-blockchains-now-targeting-sub-second-latency-in-eos-2577/
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [AMY](https://github.com/lindasayer)
> 
> 翻译时间：2017-10-14

The rapid increase in demand for cryptocurrencies has led to a significant increase in transactions on public blockchains. It’s no surprise the value of these networks has grown in turn as suggested by applying Metcalfe’s law to transactions. However, attempted transactions have at times outgrown the capacity that the individual blockchains permit. In effect, each blockchain acts as a scarce resource for use due to the limits in the security focused designs, bandwidth, and hardware.

加密货币需求的急剧增长导致公链的交易量大幅增加。根据梅特卡夫定律，这些网络价值随着交易量增长而增加并不奇怪。然而，尝试的交易量有时会超出一些区块链的允许容量。实际上，由于集中安全的设计、带宽、硬件的限制，每个区块链作为稀缺的资源在使用。

Differences in performance are observed in the four currently most used blockchains: Bitcoin, Bitshares, Steem, and Ethereum. In the last year, both Bitcoin and Ethereum were observed to hit their limits in transaction throughput. Hitting the ceiling resulted in backlogs and delays or higher fees, but both were able to adapt slightly for more capacity. In contrast, Steem and Bitshares this year have been processing more than double the transactions of both Bitcoin and Ethereum with untouched limits thousands of times higher.

在目前使用最多的四个区块链中可以观察到性能的差异：比特币、比特股、Steem、以太坊。在过去一年中，比特币和以太坊的交易吞吐量明显受到了限制。撞上天花板的结果是积压延迟或者更高的手续费，但是两者都可以略微适应更多的交易量。相反的，Steem和比特股处理了相较比特币和以太坊两倍还多的交易量，也拥有数千倍的不变限制。

Dan Larimer created Bitshares (2014) and Steem (2016) with the original Delegated Proof of Stake (DPoS) and graphene technology. His involvement with blockchains dates back to the early days of Bitcoin where he would have forum discussions with the mystery inventor of Bitcoin, Satoshi. The DPoS design is often criticized for relying on only 20 to 100 validators, security nodes that decide the validity of transactions. Dan argues delegating control by far more users via voting to 21 even in power validators is more decentralized than delegating hashing power to far fewer dominant mining pools observed in Bitcoin or Ethereum. Dan claims DPoS to be “the most decentralized” by formalizing the decentralized peer review of 21 equivalent validators for security instead of a strict reliance on wealth for selection used in other designs, often too concentrated according to Pareto principle. Currently he is working with block.one on EOS, a new blockchain for decentralized applications (dApps), based on the next evolution of these technologies. The proposed list of features is not entirely new as many can be observed in action today on the blockchains of the previous two evolutions.

丹·拉里默在2014创造了比特股，于2016年创造了Steem，使用的是自己原创的DPOS共识算法和石墨烯技术。他参与区块链可以追溯到比特币的早期，他当时和神秘的比特币创始人中本聪在论坛里讨论。DPOS设计经常被批评为仅依赖于20到100个验证者，决定交易有效性的安全节点。丹认为，使用者通过投票委托21个有权利的验证者控制，这比比特币和以太坊中委托哈希算力给更少的主导矿池要更加去中心化。丹声称DPOS是最去中心化的，通过模拟去中心化同行评审，创造21个同权的验证者来保证安全，而不是像其他区块链仅仅依靠财富来选择，这些区块链根据帕累托原则也更加集中化。目前他与block.one合作开发EOS,一个运行去中心化应用的新区块链，基于这些技术的下一步革新。提出的功能列表并不是全新的，因为许多可以在以前的两个演变的区块链上被观察到。
 
Bitshares launched after the 2013 collapse of Mt. Gox to help replace existing cryptocurrency exchanges. To achieve this, the cryptocurrency was designed as the fastest in existence (claims 100,000 compared to 20 transactions per second possible on Ethereum), surpassing even VISA. The block time, that determines how fast users transaction can be included on the blockchain, were at unprecedented 3 seconds compared to 10 minutes on bitcoin. The platform included a decentralized exchange (DEX), prediction markets, tokens, easy to read account names, and the only trustless pegged tokens such as bitUSD with a stable value of a US dollar via smart-contract locked collateral and oracles. It was also the first self-sustaining blockchain with a decentralized autonomous organization (DAO) funding development from the treasury to this day. Notably, Bitspark, a global remittance business working with the UN, have recently switched to Bitshares.
 
 比特股在2013年门头沟倒闭之后发起，目的是帮助替代现存的加密货币交易所。为了达到这个目的，这个加密货币被设计成最快的（声称100000tps,以太坊的是20tps），甚至超越VISA，确定用户交易可以记入区块链的时间是前所未有的3秒，而在比特币上为10分钟。该平台包含一个去中心化的交易所（DEX）、预测市场、代币、易于读取的帐户名称，以及唯一无信任的瞄定代币，例如通过智能合约锁定的抵押品和债券的稳定的美元价值的bitUSD。这也是第一个拥有去中心化自治组织（DAO），资金自给自足的区块链。值得注意的是，与联合国合作的全球汇款平台Bitspark，最近已转向比特股。
 
All these advances Dan Larimer later included in Steem which also uniquely eliminated all transaction fees via the bandwidth model. Fees are a standard security measure to prevent spam but charged to users. The bandwidth model prevents spam without charging users by splitting total capacity between users who simply have the currency. The design allowed them to build on it a seamlessly fast fee-free steemit dApp, a social media platform. Lack of fees combined with the speed enabled microtransactions, free actions like voting, and a user experience aimed to let users forget they are using a blockchain. Dan’s focus then switched to smart contracts.
 
所有这些进展丹·拉里默后来都添加到了Steem中，这个区块链也通过带宽模式独特地消除了所有的交易费用。费用是防止垃圾信息的标准的保护模式，但这需要向用户收费。带宽模式可以防止垃圾信息，而不需要向用户收取费用，只需要在拥有代币的用户之间的分割总带宽容量。该设计使他们能够在其上建立一个无缝快速的免费去中心化应用：steemit，一个社交媒体平台。免费快速的小额交易、例如投票之类自发的行为，和旨在让用户忘记他们正在使用一个区块链的用户体验。之后丹的重点转向了智能合约。
 
According to Dan Larimer and the white papers, EOS will add even more to these demonstrated features. This platform attempts to generalize graphene with custom smart contracts, cross blockchain communication, and data storage solutions allowing the creation of any dApps including the likes of the DEX or steemit. The network also allows parallel execution via asynchronous communication – a breakthrough of the prior rate-limiting step.
 
根据丹·拉里默和白皮书，EOS将为这些演示的功能增添更多的功能。该平台尝试通过定制智能合约、跨链通信和数据存储解决方案来推广石墨烯，从而允许创建任何包含DEX或steemit的去中心化应用。该网络还允许通过异步通信并行执行—先前限速步骤的突破。
 
Dan Larimer announced this week in the official Telegram channel that EOS will be the first blockchain with unprecedented sub-second block times of 500 milliseconds and sub-second last irreversible block (LIB) providing finality. In other words, the time between a user sending a transaction or a command and being included in the blockchain could be consistently under a second compared to 10 minutes on Bitcoin. The drop from the already unique 3 second blocks in dPoS to 0.5 second blocks would be done through unique proximity-based signal routing around the globe. Combining asynchronous communication and the block time improvements, EOS is aimed to be the fastest lowest latency blockchain with customizable smart contracts executing millions of operations per second with no fees. The success of previous incremental results suggests the targets for block.one are realistic, with implications of possibly providing the first programmable blockchain ready for global adoption. When asked to compare with Ethereum, Dan responded “EOS can run [Ethereum] inside a single contract.” However, the team is temporarily using Ethereum for their coin distribution.
 
丹·拉里默本周在官方电报频道中宣布，EOS将是第一个拥有前所未有的半秒（500毫秒）级出块时间的区块链，并提供最后一个不可逆块（LIB）。换句话说，从用户发送交易或命令到该交易或命令添加到区块链中的时间将持续低于1秒，而比特币的需要10分钟。从DPOS中独特的3秒出块到0.5秒的出块，这将通过全球独一无二的基于邻近的信号路由进行。结合异步通信和出块时间的改进，EOS旨在成为最快的超低延迟区块链，可定制的智能合同每秒执行数百万次操作，无需付费。先前增量成果成功表明，block.one的目标是现实的，这可能提供了可供全球采用的第一个可编程区块链。当被要求与以太坊进行比较时，丹回应“EOS可以在一份合同中运行以太坊”。但是，该团队暂时使用以太坊进行代币分发。
 
The block.one team invented a new method for coin sale distribution to aid consensus security by discouraging coin power grabs, issue often ignored in distribution design of other prominent projects such as Ethereum, Cosmos, or OmiseGo. Coins are released daily in 350 rounds while trading on the markets. The low liquidity is expected to punish anyone trying to buy the majority of the coins with higher prices. The built-in DAO helps fund other developers in a decentralized manner. The testing and distribution phase is expected to end in June 2018 to allow creation of a public chain. Achieving his goals would once again demonstrate how Dan Larimer is disruptive to disruptive tech.
 
block.one团队发明了一种用于代币售卖的新方法，通过防止大户垄断购买代币以达成一致的安全性，这在其他知名项目如以太坊、Cosmos或OmiseGo的代币销售设计中经常被忽视。代币每天销售，共350轮，同时代币也在市场上交易。低流动性将惩罚任何试图以较高价格购买大部分代币的人。内置的DAO以分散的方式帮助其他开发人员。测试和分配阶段预计将于2018年6月结束，以创建一个公有链。实现他的目标将再次表明丹·拉里默如何颠覆那些颠覆性技术。
 
It’s important to note there’s always an additional risk with new design choices in trade-offs and less studied attack surfaces. All cryptocurrencies are still highly experimental, prone to failure, and the field is rapidly changing.
 重要的是要注意，选择这些新事物总是存在额外的风险，它们出现于交易场景，且对攻击面研究较少。所有加密货币仍然是高度实验性的，容易出现失败，形势也正在迅速变化。
 
-----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。
 
如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。
 
[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)
 
#### 本文译者简介
 
AMY REN 区块连爱好者，公众号“区块连学习笔记”建立者，欢迎加微信：Amyrenlin
 
本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。
 
 -----------------------------------------------------

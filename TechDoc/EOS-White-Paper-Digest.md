# EOS White Paper Digest 对EOS白皮书的摘要

> 本文翻译自：https://steemit.com/eos/@vitkolesnik/eos-white-paper-digest
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [林炜鑫](https://github.com/weixin1993)
> 
> 翻译时间：2017-10-21
https://steemitimages.com/DQmafheTXv6z8UKHzRKTRuABjTPbKRtmnq2BknQDeKDueKb/152258-eos.jpg

Probably you’ve already heard about EOS, a blockchain project of Steemit confounder Dan Larimer, and asked yourself how exactly it differs from other blockchains. Especially if you think about investing in EOS ICO or building apps on it. The best answers yet given can be found in [EOS Technical White Paper](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md), but if you aren’t prepared to read the whole of it (about 47 000 characters), then this post is for you.

很可能你已经听说过一个Steemi创始人Dan Larimer刚创立的项目——EOS，并对它与其他区块链项目的不同之处表示疑惑。尤其是你想投资EOS的ICO或者在链上创立应用的话。最好的答案你能够在EOS的白皮书里找到，不过如果你还没有准备好阅读白皮书全文（大概47000字数），那么这篇摘要很适合你阅读。


## Basic Characteristics 基本特征

EOS is a blockchain in production meant to be an operating system for decentralized apps. It will be capable of supporting millions of users and is built for apps as big as Facebook, Uber, AirBnB, or Ebay. It will be free for end users with no transactions fees, unlike Bitcoin and Ethereum. It will be lightning fast and able to compete by performance with non-blockchain apps. It will be easy to upgrade and the upgrades won’t result in blockchain forks, again unlike it’s the case with Bitcoin and Ethereum.

EOS是一个为了给分布式应用提供操作系统的区块链产品。它能够支持百万级用户并为类似Facebook, Uber, AirBnB, 或者 Ebay 这么大体量的应用程序提供操作系统。不同于比特币和以太坊，它将是免费提供给终端用户并且不收取交易费用。它将是闪电般的快速，并且能够通过与非区块链应用程序的性能竞争。与比特币和以太坊不同的是，它很容易升级并且它的升级不会导致区块链分叉。

## Consensus 一致性

EOS software uses [Delegated Proof of Stake](https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this-missing-white-paper) (DPOS) consensus algorithm as the only one capable to meet the the performance requirements. It means EOS token holders vote for block producers which don’t compete for blocks but rather cooperate.

EOS软件使用授权的股份(DPOS)共识算法作为唯一能够满足性能需求的算法。这意味着EOS令牌持有者将投票支持那些不参与区块链竞争而是彼此合作的区块生产商。

In case of a software fork the longest chain branch will be chosen automatically, so a blockchain fork can’t happen.

面临软件分叉时，最长的链分支将会自动被选中，所以区块链分叉将不会分生。

## Accounts 账户
All EOS accounts have human readable names chosen by the account creator, like in Steem blockchain. There will be also namespaces like @user.domain available for @domain account owners.

就像在Steem区块链中一样，所有EOS账户都是由账户创建者选择的人类可读的名字。同样的，这也会有名称空间像@@user.domain提供给@domain账户所有者。

The account creation fees (which are promised to be insignificant) will be paid by app developers. (That‘s why, if you plan to create EOS based apps, it’s important to get as much EOS tokens as possible.)

账户创建费（EOS承诺将是微不足道的）将会付给应用程序开发者。（这就是如果你要基于EOS开发应用程序，你要尽可能多获得EOS令牌的原因。）


Accounts and scripts can exchange messages and this is how smart contracts will be defined.

账户和脚本能够自动交换消息，这就是智能合约的定义。

## Security 安全性

EOS implements sophisticated permission management and multi user control over funds which is the best defence against hacking.

EOS实现了复杂的权限管理和对资金的多用户控制，这是防范黑客攻击的最佳防御手段。

Sensitive actions could have a mandatory delay defending account owners against key theft. Advanced account recovery will provide protection even if the keys are stolen.

敏感的机制设计会有一个强制性的延迟，来保护账户所有者不受密钥盗窃的影响。即使密钥被盗，先进的帐户恢复也会提供保护。

## Tokens 代币

The EOS blockchain will be resource constrained. There are 3 types of resources in EOS — bandwidth and log storage, CPU, and RAM. Resources allocated to apps will be measured in tokens directly and so will be independent on token price volatility. Block producers will be paid in tokens and will spend these for better equipment increasing the network performance.

EOS区块链将会受到资源的限制。在EOS中有三种类型的资源——带宽和日志存储、CPU和RAM。分配给应用程序的资源将直接用代币来衡量，因此将独立于代币价格波动。区块开发者将获得代币支付并利用它们购买更好的设备，为了提升整个网络性能。


3 community benefit apps will be chosen by user votes to receive a percentage from new annual token supply which could be capped to 5%.

用户将会投票选出3款社区福利应用程序，它们能够在新的年度中获得一定比例的代币供应份额，这个比例将是5%。

## Governance 治理
Governance is the process of reaching consensus in cases when no software algorithms can help.

治理是指在没有软件算法能起效的情况下达成共识的过程。

The source of power in EOS are the token holders and this power is delegated by them to block producers. If block producers refuse to implement necessary changes proposed by token holders, they can be voted out.

EOS的影响力是来自令牌持有者，并且这个影响力将由它们授权给区块链开发者。如果区块链开发者拒绝使用令牌持有者们提出的必要改变，他们将会被投票出局。

EOS is enabled to have a constitution, i.e. a p2p contract among its users, and a hash of its current version will be included in every transaction.

EOS能够形成一个宪法即用户之间的p2p协议，而在每一笔交易中，当前版本的一个散列函数将会被包含进去。

The constitution and the EOS protocol can be updated if at least 17 of 21 block producers maintain approval of it during 30 days. Another 30 days approval will be needed to implement the changes. So non-critical fixes will take 1-2 months and important forks about 2-3 months. Emergency bugs will be fixed immediately and glitchy apps will be freezed without affecting the whole blockchain.

如果21个区块开发者中，至少有17个在30天内保持对其的同意，则社区宪法和EOS协议将可以升级。接下来还需要30天的同意来部署这一改变。因此，非关键的修复需要1-2个月的时间，重要的软件分叉则大约需要2-3个月。紧急漏洞会被立刻修复。在不影响整个区块链的情况下，关键性应用程序将被冻结。

## Thank you for reading! Feel free to share ideas and information related to EOS in comments!

## 谢谢你的阅读！欢迎你在评论区自由地分享关于EOS的想法和资讯
## Credits 感谢
[Photo by paul morris](https://unsplash.com/photos/IHKBF23A_iw) on Unsplash

图片是来自paul morris在Unsplash平台上发布

## Related posts 相关文献
[How to buy and claim EOS tokens: a step by step tutorial](https://steemit.com/eos/@vitkolesnik/how-to-buy-and-claim-eos-tokens-a-step-by-step-tutorial)

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

林炜鑫，在读硕士，专注区块链技术研究与行业分析，欢迎加微信号:happyzai1993。

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------





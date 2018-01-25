# 加密货币差价套利分析

> 本文翻译自：[The Case For Never-Ending Cryptocurrency Arbitrage Spreads](https://hackernoon.com/the-case-for-never-ending-cryptocurrency-arbitrage-spreads-788e94441d60)
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [咪咪](https://github.com/mimizhang)
>
> 翻译时间：2018-02-22

I launched [Token Spread](https://www.tokenspread.com/) in Oct 2017. The project came out of my adventures with different arbitrage strategies in the crypto markets. Two things have happened since the launch of Token Spread, 1) arbitrage spreads have been extremely consistent, and 2) the crypto space has continued to expand at a rate that melts my brain. When I put my head down for a couple weeks to work on new features (like Telegram integration for our [spread alerts](https://www.tokenspread.com/alerts)), I pop my head back out and it feels like the crypto world has passed me by all over again.

我在2017年10月上线了[Token Spread](https://www.tokenspread.com/)。这个项目是我在加密货币市场的不同套利经验中诞生的。从Token Spread上线以来，发生了两件事：1. 差价套利一直存在；2. 加密货币市场以让我无法想象的速度持续膨胀。当我花几周时间埋头苦干开发新功能（比如将Telegram整合进[spread alerts](https://www.tokenspread.com/alerts)），等我回过头来，加密货币市场让我恍如隔世。

In many conversations about arbitrage, there seems to be a common opinion that arbitrage spreads will continue to tighten over time and/or disappear (i.e. be unattainable for the everyday trader).

在关于套利的很多讨论中，似乎普遍观点都认为，差价套利的空间会慢慢变窄甚至消失（比如，对日常交易员来说差价套利更是不可能）。

Despite the suspicions of many, the distributed nature of cryptocurrencies and the natural interplay between availability, security, regulation and anonymity will continue to create persistent market inefficiencies. I am confident that arbitrage opportunities will continue indefinitely due to the following:

尽管有许多人怀疑，但加密货币的分布式的特性以及在可用性、安全性、监管和匿名性的相互作用下，这个市场的低效率将持续存在。我相信，由于以下原因，套利的机会将无限期的持续下去：

## 1) Staggering regional competition between exchanges.

## 1. 交易所之间的地区竞争越来越激烈

There has been a gross proliferation of trading exchanges. Regional interests and trends continue to result in predictable arbitrage opportunities and inefficiencies.

交易所的数量一致在急剧增长。地区利益和趋势持续导致可预测的套利机会和市场的低效率。

At present, the top 10 exchanges on CoinMarketCap based on volume are listed below. This list has changed a lot in 24 months. It will continue to be a revolving door.

以下是目前在CoinMarketCap上交易量排名前十的交易所。这个排名在在过去一年里发生了很大的变化。他将一直像个旋转门不停的发生变化。

1. Upbit
2. Binance
3. Bithumb
4. OKEx
5. Bitfinex
6. Huobi
7. Bittrex
8. HitBTC
9. Kraken
10. GDAX

The current BTC/USD spreads on Token Spread are:

当前在Token Spread中BTC/USD的差价是：

![](https://cdn-images-1.medium.com/max/1600/1*eLiQ7AORkxMNTgbKE1iw3w.png)

## 2) Inability of exchanges to keep pace with demand.

## 2. 交易所跟不上市场需求

Kraken was recently down for 48+ hours while upgrading their trading platform. This is what response times look like post-upgrade:

最近，Kraken为了升级交易平台停摆了超过48小时。这就是所谓升级后的响应时间：

![](https://cdn-images-1.medium.com/max/1600/1*0hMNj199MFt8cM1xjo22rQ.png)

This is not meant to pick on Kraken, a company that has raised millions in capital, but to illustrate just how hard it is to keep up with demand. It’s very easy to say “let’s start an exchange.” It’s a different thing altogether to achieve a level of scale, stability and super low response times like Etrade or Interactive Brokers.

不是故意选择Kraken作为例子，而是为了说明为了跟上需求是多么困难，要知道Kraken是一家已经融资数百万美元的公司。说一句“让我们开始交易吧”很容易。这和像Etrade和Interactive Brokers那种程度的规模、稳定性以及超低的响应时间完全不同。

API connectivity across the major crypto exchanges has proven to be highly unpredictable, without exception. This has been one of the big learnings from building Token Spread.

无一例外，各大交易所的接口都被证明是十分不稳定的。这是我在做Token Spread时学到的重要经验之一。

## 3) Massive proliferation of individual cryptocurrencies.

## 3. 个别加密货币的急剧增长

There are currently over 50 legitimate contenders for the next best cryptocurrency. While Bitcoin and Ethereum are the clear leaders, there is an arms race for the next best blockchain. Regional influences and the unpredictable addition of new currencies to exchanges around the globe will continue to bring persistent arbitrage opportunities. Because cryptocurrencies are decentralized in nature, with the community able to host its own nodes, there can be no predictable and centralized authority over the global exchanges, protocols, or methods of transfer and remuneration.

目前有超过50种加密货币在竞争成为下一个最好的加密货币。尽管比特币和以太坊是毫无疑问的领跑者，但为了成为下一个最好的加密货币，还是有一场军备竞赛。全球交易所的地区性影响以及不可预测的新货币会持续影响带来机会。因为加密货币的性质是去中心化的，社区能够自己托管自己的节点，所以在全球交易，协议，以及转让和获取报酬的方式中，不可能出现可预测及中心化的当权者。

## 4) Security breaches and hacking will continue to destabilize the environment.

## 4. 安全漏洞以及黑客行为将继续破坏市场

1. [NiceHash hacked](http://bitcoinist.com/nicehash-ceo-steps-63-million-bitcoin-stolen-cyber-attack/) for $63M in Bitcoin.
2. [CEX breached](http://www.telegraph.co.uk/technology/2017/08/30/two-million-cex-customers-details-stolen-cyber-attack/) for 2M in user data.
3. [Mt. Gox hacked](https://en.wikipedia.org/wiki/Mt._Gox) or $473M in Bitcoin.
4. [Ethereum DAO](https://www.cryptocompare.com/coins/guides/the-dao-the-hack-the-soft-fork-and-the-hard-fork/) hack for $70M in Ethereum.
5. [Bitfinex hacked](https://en.wikipedia.org/wiki/Bitfinex_hack) for $72M in Bitcoin.
6. [CoinDash ICO compromised](https://www.coindesk.com/7-million-ico-hack-results-coindash-refund-offer/) for $7M in Ethereum.


1. [NiceHash](http://bitcoinist.com/nicehash-ceo-steps-63-million-bitcoin-stolen-cyber-attack/)6300万美元比特币被黑客盗取
2. [CEX](http://www.telegraph.co.uk/technology/2017/08/30/two-million-cex-customers-details-stolen-cyber-attack/)200万的用户数据被破坏
3. [以太坊DAO](https://www.cryptocompare.com/coins/guides/the-dao-the-hack-the-soft-fork-and-the-hard-fork/)被黑造成7000万美元的以太币损失
4. [Mt. Gox](https://en.wikipedia.org/wiki/Mt._Gox)4.73亿美元比特币被黑客盗取
5. [Bitfinex](https://en.wikipedia.org/wiki/Bitfinex_hack)7200万美元比特币被黑客盗取
6. [CoinDash](https://www.coindesk.com/7-million-ico-hack-results-coindash-refund-offer/)在ICO中损失了700W美元以太币

## 5) Regulators will not be able to keep pace with the proliferation of exchanges.

## 5. 监管将无法跟上急剧增长的交易所的步伐

Regulation will keep the cryptocurrency environment unstable, with large players being handicapped at random, as we’ve seen with [Bitfinex](https://news.bitcoin.com/bitfinex-to-terminate-services-to-us-retail-customers-by-november-9/) in China and may soon see in South Korea and the United States.

监管将继续是的市场环境变得不稳定，大型玩家将随时可能受到伤害，就像我们在中国看到的Bitfinex一样，很快的同样的情况就会在韩国和美国发生。

Regulation will also cause exchanges to move to more favorable countries. Moves like this will cause significant disruption.

监管也将使交易所转移到更加有利的国家。这些监管行为会对市场环境造成严重的破坏。

## 6) Transferring U.S. Dollars will remain a nightmare.

## 6. 美元转账依然是一个噩梦

Wiring large sums of native fiat currencies (like USD, GPB, Euro, etc.) is not fun. It takes a long time. There is no anonymity from local banking systems.

连接大量的法币（比如美元，英镑、欧元等）并不好玩。要花很多时间。银行系统都是实名的。

One of the greatest gifts that cryptocurrencies will bring to the global banking system is forcing the institutional players to address the current problems with money transfer. However, this will take a very long time, and the interested parties (Banks and government regulators) are fundamentally incentivized by compliance, transparency and safety, as opposed to speed and anonymity.

加密货币给全球银行体系带来的最大礼物之一就是迫使机构人员使用汇款来解决当前的问题。然而，它很费时。银行以及政府监管部门的根本出发点在于合规性，透明性以及安全性，而不是速度和匿名性。

## 7) The future of trading will be peer-to-peer.

## 7. 点对点交易是未来

Along with greater regulation and transparency will come natural anti-trends. One such trend will be more efficient peer-to-peer trading, or even blockchains whose host nodes support a standardized peer-to-peer trading exchange. In the quest for greater privacy, efficiency and autonomy, the decentralized nature of cryptocurrencies will naturally send many projects deeper into the dark and anonymous web.

监管和透明化是逆势而行，点对点交易甚至是主机节点支持标准的点对点交易的区块链才是趋势。为了寻求更大的隐私、效率和自主权，加密货币去中心化的本质将自然而然的使得许多项目更加的深入到黑暗且匿名的网络中。

------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

咪咪 爬虫工程师，区块链技术爱好者，相信区块链技术能够重构社会的信任基础，欢迎加微信号:miao-mimi-miao

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

------


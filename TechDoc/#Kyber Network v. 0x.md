# Kyber Network v. 0x    
# Kyber网络与0x协议的比较

> 本文翻译自：https://www.reddit.com/r/kybernetwork/comments/7btkms/0x_v_kyber_network/
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)  [范楷书](https://github.com/van888888/EOS)
> 
> 翻译时间：2017-11-24

Kyber is an emerging decentralized exchange. The platform ultimately has several unique aspects that separates it from both centralized and other decentralized exchanges. Vitalik Buterin is an official advisor for the project. In contrast, 0x is a platform, not an exchange. 0x allows any user or application to set up a decentralized trading application. It is already being utilized by a number of DApps including Ethfinex, District0x, Augur, and Melonport. As such, Kyber and 0x aren’t truly direct competitors as their methods are different; however they are effectively both trying to capitalize on the decentralized exchange market.

KYBER TOKEN: KNC 0x TOKEN: ZRX

Kyber是即将诞生的新一代去中心化交易所，它在许多方面与传统的中心化交易所和其他去中心化交易所有着根基上的不同，以太坊创始人Vitalik Buterin是该项目的官方顾问。 相较Kyber, 0x 是一个平台，而不是交易所，它已经被用作搭建Ethfinex 、District0x、 Augur和Melonport等去中心化项目（DAPP）。因此，Kyber和0x 并不是真正意义上的竞争对手，它们运行的方式是不一样的，但是它们都正在扩大着去中心化交易市场的份额。

Kyber的代币：KNC， 0x的代币：ZRX

Kyber details:

·Today, decentralized exchanges face a problem. The issue is how to connect buyers with sellers. Some solve this via order books kept on chain. The issue here is that then there is a fee for every order placed (even if it’s later canceled). Some attempt to solve this by instead conducting the matching off chain via an intermediate party — only moving on chain for the actual trade — this is how 0x solves the problem. The issue with this is that is then trust needs to be placed in the hands of an intermediary. Kyber solves this with reserves (read more later).
·Instant exchange which creates a faster and safer transaction。
·No modification of code to adopt new coins - this prevents bugs and errors from corrupting the network. Smart contract already allows for seamless coin integration.
·API allows for merchants to accept any currency but still get paid in ether. *Wallet and API allows for a user to pay for goods in one cryptocurrency and convert it to the necessary currency, seamlessly and in one process. Imagine that an ICO only accepts ether. You can send NEO to the address, Kyber converts it to ETH, and the ICO accepts it - all the merchant sees is that you sent ether.
·No fees besides the associated gas
·Future advanced trading abilities such as forwards and options. These would allow people to hedge against Ether’s price. As an example, imagine you want to participate in an ICO in three weeks. You can buy your ether now and risk the price of ether dropping, or you can wait to buy your ether and risk it rising. With Kyber, you can utilize a forward to agree to the future purchase at today’s price.
·Future cross chain trading - think atomic swaps
·Exchange rates are readable by smart contracts - thus, imagine a network where an exchange request is broadcasted, and all relevant rates are compared across all relevant exchanges, and the best one is selected.

Kyber详细信息：

·今天的去中心化交易所面临一个问题：怎样链接买家与卖家。如bitshare和etherdelta之类的去中心化交易所，通过将挂单信息存入区块链中来实现链接，但这会让每一笔挂单（甚至取消挂单）都需要收取网络手续费。0x尝试通过单独把每笔真实的交易搬入区块链中，而不是由传统的中介来进行撮合，以此解决链接买卖双方的问题，但是这一方式又需要双方都信得过的中间平台。Kyber使用储备交易服务商解决这一问题（详见后文）。

·Kyber能完成极速交易，让转账和成交更快更安全。

·上新代币交易时不会修改代码，这样可以防止漏洞和系统错误使网络瘫痪。智能合约早已部署好代币的无缝集成。

·允许买方使用以太坊支付但卖方能接收到任意货币的API接口。Kyber钱包和API都允许使用者用任一种加密数字货币支付支付商品，并把它一步无缝转化为商家接受的货币种类。 假设某一项目的ICO只接受以太坊，你可以将Kyber钱包中的NEO（小蚁股）转入其地址，kyber会自动转换其为以太坊，ICO项目成功接收，并且项目方只会看到你发送了以太坊。

·除了相关的gas费用外再无其他费用。

·未来开放期权交易和双向交易等高级交易功能，这些功能可以对冲投资者在以太坊价格波动前的风险。举个例子，假设你想在三周之后参加一个项目的ICO，你选择现在就买入以太坊，那么你会承担以太坊价格可能会下跌的风险；如果你选择届时再买入以太坊，那么你亦会承担其价格上涨带来的损失。但是有Kyber的帮助的话，你可以使用期权交易，以现在的价格完成三周后的购买行为。

·未来开放跨链交易——想象代币间的原子转换。

·交易汇率通过智能合约实时可读——所以可以想象一个未来的网络，一个交易订单被广播出来之后，自动比较所有交易所之间的相关汇率，再选择最实惠的一个进行成交。

0x details:

·Unlike Kyber, which exists entirely on chain, utilizing reserves for conversion and exchange, 0x has a hybrid method. Matchmaking is done off chain and only brought on chain for the transaction. Anyone can act as a matchmaker by maintaining an order book of open orders. The programmable smart contract allows the market maker to set a fee for service for managing the transaction. A seller submits a sell order. This is accepted by the matchmaker and posted in the order books. A buyer comes along, accepts the sell order and the transaction is moved on chain and executed by the smart contract.

·While ultimately, no trust is required in the matchmaker in the actual transaction, one must still trust them to accept all relevant orders.

·Sellers can submit two kinds of sell orders, private and public ones. Public orders are exactly what is explained above - a generic order that can be filled by any buyer address. Private orders are specifically for one buyer address. Private orders can be completed over any network (Facebook, WhatsApp, SMS, etc.).

0x详细信息：

·与kyber完全在建立区块链上不同，0x有着混合式的方法来实现价值的转换和交易：在链下完成订单的撮合，只把有效的交易信息带入区块链中。任何机构都可以通过维护一个公开的报价单来扮演中间人的角色，可编程的智能合约允许中间人为交易服务的正常开展设定一定的手续费。一个卖家发布一个卖单，中间人接受后发布到报价单中，买家随后而来，接受卖家的报价，交易被存入区块链中，再由智能合约执行成交。

·虽然有区块链的帮助，不必担心最终成交过程中中间人的信用问题，但交易者扔需要信任中间人能公正的处理所有的相关报价。

·卖家可以提交私人的或公开的两种类型的订单。公开卖单的执行正如上文所述，会被任意买家的公钥地址部分或完全成交掉。私人卖单则不同，只能被一位特定买家的公钥地址成交，并且能够在任意的网络程序（如Facebook,WhatsAPP,甚至微信等）完成交易。

Additional Relevant Kyber Information:

·Kyber utilizes reserves for their network. Reserves are how they provide liquidity for the network. There will always be a singular reserve that is managed by Kyber and provides an appropriate amount of crypto tokens for transactions. However, there are also additional reserves, both public and private. Private reserves are simply private coin holders who wish to act as a source of tokens for exchanges. Reserve managers can set their own rates. They also get access to far greater exposure by using Kyber. Public reserves are similar except that they can receive contributions from the public who then share in the profits. This allows longterm holders to capitalize on some of their assets now and make a profit. Kyber’s platform also offers tools for reserves that assist them in managing and rebalancing their portfolio. All reserve transactions are managed by the smart contracts so no trust of reserve managers is necessary.

·In a practical example, imagine that you want to convert Golem to Ark. You send Golem to Kyber. Kyber examines all the possible exchange rates from all the possible reserves on Kyber and chooses the best rate. The reserve then receives Golem and the smart contract sends Ark in return.

·Reserves also provide liquidity for lower market cap coins since it is impossible for Kyber to list all the tokens, but there is likely someone who wishes to create a reserve with that coin. Reserves also provide a kind of free market competition for low exchange rates.

Kyber的额外相关信息：

·Kyber网络使用储备交易服务商（以下简称交易服务商），作为为自身提供流动性的方式。网络内始终会有一组由Kyber单独管理的交易服务商，并且会提供适当额度的代币用于交易处理奖励，同时也有额外的公共和私人的交易服务商。私人服务商即希望在交易中扮演介质角色的代币持有者（如EOS的交易后备队由诸多EOS代币持有者组成），服务商可以自由制订报价，并且通过Kyber网络大大提高自己的曝光率。公共服务商性质亦类似，除了能够从在交易中获利的公众交易者那里取得捐赠。这就使得长线投资者能够让手中的筹码重新进入资本市场，并且从中盈利。Kyber的平台也为交易服务商提供能够帮助他们管理和完善投资组合的工具。所有经由交易服务商处理的交易都由智能合约管理，因此不必有针对其的信任问题。

·举个实际的例子，假设你想要把手里的Golem代币转换为Ark, 
第一步：你将Golem发送到Kyber
第二步：Kyber检索网络中所有交易服务商的报价后，选择最优的报价
第三步：服务商收到Golem,智能合约将Ark代币发回给你。

·Kyber不可能上市所有的代币交易，但是有投资者希望成为一些低市值代币的交易服务商，因此这一模式也为一些低市值代币增添了流动性。同时，交易服务商之间的自由市场竞争也促使了整体交易费用的降低。

— Unique Token Valuation —
Kyber Supply: A maximum amount of coins minted will be 226 million tokens. Currently there are 134,132,697 in circulation. 

0x Supply: Capped at 1 billion tokens. Currently there are 500 million in circulation

Kyber (KNC) Value: fees paid by reserves to the network are in the form of KNC. Thus, reserves need to stockpile tokens as they are a vital component to the eco system.

0x (ZRX) Value: As with Kyber, fees are paid by buyers and sellers to the matchmaker. In addition, holders of ZRX are entitled to participate in the decentralized governance of 0x - voting on upgrades and changes to the system.

Kyber Inflationary/Deflationary Factors: All tokens paid in fees by the reserves are burnt after paying for operation expenses. Fees are a percentage of the coins in circulation so the supply will never by exhausted. Ultimately this creates an upward price movement as more users adopt Kyber.

0x Inflationary/Deflationary Factors: Over the next four years, the token supply will double. Unlike, with Kyber, there is no burning of tokens. Tokens used for fees are simply recycled in the ecosystem.

Kyber Allocation: the token was allocated via an ICO. 19.5% of tokens are held by the company. 19.5% are held by founders, advisors and seed investors. 61% is held by the public.

0x Allocation: 50% of tokens were sold to the public during the ICO. The additional allocation breakdown is such: 15% held by 0x, 15% held in a developer fund for the purpose of developing projects, 10% held by the founding team, 10% held by early investors and advisers

— 独立代币价值评估 —

KNC(Kyber)总量:最大设计总量为2亿2千6百万KNC，目前流通中数量为1,3413,2697KNC

ZRX（0x）总量：十亿总量硬顶，目前流通中5亿ZRX。

KNC价值：交易服务商会以KNC作为费用支付给Kyber网络，同时也需要储存KNC来增强在生态中的竞争力。

ZRX价值：和Kyber类似，买卖双方也需要用ZRX作为手续费支付给中间人。除此之外，ZRX持有者还享有0x中去中心化自治生态体系中的政治权利，可以对0x系统的升级或调整进行投票。

KNC的通货膨胀/紧缩因素：所有交易服务商支付给Kyber的KNC在收取固定的操作费用后将被燃烧，而支付KNC的数量是根据流通中代币的总量算出的，所以KNC永远不会被燃尽。最终当越来越多的人开始使用Kyber时，KNC的价值也会水涨船高。

KNC的通货膨胀/紧缩因素：在接下来的四年中，ZRX流通中的总量将翻倍。与Kyber将作为手续费的KNC燃烧不同，0x生态中的ZRX将被循环使用。

KNC分配：KNC通过今年第三季度的ICO发行，Kyber公司持有总量的19.5%，开发者、顾问、种子投资人持有总量的19.5%,公众持有剩下的61%。

ZRX分配：总量50%的代币通过今年第三季度的ICO发向公众，额外的代币分配如下：0x公司持有15%, 用于奖励基于0x平台开发项目的开发基金持有15%，资方团队持有10%，早期投资者和顾问持有10%。

—— Conclusion ——
Why I like Kyber: I really like the prospects of this platform. I think it solves many of the issues facing decentralized exchanges at the moment. Its role in facilitating the adoption of crypto could be huge and within crypto, it will be critical in supporting cryptocurrency which will have an ever increasing amount of tokens. It’s API and wallet offer user friendly systems for the platform. I like how there is an intrinsic worth to the KNC token and that it’s demand is proportional to the amount of people who use Kyber. The burning of tokens is a solid deflationary method. I think Kyber is a solid short term investment, especially considering its recent drop to just 2X its ICO price. Longterm, it is a risky yet potentially highly profitable investment.

—— 结论 ——
我为什么喜欢Kyber：我非常欣赏Kyber平台的前景，它解决了当下很多去中心化交易平台所面临的问题。它对加密货币的大面积普及和使用具有着促进作用，并且是不断出生的新代币的好去处，用户可以很轻松的通过Kyber移动端和钱包使用Kyber网络。我同样欣赏在网络中有着内在价值的KNC代币，并且使用Kyber网络的人越多，它的价值也会相应提升。KNC代币的燃烧也是一种固定制造通货紧缩的手段。考虑到KNC代币近期的价格回调到ICO价格的2倍左右，我认为它是一项绝佳的短期投资，但就长期投资而言，在承担一定风险的前提下非常有可能取得可观的回报。

Concerns for Kyber： 1. Much of the project is undeveloped. Whether it can achieve what it aims to achieve requires a lot of supporting technology as well - some of which is still in its early stage. Examples of technology that Kyber will rely upon includes: melonport, polkadot, and cosmos. If this tech doesn’t come to fruition, or takes longer than expected, Kyber will suffer. 2. I can see a bit of a “chicken and egg” scenario developing. Much of Kyber’s potential lies in its ability to create a robust reserve network - ultimately keeping rates low and supporting liquidity for a wide selection of tokens. People will only begin using Kyber when this occurs. Reserves will only come when it is profitable — profitability depends on a larger user base. Thus the potential issue. 3. Limited to ER20 - this problem isn’t unique to Kyber, but their growth potential is limited until cross-chain conversions are possible. 4. Autocorrect changing Kyber to Cyber every single time I type it - just kidding, kind of…

对Kyber的担忧：
1.许多的技术环节仍待开发。Kyber想要实现上文目标中的状态的话还需要很多技术上的支持，并且其中一些还处于早期开发阶段，比如需要Melonport、Polkadot、Cosmos等技术的完善作为基础。如果这些技术没能预期完成开发甚至流产的话，Kyber的发展会受到影响。
2.我能看见在Kyber网络中有一些”先有鸡还是先有蛋’的悖论。Kyber的良性发展需要许多强大的储备交易服务商作为支撑，有越多越强大的交易服务商，就能让交易费率尽可能的降低并且为网络中的各种代币带来巨大的流动性。但人们又只会在交易费率较低和流动性较大时才大量使用Kyber，交易服务商此时才会有利可图并介入，这就成了一个悖论。
3.限制于交易ERC20代币，当然并不是只有Kyber面临这一问题。如果成熟的跨链技术没有即时出现的话，Kyber的发展将受到很大限制。

Why I like 0x: 0x is far less ambitious than Kyber. This means that right now, it’s simple, functional, easy to use model is the go to platform for decentralized exchanges. The fact that already, DApps are using them gives them a big advantage over Kyber. Over the next couple of years, I think 0x could own the decentralized market making them a great investment. Longterm, I think they are overtaken by more advanced trading platforms.

我为什么喜欢0x:比起Kyber，0x的野心没有大，这也意味就当下而言，0x更加简单实用，而简单实用的模板是去中心化交易所最需要的。有许多DAPP（去中心化应用）已经开始使用0x，这让它有了相对Kyber更多的优势。就之后几年来看，0x能够建立在去中心化交易市场上的绝对优势，并且让在其上搭建的平台和其本身拥有巨大的投资价值。但如果放眼更长期的话，可能会有更先进的交易模式取而代之。

Concerns for 0x: 1. Unclear about how governance will work - as of now, there is very little information on how the actual voting model will work. Within the token code, there is nothing relating to governance. This will come, but we saw with the DAO hack the risk of design flaws in regards to this. 2. The potential for buyers and sellers to cut out the middleman - there exists the potential for fee avoidance by buyers finding sellers on the order books, contacting them directly, and performing the transaction privately. This would eliminate a huge value for the ZRX token. 3. Risk of arbitrage - because 0x isn’t instant, users are vulnerable to savvy traders who can take quick advantage of stagnant orders on the book during rising or falling prices. The same can be said for limit orders on centralized exchanges - however with say Bittrex, the option for putting a market order is always available.

对0x的担忧：
1.目前还不清晰如何履行社区自治，关于实际的投票模式的信息还非常少。在代币的代码里面，几乎看不到与社区治理相关的内容。虽然这些很快会被设计出来，但是诸如DAO黑客事件之类的因素让社区治理充满了挑战。
2.存在买卖双方跳过中间人交易的潜在情况。买方为了节省一些交易手续费，直接在报价单上寻找卖方，并私下联系卖方交易的可能性是存在的。这样的事件会让ZRX的价值大大下降。
3.套利的风险。因为0x的交易系统不是即时的，在行情剧烈的波动中，用户的一些类似限价单的交易可能会被聪明的交易者用于套利。但类似Bittrex这样的中心化交易所中，总是能够在市价和限价交易之间进行选择。


—— Ultimately, the decentralized market needs a Kyber like platform - with it’s guaranteed liquidity, instant conversions, advanced financial tools like forwards and options, and cross chain trading. 0x is winning now because Kyber can currently do none of this. 0x will likely always have functional use but I think that they are vulnerable to competition from more advanced platforms long term. Whether Kyber is the one that accomplishes this remains to be seen.

——最终，去中心化交易市场需要一个像Kyber这样的平台，能够保证交易的流动性、及时性，并提供能够期货和期权等高级交易和跨链交易。0x暂时取得领先，因为Kyber目前还处于襁褓之中。0x可能会一直作为底层协议存在于市场，但长期来看可能会有更先进的平台取而代之。Kyber会不会成为这一更先进的平台，让我们拭目以待。 

— On a side note — We should all understand the dangers and potentials for front running with regards to decentralized exchanges. This applies to both 0x and Kyber. The term comes from old stock exchanges where orders were literally submitted by hand. Brokers would literally walk across the room with their trade order. A broker could thus quickly write their own trade order and run in front of the other traders to benefit from the transaction themselves.

In blockchain, miners can do this. Because the miner can see the buy and sell orders coming in and ultimately control the order in which the transactions are confirmed, he or she could write a new order for themselves, submit it before the original buy order, and profit. Even more maliciously, because buying bumps the price slightly, the miner could receive the original buy order (A); then he would write his own buy order (B). Immediately after B executed, he would sell his newly acquired tokens at a slightly higher price to the original A order. Nice, quick profit.

This doesn’t happen with bitcoin because every transaction is one to one. It happens with Ethereum because there are multiple users vying for the same resource. Neither 0x or Kyber solves this
As always, do your own investment research.

— 写在最后—我们都需要知道在去中心化交易市场上存在着扒头皮交易（非法抢先交易）的潜在危害。Kyber和0x上都可能会存在这一行为。这一典故来源于最早的股票交易市场，那时交易订单还完全由人工递交，股票经纪人会拿着订单穿越交易大厅进行报价，这时他们可能会快速地把自己的订单写在所有客户订单的前面，以从交易中套利。
   在区块链系统中，矿工也可能会这么做，因为他们能看见所有过手的买卖订单，通过把自己的新订单以更有优势的价格在市场上成交，从中获利。更加荒唐的做法是，因为大额买单可能抬高市场价格，矿工在收到原买单(A)后，立即制定自己的新买单（B）。在新买单（B）即时成交后，马上将获得的代币以稍微高一些的价格卖给原买单（A），以此获利。
   比特币的系统中不会出现这种情况，因为每笔交易是由单一节点处理的。以太坊上则可能出现这一情况因为会有多个节点来争夺同一笔资源的处理。目前除非能够保证足够大的流动性，Kyber和0x都还不能很好的解决这一问题。
   总而言之，区块链行业的投资充满着机遇与挑战，在投资前务必做好充分的调研与准备。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

范楷书 区块链技术爱好者，区块链项目与比特币价值投资者，EOS粉丝. 欢迎加微信号:FSK818

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

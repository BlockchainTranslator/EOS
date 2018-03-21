# On Accelerating Blockchain Evolution using Different Funding and Team Models | 通过不同的资金和团队模型加速区块链的革命

> 本文翻译自：https://medium.com/dfinity/on-accelerating-blockchain-evolution-using-different-funding-and-team-models-1c04c3d0893a
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [何德林](https://github.com/BlockchainTranslator/EOS)
> 
> 翻译时间：2018-2-4

I originally started this article as a comment on Fred Ehrsam’s similarly themed post. The comment just got too big because I was sipping my way through a large coffee, so I broke it out into its own article. Enjoy!

这篇文章起源于对Fred Ehrsam类似主题文章的评论。这条问题太大了，因为我当时正在喝一大杯咖啡，所以我把它细化后写进了自己的文章。享受吧!

Many people in the blockchain industry want to see faster progress in R&D with respect to blockchain performance, capacity (scaling), privacy, governance and secure “stable value” tokens. Naturally the question arises as to what funding and team models would best achieve this goal.

区块链行业的许多人都希望看到，区块链能在性能、容量(扩展性)、隐私、治理和安全“稳定”代币方面，取得更快的研发进展。自然地，会引出问题：什么样的资金和团队模型最能达到这个目标。

Clearly the problem is not limited to funding. The Ethereum Foundation holds ~$200M in its endowment, and Tezos and EOS have collected even greater funds from public investors in recent ICOs. That is a huge amount of financial ammo that the leaders of these projects can throw at engineering and research work. The interesting question is how such resources can best be directed towards developing blockchain protocols as fast as possible.

显然，问题不是受限于资金。以太坊在其捐赠基金中持有2亿美元，Tezos和EOS在最近的ICO中，从大众投资者那里获得了更多的资金。项目的领导者们可以把这些巨大的金融弹药，投入到项目工程和研究工作中去。有趣的问题是，这些资源如何有效地投入到项目中，以便最快地开发区块链协议。

Fred makes the case that R&D work should be thrown open to the market, with substantial bounties offered to teams that can add functionality such as sharding that would allow blockchain networks to scale-out their capacity (sharding increases capacity by partitioning responsibilities for computation and storage across the network). Tezos plans a similar approach, and explicitly states that it will foster the formation of decentralized teams that compete for chunks of its funds dispersed as bounties. The idea is that competition amongst teams, and having a larger pool of brains working on the core problems and code, will drive faster progress. There must at least be some merit to this thinking.

Fred认为研发工作应该向市场开放，有大量的奖金提供给增加功能的团队，比如，可以让区块链网络扩展他们容量的分片(分片通过划分网络中的计算和存储的能力来增加容量)。Tezos计划采用类似的方法，并明确表示，它将促进去中心化团队的形成，而这些去中心化的团队将会竞争留出奖金。这个想法是，团队之间的竞争，以及在核心问题和代码上拥有更大的智力，将推动更快的进展。这种想法有一些可取之处。

However in my view there are two major reasons why this approach is not entirely practical: (1) the creation of novel decentralized protocols and cryptography often involves years of thinking and skills that are rare and thus these technologies cannot just be conjured on demand by those wishing to earn bounties, or indeed those who have just run ICOs (2) even though such pieces of fundamental science can often be described in isolation, their introduction into a decentralized network stack often involves far reaching technical changes, making it very difficult for teams to work independently and for critical pieces to be built out incrementally. For example, the implementation of sharding also involves the adoption of a new smart contract programming model (in which contracts communicate using asynchronous message passing) and this involves yet more complex science and engineering.

但是在我看来,这种方法是不完全实用，主要原因有两个:(1)创建去中心化协议和加密技术，通常需要多年的思考和技能,并且是极为少见的,因此这些技术不能指望那些希望赚取赏金的人或者刚刚完成ICO的人，魔幻般地变出来。(2)即使这样的基础科学中可以分开予以独立地描述，但他们引入一个去中心化的网络往往涉及深刻的技术变化,使它很难独立完成，或者关键部分由逐步累积的方式建立起来。例如，分片的实现需要采用一种新的智能合约编程模型(在该模型中可以使用异步消息)，而这涉及到更复杂的科学和工程。

For such reasons, my claim is that a far better approach is to create a “Google style” team to develop the stack. The problem here is that if you really want to build a team of similar quality to the one Google had in the early days, you need to start with extremely strong authentic original science or you will not be able to attract the initial core team of superstar talent — they would easily see through white papers that are really ICO marketing documents, and of course beautiful technical designs where what the initial Google operation was built around, not marketing. Once you have meaningful novel science supported by such a team of superstars, you then need to add further layers of superstars to the team, in the form of an onion, where the quality of each new layer will determine the quality of later layers because superstars strongly prefer to join other superstars. This is a very, very difficult thing to do — especially in a rush — and in the blockchain industry would demand a combination of technical and entrepreneurial experience that is in short supply.

基于上述原因，我认为，一个更好的方法是创建一个“谷歌风格”的团队来开发项目。这里的关键问题是,如果你真的想在早期建立类似谷歌质量的,你需要在开始就有极强的原创科学技术否则你将无法吸引超级天才加入初始团队,他们会很容易地明白，通过白皮书这一ICO营销文件,当然还有美丽的技术设计,最初的谷歌操作是建立在什么,不是销售。一旦你有一个意义非凡的原创科学技术，并由一个超级明星团队支撑,你可以进一步的扩展项目团队，就像一个洋葱,每一层的质量将决定后层的质量,因为技术明星强烈倾向于加入其他的超级明星团队。这是一件非常困难的事情——尤其是在匆忙中——在区块链的行业中，需要将技术和创业经验结合在一起，这样的人才非常短缺。

The quantities of funds being raised helps to hide the problem from the masses. Tezos may have raised $350M in ICO funding after the rise in crypto prices but in their last update they have only just made their very first hire — a business development executive in San Francisco (when Tezos ran their ICO, their team page displayed software developers working at an OCaml company in France that had agreed to do some contractual work for them rather than their own full time employees). There are many questions yet to be answered: Is their initial technical work weighty enough to build a superstar core around? And, if it is — or alternatively they can somehow attract and enthuse talent using monumental salaries— will they be able to build out the team layer-by-layer and create the kind of culture they need to win the technology race?

筹集的巨额资金把问题隐藏了起来。Tezos的ICO筹资350百万美元，加密货币上涨后的价格。但在最近更新中，他们才刚刚招聘了一个在旧金山的业务拓展总经理(当Tezos启动他们的ICO时,相关文件显示，在一个法国OCaml公司工作的开发人员已经同意做一些合同性质的工作,而不是自己的全职员工完成)。还有很多问题有待求证:他们最初的技术是否足以打造一个超级明星核心团队？而且，如果是，——或者他们可以用巨额薪酬吸引技术天才——他们是否能够建立一个洋葱式的明星团队，以创造出他们需要赢得竞争的那种技术文化?

Only time will tell whether they can, but it is certainly true that their path does not reflect the much more organic way incredible technical organizations such as Google have arisen and developed their systems in the past. While I genuinely wish the Tezos and EOS teams the very best of luck, I think they will have their work cut out making their ICO funds work for them whether they pursue Google or decentralized team models.

只有时间才能证明他们是否能做到，但可以肯定的是，他们的发展路线，并没有建立像过去谷歌那样令人难以置信的技术组织。我真诚地希望Tezos和EOS团队好运，我认为他们将找到办法推动他们的工作，以充分利用让他们的ICO资金，不管他们是追求谷歌式团队还是去中心化的团队。
 
But again, the proof will be in the pudding — and of course I’m biased because I am strongly invested in the modus operandi of DFINITY where we put stellar team and science first, and mostly neglect chasing ICO money and press coverage. Our philosophy and claim is that we can win simply by launching a world-changing network in the form of a performant blockchain computer that has unbounded capacity upon which it is very easy to develop new applications and systems. Anyone interested in what we do should start by looking at our team page. If you are suitably impressed, you will also be interested to know we have many more HUGE hires in the pipeline that will rock the tech world. Superstars are now joining us in droves because of our authentic novel science and the team we already have. This is what real momentum looks like and what I think is truly necessary to accelerate the development of blockchain networks.

同样的，证据也会出现在我的作品中——当然，我也有偏见，因为我对DFINITY的运作方式进行了强烈的投资，我们把一流的团队和科学放在第一位，把ICO资金和媒体报道放到第二位。我们的理念和主张是，通过启动一个改变世界的网络，建立一种具有无限容量的高性能区块链平台，并且在这种平台上非常容易开发新的应用程序和系统。任何对我们的工作感兴趣的人都可以从查看我们的团队页面。如果你对此印象深刻的话，你也会有兴趣知道，我们还有更多的大咖，将震动技术世界。现在，超级明星们纷纷加入我们的行列，因为我们已经拥有梦幻般地技术和团队。这才是真正的动力所在，我认为这将真正加速区块链技术的发展。

For me personally my experience switching to the Google search engine back in the early 2000’s was defining. I remember being an “AltaVista head” until somebody told me to try out Google and I duly typed in http://google.com. I did a search and immediately saw how much better the results were and how much more quickly they were produced. Being an AltaVista head I nonetheless went back to AltaVista feeling faintly offended that my religion had been challenged. However I still became a full-time Google user within 2 days. DFINITY plans to win in a similar way and is obsessed about product/market fit, game changing technology, superstar science and engineering and culture. Given what our team is cooking, I expect the forthcoming release of the DFINITY network will ring major changes in the pace of blockchain advancement.

就我个人而言，我的经验是，在2000年初，我加入到谷歌的搜索引擎。我记得我是一个“AltaVista的头”，直到有人告诉我试试谷歌，然后我就在 http://google.com 上输入了。我做了一个搜索，并立即看到结果有多好，以及他们的输出速度有多快。作为一个AltaVista的领导者，我还是回到了AltaVista，我的领域受到了挑战。然而，我还是在2天内成为了一个全职的谷歌用户。DFINITY计划以类似的方式赢得胜利，并痴迷于产品/市场适应、游戏改变技术、超级明星科学、工程和文化。考虑到我们团队正在做的事情，我预计即将发布的DFINITY网络将会对区块链升级的速度带来重大的改变。


----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

何德林 区块链技术爱好者，热衷于区块链业务创新研究与分析，欢迎加微信号:tongxwl

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

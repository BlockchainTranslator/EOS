# Against on-chain governance | 反对链上治理

### Refuting (and rebuking) Fred Ehrsam’s governance blog | 兼驳Fred有关治理的博客

> 本文翻译自：https://medium.com/@Vlad_Zamfir/against-on-chain-governance-a4ceacd040ca
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [何德林](https://github.com/BlockchainTranslator/EOS)
> 
> 翻译时间：2018-4-19

I’ve been thinking about blockchain governance for a long time, and recently my understanding of the process has become (I think) a lot more clear.

我长期以来一直在思考区块链治理，最近我对这个问题的理解更加清晰了。

I was (and still am) working on a blog post titled “Blockchain Governance 101”, which I hope will share some basic language for reasoning about governance.

我曾经(现在也在)写一个名为“区块链治理 入门”的博客文章，我希望我的博文能分享一些关于治理的基础内容。

Before I managed to finish (the research is ongoing, and it’s not my top priority), Fred Ehrsam published a blog post “Blockchain Governance: Programming Our Future”, framing the discussion as a primarily design problem.

在我快要完成的时候，Fred Ehrsam发表了一篇博客“区块链治理:设计我们的未来”，把区块链的治理作为一个设计问题来讨论。

I really don’t think blockchain governance (or governance in general) can be understood as a design problem. I think it’s almost always a mistake to imagine that you can design and institute a governance process, especially for an existing blockchain community with existing processes, and especially without adequate knowledge of the existing governance processes.

我真的不认为区块链治理(或更一般意义上的治理)可以理解为设计问题。我认为，设想能设计出一个治理流程，是一个错误的想法，尤其是对于已经有流程的区块链社区。如果对已有的治理流程又缺乏了解那更是难上加难。

This blog post is not an introduction to blockchain governance (that is still in the pipeline) and won’t give an overview of key concepts, issues or questions. Nor will it provide any blockchain governance solutions or suggestions. It is instead refutation of core positions that Fred takes in his blog, along with a warning about the dangers of suggesting that people should try to institute their favorite formalized governance model without clear regard for the existing blockchain governance processes.

这本文不是区块链治理的介绍，也不是出治理的主要概念和关键问题概述。它不会提供任何区块链治理解决方案或建议。本文主要是驳斥Fred在他的博客中所持有的核心观点，并警告其风险。Fred认为人们应该尝试建立他们喜欢的正式治理模型，而不用考虑现有的区块链治理过程。

I think that Fred’s intentions are good, and the views he expressed in his blog post are understandable. But I also I think the blog is missing important concepts and context to the point that I consider it harmful, warranting a long-form response (i.e. a response outside of Tweet storms).

我认为Fred的用意是好的，他在博客中表达的观点也是可以理解的。但我也认为博客忽略了重要的概念和背景，我认为这是有害的。

## Blockchain governance is not a design problem | 区块链治理不是一个设计问题

Fred and I agree that blockchain governance is extremely important. I think it’s the second (rather than first) most important factor that will determine whether blockchains end up being a public good, or a menace to the public. Second only after the shared purpose of the blockchain community (a purpose that legitimate governance presumably is supposed to bear out).

Fred和我都同意区块链的治理问题非常重要。我认为，他是决定一个区块链项目最终是为公众带来利益，还是对公众造成威胁的第二大重要要素。第一大的要素是社区贡共享的目的。

There is no question that governance decisions matter, and big time. And the structure of a blockchain governance process can dramatically effect governance outcomes. However, this does not make blockchain governance a design problem.

毫无疑问，治理决策是至关重要，而且是一个重大的关键时刻。区块链治理流程的结构可以显著地影响治理结果。但是，这并不能使区块链治理成为一个设计问题。

Governance is a process. It involves players who participate in that process to produce decisions that affect the governed resources. These decisions can have a lasting impacts on many stakeholders.

治理是一个过程，它包括该过程各方面的参与者。参与者们的决策对受治理的资源产生影响，也对各方利益相关者产生持久的影响。

The participants coordinate around this process, and they build knowledge about the governance processes, about each other, about their incentives and about their states of knowledge. This knowledge can be tacit or formal, it can be local knowledge or it can be common knowledge. Participants can develop strong norms (e.g. no contentious hard forks).

参与者围绕治理过程进行协调，他们建立关于治理过程、激励机制、状态的知识。这种知识可以是隐性的，也可以是正式的，可以是局部，也可以通用的。参与者可以制定强有力的行为规范(例如，没有争议的硬分叉)。

The information and incentives of participants constrains their participation, and they need to be understood in the context of the underlying culture, as well as their individual contexts. The information and incentives of participants can change over time, but they don’t change instantly, nor do they change independently of each other’s incentives and states of knowledge. The process of changing the way that something is governed is not magic, and in our case it’s also very human.

参与者的信息和激励约束了他们的参与行为，他们需要在当前的文化背景下，以及个人背景下才能被理解。参与者的信息和激励可以随着时间的推移而改变，但他们不会很快改变，也不会彼此独立地改变自己的动机和知识状态。治理方式的改变过程不是魔术般的变化，就我们的研究而言，它是非常人性化的。

So even if it was possible to come up with an ideal solution to “the governance design problem”, it might not be possible for the participants to adopt it. There are pre-existing constraints on participants’ ability to coordinate to adopt any proposed governance solutions. And these constraints can even be entirely in their heads, in the form of local or tacit knowledge, or norms and common knowledge.

因此，即使有可能设计一个理想的解决方案，参与者也可能不会采用它。参与者有能力协调一致地采用某个提议的治理方案，存在着一些预先约束限制。这些约束可能完全存在于他们的头脑中，可以是本地或隐性知识、执行规范或者通用常识等。

So when you make a governance proposal, the participants in the current governance process are going to ask themselves “is this a significant improvement over the process we are using now?”, “Will the other participants in the process think so, too?”, “What will it take to switch from our current process to this one?”, and “Is it worth the disruption to existing processes?”

因此，当您制定治理方案时，当前治理过程的参与者会问:“这是对我们现在正在使用流程的重大改进吗?”“其他参与人也会这么想吗?”，“如何从目前的流程转换到目标治理过程?”，以及“彻底改变现有流程是否值得?”

Even if you somehow come up with an ideal governance design, you haven’t “solved governance” for anyone until it is successfully adopted.

想出了一个理想的治理设计，不算成功解决治理的问题，方案成功被地采用才算。

Fred seems to have missed the fact that information is just as important of a “critical component of governance” as incentives or “mechanisms for coordination” (which is a subset of a broader “critical component” called “governance structure”, from my point of view). Not a huge deal!

Fred似乎忽略了一个事实，即信息与激励、“协调机制”一样，是“治理的关键组成部分”的重要部分。

## Look at the system before you call for revolution | 提出革命性设计之前请先了解系统现状

When you propose an alternative governance process, and especially when you suggest that we need an alternative process, you’re proclaiming “the existing governance processes are not good enough” and you’re begging the question of “are the existing processes legitimate?”. You’re a stone’s throw away from advocating for revolution; a replacement of the existing governance processes.

当你提出一个治理过程的解决方案时，特别是你提出需要一个新的治理流程时，你其实是在说“现有的治理过程还不够好”，你正在质疑“现有流程是否合理?”。你是在抛出砖头，鼓吹革命性变革，要彻底地替换现有的治理流程。

Revolution isn’t easy or risk-free, and forking means that you will leave some of your peers behind. When you are advocating for revolution, you had better be sure that the revolution will succeed, and that the new process will be effective and legitimate

革命并不容易，或者无风险，分叉意味着会让你会落下一些先前的同行者。当你主张革命性变革的时候，你必须确信革命性变革会成功，新的治理过程将是有效并且合理的。

Fred’s blog post showed no almost acknowledgement of the existence of functoning blockchain governance processes in either Bitcoin or Ethereum. He dismissed them out-of-hand with little consideration, perhaps because Fred knows that the reader likely already assumes that Bitcoin governance is broken and that Vitalik controls Ethereum governance.

Fred的博客几乎没有认识到在比特币或以太网络中已有的治理过程。他完全忽略这些，或许是因为Fred知道，读者可能已经认为比特币的治理是失败的，以太坊治理是Vitalik控制的。

He showed very little knowledge about how the Ethereum governence process works. That’s fair enough, because the Ethereum governance process are not very well documented, and it’s hard to understand them without actively participating in them. They evolved over time, and are not an institutionalization of a formal model, and therefore have no inherent reason to be easy to identify or communicate.

他对以太坊治理过程的运行情况知之甚少。这是很公平的，因为以太坊治理过程没有很好地文档化，如果没有积极地参与其中是很难理解它们的。它们随着时间的推移而升级，也并不是一个正式模型的制度化表达，因此不易于理解或交流。

No one has full information about the structure of the processes involved. Partly because documenting reality is hard work, and so is communication and education. Partly because the processes are still evolving. And also partly because people only inevitably learn about the processes that they participate in themselves. Most observers don’t participate, and can’t be expected to understand the process, at least until clear documentation is available.

没有人对以太坊的治理过程有充分的了解。部分原因在于现实操作的文档化是一项艰苦的工作，沟通和教育工作也是如此；部分原因是这些过程仍在发展中；还有一部分原因是，人们往往只了解他们自己参与过的过程。大多数人是不参与治理过程的，不能指望完全了解整个过程，至少在清楚的文档描述出来之前。

To clear up some of the misinformation about Ethereum governance shared in Fred’s blog: Proof-of-stake will not change the Ethereum governance processes at all, and miners *do not* have a significant influence on the governance process today. Moreover, Vitalik does not have nearly the amount of power to influence governance outcomes that Fred (and lots of other people) assume that he does. The structure of the governance processes limit Vitalik’s power, just as it limits everyone’s power.

需要消除的Fred博客中的一些错误信息包括：POS不会改变以太坊的治理过程，今天矿主也不会对以太坊的治理过程有重大影响。此外，Vitalik没有很大的权力，像Fred说认为那样，能直接影响治理结果。以太坊的治理过程限制了Vitalik的权力，就像限制了其他人的权力一样。

Unfortunately for the curious reader, documenting the Ethereum governance process is out of scope for this blog. Stay patient! :)

当然，对于好奇的读者来说，文档化的以太治理过程已经超出了这个博客的范围。请保持耐心!:)

## Against on-chain governance | 反对链上治理

“On-chain governance” refers to the idea that the blockchain nodes automatically upgrade when an on-chain governance process decides on an upgrade and that it’s time to install it. No hard forks required.

“on-chain governance”指的是，当治理过程决定升级时，区块链节点会自动升级，不需要进行硬分叉操作。

Adopting on-chain governance is incredibly risky because it always represents a revolution. It’s not necessarily a revolt against the governance processes that merge code into software repositories (as those could conceivably be encoded on-chain, though this notably isn’t normally what is proposed), but a revolution that overthrows the processes that govern full nodes.

采用链上治理是非常危险的，因为它代表着一场彻底的革命。对于将代码合并到软件存储库中的开发治理过程来说，这并不一定是一种革命(它们可以被链上编码，尽管这是不是建议方式)，但对于目前的节点治理来说则是一场颠覆性的革命。

With off-chain governance (the current norm), a node operator has to consciously decide whether to install a hard fork to have his node be consensus-compatible with the nodes of operators who also decided to install that hard fork.

对于链下治理(即当前的操作方式)，一个节点必须有意识地自主决定是否安装升级，以便与他的节点保持一致。

With off-chain blockchain governance, node operators’ decision processes are absolutely necessary parts of blockchain governance, and therefore node operators are necessary participants in blockchain governance.

对于链下治理，节点的决策过程是区块链治理必不可少的部分，节点也是区块链治理的必要参与者。

On-chain governance makes node operator participation in governance completely unnecessary. It makes it so that a node operator, making no decision, follows the decisions made by the on-chain process. Defaults are incredibly powerful: The more nodes follow the default, the less feasible it is for a concerned node operator to refuse to install a hard fork. (Technically, it’s not actually a hard fork or a soft fork, though the upgrade would have been a hard or soft fork in an off-chain governance model.)

链上治理使得节点完全没有必要参与治理过程。它使得一个节点不参加任何决策，只是决策结果的执行者。默认是非常强大的力量：默认决策结果的节点越多，其他相关节点就越不可能拒绝一个硬分叉。

Why is this a big deal? Well, the protocol doesn’t have an anti-Sybil measure on node operators (or on their users). This means that node operators (and therefore users) will necessarily be robbed of their participation in governance, by any on-chain governance proposal.

这为什么是一个大问题？该协议没有抗Sybil攻击的节点措施。这意味着节点(当然包括用户)被剥夺他们参与治理的权利，任何链上治理方案都是如此。

The role of full nodes in off-chain governance provides an important check to balance against the power of processes that make changes to software. On-chain governance removes that check, and the balance it provides.

在离线治理中，全节点的角色提供了一个重要的检查机会，来制衡软件更新力量。链上治理消除了这种检查机会，以及它所提供的制衡力量。

Unless there are governance processes that get Sybil-resistant input from node operators, on-chain governance therefore has always has the potential to disenfranchise node operators (and users) of the blockchain. If you are a blockchain node operator (or user), or if you care about blockchain node operators (or users), then I hope you will learn to regard on-chain governance proposals with extreme apprehension.

除非治理流程允许节点能够抗Sybil攻击，否则链上治理始终有可能使区块链节点的权力被剥夺。如果您是区块链节点，或者你关心区块链节点，那么我希望你能深刻的理解链上治理的这一弊端。

## Against plutocracy and all of its infinite variants | 反对财阀垄断及其变种

Coin holder interests and user interest are not naturally aligned. Users have to buy coins from coin holders to use the blockchain. Coin holders would prefer if users had to pay more. While users would prefer if they had to pay less.

投币者的利益和用户的利益并不总是不一致的。用户必须从持币者手中买币以使用区块链的服务。持币者，希望币价越高越好。而用户则希望币价越低越好。

It is critical to recognize that “user” and “coin holder” are roles that have distinct incentives corresponding to their roles. Just because you’re both a user and a coin holder, or even if most users today are also coin holders, does not mean that we should design our blockchain protocol or our blockchain governance processes to favour coin holder interests over user interests.

重要的是，要认识到，“用户”和“持币者”根据他们角色的不同，具有不同的激励需求。不能仅仅因为一个用户也是持币者，或者大多数用户也是持币者，我们就在设计区块链协议或区块链治理过程中，只考虑持币者的利益而不考虑用户的利益。

The market between blockchains is absolutely not perfectly competitive. It is highly oligopolistic because blockchains have strong network effects (obviously because they are p2p protocols, and more subtly because different blockchain communities have different cultures). So it’s very risky to assume that coin holders want what’s good for users because the price of coins will go down as a result. That will only happen if the users bear sufficient cost. And that cost might be high, and even if it isn’t, any cost is something I wouldn’t wish on all of the users of the blockchain.

区块链市场竞争不是完全充分的。因为区块链有强大的网络效应(由于它们是p2p协议，而且更可能的原因是不同的区块链社区有不同的文化)，所以也有高度的寡头垄断。因此，假设由持币者决定用户需求是危险的，因为用户需求是币价下降。只有在用户承担了足够的成本，这种假设才会发生。而这个成本可能很高，即使不高，我也不希望是所有用户来承担任何的成本。

If on-chain governance is a big risk to node operators and users, then plutocratic on-chain governance is at least as risky. And any on-chain governance proposal that is driven by coin holder votes has this problem. Yes, even if it’s based on prediction markets (futarchy), and even if the coins are locked up.

链上治理对节点和用户来说是一个很大的风险，财阀垄断的链上治理也更是一种风险的。任何由持币者投票的链上治理提案都有这个问题，即使是基于预测市场(futarchy)，或者锁币机制。

Not only is on-chain coin-based governance inconsistent with user interests, it is also antithetical to the ethos of public blockchains. The blockchain is for the public, to serve the public interest. It isn’t for cryptocurrency whales to get more rich. Cyptocurrency holdings (like wealth in global society) is highly concentrated in the hands of a very small number of people. The blockchain isn’t supposed to be owned by anyone… nevermind by a small group of superrich individuals.

基于持币数量的链上治理不仅与用户利益不一致，而且与区块链的公共目标背道而驰。区块链是为公众利益服务，不是为了让持币大鲸变得更为富有。加密货币(就像全球的社会财富)高度集中在极少数人手中。区块链本不应该属于任何一个人，但却可能由一小群超级富豪控制。

Blockchain governance is too important for us to let a small handful of cryptocurrency whales make arbitrary decisions.

区块链治理对我们来说太重要了，我们不能让一小部分的持币大鲸随意做出决定。

## Caveats | 其他说明

I agree with Fred that the blockchain itself is a tremendously valuable tool for experimenting with governance tools and processes. I am a fan (in theory) of on-chain tools that are in smart contracts but aren’t part of the blockchain protocol. And I think we should experiment with that. I also agree that off-chain tools can be extremely valuable as a way for participants to signal to each other.

我同意Fred的观点，对于治理相关的工具和过程试验，区块链本身是一个非常有价值的。我是一个智能合约链上工具的粉丝。我认为我们应该尝试一下这方面的工作。我也同意，链下工具，作为一种参与者相互之间沟通的方式，也非常有价值。

These kinds of tools can provide a signal to node operators that actually helps them make a decision, as opposed to on-chain processes that make their decision unnecessary. These tools can also help participants in the governance processes that affect changes to software repositories.

这类工具可以帮助节点更好地做出决策，而不是让他们不能参加决策。这些工具，还可以帮助治理过程中能够影响到软件变更的各种参与者。

If we find that we can build useful blockchain governance tools using the blockchain, that’s great! However, overthrowing the processes that govern the software implementations of the blockchain, or the processes that govern full nodes is most probably not well-advised.

如果我们发现，可以使用区块链构建一个好用的区块链治理工具，那是非常好的！然而，完全推翻区块链软件实现的治理过程，或者管理全节点的过程，很可能是极不明智的。

## Last words (Conclusion) | 结论

Blockchain governance is not an abstract design problem. It’s an applied social problem. It’s a problem that is defined in the context of existing governance structure, and in the context of the current information and incentives of today’s participants in today’s governance processes.

区块链治理不是一个抽象的设计问题。这是一个应用型的社会问题。这是一个需要在现有治理结构下考虑的问题，也是需要在当前信息和激励机制下考虑的问题。

We need to look very carefully at the blockchain governance processes that we already have before we declare that they don’t exist, are illegitimate, propose alternatives, fork, or advocate for revolution.

我们需要非常仔细地了解我们已有的区块链治理流程，在我们宣称它们不存在、不合理的时候，以及在提出替代方案、分叉、倡导革命性变革的时候。

It is your right to propose the institutionalization of your favorite formal governance model as a replacement to the existing structure of governance, of course.

当然，您也有权，就你喜欢的治理模型取代现有的治理结构，提出建议。

However, consider that insodoing you may be sabotaging the legitimacy of the existing governance process. The existing process may have evolved over time and may not be well understood or documented. Replacing something you don’t understand with something you do has obvious appeal, but it is reckless. So maybe hold off until recklessness is the only tenable option?

但是，这样做，可能正在破坏现有治理过程的合理性。你可能没有了解到，现有的过程可能已经随着时间的推移而发生了变化，并且可能没有被很好地理解或文档化。用一个重新的设计来代替你尚没有完全了解的东西可能很有吸引力，但它是鲁莽的。所以，也许最好再等，直到我们不得不做出选择的时候？

Please be careful. The effectiveness and legitimacy of our blockchain governance processes are critically important. Don’t needlessly put them at risk! Treat your articulation of governance problems and proposals as a loaded weapon and don’t shoot in the dark.

小心为上。区块链治理过程的有效性和合理性至关重要。除非必要，我们不要把他们置于危险之中!把你的治理问题和建议当作一件准备好的武器来对待，但不能还在黑暗中就开枪。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

何德林 区块链技术爱好者，热衷于区块链业务创新研究与分析，欢迎加微信号:tongxwl

译文版权所有，转载需完整注明以上内容。

----------------------------------------------------

# The Meaning of Decentralization   去中心化的含义

> 本文翻译自：https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [小丹](https://github.com/zhuangjun)
> 
> 翻译时间：2017-10-12

“Decentralization” is one of the words that is used in the cryptoeconomics space the most frequently, and is often even viewed as a blockchain’s entire raison d’être, but it is also one of the words that is perhaps defined the most poorly. Thousands of hours of research, and billions of dollars of hashpower, have been spent for the sole purpose of attempting to achieve decentralization, and to protect and improve it, and when discussions get rivalrous it is extremely common for proponents of one protocol (or protocol extension) to claim that the opposing proposals are “centralized” as the ultimate knockdown argument.

“去中心化”是最常在密码经济学领域中使用的词之一, 而且经常被认为是区块链的存在的全部理由, 但它也是被定义的最糟糕的词之一。人们已经花了数千小时的研究, 以及数十亿美元的算力, 来尝试实现去中心化, 并加以保护和改进。 在争论中, 一个协议 (或扩展协议) 的支持者经常以反对者的提议是 "中心化"的作为最终论据。

But there is often a lot of confusion as to what this word actually means. Consider, for example, the following completely unhelpful, but unfortunately all too common, diagram:

但这个词实际上意味着什么, 经常会有很多混淆。如下图:

![](pics/meaning-of-decentralization-1.png)

Now, consider the two answers on Quora for [“what is the difference between distributed and decentralized”](https://www.quora.com/Whats-the-difference-between-distributed-and-decentralized-in-Bitcoin-land). The first essentially parrots the above diagram, whereas the second makes the entirely different claim that “distributed means not all the processing of the transactions is done in the same place”, whereas “decentralized means that not one single entity has control over all the processing”. Meanwhile, the top answer on the Ethereum stack exchange gives [a very similar diagram](https://ethereum.stackexchange.com/questions/7812/question-on-the-terms-distributed-and-decentralised), but with the words “decentralized” and “distributed” switched places! Clearly, a clarification is in order.

现在, 来看一下 Quora 上关于[“分布式和去中心化的区别是什么”](https://www.quora.com/Whats-the-difference-between-distributed-and-decentralized-in-Bitcoin-land) 的两个答案。第一个答案重用了以上的图表, 而第二个给出了完全不同的说法, "分布式指不是所有的处理交易在同一个地方完成", 而 "去中心化是指没有任何单一节点可以控制所有处理 "。同时, Ethereum stack exchange 的最高答案给出来[一个非常类似的图](https://ethereum.stackexchange.com/questions/7812/question-on-the-terms-distributed-and-decentralised), 但是 "去中心化" 和 "分布式" 两个词的解释对换了! 显然, 有必要对他们澄清一下。

### Three types of Decentralization

### 去中心化的三种形式

When people talk about software decentralization, there are actually three separate axes of centralization/decentralization that they may be talking about. While in some cases it is difficult to see how you can have one without the other, in general they are quite independent of each other. The axes are as follows:

当人们谈论软件去中心化时, 实际上他们可能在谈论三种独立的中心化/去中心化的维度。虽然在某些情况下, 你很难看到他们其中一个单独使用, 总的来说, 他们还是相当独立的。

* **Architectural (de)centralization** — how many physical computers is a system made up of? How many of those computers can it tolerate breaking down at any single time?

* **架构 (去) 中心化** - 系统有多少台物理计算机组成？能容忍多少台计算机随时发生故障？

* **Political (de)centralization** — how many individuals or organizations ultimately control the computers that the system is made up of?

* **政治（去）中心化** - 有多少个人或者组织控制了系统服务器

* **Logical (de)centralization** — does the interface and data structures that the system presents and maintains look more like a single monolithic object, or an amorphous swarm? One simple heuristic is: if you cut the system in half, including both providers and users, will both halves continue to fully operate as independent units?

* **逻辑（去）中心化** - 系统接口和数据结构更像是单体模块, 还是非晶群？一个简单的判断方法是: 如果你把系统（服务器和用户）切成两半, 两个部分是否能继续作为独立单元运作？

We can try to put these three dimensions into a chart:
我们把以上三个维度画成图：

![](pics/meaning-of-decentralization-2.png)

Note that a lot of these placements are very rough and highly debatable. But let’s try going through any of them:
示意图很粗糙也很有争议。但我们分别来看一下：

* Traditional corporations are politically centralized (one CEO), architecturally centralized (one head office) and logically centralized (can’t really split them in half)

* 传统的公司是政治中心化 (一个 CEO), 架构中心化 (一个总部) 和逻辑中心化的 (不能分成一半)

* Civil law relies on a centralized law-making body, whereas common law is built up of precedent made by many individual judges. Civil law still has some architectural decentralization as there are many courts that nevertheless have large discretion, but common law have more of it. Both are logically centralized (“the law is the law”).

* 民法依赖于一个中心化的立法机构, 而普通法是在许多个人法官的判案先例所建立的。民法任然有一部分是架构去中心化的, 因为许多法院有很大的酌处权, 而普通法有更多的酌处权。两者都是逻辑中心化的 ("法律即法律")。

* Languages are logically decentralized; the English spoken between Alice and Bob and the English spoken between Charlie and David do not need to agree at all. There is no centralized infrastructure required for a language to exist, and the rules of English grammar are not created or controlled by any one single person (whereas Esperanto was originally invented by Ludwig Zamenhof, though now it functions more like a living language that evolves incrementally with no authority)

* 语言是逻辑去中心化的; 两个人的英语沟通和另两个人的英语沟通完全可以独立进行。语言不需要中心化结构的存在, 并且英语语法也不是由个人创建或控制的。

* BitTorrent is logically decentralized similarly to how English is. Content delivery networks are similar, but are controlled by one single company.
* 
* BitTorrent 也是逻辑去中心化的， 和英语类似。 CDN也类似， 但是是由一个公司控制的。

* Blockchains are politically decentralized (no one controls them) and architecturally decentralized (no infrastructural central point of failure) but they are logically centralized (there is one commonly agreed state and the system behaves like a single computer)

* 区块链是政治去中心化的（没人控制它们）和架构去中心化的（没有单点失败）， 但是是逻辑中心化的（有共识机制并且系统看起来就像只有一台电脑）

Many times when people talk about the virtues of a blockchain, they describe the convenience benefits of having “one central database”; that centralization is logical centralization, and it’s a kind of centralization that is arguably in many cases good (though Juan Benet from IPFS would also push for logical decentralization wherever possible, because logically decentralized systems tend to be good at surviving network partitions, work well in regions of the world that have poor connectivity, etc; see also [this article from Scuttlebot](http://scuttlebot.io/more/articles/design-challenge-avoid-centralization-and-singletons.html) explicitly advocating logical decentralization).

许多时候人们谈论区块链的优点时, 他们会说它拥有 "一个中心化的数据库"。 这个中心化是指逻辑中心化, 在许多情况下它是好的 (尽管IPFS 的 Juan Benet 也会尽可能地推动逻辑去中心化, 因为逻辑去中心化的系统往往在子网络生存的更好, 在网络环境较差的地区也能工作良好; 请参考[Scuttlebot 的这篇文章](http://scuttlebot.io/more/articles/design-challenge-avoid-centralization-and-singletons.html)。

Architectural centralization often leads to political centralization, though not necessarily — in a formal democracy, politicians meet and hold votes in some physical governance chamber, but the maintainers of this chamber do not end up deriving any substantial amount of power over decision-making as a result. In computerized systems, architectural but not political decentralization might happen if there is an online community which uses a centralized forum for convenience, but where there is a widely agreed social contract that if the owners of the forum act maliciously then everyone will move to a different forum (communities that are formed around rebellion against what they see as censorship in another forum likely have this property in practice).

架构中心化经常导致政治中心化， 虽然这不是必须的 - 传统的民主, 政客在一些有形的政府会议室里开会和投票, 但这个会议室的维护人士最终不会产生任何实质性决定。在计算机化的系统中, 架构去中心化，政治中心化是可能发生的，比如有个在线社团， 他们使用同一个论坛。如果论坛所有者恶意行动，号召大家搬去另一个论坛并得到大家的同意， 那大家就会搬到另一个论坛。

Logical centralization makes architectural decentralization harder, but not impossible — see how decentralized consensus networks have already been proven to work, but are more difficult than maintaining BitTorrent. And logical centralization makes political decentralization harder — in logically centralized systems, it’s harder to resolve contention by simply agreeing to “live and let live”.

逻辑中心化使架构去中心化变得更难， 但并非不可能 - 去中心化的共识网络已经被证实是可以运行的， 但比维护 BitTorrent 要难。并且逻辑中心化使得政治去中心化更难 - 在逻辑中心化的系统中， 通过简单地同意 "自己活着和让别人活着" 来解决争论就更困难了。

Three reasons for Decentralization

去中心化的三个理由

The next question is, why is decentralization useful in the first place? There are generally several arguments raised:
第一个问题是， 去中心化为什么有用？有这么几个论点：

* **Fault tolerance**— decentralized systems are less likely to fail accidentally because they rely on many separate components that are not likely.

* **容错性**— 去中心化的系统不太可能意外的出错， 因为它们依赖的独立模块不容易出错。

* **Attack resistance**— decentralized systems are more expensive to attack and destroy or manipulate because they lack sensitive central points that can be attacked at much lower cost than the economic size of the surrounding system.

* **抗攻击性**— 去中心化的系统攻击，毁坏， 或者篡改的代价更高，因为没法低成本的攻击敏感的中心点。

* **Collusion resistance** — it is much harder for participants in decentralized systems to collude to act in ways that benefit them at the expense of other participants, whereas the leaderships of corporations and governments collude in ways that benefit themselves but harm less well-coordinated citizens, customers, employees and the general public all the time.

* **抗共谋性** — 去中心化系统的参与者很难串通起来, 以牺牲其他参与者的利益为代价来采取行动, 而公司和政府的领导人则经常以利己但不伤害公民或客户的方式来共谋。

All three arguments are important and valid, but all three arguments lead to some interesting and different conclusions once you start thinking about protocol decisions with the three individual perspectives in mind. Let us try to expand out each of these arguments one by one.

这三个论点都是重要且有效的, 但一旦您开始考虑满足这三个不同方面的协议，它们都导致了一些有趣的和不同的结论。让我们试着把这些论点一个个地展开。

--------

Regarding fault tolerance, the core argument is simple. What’s less likely to happen: one single computer failing, or five out of ten computers all failing at the same time? The principle is uncontroversial, and is used in real life in many situations, including jet engines, backup power generators particularly in places like hospitals, military infrastructure, financial portfolio diversification, and yes, computer networks.

关于容错性， 核心论点很简单。 哪种情况更可能会发生： 一台电脑出错， 还是十台电脑中的五台同时出错？ 这个原则是无可争议的，而且应用在生活中的方方面面，包括飞机发动机, 备用发电机, 特别是在医院, 军事基础设施, 金融投资组合多样化, 当然， 还有计算机网络。

However, this kind of decentralization, while still effective and highly important, often turns out to be far less of a panacea than a naive mathematical model would sometimes predict. The reason is common mode failure. Sure, four jet engines are less likely to fail than one jet engine, but what if all four engines were made in the same factory, and a fault was introduced in all four by the same rogue employee?

然而, 这种去中心化虽然有效和重要, 但往往远不及一个简单的数学模型所能预见。原因是常见失败模式。当然, 四喷气式发动机比一台喷气发动机更不容易失灵, 但是如果所有的四引擎都是在同一工厂制造的, 而且所有四个都是同一个坏员工引入的, 那该怎么办呢？

Do blockchains as they are today manage to protect against common mode failure? Not necessarily. Consider the following scenarios:

今日的区块链能防止常见的失败模式吗？ 不一定。 考虑以下场景：

* All nodes in a blockchain run the same client software, and this client software turns out to have a bug.

* 区块链中的所有节点都运行同一个客户端软件，而这个客户端软件有一个bug。

* All nodes in a blockchain run the same client software, and the development team of this software turns out to be socially corrupted.

* 区块链中的所有节点都运行同一个客户端软件， 而这个软件的开发团队意图不正。

* The research team that is proposing protocol upgrades turns out to be socially corrupted.

* 研究小组提出的协议升级是邪恶的。

* In a proof of work blockchain, 70% of miners are in the same country, and the government of this country decides to seize all mining farms for national security purposes.

* 在基于POW的区块链中， 70%的旷工来自同一个国家， 而这个国家的政府由于安全原因决定关闭矿池。

* The majority of mining hardware is built by the same company, and this company gets bribed or coerced into implementing a backdoor that allows this hardware to be shut down at will.

* 挖矿的硬件来自于同一个公司，而这个公司在硬件里面加了后门， 可以随时关闭这个硬件。

* In a proof of stake blockchain, 70% of the coins at stake are held at one exchange.

* 在基于POS的区块链中， 70%的代币在同一个交易所。

A holistic view of fault tolerance decentralization would look at all of these aspects, and see how they can be minimized. Some natural conclusions that arise are fairly obvious:

从整体角度来看, 去中心化的容错将着眼于所有这些方面, 并看看如何将它们降到最低。结论相当明显:

* It is crucially important to have multiple competing implementations.

* 有多个相互竞争的实现至关重要。

* The knowledge of the technical considerations behind protocol upgrades must be democratized, so that more people can feel comfortable participating in research discussions and criticizing protocol changes that are clearly bad.

* 对协议升级背后的技术考虑的知识必须是民主化的, 这样更多的人可以愉快的参与研究讨论，批评不好的协议的变化。

* Core developers and researchers should be employed by multiple companies or organizations (or, alternatively, many of them can be volunteers).

* 核心开始或者研究员必须来自多个公司或者组织（或者有些可以是志愿者）。

* Mining algorithms should be designed in a way that minimizes the risk of centralization

* 挖矿算法要避免挖矿中心化

* Ideally we use proof of stake to move away from hardware centralization risk entirely (though we should also be cautious of new risks that pop up due to proof of stake).

* 利润上我们应该使用POS来避免硬件中心化（虽然我们也应该谨慎POS带来的贡献）。

Note that the fault tolerance requirement in its naive form focuses on architectural decentralization, but once you start thinking about fault tolerance of the community that governs the protocol’s ongoing development, then political decentralization is important too.

注意容错性的需求只是简单的要求架构去中心化， 但你一旦开始控制该协议的社区的容错性， 那政治的去中心化也是很重要的。

--------

Now, let’s look at attack resistance. In some pure economic models, you sometimes get the result that decentralization does not even matter. If you create a protocol where the validators are guaranteed to lose $50 million if a 51% attack (ie. finality reversion) happens, then it doesn’t really matter if the validators are controlled by one company or 100 companies — $50 million economic security margin is $50 million economic security margin. In fact, there are deep game-theoretic reasons why centralization may even maximize this notion of economic security (the transaction selection model of existing blockchains reflects this insight, as transaction inclusion into blocks through miners/block proposers is actually a very rapidly rotating dictatorship).

现在, 让我们来看看抗攻击性。在一些纯粹的经济模式中, 你有时会得到去中心化不重要的结果。如果您创建了一个协议, 当51% 攻击发生时, 就会损失5000万美元, 那么, 这个程序是由一家公司或100家公司控制的就无关紧要了。 事实上, 有深层次的博弈论的原因, 为什么中心化甚至可以最大化这种经济安全的概念 (现有区块链的交易选择模型反映了这种洞察力, 因为通过矿工/区块的交易实际上是一个快速轮流的专政)。

However, once you adopt a richer economic model, and particularly one that admits the possibility of coercion (or much milder things like targeted DoS attacks against nodes), decentralization becomes more important. If you threaten one person with death, suddenly $50 million will not matter to them as much anymore. But if the $50 million is spread between ten people, then you have to threaten ten times as many people, and do it all at the same time. In general, the modern world is in many cases characterized by an attack/defense asymmetry in favor of the attacker — a building that costs $10 million to build may cost less than $100,000 to destroy, but the attacker’s leverage is often sublinear: if a building that costs $10 million to build costs $100,000 to destroy, a building that costs $1 million to build may realistically cost perhaps $30,000 to destroy. Smaller gives better ratios.

然而, 一旦你采取了更丰富的经济模式, 特别是承认可能的胁迫 (或更温和的事情, 如针对节点的 DoS 攻击), 去中心化变得更加重要。如果威胁到一个人的生命, 5000万美元将不再对他们有多大的关系。但是如果5000万美元在十人之间传播, 那么你就必须同时威胁到十倍的人。总的来说, 在许多情况下, 现代世界的特点是攻击/防御的不对称性， 更倾向于攻击者。一栋耗资1000万美元的建筑可能耗资不到10万美元就能摧毁。 但攻击者的杠杆往往是亚线性的: 如果一栋1000万美元的大楼需要耗资10万美元来摧毁, 那么耗资100万美元建造的大楼可能实际需要花费3万美元来摧毁。规模越小， 比率越高。

What does this reasoning lead to? First of all, it pushes strongly in favor of proof of stake over proof of work, as computer hardware is easy to detect, regulate, or attack, whereas coins can be much more easily hidden (proof of stake also has strong attack resistance for other reasons). Second, it is a point in favor of having widely distributed development teams, including geographic distribution. Third, it implies that both the economic model and the fault-tolerance model need to be looked at when designing consensus protocols.

这个推理会导致什么？首先, 它有力的说明了POS比POW更好, 因为计算机硬件是更容易被检测, 调节, 或攻击, 而代币可以更容易隐藏 (POS还有其他原因说明它是抗攻击的)。其次, 是拥有一个来自不同地域的分布式的开发团队。第三, 它意味着在设计协商一致协议时, 需要研究经济模型和容错模型。

--------

Finally, we can get to perhaps the most intricate argument of the three, collusion resistance. Collusion is difficult to define; perhaps the only truly valid way to put it is to simply say that collusion is “coordination that we don’t like”. There are many situations in real life where even though having perfect coordination between everyone would be ideal, one sub-group being able to coordinate while the others cannot is dangerous.

最后, 我们来看一下三个论点中最复杂的, 抗共谋性。共谋很难定义，也许一个简单有效的说法是, 共谋是 "我们不喜欢的协调"。在现实生活中有很多情况, 即使每个人之间有完美的协调是理想的, 一个小组能够协调, 而其他小组不能协调也是危险的。

One simple example is antitrust law — deliberate regulatory barriers that get placed in order to make it more difficult for participants on one side of the marketplace to come together and act like a monopolist and get outsided profits at the expense of both the other side of the marketplace and general social welfare. Another example is rules against active coordination between candidates and super-PACs in the United States, though those have proven difficult to enforce in practice. A much smaller example is a rule in some chess tournaments preventing two players from playing many games against each other to try to raise one player’s score. No matter where you look, attempts to prevent undesired coordination in sophisticated institutions are everywhere.

一个简单的例子就是反垄断法--故意设置的监管壁垒, 为了使市场上的参与者更难勾结起来, 像垄断者一样行事, 并以牺牲其他人的利益为代价获得超额的利润。另一个例子是反对在美国的候选人和超级 PACs 之间的积极协调的规则, 尽管那些已经证明在实践中很难实施。一个更小的例子是一些国际象棋锦标赛中的一个规则, 防止两个玩家互相打很多比赛来提高得分。无论你看哪个领域, 你会发现防止共同作弊的机制无处不在。

In the case of blockchain protocols, the mathematical and economic reasoning behind the safety of the consensus often relies crucially on the uncoordinated choice model, or the assumption that the game consists of many small actors that make decisions independently. If any one actor gets more than 1/3 of the mining power in a proof of work system, they can gain outsized profits by selfish-mining. However, can we really say that the uncoordinated choice model is realistic when 90% of the Bitcoin network’s mining power is well-coordinated enough to show up together at the same conference?

在区块链协议方面, 共识安全背后的数学和经济推理往往依赖于不协调的选择模型, 或者假设这个游戏由许多小参与者组成, 它们各自做出独立的决定.如果任何一个参与者在POW中获得超过1/3 的采矿权, 他们可以通过自私的采矿获得超额利润。然而, 我们真的可以说, 当90% 的比特币网络的旷工同时出现在一个会议上, 他们的选择是一致的吗？

![](pics/meaning-of-decentralization-3.png)

Blockchain advocates also make the point that blockchains are more secure to build on because they can’t just change their rules arbitrarily on a whim whenever they want to, but this case would be difficult to defend if the developers of the software and protocol were all working for one company, were part of one family and sat in one room. The whole point is that these systems should not act like self-interested unitary monopolies. Hence, you can certainly make a case that blockchains would be more secure if they were more discoordinated.

区块链的拥护者还指出, 区块链软件更安全, 因为它们不能被随意改变， 除非软件和协议的开发者来自同一家公司, 一个家庭, 或坐在同一个房间。总体而言， 系统不应该被垄断。因此你可以肯定, 如果区块链不被协同控制， 它们将更安全。

However, this presents a fundamental paradox. Many communities, including Ethereum’s, are often praised for having a strong community spirit and being able to coordinate quickly on implementing, releasing and activating a hard fork to fix denial-of-service issues in the protocol within six days. But how can we foster and improve this good kind of coordination, but at the same time prevent “bad coordination” that consists of miners trying to screw everyone else over by repeatedly coordinating 51% attacks?

然而，这是一个根本的悖论。 许多社区，包括以太坊社区，经常被称赞是为了具有强大的社区精神，并能够在六天内迅速协调实施，发布和激活硬分叉来解决协议中的拒绝服务问题。 但是我们如何能够促进和改善这种好协调，同时防止矿工们通过反复协调51％的攻击力量来扭转其他人的“坏协调”？

--------

There are three ways to answer this:

有三种方法来回答这个问题：

* Don’t bother mitigating undesired coordination; instead, try to build protocols that can resist it.

* 不要费心缓和不受欢迎的协调;相反, 尝试构建能够抵御它的协议。

* Try to find a happy medium that allows enough coordination for a protocol to evolve and move forward, but not enough to enable attacks.

* 试着找到一个好的媒介, 让一个协议有足够的协调来进化和向前迈进, 但不足以被攻击。

* Try to make a distinction between beneficial coordination and harmful coordination, and make the former easier and the latter harder.

* 试着区分有益的协调和有害的协调, 使前者更容易, 后者更难。

The first approach makes up a large part of the Casper design philosophy. However, it by itself is insufficient, as relying on economics alone fails to deal with the other two categories of concerns about decentralization. The second is difficult to engineer explicitly, especially for the long term, but it does often happen accidentally. For example, the fact that bitcoin’s core developers generally speak English but miners generally speak Chinese can be viewed as a happy accident, as it creates a kind of “bicameral” governance that makes coordination more difficult, with the side benefit of reducing the risk of common mode failure, as the English and Chinese communities will reason at least somewhat separately due to distance and communication difficulties and are therefore less likely to both make the same mistake.

第一种方法构成了Casper设计哲学的一大部分。然而, 它本身并不充分, 因为依靠经济本身不能处理其他两类关于去中心化的问题。第二个是很难明确的工程，特别是长期的，但它经常发生意外。例如, 比特币的核心开发者通常会说英语, 但矿工一般会说中文, 这是一个幸福的意外, 因为它创造了一种 "两院制" 的治理, 使得协调更加困难, 其好处在于减少共同模式失败的风险, 因为由于距离和沟通的困难, 英语和华人社区至少会有理由分开, 因此不太可能犯同样的错误。

The third is a social challenge more than anything else; solutions in this regard may include:

第三个是社会挑战, 而不是其他任何东西;这方面的解决办法可能包括:

Social interventions that try to increase participants’ loyalty to the community around the blockchain as a whole and substitute or discourage the possibility of the players on one side of a market becoming directly loyal to each other.
社会干预会试图提高参与者对整个区块链社区的忠诚度, 并替代或劝阻市场一方的参与者终于另一方。

Promoting communication between different “sides of the market” in the same context, so as to reduce the possibility that either validators or developers or miners begin to see themselves as a “class” that must coordinate to defend their interests against other classes.

在同一背景下促进不同“市场角色”之间的沟通，以减少验证者，开发者或矿工开始认为自己是“不同角色”的可能性，这种“角色”必须协调捍卫自己与其他角色的利益。

Designing the protocol in such a way as to reduce the incentive for validators/miners to engage in one-to-one “special relationships”, centralized relay networks and other similar super-protocol mechanisms.

设计协议时要考虑减少由于验证者/矿工从事一对一“特殊关系”，集中式中继网络和其他类似超协议机制的产生激励。

Clear norms about what the fundamental properties that the protocol is supposed to have, and what kinds of things should not be done, or at least should be done only under very extreme circumstances.

协议应该明确规定它具有的基本属性以及不应该做什么样的事情，和在极端情况才能做的事情。

This third kind of decentralization, decentralization as undesired-coordination-avoidance, is thus perhaps the most difficult to achieve, and tradeoffs are unavoidable. Perhaps the best solution may be to rely heavily on the one group that is guaranteed to be fairly decentralized: the protocol’s users.

这第三种去中心化， 避免有害协调，也最难达到，权衡是不可避免的。也许最好的解决方案可能是, 依赖一个保证相当分散的群体: 协议的用户。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

小丹 区块链技术爱好者  热衷于区块链底层技术研究 ， 欢迎加微信号 zhuangjun0606

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

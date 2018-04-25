> 本文翻译自：https://vitalik.ca/general/2018/03/28/plutocracy.html
>
> 译者：[区块链中文字幕组 鱼](https://github.com/oscnet)
>
> 翻译时间：2018-4-15

5 http://www.huoxing24.com/newsdetail?id=2018033111584602075

# Governance, Part 2: Plutocracy Is Still Bad

＃治理 第二部分：金权政治的弊端

Coin holder voting, both for governance of technical features, and for more extensive use cases like deciding who runs validator nodes and who receives money from development bounty funds, is unfortunately continuing to be popular, and so it seems worthwhile for me to write another post explaining why I (and [Vlad Zamfir][1] and others) do not consider it wise for Ethereum (or really, any base-layer blockchain) to start adopting these kinds of mechanisms in a tightly coupled form in any significant way.

不管是用于技术参数的治理调整，还是用在如决定谁来运行验证节点，或是决定谁能得到开发资金等更为广泛的事务上，特币者投票不幸正在变得越来越流行。这使得我认为有必要再写一篇文章来说明，为什么我(和[Vlad Zamfir][1]或其它人)认为在以太坊（或者在任何其它基础链）上采用这种投票机制是不明智的。

I wrote about the issues with tightly coupled voting [in a blog post][2] last year, that focused on theoretical issues as well as focusing on some practical issues experienced by voting systems over the previous two years. Now, the latest scandal in DPOS land seems to be substantially worse. Because the delegate rewards in EOS are now so high (5% annual inflation, about $400m per year), the competition on who gets to run nodes has essentially become yet another frontier of US-China geopolitical economic warfare.

我在去年写了篇[关于关联投票的文章][2]，重点讨论了理论层面的问题，并关注了投票系统在过去两年中遇到的一些实际问题。现在，DPOS 界的最新丑闻显示这个问题似乎变得更为严重了。由于 EOS 的节点奖励现在如此之高（年通货膨胀率为 5％，大约每年为 4 亿美元），因此谁来运营节点的竞争基本上已成为美中地缘政治经济战争的另一个前沿领域。

![][3]

And that's not my own interpretation; I quote from [this article (original in Chinese)][4]:

这不是我自己的观点；让我引用中文[原文][4]：

> **EOS supernode voting: multibillion-dollar profits leading to crypto community inter-country warfare**

> ** EOS超级节点投票：「千亿」利润下的币圈国家战争**

> Looking at community recognition, Chinese nodes feel much less represented in the community than US and Korea. Since the EOS.IO official Twitter account was founded, there has never been any interaction with the mainland Chinese EOS community. For a listing of the EOS officially promoted events and interactions with communities see the picture below.

> 从社区认可度这方面来看，中国节点在 EOS 社区的存在感远远不及美国和韩国。自从 http://EOS.IO 的官方 Twitter 上线以来，从来没有跟中国大陆的 EOS 社区进行过互动，与 http://EOS.IO 官推进行过活动和互动的社区见下图。

![][5]

> With no support from the developer community, facing competition from Korea, the Chinese EOS supernodes have invented a new strategy: buying votes.

> 在不被开发者社区支持，又面对韩国竞争之后，中国的 EOS 超级节点竞选者发明了一个新的策略：贿选。

The article then continues to describe further strategies, like forming "alliances" that all vote (or buy votes) for each other.

然后文章继续描述进一步的策略，比如形成相互投票（或买票）的“同盟”。

Of course, it does not matter at all who the specific actors are that are buying votes or forming cartels; this time it's some Chinese pools, [last time][6] it was "members located in the USA, Russia, India, Germany, Canada, Italy, Portugal and many other countries from around the globe", next time it could be totally anonymous, or run out of a smartphone snuck into Trendon Shavers's prison cell. What matters is that blockchains and cryptocurrency, originally founded in a vision of using technology to escape from the failures of human politics, have essentially all but replicated it. Crypto is a reflection of the world at large.

当然，具体的是谁在购买选票或组建同盟并不重要；这次是中国，[上一次][6]是“位于美国，俄罗斯，印度，德国，加拿大，意大利，葡萄牙和来自世界各地的许多其他国家的成员”，下一次可能就是一个完全的匿名或使用安全手机隐藏身份的某人。重要的是区块链和加密货币，最初是建立在利用技术来克服人类政治体制中的缺陷的愿景上的，现在如同现实世界一样，区块链就是整个世界的一个缩影。

The EOS New York community's response seems to be that they have issued a strongly worded letter to the world stating that [buying votes will be against the constitution][7]. Hmm, what other major political entity has [made accepting bribes a violation of the constitution][8]? And how has that been going for them lately?

EOS 纽约社区对此进行了回应，他们向外界发出了措辞强硬的信，声称[购买选票违反宪法][7]。嗯，还有哪个主要政机构[接受贿赂违反了宪法的说法][8]？最近他们怎么样？

The second part of this article will involve me, an armchair economist, hopefully convincing you, the reader, that yes, bribery is, in fact, bad. There are actually people who dispute this claim; the usual argument has something to do with market efficiency, as in "isn't this good, because it means that the nodes that win will be the nodes that can be the cheapest, taking the least money for themselves and their expenses and giving the rest back to the community?" The answer is, kinda yes, but in a way that's centralizing and vulnerable to rent-seeking cartels and explicitly contradicts many of the explicit promises made by most DPOS proponents along the way.

本文的第二部分将涉及到我，一个“躺椅上的经济学家”([Armchair Economist](https://book.douban.com/subject/1471496/))，希望能说说服读者：贿选实际上是很不好的事情。当然有人不同意这种说法。通常的观点与市场效率有关，“这不是很好吗？因为这意味着获胜的节点将成为最便宜的节点，可以最小化他们自己的开支，还能回馈社区？“答案确实是这样，但是这将引起中心化问题，并涉及联合寻租交易，这明显违背了大多数 DPOS 支持者在此过程中所做的许多明确承诺。

Let us create a toy economic model as follows. There are a number of people all of which are running to be delegates. The delegate slot gives a reward of $100 per period, and candidates promise to share some portion of that as a bribe, equally split among all of their voters. The actual N delegates (eg. N = 35) in any period are the N delegates that received the most votes; that is, during every period a threshold of votes emerges where if you get more votes than that threshold you are a delegate, if you get less you are not, and the threshold is set so that N delegates are above the threshold.

我们来假设一个经济模型。有许多人在竞选代表。当选人在选期内能得到 100 美元奖励，有候选人承诺将奖励的一部分平分给选民。当选的 N 个代表（例设 N = 35）就是获得最多选票的代表；也就是说，在每个阶段都会出现一个投票的门槛，如果您获得的投票数超过该门槛，您就成为代表，如果投票数减少了，那么您就不会当选，那么就会出现一个让 N 个代表当选的阈值。

We expect that voters vote for the candidate that gives them the highest expected bribe. Suppose that all candidates start off by sharing 1%; that is, equally splitting $1 among all of their voters. Then, if some candidate becomes a delegate with K voters, each voter gets a payment of 1/K. The candidate that it's most profitable to vote for is a candidate that's expected to be in the top N, but is expected to earn the fewest votes within that set. Thus, we expect votes to be fairly evenly split among 35 delegates.

我们预计选民将投票给那些给予他们最多贿赂的候选人。假设所有候选人拿出以 1％ 的奖励平分给选民；即在所有选民中平均分配 1 美元。然后，如果有 K 个投票人投票使得某候选人当选，每个选民就可以得到 1/K 的回报。所以最有利的投票策略是投给预计排名前 N 的候选中获得最少的选票的那个候选人。在这种情况下，我们预计投票将在 35 名代表中平均分配。

Now, some candidates will want to secure their position by sharing more; by sharing 2%, you are likely to get twice as many votes as those that share 1%, as that's the equilibrium point where voting for you has the same payout as voting for anyone else. The extra guarantee of being elected that this gives is definitely worth losing an additional 1% of your revenue when you do get elected. We can expect delegates to bid up their bribes and eventually share something close to 100% of their revenue. So the outcome seems to be that the delegate payouts are largely simply returned to voters, making the delegate payout mechanism close to meaningless.

现在，一些候选人将希望通过让出更多利益来保证自己当选；拿出收益的 2％，就有可能会获得两倍于只拿出 1％ 的候选人的投票数，因为这是一个投给你跟投给其它人收益一致处的平衡点。虽然损失了 1％ 的收入，但得到了当选的额外保证。所以最后候选人会选择使用他们 100% 的收入来回报给投票人。最后的结果就是当选人的收益会绝大部分归还给选民，使得当选者的奖励机制变得毫无意义。

But it gets worse. At this point, there's an incentive for delegates to form alliances (aka political parties, aka cartels) to coordinate their share percentages; this reduces losses to the cartel from chaotic competition that accidentally leads to some delegates not getting enough votes. Once a cartel is in place, it can start bringing its share percentages down, as dislodging it is a hard coordination problem: if a cartel offers 80%, then a new entrant offers 90%, then to a voter, seeking a share of that extra 10% is not worth the risk of either (i) voting for someone who gets insufficient votes and does not pay rewards, or (ii) voting for someone who gets too many votes and so pays out a reward that's excessively diluted.

但情况可能变得更为糟糕。从这一点上看，这将促使代表们组成同盟（即政党，又名卡特尔）来协调这个百分比份额；以减少无序竞争对同盟造成的损失，无意中这种竞争会导致一些代表得不到足够的选票。一旦同盟成立，就可以开始减少其分配的份额，引出一个很难协调的问题：如果一个同盟拿出 80％ 的收益，而一个新候选人拿出 90％ 收益，对于投票人来说，就有一个为了这多出的 10％ 收益，风险和收益的选择问题（i）投给得不到足够选票的候选人，从而得不到作保回报，或者（ii）投票给有太多人投票的候选人，但（因为分成的人很多）只得到很少的收益。

![][9]

*Sidenote: [Bitshares DPOS][10] used approval voting, where you can vote for as many candidates as you want; it should be pretty obvious that with even slight bribery, the equilibrium there is that everyone just votes for everyone.*

*旁注：[Bitshares DPOS][10] 使用同意投票，您可以根据需要投票给尽可能多的候选人；很明显的，即使存在轻微的贿赂，这里有一个均衡即每个人为所有人投票（我为人人，人人为我）。*

Furthermore, even if cartel mechanics _don't_ come into play, there is a further issue. This equilibrium of coin holders voting for whoever gives them the most bribes, or a cartel that has become an entrenched rent seeker, contradicts explicit promises made by DPOS proponents.

此外，即使同盟机制不起作用，还存在着另一个问题。特币者投票给贿赂他们最多的候选人或牢固的寻租者同盟。这与 DPOS 支持者的明确承诺相违背。

Quoting "[Explain Delegated Proof of Stake Like I'm 5][11]":

引用 “[如何向 5 岁的孩子解释权益证明][11]”：

>If a Witness starts acting like an asshole, or stops doing a quality job securing the network, people in the community can remove their votes, essentially firing the bad actor. Voting is always ongoing.

>如果节点变成混蛋，不再高效地为网络安全而工作，社区可以撤消对他们的投票，本质上就是把这个混蛋给解雇了。而且投票是时刻进行的，永不停息。

From "[EOS: An Introduction][12]":

摘自 “[ EOS 简介][12]”：

>By custom, we suggest that the bulk of the value be returned to the community for the common good - software improvements, dispute resolution, and the like can be entertained. In the spirit of "eating our own dogfood," the design envisages that the community votes on a set of open entry contracts that act like "foundations" for the benefit of the community. Known as Community Benefit Contracts, the mechanism highlights the importance of DPOS as enabling direct on-chain governance by the community (below).

>按照惯例，我们建议将大部分价值回馈给社区以实现共同利益 - 如软件改进，争议解决等等是受欢迎的。本着“吃我们自己的狗食”的精神，该设计设想，社群的投票基于“社群利益协议”进行，这个机制强调了 DPOS 作为社区链上治理的重要性。

The flaw in all of this, of course, is that the average voter has only a very small chance of impacting which delegates get selected, and so they only have a very small incentive to vote based on any of these high-minded and lofty goals; rather, their incentive is to vote for whoever offers the highest and most reliable bribe. Attacking is easy. If a cartel equilibrium does not form, then an attacker can simply offer a share percentage slightly higher than 100% (perhaps using fee sharing or some kind of "starter promotion" as justification), capture the majority of delegate positions, and then start an attack. If they get removed from the delegate position via a hard fork, they can simply restart the attack again with a different identity.


当然，这一切的缺陷是，普通选民对哪些代表被选中的影响很小，所以非常小的激励他们就会对基于高尚而崇高的目标进行投票。谁能给他最高且最可靠的贿赂，他就会投给谁。这样就很容易攻击。如果同盟没有形成一致，那么攻击者可以简单地提供略高于 100％ 的百分比份额（可能用分享收益或某种“起动促销”作为理由），来取得大部分的代表位置，然后启动一个攻击。如果通过硬分叉将他们从代表位置被移除，他们还可以简单地以不同的身份再次重新启动攻击。

---

The above is not intended purely as a criticism of DPOS consensus or its use in any specific blockchain. Rather, the critique reaches much further. There has been a large number of projects recently that extol the virtues of extensive on-chain governance, where on-chain coin holder voting can be used not just to vote on protocol features, but also to control a bounty fund. Quoting a [blog post from last year][13]:

以上内容并非纯粹是对 DPOS 共识机制或其在其它任何特定区块链中的使用的批评。与此相反。最近对这种链上治理的方式的优点得到了很多的赞颂。链上持有人的投票不仅可以用于决定协议特征，还可以来控制奖金基金，下面引用[去年的博客文章][13]：

>Anyone can submit a change to the governance structure in the form of a code update. An on-chain vote occurs, and if passed, the update makes its way on to a test network. After a period of time on the test network, a confirmation vote occurs, at which point the change goes live on the main network. They call this concept a "self-amending ledger".

>任何人都可以以代码更新的形式向治理结构提交更改。进行连续投票，如果通过，更新将进入测试网络。在测试网络上经过一段时间之后，会发生确认投票，此时该更改将在主网络上进行。他们称这个概念为“能自我修正的账本”。

Such a system is interesting because it shifts power towards users and away from the more centralized group of developers and miners. On the developer side, anyone can submit a change, and most importantly, everyone has an economic incentive to do it. Contributions are rewarded by the community with newly minted tokens through inflation funding. This shifts from the current Bitcoin and Ethereum dynamics where a new developer has little incentive to evolve the protocol, thus power tends to concentrate amongst the existing developers, to one where everyone has equal earning power.

这样的系统很有趣，因为它将更中心化的开发人员和挖矿者的权力转移给用户。开发人员这一边，任何人都可以提交更改，最重要的是，每个人都有经济激励去做这件事。贡献人可以通过通货膨胀从新挖的代币中从社区取得报酬。与现在的比特币以及以太坊，新的开发者没有什么动力去发展协议，权力往往集中在现有的老开发者中不同，每个人都有相同的收益权力。

In practice, of course, what this can easily lead to is funds that offer kickbacks to users who vote for them, leading to the exact scenario that we saw above with DPOS delegates. In the best case, the funds will simply be returned to voters, giving coin holders an interest rate that cancels out the inflation, and in the worst case, some portion of the inflation will get captured as economic rent by a cartel.

当然，实际上，这很容易导致向为其投票的用户提供回扣，从而发生前面我们看到的 DPOS 投票现象。在最好的情况下，资金将被简单地归还给选民，从给代币持有人一个抵消通货膨胀的利率，在最坏的情况下，通货膨胀的一部分将被垄断者独吞。

Note also that the above is not a criticism of _all_ on-chain voting; it does not rule out systems like futarchy. However, futarchy is untested, but coin voting _is_ tested, and so far it seems to lead to a high risk of economic or political failure of some kind - far too high a risk for a platform that seeks to be an economic base layer for development of decentralized applications and institutions.

还要注意的是，上述并不是对所有链上投票的批评；它不排除像 futarchy (译者注：可以查看[这里](https://ethfans.org/posts/introduction-futarchy-one)了解)这样的系统。然而，futarchy 系统还没经过测试，但持币投票方式已经过测试，现在似乎导致某种形式的经济或政治失败的高度风险 - 对于试图成为发展去中心化应用和机构的经济基础平台来说，风险太大了。

---

So what's the alternative? The answer is what we've been saying all along: _cryptoeconomics_. [Cryptoeconomics][14] is fundamentally about the use of economic incentives together with cryptography to design and secure different kinds of systems and applications, including consensus protocols. The goal is simple: to be able to measure the security of a system (that is, the cost of breaking the system or causing it to violate certain guarantees) in dollars. Traditionally, the security of systems often depends on _social_ trust assumptions: the system works if 2 of 3 of Alice, Bob and Charlie are honest, and we trust Alice, Bob and Charlie to be honest because I know Alice and she's a nice girl, Bob registered with FINCEN and has a money transmitter license, and Charlie has run a successful business for three years and wears a suit.

那么还有其它的选择吗？答案就是我们一直在说的：_cryptoeconomics_（加密经济）。 [加密经济][14]基本上就是相关的利用经济激励和密码学来设计和保护不同种类的系统和应用，包括共识协议。目标很简单：能够以美元来衡量系统的安全性（即破坏系统或违约的的成本）。传统上，系统的安全性通常取决于社交信任假设：如果 Alice、Bob 和 Charlie 中有 2/3 是诚实的系统就可以工作，并且我们相信 Alice、Bob 和 Charlie 是诚实的，因为我认识 Alice 知道她是一个好女孩，Bob 在 FINCEN （金融犯罪执法网络）注册并拥有发卡机构的许可，Charlie 已经成功运营一家公司三年，并穿着西装。

Social trust assumptions can work well in many contexts, but they are difficult to universalize; what is trusted in one country or one company or one political tribe may not be trusted in others. They are also difficult to quantify; how much money does it take to manipulate social media to favor some particular delegate in a vote? Social trust assumptions seem secure and controllable, in the sense that "people" are in charge, but in reality they can be manipulated by economic incentives in all sorts of ways.

社交信任假设在许多情况下都能很好地发挥作用，但它们难以普及；在一个国家或一个公司或一个政治部落中信任的东西可能不会被其他人信任。他们也很难量化；在投票中操纵社交媒体以支持某个特定代表需要多少钱？社交信任假设似乎是安全和可控的，从某种意义上说，人民是被管理的，但实际上他们可以通过各种方式受到经济激励的操纵。

Cryptoeconomics is about trying to reduce social trust assumptions by creating systems where we introduce explicit economic incentives for good behavior and economic penalties for ban behavior, and making mathematical proofs of the form "in order for guarantee X to be violated, at least these people need to misbehave in this way, which means the minimum amount of penalties or foregone revenue that the participants suffer is Y". [Casper][15] [is][16] [designed][17] to accomplish precisely this objective in the context of proof of stake consensus. Yes, this does mean that you can't create a "blockchain" by concentrating the consensus validation into 20 uber-powerful "supernodes" and you have to [actually think][18] to make a design that intelligently breaks through and navigates existing tradeoffs and achieves massive scalability in a still-decentralized network. But the reward is that you don't get a network that's constantly liable to breaking in half or becoming economically captured by unpredictable political forces.

加密经济是通过创建系统来减少社交信任假设，我们引入明确的经济激励措施来实现好人得好报，恶人有恶报。并对"为了保证当违反 X ，至少这些人有错误行为，参与者意味着遭受的最小惩罚金额或预知的损失 Y"形式进行数学证明。[Casper][15]就是为了在权益证明的共识背景下完成这个目标而[设计][17]的。是的，这意味着您不能将共识验证集中到 20 个超级强大的“超级节点” 来创建“区块链”，你必须[真实地思考][18]来设计以突破现有设计权衡，在去中心化的网络中实现大规模的可扩展性。但是回报是你会得到一个更为可靠，更受信赖的网络，它不会在经济上被不可预测的政治力量俘虏。

---

1. _It has been brought to my attention that EOS may be reducing its delegate rewards from 5% per year to 1% per year. Needless to say, this doesn't really change the fundamental validity of any of the arguments; the only result of this would be 5x less rent extraction potential at the cost of a 5x reduction to the cost of attacking the system._

1. 引起我的注意的是，EOS 可能将其节点奖励从每年 5％ 降至每年 1％。毋庸置疑，这并不会真正改变任何论点的根本有效性；这样做的唯一结果是将收益潜力减少 5 倍，而将攻击系统的成本降低 5 倍。

2. _Some have asked: but how can it be wrong for DPOS delegates to bribe voters, when it is perfectly legitimate for mining and stake pools to give 99% of their revenues back to their participants? The answer should be clear: in PoW and PoS, it's the protocol's role to determine the rewards that miners and validators get, based on the miners and validators' observed performance, and the fact that miners and validators that are pools pass along the rewards (and penalties!) to their participants gives the participants an incentive to participate in good pools. In DPOS, the reward is constant, and it's the voters' role to vote for pools that have good performance, but with the key flaw that there is no mechanism to actually encourage voters to vote in that way instead of just voting for whoever gives them the most money without taking performance into account. Penalties in DPOS do not exist, and are certainly not passed on to voters, so voters have no "skin in the game" (penalties in Casper pools, on the other hand, **do** get passed on to participants)._

2.有人问道： 为什么节点完全合法地挖矿并将其收入的 99％ 返还给投票者，这种贿赂选民的行为是错误的？答案应该很清楚：在 PoW 和 PoS 中，根据矿工和验证人的性能表现，确定矿工和验证人得到的回报是由协议决定的，对矿工和验证人的奖惩机制会传递给参与者并给予参与者一个不做恶的动机。在 DPOS 中，奖励金额是固定的，投票者的任务是投票给表现好的节点。这里就存在一个关键问题，就是没有机制来鼓励选民以节点的性能表现来投票，而不是投给那些给他们最多钱的人。DPOS 中不存在惩罚，而且这个惩罚不会传递给选民，因此，选民们没有切肤之痛（Casper 有惩罚并且这个惩罚切切实实会传递给参与者）。

[1]: https://medium.com/@Vlad_Zamfir/against-on-chain-governance-a4ceacd040ca
[2]: https://vitalik.ca/general/2017/12/17/voting.html
[3]: https://pic4.zhimg.com/v2-a4b7403626be584f21d47837190e99e0_1200x500.jpg
[4]: https://zhuanlan.zhihu.com/p/34902188
[5]: http://vitalik.ca/files/plutocracy_image1.png
[6]: https://liskgdt.net/
[7]: https://steemit.com/eos/@eosnewyork/block-one-confirms-vote-buying-will-be-against-eos-io-proposed-constitution
[8]: https://en.wikipedia.org/wiki/Emoluments_Clause
[9]: http://vitalik.ca/files/plutocracy_image2.png
[10]: https://bitshares.org/technology/delegated-proof-of-stake-consensus/
[11]: https://hackernoon.com/explain-delegated-proof-of-stake-like-im-5-888b2a74897d
[12]: https://eos.io/documents/EOS_An_Introduction.pdf
[13]: https://medium.com/@FEhrsam/blockchain-governance-programming-our-future-c3bfe30f2d74
[14]: https://www.coindesk.com/making-sense-cryptoeconomics/
[15]: http://arxiv.org/abs/1710.09437
[16]: https://github.com/ethereum/cbc-casper/wiki
[17]: https://medium.com/@jonchoi/ethereum-casper-101-7a851a4f1eb0
[18]: https://medium.com/@icebearhww/ethereum-sharding-workshop-in-taipei-a44c0db8b8d9


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

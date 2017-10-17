The next step for DPOS: Decentralized block producers  DPOS 的下一步: 区块生产者的去中心化
--------------------------------------------------

> 本文翻译自：https://steemit.com/eos/@samupaha/the-next-step-for-dpos-decentralized-block-producers
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)  [荆凯](https://github.com/shuke0327)
> 
> 翻译时间：2017-10-14

---------------------------

One of the most common criticisms against delegated proof of stake systems is the perceived lack of decentralization. 21 block producers (per round) might seem very low number, even though it's still very high compared to proof of work systems which are usually fully controlled by less than ten mining pools.

对委托权益证明系统最常见的批评之一是其缺乏去中心化。区块生产者有21个(每一轮)，这数量似乎很少，虽然与工作量证明系统相比已经算很多了，后者通常被不到十个矿池全权掌控。

When the centralization by mining pool is pointed out, POW proponents will give a counter-argument:  _"It's not really that bad because miners can change their mining pool whenever they want."_  Which is true, of course. If a mining pool does something bad, it can lose a lot of hashing power very quickly because miners just choose another pool.

当人们指出矿池的中心化时，POW 拥护者会反驳称: _"由于矿工可以随时切换矿池，所以这并没有那么糟糕。“_ 这说法当然正确。如果矿池做了坏事，矿工只要选择其它矿池，它会很快失去大量的hash算力。

That made me think... Could we implement something similar in DPOS?

这促使我思考... 我们在 DPOS 中，能否做类似的实现？

This post is mostly from the perspective of EOS, but ideas can be applied to Steem, Bitshares and other DPOS blockchains, too.

这篇帖子主要从 EOS 的角度讨论，但这一思路对 Steem、Bitshares 和其它采用 DPOS 的区块链也同样适用。


## Formalization of block producer's responsibilities 生产者责任的构成

In EOS, block producers will have quite a lot of responsibilities.

在EOS中，区块生产者将会有很多职责。


Technical-技术：

*   Creating blocks-创建区块
*   File hosting-文件托管
*   Back-up servers-备份服务器
*   Seed node-种子节点


Governance-治理：

*   Following the constitution-遵照宪法

*   Account freezing, misbehaving contracts-冻结账户和恶意的合同

*   Take-down notices of file-记录文件通知

*   Hard and soft forks, fees (account creation), parameters (blocksize, rate-limited capacity)
*   软硬分叉，费用 （创建帐户），参数 （块大小，限速容量）


Leadership-领导力：

*   Something like a CEO in a traditional company, keeping everything internal in control（类似传统公司的 CEO，掌控内部所有事物）

*   Communication with other block producers（与其他区块生产者沟通）

*   Campaign to get elected as a BP-竞选 BP (区块生产者)


Possible extra services-可能的额外服务：

*   Account recovery-帐户恢复

*   Account creation-创建帐户

*   Oracles-预言

*   Price feeds-喂价

*   Dispute resolution service-解决冲突的服务


As you can see, running a BP is much more than just a server creating blocks. One person might be able to handle everything in the beginning, but when the ecosystem grows, this will require a team.

如你所见，运行 BP 远远不止用一台服务器创建区块那么简单。刚开始也许一个人能够处理所有事情，但随着生态系统的成长，就需要团队了。


## Decentralization of a block producer 单个区块生产者的去中心化

When we know all the responsibilities of a BP, we can break them down into smaller jobs which can be done by separate individuals or organizations. This will give us several different options.

了解了 BP 的所有职责之后，我们可以将其分成较小的任务，这些任务可以由不同的个人或组织来完成。这为我们提供了不同的选择。

There can be fully centralized BP, for example, an IT company that has professionals who can take care of everything. Or there can be fully decentralized BP, which works like a DAO: BP is just a smart contract which is governed by BP-tokens. Or some combination of those.

可以存在完全中心化的 BP，例如，一家 IT 公司，由专业人士打理所有事物。或者是完全去中心化的 BP，像 DAO (译者注： 去中心化组织)一样运作：BP 只是一个智能的合同，受 BP 代币监管。或者，这两种方式的结合。

Decentralized block producers (DBP) will create some benefits for the ecosystem. Let's look at them more closely.

去中心化的区块生产者 (DBP) 会使生态系统收益。让我们做一下更详细的分析。


### Additional layer of decentralization 去中心化的附加层

While 21 BPs for DPOS is probably more than enough to create a robust system, a little bit more decentralization wouldn't be a bad thing. Adding more BPs per round isn't a good option, it would mean that the BP layer just gets a little bit more decentralized. But adding another layer to the system would create more decentralization without any negative side effects, like slowing the system or making it more expensive to run.

虽然 DPOS 拥有21个BP节点对创建健壮的系统而言也许已经远远足够了，但是多一点去中心化也不坏。每轮增加更多的 BP 并不是个好的选择，这只会让 BP 这一层的去中心化程度提高一点点而已。但是，给系统添加另一层就可以更加去中心化，而不会带来任何不良副作用，如拖慢系统或者增加运行成本等。

The first layer of the blockchain decentralization is the BPs. The second layer should be different tasks of a BP.
Blockchain 去中心化的第一层是 BP。第二层应该是一个 BP 节点的不同任务。

Because DPOS is perceived as not having enough decentralization, this is also good for the marketing. It will be harder to claim that DPOS is too centralized when a BP is not one entity but several entities which can be easily replaced.

因为人们认为 DPOS 去中心化程度不足，（上述方式）对市场营销也会有益。如果一个 BP 并不是一个实体，而是可以被很容易换掉的多个实体，就更难指责 DPOS 太过中心化了。

It will be much harder for BPs to conspire against the ecosystem. And of course, it will make harder to anyone attack against BPs because they are not one entity.

这也会让 BP（译者注： 区块生产者）密谋反对生态系统的难度大大增加。当然，对 BP 的攻击也会更难，因为 BP 并不是单个实体。


### Lower barriers to entry 降低进入门槛

There have been fears that when the system grows, the barrier to entry will become too high. Being a BP might require big investments to server infrastructure to ensure capacity and that will discourage people to become a BP.

有人担心随着系统增长，进入门槛会变得太高。成为 BP 可能需要大量的资金购置服务器基础设施以确保其能力，而这会阻碍人们成为 BP。

Instead of taking care of all responsibilities of a BP, individual or organization can start with just one thing, like file storage. They can identify a DBP whose file storage is lower than others and offer to replace it. After they have earned money and reputation, they can start to take care of other responsibilities, too.

个人或组织可以不必承担 BP 的全部职责，而是只从其中一件事开始做起，比如文件存储。他们可以识别出文件存储能力比别人低的DBP，然后主动提出来替换它。获得了金钱和声誉后，他们也可以开始承担其它的职责。


### Specialization 专业化分工

Usually, the system becomes more efficient when individuals and organizations specialize in certain work. They can focus on the one thing and become really good at that. They don't need to spend resources trying to become great at everything – often that means they are going to be weak at some things.

通常而言，当个人和组织分工明确时，系统的效率会越高。他们可以专注于一件事情，并精于此道。他们不需要耗费资源试图把所有事情都做好 — 这往往意味着他们在一些事情上会变弱。

When people/organizations specialize, they can produce the services at lower cost. In the case of EOS, this is very beneficial because BPs can then offer more capacity for the blockchain.

当人/组织分工明确时，他们能够以更低成本提供服务。在 EOS 之中这会非常有益，因为 BP 可以为 blockchain 提供更强的处理能力。


### Self-healing 自我修复

DBPs can monitor their capacity and uptime and see how well they are doing compared to others. If some part of their DBP organization seems to be weaker than others, they can find a better partner. This is probably more efficient compared to a centralized BP, which has to either make an effort to learn how to do a better job or hire somebody to do it.

DBPs 可以监控他们的处理能力和正常运行时间（uptime），观察与其它节点相比自己的表现如何。如果他们的 DBP 组织中的某些部分似乎比别人差，他们可以寻找更好的合作伙伴。相比中心化的 BP，这样做可能效率更高，后者必须努力学习如何自己做到更好，要么雇人来做。

DBP can just look at possible alternatives (assuming there are markets for them) and replace low-performing partner with a better one. When the process of integrating different BP services is formalized, this should be very easy to do.

DBP 只用考虑可能的备选方案 （假设存在这一供应市场），将表现差的合作者换成表现更好的。当集成不同的 BP 服务的流程正式形成时，可以很容易做到。


### Voter apathy 投票者的冷漠

One of the weaknesses of DPOS is voter apathy. A large percentage of the voters don't check their voting list often enough and make changes when necessary. The result is that many potentially good BPs won't be voted in and some underperforming will be staying.

DPOS 的弱点之一就是投票者冷漠（voter apathy）。很大比例的选民并不经常检查他们的投票列表，也不会在必要时做出更改。结果导致许多潜在的优秀 BP 没有选出，而一些表现不佳的 BP 则继续留任。

Instead of changing their votes, stakeholders could just voice their opinion about weak BPs. For example, if a DBP has low file storage capacity, stakeholders could demand that they will replace the file storage partner with better one or else they will be voted out. In many cases, this will be enough and the result is better performing BPs without a need for voters to change their vote.

利益相关者可以不用修改投票，只需要对表现差的 BP 发声表达意见即可。例如，若一个 DBP 的文件存储能力弱，利益相关方可以要求他们将文件存储方面的合作伙伴换成更好的，否则就投票淘汰他们。在很多情况下，这样做就够了，投票者无需更改他们的投票，就可以得到表现更好的 BP。

It's much easier to handle certain questions one at a time, like file storage capacity. It's harder to compare different BPs with different strengths and weaknesses and try to choose which combination is the best for the whole ecosystem. Most people are too lazy to do it very often.

一次处理一个特定问题要容易得多，例如文件存储能力的问题。很难对有不同长处和短处的 BP 进行比较，并选出对整个生态系统而言更有利的组合。大部分人都很懒，不会经常这么做。


### Learning decentralized governance 学习去中心化的治理

Good governance is hard. Especially when the governed group is distributed around the world. DBPs have to be well-governed, otherwise, they will be voted out. Block producing is so essential task that underperformance won't be tolerated for long. This creates a big incentive for DBPs design efficient governance models for cooperation.

好的治理很难。尤其是当管理团队分散在世界各地时，更是如此。DBPs（注：去中心化的区块链生产者们）必须进行有效的治理，否则就会被投票淘汰。区块生产的任务非常关键，如果表现不佳，人们不会容忍太久。这大大刺激了 DBPs 去设计有效率的治理模式以便协作。

DBP can be designed like a DAO. There will be BP-tokens that hold voting power over the BP. All decisions are made by stakeholders vote, like deciding who will be a partner responsible for a particular task. All the profit will be paid as an interest for BP-token holders, which can attract investors to support the DBP. With EOS permission management, this should be pretty easy to do.

DBP 可以设计成类似 DAO 的方式。会出现 BP 代币，拥有代币，就可以在 BP 上拥有投票的权力。所有的决定应由利益相关者投票，例如决定负责特定任务的合作方由谁来担任。所有产生的利润，将会作为利息支付给 BP 代币的持有者，可以吸引投资者支持 DBP 。借助 EOS 的权限管理功能，这应该非常容易实现。

Hopefully, there will be lots of different governance models tried for DBPs. Over time the bad ones will be voted out and the best will flourish. It will be a great lesson how to actually create successful decentralized organizations. So far it has been mostly talking and not enough deliberate learning through trial and error.

有希望出现很多对不同的 DBPs 治理模式的尝试。随着时间的推移，坏的模式会被淘汰，好的将会蓬勃发展。可以从中学到很多经验，如何成功创建真实的去中心化组织。 迄今为止还只是谈论（如何创建去中心化的组织），通过反复试错来进行的有意识的学习并不够。


## Conclusion 结论

If we think block producers as "mining pools" instead of single entities, we can achieve an additional layer in the decentralization of DPOS. This will create several benefits for the ecosystem.

如果我们将区块生产者视作“矿池”，而不是单个的实体，我们会在 DPOS 的去中心化中得到一个附加层。这会为生态系统带来多种益处。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

荆凯，程序员，坚信区块链将会改变潮水的方向。欢迎加微信: shuke0327，或者关注公众号: 增长之道

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

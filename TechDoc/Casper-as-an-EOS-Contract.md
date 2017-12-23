Casper as an EOS Contract | 将 Casper 作为 EOS 智能合约
--------------------------------------------------

> 本文翻译自：https://steemit.com/eos/@dan/casper-as-an-eos-contract
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)  [荆凯](https://github.com/shuke0327)
>
> 翻译时间：2017-11-25

---------------------------


I recently reviewed the latest[Casper Research Paper](https://github.com/ethereum/research/tree/master/casper4/papers) in light of an ongoing discussion with Vitalik Buterin over consensus mechinisms. It is my intent to be as objective and practical as possible while recognizing all factors of the greater picture.

根据与Vitalik Buterin 对共识机制正在进行的讨论，我最近对最新的[Casper研究论文](https://github.com/ethereum/research/tree/master/casper4/papers)做了一些修订。我尽可能做到客观和实用，同时考虑到更广的图景中的所有因素。
![](https://steemitimages.com/DQmbA4wvwzeu4s6YELBpkJQGvhMRJZFqb6x8U58fBMwKfvZ/image.png)


One thing that has become abundantly clear in my research is that the various consensus camps have been talking past each other due to a general lack of language precision. For the sake of clarity I will attempt to use the language and terms found in the Casper papers.

在我的研究中已经非常清楚地表明，由于普遍缺乏语言准确性，各种共识阵营之间一直在各说各话。为了清晰起见，我会尝试使用在Casper论文中的语言和术语。


## Two Parts of the Problem | 问题的两部分

There are two parts to the Casper protocol, the **proposal mechanism** and the  **consensus mechanism**.  The proposal mechanism produces a sequence of blocks that link together and the consensus mechanism creates a checkpoint every 100 blocks.

Casper协议有两个部分，**提议机制** 和**共识机制**。提议机制产生一系列相互连接的区块，而共识机制每隔100个块创建一个检查点。

Under the hybrid proof-of-work model Ethereum will use POW blocks as the **proposal mechanism** and the Casper algorithm to reach consensus on checkpoints.

在Ethereum将使用的混合工作机制证明(proof-of-work)模型中，使用POW块作为**提议机制**, 使用Casper算法在检查点上达成共识。

> The proposal mechanism is deliberately kept abstract; this can be a dictator, it can be a round-robin scheme between the participants in the consensus, or, as in our case with hybrid Casper, it will be the original proof of work chain.

> 提议机制刻意保持抽象性; 它可能是一个独裁节点，也可以是参与者之间达成共识的循环方案(round-robin scheme)，或者，就像我们在混合Casper机制中的例子一样，它是原始的工作量证明链。

Given that the proposal system is abstract, it is trivial to replace it with DPOS. In other words, where Ethereum uses POW we can use DPOS. Note that using POW with casper does [require changing the Fork Choice Rule](https://medium.com/@VitalikButerin/minimal-slashing-conditions-20f0b500fc6c) away from the “longest chain” to a new rule that factors in Casper first and only uses longest chain rule to break the tie.

考虑到提议系统的抽象性，使用DPOS替换它是无关紧要的。换句话说，在Ethereum使用POW的地方，我们都可以使用DPOS。注意，Casper使用POW确实需要改变“分叉选择规则”(https://medium.com/@VitalikButerin /minimal- slashs-conditions-20f0b500fc6c)，从“最长的链”转移到一个新的规则即Casper优先的规则，最长链规则只被用来打破僵局。

## Casper Protocol Messages　| Casper协议信息

Because the Casper papers keep the **proposal mechanism** deliberately abstract, their initial proposal mechanism will be proof of work, and I am not aware of any proposed alternative proposal mechanisms, we can skip straight to the **consensus mechanism** of Casper.

因为Casper的论文中刻意使**提议机制**保持抽象，他们最初的提议机制是工作量证明机制，我不知道还提出了提议机制的什么其它替代方案，我们可以直接跳到Casper的**共识机制**。

Casper is first and foremost a protocol based on mathematics and game theory. This protocol attempts to reward those who agree while punishing those who disagree. It also has properties that punish all participants if certain objective measures of mischief are observed.

Casper首先是一个基于数学和博弈论的协议。这个协议试图奖励同意者而惩罚反对者。如果经过客观的衡量，观察到参与者存在不当行为，也会对他们进行惩罚。

In the Casper protocol there is a set of validators and all validators are expected to send two messages per epoch: PREPARE and COMMIT over their preferred last blocks in the chain of the epoch. The proposed epoch is 100 blocks; under Ethereum an **epoch** is 1500 seconds, under DPOS it would be 300 seconds.

在Casper协议中，有一组验证人，所有的验证人预期会在每一个周期发送两条消息: 准备并提交(PREPARE and COMMIT )他们在epoch的链中所选择的最近的多个区块。提议的epoch是100个区块;以太坊中**epoch**是1500秒，在DPOS机制下是300秒。

The bandwidth required grows order N with the number of participating validators and comes at the expense of potential bandwidth for other transactions. It is for this reason that an Epoch is 100 blocks and not 1 block.

随着参与的验证人数量增加，所需的带宽会呈N阶增加，同时还会消耗其他事物的潜在带宽。因为这个原因，一个Epoch是100个区块，而非一个区块。

## Casper as an EOS Application　| 作为 EOS 应用的Casper

With this basic understanding, the EOS community could elect to adopt Casper as a contract to increase the perceived security of their blockchain. The rewards for participation could be funded by one of the 3 community benefit applications elected by stakeholders. Delegated Proof of Stake currently uses the longest-chain rule.

有了这些基本理解，EOS社区可以投票选择采用Casper作为智能合约，以增加区块链的直觉上的安全性。参与者的奖励可以由利益相关者选出的3个社区福利应用之一资助。委托权益证明机制(Delegated Proof of Stake)目前使用的是最长链式法则。

All of this could be implemented without actually changing the EOS protocol or at most tweaking the fork-choice rule to account for information from Casper validators. However, given the almost complete lack of forks in DPOS this hardly seems necessary.

所有这些都可以在不实际改变EOS协议的情况下实现，或者最多调整分叉选择规则用于解释来自Casper验证人的信息。然而，由于在DPOS中几乎完全没有分叉，这似乎没什么必要。

## The Importance of the Proposal Mechanism | 提议机制的重要性

The proposal mechanism determines what transactions get included in blocks and what transactions are censored. It also determines the set of blocks available to the casper consensus process.

提议机制决定了哪些交易会包含在块中，哪些交易会被审查删除。还决定了casper 共识过程中可用的区块集。

The proposal mechanism controls the following aspects of a protocol:
提议机制包括了协议的如下方面：

1.  When is a block produced
2.  Who produces it
3.  What transactions are included
4.  Potentially who gets the fees
5.  When hard forks are adopted
6.  What soft forks are enforced
7.  The speed of short-term transaction confirmation
8.  The probability of short-term forks

1.  何时产生区块
2.  谁产生区块
3.  哪些交易会包含到区块中
4.  可能由谁获得交易费用
5.  何时采纳硬分叉
6.  何种软分叉会被强制执行
7. 短期交易确认的速度
8. 短期分叉的概率

This means that the proposal process is what determines centralization of production and censorship. Shutting down the proposal process shuts down the network as the Casper Consensus process depends upon a valid source of produced blocks. All Casper provides is a economic measure of finality every 30 minutes (Eth POW hybrid) or 5 minutes (DPOS hybrid).

这意味着，是提议过程决定了生产和审查的集中化。关闭提案过程会使网络停止，因为Casper共识过程依赖于生成区块的一个有效来源。每隔30分钟(Eth POW混合机制)或隔5分钟(DPOS混合机制)，Casper会提供一个衡量最终性(finality)的经济指标。

We can conclude from this that the vast majority of the real consensus problems fall within the responsibility of the proposal mechanism. We can also see that Casper does nothing to improve the performance. Lastly, by the time an Ethereum block is buried under 30 minutes of POW the probability of reversal is so small that the relative cost of "casper insurance" likely far outweighs the actual risks involved.

我们可以由此得出结论，绝大多数真正的共识问题都属于提议机制的范围。我们也可以看到，Casper并没有提高性能。最后，当一个以太区块被埋在30分钟的工作量证明(POW)之下时，反转的概率很小，“casper保险”的相对成本可能远远超过所涉及的实际风险.

## My Proposed Proposal Mechanism　| 我提出的提议机制

If we allow anyone to propose anything at anytime then Casper validators could reach a deadlock by not knowing which blocks to sign PREPARE messages for. It is in the validators interests to cooperate to reach consensus.

如果我们允许任何人在任何时候提出任何提议，那么Casper验证人可能会因为不知道该为哪些块签署准备(PREPARE)消息而陷入僵局。与其他验证人合作达成共识，是符合他们利益的。

The Casper Validators may be wise to the deadlock issue and agree to “take turns” sending PREPARE messages. In this way the validators always send PREPARE for a valid block which already has the most PREPARE messages. Once we have established that validators will cooperate to schedule and synchronize timing of sending PREPARE messages we can also suggest that the first to send PREPARE will do so for a block that they themselves produced.

Casper验证人在死锁问题上可以采取明智的做法，同意“轮流”发送准备(PREPARE )消息。通过这种方式，验证人总是可以为一个已经拥有最多准备消息的有效区块发送准备信息。一旦我们确定了验证人将会合作，进行调度，同步发送准备消息的时间，我们还可以建议，第一个发送准备信息的验证人将会对他们自己所生成的区块进行处理。

Therefore we can model Casper as a protocol of N validators that each submit a PREPARE message at individually allocated time slices, say once every 3 seconds. This means that with a 100 block epoch and 3 second blocks you could have over 100 validators. You could support more validators if you reduce the interval and start allowing multiple validators to submit PREPARE messages in parallel after enough momentum has built up. Think of it as an avalanche started by a single PREPARE snowflake.

因此，我们可以将Casper建模为包含N个验证人的协议，每个验证人都在每个分配的时间片上提交一个准备消息，比如说每3秒钟一次。这意味着，在100块的epoch和3秒的块中，可以拥有超过100个验证人。如果减少时间间隔，在构建了足够的动量之后，开始允许多个验证人并行提交准备消息，那么您可以支持更多的验证人。把它想象成一场雪崩，由一个“准备”的雪花开始。

While any number of validators is possible, a protocol would be wise to limit the absolute number. My understanding of Casper is that the minimum required bond grows as the number of validators increases. To support scaling Casper expects validators to create pools of bonds and potentially apply multisig to the PREPARE and COMMIT messages.

尽管有可能会有任意数量的验证人，但协议的明智做法，是限制验证人的绝对数量。我对Casper的理解是，随着验证人数量的增加，最低要求的bond也会增长。为了支持Casper扩容，希望验证人能创建一个 bond 池，并潜在地将多重签名( multisig )应用在准备和提交消息上。


## DPOS is Pipelined Casper |  DPOS与Casper管道相连(pipelined)

For bandwidth and performance reasons Casper currently executes one round (called an epoch) every 100 blocks. You could improve upon this by pipelining the epochs so that you have 100 epochs being processed in parallel with a new epoch finalizing every block. If we assume that the validators are taking turns being first to PRODUCE and PREPARE then we can view each DPOS block as a PREPARE message on all prior blocks for 99 prior epochs and a PROPOSE message for a block in the next epoch. In this same pipeline we can consider a PREPARE a COMMIT for the previous PREPARE.

考虑到带宽和性能，Casper目前每100个块执行一次(称为一个epoch)。你可以通过管道(pipeline)来改进这一点，这样你就可以并行处理100个不同的epoch，每个区块都终结于(finalizing)一个新的epoch。如果假设验证人正在轮流成为第一个生成和准备信息的，那么可以将每个DPOS块看作是为之前的99个epoch的所有区块的准备消息，以及在下一个epoch中区块的提议消息。在这条管道中，我们可以考虑为之前的准备信息，创建一条准备和一条提交信息。

So if you pipeline Casper and make each block Proposal a PREPARE for the current round (epoch 0) and a COMMIT for the prior round (epoch -100) then it is possible to apply the similar slashing conditions while getting much higher performance.

如果你将Casper管道化，让每个区块为当前这一轮(epoch 0)提出一个准备信息,　并且为前一轮（epoch -100）提起COMMIT信息，也许可以在得到更高性能的同时，使用类似的削减条件(slashing conditions).

## Two Phases to DPOS | DPOS 的两个阶段

There are two independent parts of the DPOS algorithm:
DPOS算法中，有两个独立的部分:

1.  Selecting the Producers
2.  Reaching Consensus

1. 选择区块生产者
2. 达成共识

If you make the producer selection based upon size of the producer bond then you replace voting for producers with producer bonds. If you reinterpret the DPOS block production schedule as a pipelined sequence of Casper epochs then you can apply the Casper slashing conditions while having all the speed and benefits of DPOS.

如果基于生产者的bond大小选择生产者，那么就会将投票选择生产者替换为根据producer bonds来选择的方式。如果重新将DPOS生产调度阐释为Casper epochs的管道顺序，那么可以在拥有DPOS的速度和优势的同时，使用Casper的削减条件(slashing conditions).

## Validator and Proposer Selection 验证人和提议人选择

Under the hybrid POW model, the proposers are selected by proof of work and the validators are selected by those with the highest stake. This hybrid model does nothing to prevent empty blocks or censorship from mining pools. This hybrid stage will eventually give way to some other proposal system, so let's speculate on what that might be.

在混合POW模型中，根据工作量大小来选择提议人，验证人由拥有最大份额的成员选出。这一混合模型无法防止空块，也无法防止矿池的审查。这一混合阶段，最终会让步于其它的提议系统，因此我们猜测一下可能会是什么机制。

A reasonable solution is to have the validators take turns producing blocks. The frequency of their selection could either be proportional to stake or independent of stake. If it is independent of stake then this role could be sybil attacked by someone dividing their stake into as many independent accounts as they can fund with the minimum bond. Therefore we prefer stake weighted production.

一个合理的解决方案是，让验证人轮流产生区块。他们被选择的频率，可以与持有权益的份额成比例，也可以独立于权益比例。如果独立于权益比例，那么某些将自己的权益尽可能分散到多个独立账号的人，可以对这一角色发起女巫攻击，他们只需要承担最小的bond就可以了。因为，我们选择权益比例加权的生产机制。

Under a stake weighted system each “proposer” will produce a block with a frequency proportional to their stake. This would be like the traditional proof of stake system.

在权益加权系统中，每个提议人会以与所占权益成比例的频率来生产区块。这类似于传统的权益机制证明系统。

We can assume that block producers (proposers) are rewarded with transaction fees and/or block rewards. These rewards can either be socialized or individualized. To keep incentives aligned among the validators it would appear that socialization makes the most sense to encourage cooperation rather than competition; however, under the hybrid POW model being adopted by Ethereum it would be individualized to the miners (aka producers, proposers).

我们可以假定区块生产者(提议人)的奖励来自于交易费和/或区块奖励。这些奖励可以是社会化的奖励，也可以是个人化的。为了让激励机制在验证人之间保持一致性，似乎鼓励合作而不是竞争的社会化方式是最合理的; 然而，在以太坊采用的混合POW模型下，对矿工(也就是生产者，提议者)的奖励是个人化的。

## Bias toward centralization 中心化的倾向

There are two forces at work in Ethereum’s proposal that both tend towards centralization. Firstly, assuming the operating cost for a validating node is constant, the rate of return is proportional to the stake at risk under the proposed individualized rewards structure. Therefore those with the largest bonds in a single pool have the highest rate of return.

在Ethereum的提议中，有两种力量都倾向于中心化。首先，假设验证节点的运营成本是固定的，在所提议的个人化奖励结构下，收益率与权益承担的风险成正比。因此，单个池子中拥有最多bond的节点收益率最高。

Rationally, in terms of raw return on investment, everyone should pool their stake into a single account that certifies all blocks. Not doing this is against the economic best interest of the majority. The end result will likely mirror the distribution of mining pools where there are less than 10 individuals deciding the entire consensus.

理性地说，就投资的实际回报率而言，每个人都应该把自己的权益份额汇集到同一个账户中，该账户可以验证所有的区块。不这样会违背大多数人的最大经济利益。最终的结果可能会反映出矿池的分布，只有不到10个个体决定了整体共识。

Secondly, the operating cost of the validating node actually rises with the throughput of the blockchain. As Ethereum is already straining at around 15 transactions per second, this is an immediate concern. Purchasing and operating top end hardware is going to challenge smaller operations and therefore is another force for concentration (centralization).

其次，验证节点的运行成本实际上随着区块链的吞吐量而上升。由于  Ethereum 每秒钟处理大约15笔交易已经吃紧了，这是一个迫在眉睫的问题。采购和运行高端硬件将威胁较小的运行者，因此是另一种集中(中心化)的力量。

## Governance 治理

At this point it should be clear that Casper is an application layer protocol that can be layered on top of any of the existing consensus algorithms to add check points. What Casper does not solve is the governance problem. Layered on POW governance would be left to block signaling, or layered on proof of stake it would amount to stake weighted direct democracy among validators. Under DPOS governance is multi layered delegation to a panel of equally weighted producers.

在这一点上应该清楚，Casper是一种应用层协议，它可以置于任何现有的共识算法的顶层，添加检查点。Casper没有解决治理问题。如果Casper在POW之上，治理问题将会被留给区块信号传递；或者。如果Casper位于权益证明机制的顶层，会在验证者之间实现权益份额加权的直接民主。在DPOS下，治理是多层的，委托给一个由同等权重的区块生产者组成的小组。

Absent a defined and robust governance model blockchains are governed by adhocracy which generally reduces to influence peddling to the largest validators and miners. Decisions over hard forks impact all stakeholders and all stakeholders should have some influence. This influence needs to extend beyond a basic opinion poll which could be ignored by producers, proposers, and validators. The selection of block producers (proposers) needs to be tied to community governance because it is only through the production (proposal) of blocks that decisions of governance are ultimately executed.

如果没有一个定义好的、健壮的治理模型，区块链是由临时委员会管理的，它通常会受到最大的验证人和矿工的影响。对硬分叉的决定会影响所有的利益相关者，所有的利益相关者都应该发挥一定的影响力。这种影响需要超越基本的民意测验，因为民意测验可能会被生产者、提议人和验证人所忽视。对区块生产者(提议人)的选择需要与社区治理联系在一起，因为只有通过区块生产(提议)，才能最终执行治理决策。

One thing is clear, unless a non-technical individual can trivially participate in the governance the interests among all participants on a blockchain will be misaligned. This means that individuals will have to contribute (and risk) their stake to a validator pool. The risk associated with contributing to a single pool is significant, especially if it is uncompensated. The pool operator would take on significant liability and has no incentive to share 100% of the rewards. This in turn means pool operators gain a larger percentage of the rewards.

有一件事很清楚，除非一个非技术人员能够参与治理，否则区块链的所有参与者的利益将无法保持一致。这意味着个人将不得不向验证人池贡献他们的权益份额，并且承担风险。把权益贡献给单个池的相关风险很大，尤其是在无报酬的情况下。验证池的运营者将承担很大的责任，没有动力分享他们的全部收益。这反而意味着验证池的运营者获得了更大比例的回报。

Just as in Bitcoin and Ethereum, there will be a small number of pool operators who benefit from economies of scale. The more stake a pool has the lower the risk to the pool and the lower the overhead percentage of the operator. In this case people committing their stake to pools are not “voting” based on the politics of the pool, but based on their selfish rate of return offered by the pool operator. Who knows, pool operators may even rent stake to gain a 51% control over the proposal algorithm.

就像在比特币和以太坊中一样，将会有一小部分(验证池)运营者从规模经济中获益。一个池子所占权益份额越大，风险就越低，运营人员开销所占的百分比就越小。在这种情况下，人们将赌注押在池子上，不是基于验证池的政策而“投票”，而是基于他们自私的考虑，基于池子运营者提供的回报率来考虑。谁知道呢，验证池的运营者甚至可以租赁权益，以获得对提议算法的51%的控制权。

## Conclusion 结论

Casper is an interesting algorithm to reward those willing to bet-their-stake on the validity of a block. It remains to be seen what the real-world risk/reward looks like for participating in this game. It is a game where honest mistakes caused by software bugs, network disruptions, or griefing peers may cause unexpected and undeserved losses. This risk may be difficult to access and may discourage participation of honest players. The slashing conditions are a harsh code-is-law kind of governance that leaves little room for honest mistakes that caused no measurable harm (such as accidentally running a backup node with the same key and signing twice). The intention was to maximize uptime and minimize missed epochs, but the outcome was to get slashed.

Casper是一种有趣的算法，奖励那些愿意将自己的权益押注在一个区块的有效性验证上的人们。在这个游戏中，现实世界的风险/回报是什么样子还有待观察。这个游戏中，由软件错误、网络中断或恶意破坏的节点(griefing peers)所造成的无心之过，可能会导致意外和不应得的损失。这种风险可能很难获得(access)，可能阻碍诚实玩家的参与。削减条件(The slashing conditions)是一种哈希代码即法律的治理类型，它为造成无法估量损失的无心之过，留的空间很小(比如不小心将一个备份节点用同样的密钥和签名运行了两次)。目的是最大限度地提高正常运行时间，并尽量减少错过的epoch，但结果却被削减了。

After all of this effort and game theory, it is still not clear that Casper will result in more relevant security or decentralization than we have with POW and traditional POS. I remain convinced that DPOS provides the best possible

在所有这些努力和博弈理论之后，我们仍然不清楚Casper将会比POW和传统POS带来更多的相关安全性或去中心化，我仍然相信DPOS提供了最好的可能性。

**proposal algorithm** **提议算法**

for the Casper consensus algorithm, but I am unconvinced that Casper adds any meaningful value. After all, a properly functioning bug-free version of DPOS produces no forks and achieves irreversible checkpoints 30 times faster.

对于Casper共识算法，我不相信Casper添加了任何有意义的价值。毕竟，一个正常运行的无bug版本的DPOS不会产生任何分叉，并能以30倍的速度实现不可逆的检查点。

That said, I think it would be a worthwhile experiment to implement that Casper protocol as an EOS smart contract. Using our concept of Community Benefit Contracts (CBCs) we can propose that Casper be implemented the staked EOS holders vote on how much inflation to reward the Casper contract with, if any at all.

也就是说，我认为将Casper协议作为EOS智能合约来实现，将是一个有价值的实验。利用我们的社区福利智能合约的概念(CBCs)，我们可以提出，Casper可以设计为，EOS权益的持有者，投票决定要选择多少通货膨胀来奖励Casper智能合约，如果有(通货膨胀)的话。

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

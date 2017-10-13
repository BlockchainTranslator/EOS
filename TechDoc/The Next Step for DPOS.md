The next step for DPOS: Decentralized block producers
--------------------------------------------------

DPOS 的下一步: 区块生产者的去中心化
--------------------------------------------------

> 本文翻译自：(https://steemit.com/eos/@samupaha/the-next-step-for-dpos-decentralized-block-producers)
> 
> 译者：区块链中文字幕组 [荆凯(shuke0327)] (https://github.com/shuke0327)
> 
> 翻译时间：2017-10-14

---------------------------

One of the most common criticisms against delegated proof of stake systems is the perceived lack of decentralization. 21 block producers (per round) might seem very low number, even though it's still very high compared to proof of work systems which are usually fully controlled by less than ten mining pools.

对委托权益证明系统最常见的批评之一是其缺乏去中心化。 区块生产者有21个(每一轮)，这数量似乎很少，虽然与工作量证明系统相比已经算很多了，后者通常被不到十个矿池全权掌控。

When the centralization by mining pool is pointed out, POW proponents will give a counter-argument:  _"It's not really that bad because miners can change their mining pool whenever they want."_  Which is true, of course. If a mining pool does something bad, it can lose a lot of hashing power very quickly because miners just choose another pool.

当人们指出矿池的中心化时，POW 拥护者会反驳称: _"由于矿工可以随时切换矿池，所以这并没有那么糟糕。“_ 这说法当然正确。 如果矿池做了坏事，矿工只要选择其它矿池，它会很快失去大量的hash算力。

That made me think... Could we implement something similar in DPOS?

这促使我思考... 我们在 DPOS 中，能否做类似的实现？

This post is mostly from the perspective of EOS, but ideas can be applied to Steem, Bitshares and other DPOS blockchains, too.

这篇帖子主要从 EOS 的角度讨论，但这一想法对 Steem、Bitshares 和其它采用 DPOS 的区块链也同样适用。

### Formalization of block producer's responsibilities

### 生产者责任的形式化

In EOS, block producers will have quite a lot of responsibilities.

在EOS中，区块生产者将会有很多职责。

Technical:

技术：


*   Creating blocks
*   创建区块
*   File hosting
*   文件托管
*   Back-up servers
*   备份服务器
*   Seed node
*   种子节点

Governance:

*   Following the constitution

*   Account freezing, misbehaving contracts

*   Take-down notices of files

*   Hard and soft forks, fees (account creation), parameters (blocksize, rate-limited capacity)

Leadership:

*   Something like a CEO in a traditional company, keeping everything internal in control

*   Communication with other block producers

*   Campaign to get elected as a BP

Possible extra services:

*   Account recovery

*   Account creation

*   Oracles

*   Price feeds

*   Dispute resolution service

As you can see, running a BP is much more than just a server creating blocks. One person might be able to handle everything in the beginning, but when the ecosystem grows, this will require a team.

### Decentralization of a block producer


When we know all the responsibilities of a BP, we can break them down into smaller jobs which can be done by separate individuals or organizations. This will give us several different options.

There can be fully centralized BP, for example, an IT company that has professionals who can take care of everything. Or there can be fully decentralized BP, which works like a DAO: BP is just a smart contract which is governed by BP-tokens. Or some combination of those.

Decentralized block producers (DBP) will create some benefits for the ecosystem. Let's look at them more closely.

#### Additional layer of decentralization


While 21 BPs for DPOS is probably more than enough to create a robust system, a little bit more decentralization wouldn't be a bad thing. Adding more BPs per round isn't a good option, it would mean that the BP layer just gets a little bit more decentralized. But adding another layer to the system would create more decentralization without any negative side effects, like slowing the system or making it more expensive to run.

The first layer of the blockchain decentralization is the BPs. The second layer should be different tasks of a BP.

Because DPOS is perceived as not having enough decentralization, this is also good for the marketing. It will be harder to claim that DPOS is too centralized when a BP is not one entity but several entities which can be easily replaced.

It will be much harder for BPs to conspire against the ecosystem. And of course, it will make harder to anyone attack against BPs because they are not one entity.

#### Lower barriers to entry

There have been fears that when the system grows, the barrier to entry will become too high. Being a BP might require big investments to server infrastructure to ensure capacity and that will discourage people to become a BP.

Instead of taking care of all responsibilities of a BP, individual or organization can start with just one thing, like file storage. They can identify a DBP whose file storage is lower than others and offer to replace it. After they have earned money and reputation, they can start to take care of other responsibilities, too.

#### Specialization

Usually, the system becomes more efficient when individuals and organizations specialize in certain work. They can focus on the one thing and become really good at that. They don't need to spend resources trying to become great at everything – often that means they are going to be weak at some things.

When people/organizations specialize, they can produce the services at lower cost. In the case of EOS, this is very beneficial because BPs can then offer more capacity for the blockchain.

#### Self-healing

DBPs can monitor their capacity and uptime and see how well they are doing compared to others. If some part of their DBP organization seems to be weaker than others, they can find a better partner. This is probably more efficient compared to a centralized BP, which has to either make an effort to learn how to do a better job or hire somebody to do it.

DBP can just look at possible alternatives (assuming there are markets for them) and replace low-performing partner with a better one. When the process of integrating different BP services is formalized, this should be very easy to do.

#### Voter apathy

One of the weaknesses of DPOS is voter apathy. A large percentage of the voters don't check their voting list often enough and make changes when necessary. The result is that many potentially good BPs won't be voted in and some underperforming will be staying.

Instead of changing their votes, stakeholders could just voice their opinion about weak BPs. For example, if a DBP has low file storage capacity, stakeholders could demand that they will replace the file storage partner with better one or else they will be voted out. In many cases, this will be enough and the result is better performing BPs without a need for voters to change their vote.

It's much easier to handle certain questions one at a time, like file storage capacity. It's harder to compare different BPs with different strengths and weaknesses and try to choose which combination is the best for the whole ecosystem. Most people are too lazy to do it very often.

#### Learning decentralized governance

Good governance is hard. Especially when the governed group is distributed around the world. DBPs have to be well-governed, otherwise, they will be voted out. Block producing is so essential task that underperformance won't be tolerated for long. This creates a big incentive for DBPs design efficient governance models for cooperation.

DBP can be designed like a DAO. There will be BP-tokens that hold voting power over the BP. All decisions are made by stakeholders vote, like deciding who will be a partner responsible for a particular task. All the profit will be paid as an interest for BP-token holders, which can attract investors to support the DBP. With EOS permission management, this should be pretty easy to do.

Hopefully, there will be lots of different governance models tried for DBPs. Over time the bad ones will be voted out and the best will flourish. It will be a great lesson how to actually create successful decentralized organizations. So far it has been mostly talking and not enough deliberate learning through trial and error.

### Conclusion


If we think block producers as "mining pools" instead of single entities, we can achieve an additional layer in the decentralization of DPOS. This will create several benefits for the ecosystem.


[1]:https://steemit.com/@samupaha
[2]:https://steemit.com/trending/eos

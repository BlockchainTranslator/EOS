# Accelerating Evolution Through Forking 通过分叉加速区块链进化

> 本文翻译自：https://medium.com/@FEhrsam/accelerating-evolution-through-forking-6b0bba85a2ba
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [龙心小台](https://github.com/xnylong/EOS)
> 
> 翻译时间：2017-10-14

In a prior post I proposed [funding protocol development through inflation](https://medium.com/@FEhrsam/funding-the-evolution-of-blockchains-87d160988481) as a powerful tool to evolve blockchains.

在之前的帖子中， 我提出通过[通货膨胀来资助协议](https://medium.com/@FEhrsam/funding-the-evolution-of-blockchains-87d160988481)开发是一个可以发展区块链的强大工具。

Forking is a second critical evolutionary mechanism for blockchains. Just like mutations to DNA in biological organisms allow for evolution through natural selection, forking lets us run multiple experiments in parallel where the strongest versions survive. Unlike Web 2.0 companies, forking a blockchain is possible because the current code and state of a blockchain can be freely copied. It is the equivalent of any developer being able to make a copy of Facebook’s code and spin up a competing version at any time— something a Web 2.0 company would never allow.

分叉是第二个至关重要的区块链进化机制。正如生物体的基因突变使得通过自然选择的进化得以实现，分叉让我们可以并行运行多个实验，以使最强的版本得以生存。与 Web 2.0 的公司不同，区块链分叉是可行的， 因为当前的代码与区块链状态可以被任意复制。与其相似的是任意一个开发者都可以复制 Facebook 的代码并且随时上线竞争版本，而 Web 2.0 的公司绝不能如此。

However, there is a key issue with the economic incentives with the forks we have seen so far: the groups pushing forward new forks have very little economic incentive to make their fork succeed. This is because forking behavior to date replicates the token ownership of the prior chain instead of modifying it to incentivize its new core community.

然而，我们至今所见的分叉在经济激励上有个关键的问题： 推动新分叉的团体很少有足够的经济激励来使他们的分叉成功。这是由于迄今为止的分叉是直接复制旧链的代币所有权，而非通过修改所有权来达到激励新核心社区的目的。

Let’s take an example. Say there is a group of developers who believe they can create a better version of TokenA. They probably own a modest stake in TokenA pre-fork — say 0.10%. In their new ForkedTokenA they’d also own 0.10%. So their incentives to make ForkedTokenA succeed are very small and about the same as in TokenA.

让我们来举个例子。假设，有一组开发者相信他们可以开发出一个更好的 TokenA 的版本。他们可能拥有 TokenA 分叉前的一小部分代币 -- 比如，0.10%。那么，他们也将拥有新分叉的 ForkedTokenA 的 0.10% 代币。所以，他们推动新分叉的 ForkedTokenA 成功的动力将会很小, 与推动 TokenA 成功的动力相仿。

Applying a startup lens, you’d want these “founders” of ForkedTokenA to have a strong economic incentive to make it a success. Ironically, they probably have a stronger economic incentive to improve the original TokenA than their ForkedTokenA since TokenA is likely to be more valuable to start. Let’s say TokenA is worth $10 and ForkedTokenA is worth $1 after the fork. A change which improves TokenA by 20% would net the developers $2 per coin, while a change which improves ForkedToken A by 20% would net the developers $0.20 per coin, and they own the same amount of coins. Their incentives are inverted. The developers would need to own more ForkedTokenA to fix the incentives.

从新兴公司的角度来说，你会想让这些 ForkedTokenA 的“创始人”有强大的经济激励来使 ForkedTokenA 成功。讽刺的是，他们可能有更强的经济动力去改善之前的 TokenA 而非他们自己的 ForkedTokenA , 因为改善 TokenA 可能更有价值。比如说， 分叉后 TokenA 值 $10 而 ForkedTokenA 值 $1。使 TokenA 提高20%的改变会让开发者每个代币得到 $2，使 ForkedTokenA 提高20%的改变会让开发者每个代币得到 $0.20，而开发者拥有的两种代币数量相同。所以，他们的激励是相反的。开发者们需要拥有更多的 ForkedTokenA 才能获得正确的激励。

Things become even more comical when the token holdings of the original chain’s foundation come into play. If TokenA Foundation owns 20% of the coins in TokenA, they will now own 20% of the coins in ForkedTokenA, while the development team driving ForkedTokenA own none. This happened when Ethereum Classic forked from Ethereum and the Ethereum Foundation owned a bunch of Ethereum Classic all of a sudden, despite having no interest in contributing to it.

当我们考虑原始链条的基金会时，事情将变得更加滑稽。如果 TokenA 的基金会拥有 20% 的 TokenA 代币，那么他们也将拥有 20% 的 ForkedTokenA 代币，而 ForkedTokenA 的开发团队却没有拥有代币。同样的事情也发生在以太经典( Ethereum Classic) 从以太币分叉之际，尽管以太基金会没有兴趣对以太经典做出任何贡献，却一下子突然拥有了一堆以太经典。

Finally, consider the governance implications. Forks often arise from differences of opinion in the direction of a project. And tokens are increasingly a mechanism for voting on changes to their protocols. Since the point of a fork is to try a new path, the new fork may not want to port all of the prior holders opposed to trying the new path the fork was created to take.

最后，让我们考虑下治理的影响。分叉一般是由于在项目方向上意见不合造成的。并且，代币日益成为更改协议的一种有效投票机制。而因为分叉本身就是为了尝试一条新路径，新分叉可能并不希望接纳之前反对分叉的代币持有者。

It becomes clear that redistributing tokens in forks is helpful and even necessary for many new forks to have a shot at surviving. So while token redistribution in forks is uncommon now, it feels like it will become the norm in the future.

由此看来，在分叉时重新分配代币对很多新分叉来说是有帮助的，甚至是事关存亡的。所以，尽管分叉时的代币重新分配在现阶段并不常见，它在将来可能会成为常态。

Redistributing tokens is a balancing act. In most cases forks probably want to keep ownership for users constant so users have at least the same incentives to use the new fork as the historical one. The main goal is to incentivize the groups working on the new fork — mainly through switching control of foundation-like tokens and potential dilution of all tokenholders to make grants for the new developers. The latter is similar to creating new shares in a mature company for a new employee.

重新分配代币需要考虑平衡各方利益。在多数情况下，分叉可能希望保持原来的用户所有权比例，以使用户至少有同等的激励来使用新分叉。最主要的目的是要激励新分叉的工作团队，主要通过改变基金会的控制权与稀释所有代币持有者的份额来资助新的开发者。后者类似于在一个成熟的公司为新员工创造新的股份。

It’s also important to keep in mind that forking will not always be about direct competition. Just as DNA mutations produced many different viable organisms that started from the same genetic tree, we may see one protocol grow into 3 which solve different purposes. Protocols will likely go through unbundling and rebundling of their functionality until the right equilibrium is found. And since the ecosystem itself is constantly changing, that equilibrium point will move over time.

同样需要注意的是，分叉并不总是意味着直接竞争关系。正如DNA突变产生了许多从同一遗传树开始的不同生物体，我们可能会看见一个协议成长为 3 个解决不同问题的协议。协议可能会通过拆分和重新绑定其功能，直到达到正确的平衡。而且由于生态系统本身正在不断变化，那么平衡点将随着时间推移而移动。

There are some drawbacks to forking. As with mutations in organisms, forks won’t always be successful. There can also be a loss of network effects — although if the protocols are on the same chain (ex: both built on Ethereum) or connected through future cross-chain systems (ex: Polkadot) there wouldn’t be a complete loss. Finally, there may be some splitting of development resources at the start, although both projects can also pull in new resources over time.

分叉有一些缺点。 与生物中的突变一样，分叉不总是成功的。网络效应也可能会丢失 -- 尽管如果协议位于同一个链路上（例如：建立在Ethereum上）或通过未来的跨链系统进行连接（例如：Polkadot），网络效应就不会完全丧失。最后，在分叉最初阶段可能会造成开发资源的分裂，尽管两个项目都可以随着时间推移带来新的资源。

More generally it’s worth noting that decentralized development is more complicated than building something in a centralized organization at the moment. But I suspect that will continue to shift as decentralized development techniques and incentive structures are refined.

普遍来讲，值得注意的是，分散化的发展比目前在集中式组织中建立一些东西更为复杂。但是，我认为随着分散化发展技术的进步和激励机制的改进，这种情况将会发生转变。

In conclusion, forking is an extremely powerful evolutionary mechanism. For forking to be effective it needs to provide the right incentives for groups to try new paths, which means redistributing tokens in forks to incentivize fork creators.

总之，分叉是一个非常强大的进化机制。为了使分叉切实有效，分叉需要为团体提供正确的激励措施来尝试新的路径，这意味着重新分配代币来激励分叉创建者。

Without it, I suspect we will see more innovator’s dilemma problems as we have seen with Bitcoin, where projects become slow to change out of fear of destroying existing value.

没有它，我怀疑我们会看到更多创新者的困境问题，正如我们从比特币那里看到的那样，由于担心破坏现有价值，项目变化变得缓慢。

With it, blockchain innovation can occur much faster than it currently does and it ever could in Web 2.0 companies.

有了它，区块链创新将能够以更快的速度发生，远超其现有的速度与Web 2.0公司中的速度。

Thanks to Scott Nolan, Joey Krug, and Dan Romero for conversations which lead to this blog post.

感谢与 Scott Nolan, Joey Krug, 和 Dan Romero 的对话，才有了此篇博文。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

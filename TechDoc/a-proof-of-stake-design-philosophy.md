A Proof of Stake Design Philosophy--权益证明设计哲学
------------------------------------------------------

> 本文翻译自：https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)  [Xuming Meng](https://github.com/jonas-meng)
>
> 翻译时间：2017-10-19

---------------------------
Systems like Ethereum (and Bitcoin, and NXT, and Bitshares, etc) are a fundamentally new class of cryptoeconomic organisms — decentralized, jurisdictionless entities that exist entirely in cyberspace, maintained by a combination of cryptography, economics and social consensus. They are kind of like BitTorrent, but they are also not like BitTorrent, as BitTorrent has no concept of state — a distinction that turns out to be crucially important. They are sometimes described as [decentralized autonomous corporations](https://letstalkbitcoin.com/is-bitcoin-overpaying-for-false-security), but they are also not quite corporations — you can’t hard fork Microsoft. They are kind of like open source software projects, but they are not quite that either — you can fork a blockchain, but not quite as easily as you can fork OpenOffice.

像 Ethereum（和 Bitcoin，NXT 和 Bitshares 等）这样的系统本质上是一个新一代的加密经济有机体 - 去中心化的，无管辖的实体，完全存在于网络空间中，通过密码学，经济学和社会共识的结合来维护。他们有点像 BitTorrent，但他们又不像 BitTorrent，因为 BitTorrent 没有状态的概念 - 这是一个至关重要的区别。他们有时被描述为去中心化的自治公司，但他们也不是公司 - 你不能硬分支微软。他们有点像开源软件项目，但是它们也不完全是 - 你可以分叉 blockchain，但是不像你分叉 OpenOffice 那样容易。

These cryptoeconomic networks come in many flavors — ASIC-based PoW, GPU-based PoW, naive PoS, delegated PoS, hopefully soon Casper PoS — and each of these flavors inevitably comes with its own underlying philosophy. One well-known example is the maximalist vision of proof of work, where “the” correct blockchain, singular, is defined as the chain that miners have burned the largest amount of economic capital to create. Originally a mere in-protocol fork choice rule, this mechanism has in many cases been elevated to a sacred tenet — see [this Twitter discussion between myself and Chris DeRose](https://twitter.com/vitalikbuterin/status/687050458301657088) for an example of someone seriously trying to defend the idea in a pure form, even in the face of hash-algorithm-changing protocol hard forks. Bitshares’ [delegated proof of stake](https://bitshares.org/technology/delegated-proof-of-stake-consensus/) presents another coherent philosophy, where everything once again flows from a single tenet, but one that can be described even more simply: [shareholders vote](http://docs.bitshares.org/bitshares/dpos.html).

这些加密经济网络有许多种风格 - 基于 ASIC 的 PoW，基于 GPU 的 PoW，朴素 PoS，PoS，PoC 等等，希望很快就可以使用 Casper PoS，而且每种风格都不可避免地带有自己的基本理念。 一个众所周知的例子就是工作量证明的最大愿景，其中“正确的区块链，单数”被定义为矿工消耗最大的经济资本创造的链条。最初只是一个协议的分叉选择规则，这种机制在许多情况下已经被提升为一个神圣的原则 - 请看我和克里斯·德罗斯之间的这个 Twitter 讨论，一个即使在面对哈希算法改变协议的硬分叉情况下，某人也要认真地来保护这个想法的纯粹形态的例子。Bitshares 的委托权益证明提出了另一个连贯的哲学，其中一切从一个单一的原则出发，但可以被更简单地描述：股东投票。

Each of these philosophies; Nakamoto consensus, social consensus, shareholder voting consensus, leads to its own set of conclusions and leads to a system of values that makes quite a bit of sense when viewed on its own terms — though they can certainly be criticized when compared against each other. Casper consensus has a philosophical underpinning too, though one that has so far not been as succinctly articulated.

每一个共识哲学; 中本聪共识，社会共识，股东投票共识，都有自己的一套结论，并引导了一种从自身的观点来看相当有意义的价值体系 - 虽然互相比较时肯定会受到批评。Capser 共识也有一个哲学基础，尽管迄今为止还没有那么简明扼要。

Myself, Vlad, Dominic, Jae and others all have their own views on why proof of stake protocols exist and how to design them, but here I intend to explain where I personally am coming from.

我自己 (Vitalike Buterin)，Vlad，Dominic，Jae和其他人对于权益证明协议的存在为什么存在和如何设计都有自己的看法，但在这里我打算解释我的观点来自哪里。

I’ll proceed to listing observations and then conclusions directly.

我将会列举所有观察然后直接给出结论。

- Cryptography is truly special in the 21st century because cryptography is one of the very few fields where adversarial conflict continues to heavily favor the defender. Castles are far easier to destroy than build, islands are defendable but can still be attacked, but an average person’s ECC keys are secure enough to resist even state-level actors. Cypherpunk philosophy is fundamentally about leveraging this precious asymmetry to create a world that better preserves the autonomy of the individual, and cryptoeconomics is to some extent an extension of that, except this time protecting the safety and liveness of complex systems of coordination and collaboration, rather than simply the integrity and confidentiality of private messages. Systems that consider themselves ideological heirs to the cypherpunk spirit should maintain this basic property, and be much more expensive to destroy or disrupt than they are to use and maintain.

- 加密技术在21世纪是真正特别的，因为加密技术是对抗性的冲突仍然在很大程度上有利于防御方的极少数领域之一。毁灭城堡比建造更容易，岛屿虽然可以被捍卫的，但仍然可以受到攻击，但普通人的 ECC 秘钥是足够安全到甚至可以防御国家级别的执行人员。网络朋克哲学 (Cyberpunk philosophy) 从根本上是利用这种宝贵的不对称来创造一个更好地保护个人自主权的世界，而密码经济在某种程度上是延伸的，只不过这次保护的是复杂的协调和协作系统的安全和存活，而不是私人信息的完整性和保密性。认为自己是网络朋克精神的正统思想继承的系统应该保持这个基本的属性，并且销毁或破坏的代价要比其使用和维护更高。

- The “cypherpunk spirit” isn’t just about idealism; making systems that are easier to defend than they are to attack is also simply sound engineering.

- “网络朋克精神”不仅仅是理想主义; 构建比起进攻更容易防御的系统也只不过是健全的工程学。

- On medium to long time scales, humans are quite good at consensus. Even if an adversary had access to unlimited hashing power, and came out with a 51% attack of any major blockchain that reverted even the last month of history, convincing the community that this chain is legitimate is much harder than just outrunning the main chain’s hashpower. They would need to subvert block explorers, every trusted member in the community, the New York Times, archive.org, and many other sources on the internet; all in all, convincing the world that the new attack chain is the one that came first in the information technology-dense 21st century is about as hard as convincing the world that the US moon landings never happened. These social considerations are what ultimately protect any blockchain in the long term, regardless of whether or not the blockchain’s community admits it (note that Bitcoin Core does admit this primacy of the social layer).

- 在中长期的时间尺度上，人类相当有共识。 即使对手能够获得无限制的哈希算力，而且对任何重要的区块链发动了51％的攻击，还原了上个月的历史，但是说服了社区，这个链条是合法的，比超越主链的哈希算力更难。他们需要颠覆区块探索者，社区中每个值得信赖的成员，“纽约时报”，archive.org 和互联网上的许多其他来源; 总而言之，说服世界，新的攻击链才是第一条主链在信息技术密集的21世纪和就像说美国的登月从未发生过的一样困难。这些社会学考量会最终长期的保护任何区块链，不管区块链社区是否承认它（请注意，比特币核心承认社会层面的首要地位）。

- However, a blockchain protected by social consensus alone would be far too inefficient and slow, and too easy for disagreements to continue without end (though despite all difficulties, [it has happened](http://www.npr.org/sections/money/2011/02/15/131934618/the-island-of-stone-money)); hence, economic consensus serves an extremely important role in protecting liveness and safety properties in the short term.

- 但是，单靠社会共识来保护的一个区块链将是低效和缓慢的，也很容易让分歧继续下去（尽管如此，它仍然发生了）; 因此，经济共识在短期内对保护活动和安全财产起着非常重要的作用。

- Because proof of work security can only come from block rewards (in Dominic Williams’ terms, it [lacks two of the three Es](https://twitter.com/dominic_w/status/648330685963370496)), and incentives to miners can only come from the risk of them losing their future block rewards, proof of work necessarily operates on a logic of massive power incentivized into existence by massive rewards. Recovery from attacks in PoW is very hard: the first time it happens, you can hard fork to change the PoW and thereby render the attacker’s ASICs useless, but the second time you no longer have that option, and so the attacker can attack again and again. Hence, the size of the mining network has to be so large that attacks are inconceivable. Attackers of size less than X are discouraged from appearing by having the network constantly spend X every single day. I reject this logic because (i) it [kills trees](http://digiconomist.net/beci), and (ii) it fails to realize the cypherpunk spirit — cost of attack and cost of defense are at a 1:1 ratio, so there is no defender’s advantage.

- 由于工作量证明的安全保障只能来自积极的区块奖励（在多米尼克威廉姆斯的条款中，它缺乏三个E中的两个），而对矿工的激励只能来自于他们失去未来区块奖励的风险，工作量证明必然运行在大规模算力对应大量的奖励的逻辑上。从 PoW 攻击中恢复是非常困难的：第一次发生这种情况，您可以用硬盘来改变 PoW，从而使攻击者的 ASIC 无用，但是再次不再有这种选择，所以攻击者可以重复攻击。因此，采矿网络的规模必须如此之大，以致攻击是不可想象的。通过使网络每天不断地消耗X，让小于X的攻击量不在出现。 我拒绝这个逻辑，因为（i）它消耗树木，和（ii）它没有实现网络朋克精神 - 攻击成本和防御成本是1比1，所以没有防守者的优势。

- Proof of stake breaks this symmetry by relying not on rewards for security, but rather penalties. Validators put money (“deposits”) at stake, are rewarded slightly to compensate them for locking up their capital and maintaining nodes and taking extra precaution to ensure their private key safety, but the bulk of the cost of reverting transactions comes from penalties that are hundreds or thousands of times larger than the rewards that they got in the meantime. The “one-sentence philosophy” of proof of stake is thus not “security comes from burning energy”, but rather “security comes from putting up economic value-at-loss”. A given block or state has $X security if you can prove that achieving an equal level of finalization for any conflicting block or state cannot be accomplished unless malicious nodes complicit in an attempt to make the switch pay $X worth of in-protocol penalties.

- 权益证明通过惩罚而不是奖励来确保安全，从而打破这种对称性。验证员将金钱（“存款”）置于股权之中，由于他们锁定资本并且维护节点所以获得少量赔偿，并且采取额外的预防措施来确保其私人钥匙安全，但是大部分恢复交易的成本来自于比他们所获得的奖励大数百或数千倍的惩罚。因此，用一句话来说，权益证明不是“安全来自燃烧能源”，而是“安全来自于经济价值的损失”。一个给定的区块或状态可以具有 $X 安全性，如果您可以证明对于任何冲突区块或状态达到相同级别的终止状态是不可能的，除非恶意节点同时尝试使交换机支付 $X 的协议处罚。

- Theoretically, a majority collusion of validators may take over a proof of stake chain, and start acting maliciously. However, (i) through clever protocol design, their ability to earn extra profits through such manipulation can be limited as much as possible, and more importantly (ii) if they try to prevent new validators from joining, or execute 51% attacks, then the community can simply coordinate a hard fork and delete the offending validators’ deposits. A successful attack may cost $50 million, but the process of cleaning up the consequences will not be that much more onerous than the geth/parity consensus failure of 2016.11.25. Two days later, the blockchain and community are back on track, attackers are $50 million poorer, and the rest of the community is likely richer since the attack will have caused the value of the token to go up due to the ensuing supply crunch. That’s attack/defense asymmetry for you.

- 理论上来说，多数验证者勾结可能会接管一条权益证明区块链，并开始恶意行事。然而，（i）通过巧妙的协议设计，他们这种操纵获得额外利润的能力可以被尽可能地限制，更重要的是（ii）如果他们试图阻止新的验证者加入或执行51％的攻击，那么社区可以简单地组织硬分叉，并删除有罪的验证者的存款。成功的攻击可能花费5000万美元，但清理后果的过程不会比2016年的　geth/parity 一致性失败更加繁重。两天后，区块链和社区回到正轨，攻击者损失5000万美元，其余社区可能更加富有，因为随之而来的供应紧张，攻击将导致代币的价值上升。 这是对于你的攻击/防御不对称。

- The above should not be taken to mean that unscheduled hard forks will become a regular occurrence; if desired, the cost of a single 51% attack on proof of stake can certainly be set to be as high as the cost of a permanent 51% attack on proof of work, and the sheer cost and ineffectiveness of an attack should ensure that it is almost never attempted in practice.

- 上述不应该被认为意味着不定期的硬叉将成为常规事件; 如果需要，在权益证明上的单次51％攻击的开销可以被设定为和在工作量证明上的永久的51％攻击的开销一样，成本和攻击的无效性应确保该攻击在实践中几乎不会发生。

- Economics is not everything. Individual actors may be motivated by extra-protocol motives, they may get hacked, they may get kidnapped, or they may simply get drunk and decide to wreck the blockchain one day and to hell with the cost. Furthermore, on the bright side, individuals’ moral forbearances and communication inefficiencies will often raise the cost of an attack to levels much higher than the nominal protocol-defined value-at-loss. This is an advantage that we cannot rely on, but at the same time it is an advantage that we should not needlessly throw away.

- 经济学不是一切。个人行为者可能受到超常规动机的影响，他们可能被黑客入侵，他们可能被绑架，或者他们可能只是醉酒，并有一天决定用对应的开销来破坏区块链。除此以外，从好的角度来看，个人的道义上的宽恕和沟通效率低下往往会将袭击成本提高到远远高于名义上协议定义的价值损失值。这是我们不能依赖的一个优势，但同时它是一个优势，我们不应该不必要地扔掉。

- Hence, the best protocols are protocols that work well under a variety of models and assumptions — economic rationality with coordinated choice, economic rationality with individual choice, simple fault tolerance, Byzantine fault tolerance (ideally both the adaptive and non-adaptive adversary variants), [Ariely/Kahneman-inspired behavioral economic models](https://www.amazon.ca/Honest-Truth-About-Dishonesty-Everyone-Especially/dp/0062183613) (“we all cheat just a little”) and ideally any other model that’s realistic and practical to reason about. It is important to have both layers of defense: economic incentives to discourage centralized cartels from acting anti-socially, and anti-centralization incentives to discourage cartels from forming in the first place.

- 最好的协议是在各种模型和假设下工作良好的协议 - 经济合理性和协调选择，经济合理性与个人选择，简单容错，拜占庭容错（理想情况是适应性和非适应性对手变体）， 受 Ariely/Kahneman 启发的行为经济模式（“我们都欺骗了一点”），理想情况下现实和实际的任何其他模型。同时具有两层防御是很重要的：经济激励措施阻止中心式合作团体采取反社会行动，反中心化激励措施阻止合作团体的初始形成。

- Consensus protocols that work as-fast-as-possible have risks and should be approached very carefully if at all, because if the possibility to be very fast is tied to incentives to do so, the combination will reward very high and systemic-risk-inducing levels of network-level centralization (eg. all validators running from the same hosting provider). Consensus protocols that don’t care too much how fast a validator sends a message, as long as they do so within some acceptably long time interval (eg. 4–8 seconds, as we empirically know that latency in ethereum is usually ~500ms-1s) do not have these concerns. A possible middle ground is creating protocols that can work very quickly, but where mechanics similar to Ethereum’s uncle mechanism ensure that the marginal reward for a node increasing its degree of network connectivity beyond some easily attainable point is fairly low.

- 快速运行的共识协议是有风险，并且被应该非常仔细地处理，因为如果快速运行的可能性依赖于的激励措施，则这样的组合将产生非常高的系统性风险从而引发的网络级中心化（例如，所有验证器都运行在同一主机提供商上）。 那些不在意验证器发送消息的速度，只要在一段可接受的长时间间隔内（例如4-8秒，因为我们根据经验知道，通常情况下，ethereum 的延迟时间通常为500ms- 1s）的共识协议不会有这些担忧。一个可能的中间地带是创建可以快速运行的协议，但是拥有与 Ethereum 的 uncle 机制类似的机制确保节点增加其网络连接程度超过一些易于达到的点后的边际报酬相当低。

From here, there are of course many details and many ways to diverge on the details, but the above are the core principles that at least my version of Casper is based on. From here, we can certainly debate tradeoffs between competing values . Do we give ETH a 1% annual issuance rate and get an $50 million cost of forcing a remedial hard fork, or a zero annual issuance rate and get a $5 million cost of forcing a remedial hard fork? When do we increase a protocol’s security under the economic model in exchange for decreasing its security under a fault tolerance model? Do we care more about having a predictable level of security or a predictable level of issuance? These are all questions for another post, and the various ways of implementing the different tradeoffs between these values are questions for yet more posts. But we’ll get to it :)

从这里，当然有许多细节和许多方式分歧细节，但上面至少是我理想中 Casper 版本基于的核心原则。从这里，我们当然可以辩论竞争价值之间的权衡。我们是否给予ETH 1％的年发行额，并获得5000万美元的强制补救硬分叉的成本，或0年发行额，并获得500万美元的强制补救硬分叉的成本？ 何时在经济模式下增加协议的安全性，以换取在容错模式下降低其安全性？ 我们更关心拥有可预测的安全级别还是可预测的发行级别？ 这些都是另一篇文章的问题，实现这些价值观之间的不同权衡的各种方法是更多的帖子的问题。 但我们会得到它:)

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

抖抖，在读博士，专注区块链技术研究与行业分析，欢迎加微信号:jonas-meng

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------
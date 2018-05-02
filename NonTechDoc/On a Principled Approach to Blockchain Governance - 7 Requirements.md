### On a Principled Approach to Blockchain Governance - 7 Requirements | 关于区块链治理的原则性方法-7个要求

>本文翻译自：https://steemit.com/eos/@iang/on-a-principled-approach-to-blockchain-governance-7-requirements

>作者：Iang ,  financial cryptographer

>译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [JohnnyJ](https://github.com/BlockchainTranslator/EOS)

>翻译时间：2018-4-18

One of the things that I learnt in the [CAcert adventure](http://iang.org/papers/open_audit_lisa.html)  was that governance was critical to the safe operation of large communities. How large is large ... is a question of much debate, but to put it bluntly, this is needed beyond say a 2 digit size, which I’ve always seen as around 30, but certainly well before [Dunbar’s number of 150](https://en.wikipedia.org/wiki/Dunbar%27s_number).

我在对 [CAcert (一个免费的数字证书颁发组织)](http://iang.org/papers/open_audit_lisa.html)审计过程中学到一件事：社区治理对大型社区的安全运营起着至关重要的作用。多大的社区是大型社区？关于这个问题有很多争论，但是，坦率地讲，社区人数至少要超过2位数。通常，我认为要在30人左右，只要不超过[邓巴数字150](https://en.wikipedia.org/wiki/Dunbar%27s_number)人都是可以的。

Now, the problem with governance is that once it’s in place, it becomes power. And power corrupts. So as technologists we like to try and invent things that take the power back out of the hands of the powerful, the corrupted, and place them into the technology. Tech can’t be corrupted, right? That’s a joke...

现今，治理的问题一旦存在，它就会演变成权力，以及权力的腐败。因此，作为网络技术专家，我们喜欢尝试发明一些方法将权力从那些有影响力的、腐败的人手中收回，用技术解决权力腐败的问题。技术本身无法被腐败，对吧？这个是笑话。

Some might call this decentralisation, but that places a technique to the fore, not the purpose. We don’t decentralise for the sake of it, we do that because we want its benefits, which work sometimes and sometimes not.

有些人称之为权力分散，但是这种说法是把技术放在了首位，而不是技术所要达到的目标。我们并不是为了分散而分散，我们这样做是因为我们希望获得分散带来的好处，权力分散有时候会起作用，有时候不会。

>Principle - Automate what we can, govern the rest 
>原则 - 自动化一切能自动化的事情，管理其余不能自动化的事情

A general principle in life is, what power struggles we can automate, we do, and what’s left over is the responsibility of the governance layer (which I called [layer 5 in FC7](http://iang.org/papers/fc7.html#bup5)). This is a long standing principle, going back to the invention of the chief, the secret ballot, the bribe, and although Bitcoin’s blockchain represents a stunning advance, it is probably only shifting the governance dial by 1% in the historical context.

生活中的一个普遍原则是：我们会自动化那些可以自动化的权利问题，剩下的问题放在治理层（我把这些问题定义为 [FC7中的层级5](http://iang.org/papers/fc7.html#bup5)）。这是一个长期的原则，回溯首席执行官、不记名投票和贿赂的发明，虽然比特币区块链的出现意味着惊人的进步，但是，在历史长河中，它对治理方向的改变可能只有1%的作用。

![Alt text](https://github.com/JohnnyJQ/Image/blob/master/%E6%8D%95%E8%8E%B7.PNG)

By which I’m trying to say: Governance is a thing, and I for one believe that it is an unavoidable thing. Those that are claiming it’s not necessary for e.g., blockchain are IMHO wrong, and there’s stunningly clear evidence of that in the DAO adventure. But I recognise that if you’ve made up your mind on that, and Governance isn’t part of your religious beliefs, that’s fine. You can stop reading and save your time & energy.

据此我想说：治理是一件不可避免的事情。在我看来，那些声称区块链治理没有必要的人是错误的，在去中心化自治组织的探索中有非常明显的证据。但是，我意识到如果你对此已经有了自己的主见，同时，治理并不是你宗教信仰的一部分，那也没关系，你可以停止阅读这篇文章，无需浪费你的时间和精力。

If not, then read on for Requirement #1 of a Principled Blockchain Governance... or if you're done with that, catch up on @dantheman's "How to create a meaningful Blockchain Constitution" and earlier post "Why every Blockchain needs a Constitution"

如果不是，那么请阅读有原则的区块链治理中的要求一，如果你已经阅读过了，可以接着看 Dantheman 的《如何创建一个有意义的区块链宪法》，以及他之前的文章《为什么每个区块链系统都需要一部宪法》。

****

#### Principled Blockchain Governance Requirement #1 - Open Entry | 区块链治理原则性要求一 ： 开放入口

For the rest of the world, if you're still reading from On a Principled Approach to Blockchain Governance - 7 Requirements - the big question then is how we design a governance layer for a blockchain! Let me lay that out with the help of 7 Requirements.

如果你阅读完《关于区块链治理的原则性方法 - 7个要求》，剩下最大的问题是如何给一个区块链系统设计一个治理层！我用7个要求进行阐述。

Let’s start with something simple: we need to allow open entry. Which means you and your sybil mates can join as many times as you have ports on your machine. And do stuff.

让我们从简单的事情开始：我们需要允许开放入口，也就是说，只要你的计算机有端口，你和你的伙伴可以随时加入我们的网络，然后做一些具体的事情。

To make this distinction clear, consider [R3’s Corda](https://docs.corda.net/_static/corda-introductory-whitepaper.pdf), or so-called “permissioned ledgers” in which the reverse to open entry is true - only known and accepted parties are permitted in. This follows from the world of regulated finance, where the banks in essence aren’t allowed to get involved in an unregulated and open entry system.

为了明白其中的区别，以 [R3 Corda](https://docs.corda.net/_static/corda-introductory-whitepaper.pdf) (一种为金融机构量身定做的反区块链的分布式账本)为例，或者称之为“私有账本”，Corda确实预留了公开入口，但是，只有那些知名且被接受的各方可以获得许可进入这个系统，这样的设计参照了受监管的金融世界的规则，在受监管的金融世界里，本质上，银行是不允许参与到一个不受监管且开放入口的系统中的。

In the banking scenario, “we” can’t do it any other way. In contrast, in the open Internet, we, being the other we, have to do it in the open way. By an argument of [reductio ad absurdum](https://en.wikipedia.org/wiki/Reductio_ad_absurdum), if we used a walled garden approach and allowed only known and vetted peoples in, we’d need an authority, who would be regulated, and then we’d need a banking licence. Doh!

在银行场景中，“我们”无法用其他的方式做业务。相比之下，在开放的互联网中，我们，作为另外一群我们，必须以开放的方式来做事。通过[反证法](https://en.wikipedia.org/wiki/Reductio_ad_absurdum)的论证，如果我们使用"给花园筑围墙"的方式，只允许知名且经过审查的人进入系统，我们就需要一个被监管的权威机构，然后，我们需要一个银行执照。哎!

Therefore, we can establish our first requirement:

因此，我们需要确立我们的第一个要求：

>Requirement #1 - Open Entry
>要求一：开放入口

And, watch this space for Requirement #2 in our journey of principles.

接着，请看下面我们在探索治理原则旅程中的要求二。

*****

#### Principled Blockchain Governance Requirement #2 - Toxics not Welcome! | 区块链治理原则性要求二：毒瘤不受欢迎

So open entry it is, if we're to start from a principled position of blockchain governance.

开放入口是区块链治理原则立场的出发点。

But, from that principled position of utter fairness, we hit a problem almost immediately: If we let anyone play then … we get everyone ! Now, the problem with everyone is that statistically this includes some good people and some bad people. When we’re building our community, we’ll pretty soon discover that we don’t actually want everyone. What we’d really like is the nice people, and leave the nasty people out.

但是，从完全公平的原则性立场出发，我们很快会遇到一个问题：如果我们允许任何人都可以参与，那么，就会有各种各样的人！有各种各样人伴随的问题是：从统计学的角度，一定会有一部分好人和一部分坏人。当我们在建设社区的时候，我们很快就会发现，实际上，我们不需要所有的人。我们确切想要的是那些好人，同时，让那些讨厌的人离开。

Where, nice and nasty are definitional challenges of course. Everyone had a mother, and my nasty folk might be your nice folk. To some extent we solve this problem by just allowing them, the nasty ones, to fork the code. But the nasty folk still come in if we succeed with our community, coz, that’s where the value is, right?

当然，好和坏如何定义是很大的挑战。每个人都有自己的母亲，我认为的坏家伙也许是你认为的好家伙。在某种程度上，我们只能允许那些坏家伙通过分叉来解决这个问题。但是，如果我们的社区是成功的，那些坏家伙还是会回来参与到我们的网络中，因为我们的社区拥有价值，不是吗？

Now, this is also a principled position: I want to exclude a certain group which are the criminals. Not because I dislike crime. I do, but rather because crime is toxic. It will destroy the community. We outlined this argument in that very early paper on bitcoin mining, which most people took as “bitcoin must die.” Might have been the title that triggered that response… Either way, let me lay down my requirement.

那么，这同样也是一个原则性立场：我想排除一个特定的群体，罪犯。这样做不是因为我不喜欢犯罪。我确实不喜欢，但更重要的是，犯罪是有害的。犯罪会毁了社区。我们在早期关于比特币挖矿的文章中概述了这个观点，所以很多人认为“比特币必死”。也许这个标题引发了一系列的反应，不管怎样，我要制定我的要求。

>Requirement #2 - Toxics not welcome
>要求二：毒瘤不受欢迎

And if you're still with us, head over for Requirement #3.

如果你一路读到这里，那我们再去看要求三吧。

****

#### Principled Blockchain Governance Requirement #3 - Constitution! |  区块链治理原则性要求三：宪法

The previous requirement #2, Toxics not welcome! left us with a dilemma. We want a community in which we can all deal with each other in a positive fashion, but we know from bitter experience that total openness leads to corruption.

前文的要求二是毒瘤不受欢迎，让我们处于进退两难的境地。我们希望创建一个社区，在这个社区里我们都以一种积极的方式相互对待，但是，我们从痛苦的经验中得知彻底开放会导致腐败。

So how do I exclude the criminals, but allow open entry? The trick to this is to use a self-filtering mechanism, such that the crims don’t want to be there. We do this by contract law, and specifically we set up a contract that makes them vulnerable. Actually it has to make us all vulnerable, because we don’t know who is good and who is toxic until the moment of the dread crime. So it has to be a contract that makes crime harder and valid trade easier.

那么，我如何把罪犯排除在外，同时又允许入口开放？诀窍在于使用一种自我过滤的机制，让罪犯不想待在这样的社区中。我们通过合约法来做这件事情，我专门建立了一种合约让罪犯变得脆弱。事实上，这种合约让所有人都变得脆弱，因为在可怕的犯罪发生之前，我们不清楚谁是好的、谁是有害的。因此，这必须是一种让犯罪更为困难、让有效交易更便捷的合约。

It turns out, this is really easy to do in contracts because we can set up a series of costs. Now, as this is a contract of entry, and it has to be open entry, it has to be a certain special sort of contract which I’ll call a Constitution. That’s not quite correct, but this is a blog post, and we’re making our law but we’re not lawyers, if you appreciate the subtlety here :)

事实证明，这在合约中很容易做到，因为我们可以设置一系列成本。现在，作为代表入口的一个合约，这个合约必须是开放的，这个合约必须是某种特殊的合约，我把这个合约称为“宪法”。如果你能欣赏这里的微妙之处，那么，其实这一称呼并不是非常正确的，但是作为一篇博文，我们在建立我们的“法律”，即便我们不是律师。

>Requirement #3 - Constitution!
>要求三：宪法！

If you like my Constitution you might sign up for it, or maybe you're write a better one and I'll sign up for yours! Either way, we'll have a filtering process where we all agree on what we all think is a good Constitution for our future good trade.

如果你喜欢我的“宪法”，你可以签名支持它，或者，你能写一个更好的“宪法”，我会签名支持你的“宪法”。无论哪种方式，我们都将有一个过滤过程，在这个过程中，对什么是未来诚信交易所需要的好“宪法”，我们都达成了共识。

On that spirited note, head on over to Requirement #4 of this Principled Approach to Blockchain Governance.

基于这条令人鼓舞的记录，我们接着去看区块链治理原则性要求四。

***

#### Principled Blockchain Governance Requirement #4 - Arbitration | 区块链治理原则性要求四：仲裁

Where we left off was Principle #3 - Constitution! which sets the scene.

我们刚才看完了原则性要求三宪法，这个原则性要求设定了治理的基础场景。

But, this only gets us to the point of writing out our position in rules. So I’m going to propose the Constitution for this blog post and lay out my preferred example toxicriminal: Trolls! These people are toxicrims because they take up my time with BS, and they don’t return any value to me. So their troll is my loss. That’s fraud, and in my world, I’m happy to execute the lot ‘o them. In my Constitution, then it is so writ:

但是，这只是让我们在规则中写下了我们的立场。所以，我会在博文中提出“宪法”这个建议，同时，列出我最喜欢的有害犯罪的例子：**网络喷子**。这些人是有害的罪犯，因为他们用废话占用了我的时间，我没有获得任何有价值的回报。所以，网络喷子那些废话所占用的时间就是我们的损失。这些行为是欺诈，在我的世界里，我很乐意把这些喷子锁定隔离。在我的“宪法”中，是这么写的：


>**Article 1 - Death to Trolls**
**第一条 - 网络喷子之死**

Now, note that we have a few issues here. Firstly a choice problem - Your toxicrims could well be different, you might prefer "no mafia" and another might say "no impossibly tall and scary men." All of these things are valid fears! But, to show how this all works, from end to end in 7 principles, bear with me and my rhetorical trolls.

此刻，你会注意到我们有一些问题。首先，一个关于选择问题：那些有害的罪犯可能是形形色色的，你可能更喜欢“没有黑手党”，而另一个人可能会说“不要高得难以置信的吓人的人”。所有这些都是真切的恐惧，为了说明这些恐惧是如何起作用的，请你和我以及那些夸张的喷子一起，完整看完7个原则性要求。


Secondly, now we get into a bit of a definitional problem. As we know a good troll is one who yells Troll! faster than a victim. So it’s me that’s the Troll? Or You? Damn, my defence is turned into an attack on me and I lose. Off with my head?

其次，现在我们开始进入一个定义上的问题。正如我们所知，一个优秀的喷子是一个比那些被喷的人更快输出垃圾的人！所以，我就是那个喷子？或者你？该死，我的辩护变成了对我的攻击，我输了。把我的头砍掉？

Who's to say who's a troll? Me, you or anyone?

谁说谁是喷子？我？你？或者其他任何人？

My community is going to die very quickly, or I am which amounts to the same thing, unless we can answer the trollity of any particular person. I need a defence against this, and I hope y’all agree we ALL need a defence against this. If not, troll, the lotta ya, and I’m outta here!

我所说的都是在表达一个意思：除非我们能回答某个特定的人的喷子特性是什么，要不然我的社区很快就会消亡。我们需要对此进行辩护，我希望大家都同意我们需要对此进行辩护。如果大家不同意，喷子们、各位朋友，我就此离开。

It turns out there is a really tractable defence to the decision problem of who’s the troll and who’s the victim - dispute resolution. And in short, there is a completely good, fair and legal way to do this in our community. It’s called Arbitration. Not only is it legal to set up our own “courts”, it’s backed by most countries in the world, and there are powerful treaties and so forth.

事实证明，对于谁是喷子谁是受害者这个决策问题，有一种易于实现的辩护方式 - 争端解决方案。短期内，可以在我们的社区内用一种完全适合、公平、合法的方式进行辩护。这被称之为仲裁。这不仅是合法建立我们社区“法庭”的方式，也是世界上大多数国家采用的方式，同时，也有很多强有力的条约，等等。

So, to cut this one very short, we have to write our Constitution referring all our disputes to our forum of Arbitration:

所以，简而言之，我们必须参考仲裁论坛中的所有争论点来写我们的宪法：

>Requirement #4 - Arbitration
>要求四：仲裁

Then, when we get into a tiff, we trot off to the forum, and ask for a ruling. Done deal! And we're just about yearning for Principle #5.

那么，当我们陷入争端时，我们快速进入论坛，要求做出裁决。达成一致！然后，我们渴望了解原则性要求五。

***

#### Principled Blockchain Governance Requirement #5 - Consensors are Enforcers | 区块链治理原则性要求五：共识者是执行者

Now, assuming I get my ruling from Principle #4 - Arbitration, and it says “off with the Troll’s head” I have another issue - how do I get it enforced? We all like a good Troll beheading, but who’s actually going to wield the axe? Or Le Guillotine, if we’re modern and French.

现在，我们假设经过原则性要求四仲裁，我得到了裁决结果：把喷子的头砍掉。我就会面对另一个问题：我该如何执行？我们都希望一个真正的喷子被砍头，但是谁来挥舞斧头呢？或者谁提供断头台，如果我们是现代法国人？

**Part I**

**第一部分**

Enforcement of a ruling is something we can do in the courts. One good thing about Arbitration is, assuming we’ve got a good legal and fair forum, that the ruling can be presented to any court in the world that accepts the 1974 New York Treaty on Arbitration. In effect, if I get into a fight in a bar in Dublin with a Londoner, he can pop over the Hague, and get a ruling against me, which can be enforced in my home town in Australia and have my house seized. Bugger.

裁决结果的执行是我们在法庭上可以做的。仲裁的一个优点是：假设我们有一个很好的法律和公平的论坛，裁决可以提交到世界上任何接受1974年纽约仲裁条约的法庭。实际上，如果我在都柏林的酒吧和一个伦敦人打了架，他可以到海牙法庭提出仲裁并得到一个针对我的裁决，这个裁决可以在我的家乡澳大利亚执行，查封我的房子。好家伙！

Now, this is both scary and an opportunity. What global arbitration means is that we have equalised the power of every member against every other member. No longer can someone in one country drag you into a civil case in their local courts - they have to refer it to Arbitration. Any case in your courts gives you an advantage, any case in some foreign court gives that other person an advantage. Indeed, this is practically the only way it can work; the implausibility of foreign courts for an international blockchain means your choice is basically Arbitration or nothing for most people and a brutal weapon for some few rich people.

现在，这种情况既让人感到害怕，又可以说是一次机会。全球性的仲裁意味着我们给到了每一个成员互相对峙的平等权利。不再会有某个国家的某个人因为民事案件将你拖入他们国家当地的法院了，他们必须将其提交总裁。任何在你当地法院处理的案件会给你带来一些便利，任何在国外法院处理的案件会给国外的人带来一些便利。事实上，这是唯一可行的方法，国外法院对一个跨国区块链的不相信意味着你基本上只能选择仲裁，要不然对大多数人来说可能会一无所获，仲裁对少数富人来说是不留情面的武器。

That’s Part I of the question of enforcement - and that comes with the territory of Arbitration, as it's build into the law. But then there’s...

这是裁决执行问题的第一部分，接着是仲裁涉及的领域，这会写入宪法。但是，先看第二部分。

**Part II**

**第二部分**

What happens to the Troll’s value inside the chain? He no longer needs it… so in effect the ruling could award damages to me for being trolled. Let’s say it does. Who’s going to enforce that?

在一个区块链中，喷子的价值会发生什么变化？喷子不再有价值，所以，事实上，裁决可能对作为被喷对象的我造成损害。我们假设裁决确实对作为被喷对象的我造成了损害，那么谁会执行这个裁决？

The ones that do this on a blockchain are the ones that permit or “Validate” the transactions. This might be the miners in PoW blockchain or the Producers or Witnesses or Notaries in some other designs. For sake of a fair term to all blockchains, I’ll call them all Consensors. Which leads to a new requirement:

区块链中执行裁决的是那些允许或者“验证”交易的人。这些人在以工作量证明为共识机制的区块链中就是矿工，在其他一些共识机制设计中是生产者、见证人或者公证人。为了取一个对所有链都公平的名字，我把所有这些人都称为共识者，这就会产生一个新的要求：

>Requirement #5 - Consensors are Enforcers
>要求五：共识者是执行者

If you're happy with the Consensors or Miners or Producers being the Enforcers, then we're ready for Principle #6. Almost done...

如果你对共识者、矿工、生产者成为执行者感到满意，那么，我们准备去看原则性要求六。我们快完成所有要求了...

***

#### Principled Blockchain Governance Requirement #6 - Arms of Governance are Independent | 区块链治理原则性要求六：治理机构相互独立

If you saw Principle #5 - Consensors are Enforcers, you'd realise, we’re not out of the troll woods yet.

如果你阅读了原则性要求五，共识者是执行者，你就会意识到我们还没有走出网络喷子的丛林。

Now, we have two powerful bodies. In competition. Looking for trouble... Believe me.

现在我们已经有了两个强壮的身体：处于竞争和寻找麻烦。相信我。

What happens if one orders the other? Well, that won’t work long run because the one that is more powerful will gradually accrete all the power and that’s where the crims will run. The problem with any anti-criminal power is that this is where the crims go to corrupt the power. Governments, are you listening? Never mind….

如果一方接受另一方的命令会如何？那么，这个机制就不会长久有效，因为拥有更多权力的一方会逐渐将所有权力都纳入手中，这样犯罪就应运而生。问题就在于，任何反犯罪权力都是犯罪分子破坏的对象。政府部门，你们听见了吗？没关系......

So what this means is:

那么这就意味着：

>Requirement #6 - Arms of Governance are Independent
>要求六：治理机构相互独立

OK, so the Arbitrators can issue a ruling, but the Consensors must decide themselves to implement the ruling. If the Consensors decide I cannot also behead my troll and take all his worldly chain wealth, so be it. In this sense, in a blockchain context, the Consensors are now a full arm of the governance, and they perform an appeal process over the Arbitration. Which is nice, because from experience I can tell you that Appeals are rough on friends.

好的，虽然仲裁者可以下一个裁决，但是共识者必须决定他们是否执行这个裁决。如果共识者决定：我不能砍下喷子的头，同时拿走他们所有的财富。那就只好这样。	从这个意义上说，在区块链环境中，共识者们是治理的完整机构，他们在仲裁的过程中提出上诉。这样很好，从经验来看，我可以告诉你，对朋友上述是非常粗暴的行为。

Now we're within a sparrow's breath of Principle #7 and wrapping up this cycle on a Principled Approach to the Blockchain Governance Problem. Another breath, holding, hodling....

现在，我们马上就会进入原则性要求七，以区块链治理的原则性方法一文作为圆满结束。再呼吸一下，稳住，稳住......

****

#### Principled Blockchain Governance Requirement #7 - Community exercises their Democratic voice to set rules | 区块链治理原则性要求七：根据社区成员民主的呼声来制定规则

BUT! We’re still not there because any two poles governance system as described in Principles #6 and before eventually collapses.

但是！我们还没有达到终点，因为，就像在要求六和之前的要求中描述的，任何两极治理系统最终都崩溃了。

That’s because the poles eventually form a pattern where they are equal in some ways and entirely mirrored in other senses, and when they’ve evolved into the Republocrats and the Demipublans, they enter what is known as deadly embrace. And stasis ensues. In other words, the community gets locked in terminal war and dies a long slow torturous death. 

这是因为两极最终形成了一种模式，在这种模式中，在某种程度上，他们是平等的，在另一种程度上，他们是完全一样的，当他们演变成共和党人和民主党人时，他们进入了所谓的死命拥抱状态。停滞不前随之而来。换言之，社区陷入了终极战争，死于漫长而痛苦的折磨。

The solution to this is a third chamber of governance, which creates a three-legged stool effect - strong and stable enough to support a community, but not high enough to lock the community up. And the goto answer here is to have literally that - a chamber of community governance over the various rules and processes. In that chamber, the community can vote on referenda of importance: who can be a Producer, who can be an Arbitrator, what a new rule can be, who gets beheaded, whatever your fancy.

针对这个问题的解决方案是成立一个第三方的治理议院，这就产生了强大而稳定的三脚凳效应，足以支撑一个社区，但是还不足以保护好社区。这里给出的答案，用文字表达就是：成立针对各种规则和流程的社区治理议院。在这样一个议院里，社区成员可以对重要的议题投票：谁成为生产者、谁成为仲裁者、新的规则是什么、谁被踢出社区、以及你喜欢的其他事情。

>Requirement #7 - Community exercises their Democratic voice to set rules
>要求七：根据社区成员民主的呼声来制定规则

We know how to do this - it’s the voting thing from Steem/Bitshares. Basically, you and all of you mates can vote on any issue of importance, and this includes things like changes to the rules and upgrades to the software.

我们知道如何做这件事情，其实就是 Steem/Bitshares 中采用的投票制度。基本上，你和你的所有伙伴都可以对任何重要问题进行投票，包括对规则的修改和软件的升级。

Now we’ve got a stable arrangement like legislature, judiciary, executive. Or, Oceania, Eurasia and Eastasia, if you like your literature. Now we’ve got a governance mesa on which we can trade, build, interact. Safely and securely, to the limits of the system.

现在我们有了一个稳定的安排，比如立法、司法、执行，或者Oceania、Eurasia、 Eastasia，只要你喜欢你取的名字就好。现在我们有了一个可以交易、构建、交互的治理平台。安全地、稳定地将系统运行到极致。

If you like that, let’s do it. Watch out for future developments that employ a Principled Approach to Blockchain Governance. You know you want to...

如果你喜欢这样的系统，我们一起来创建它。见证采用了区块链治理原则性方法的系统未来的发展。你知道你想这么做......

See also @dantheman's How to create a meaningful Blockchain Constitution and earlier post Why every Blockchain needs a Constitution.

你也可以阅读 @dantheman 写的《如何创建一个有意义的区块链宪法》和之前的博文《为什么每个区块链系统都需要一部宪法》。

---

**区块链中文字幕组**

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

**本文译者简介**

金强（JohnnyJ ) 区块链爱好者、投资者，微信：john82king，公众号：时间的朋友时间的力量

本文翻译已获得作者授权。

译文版权所有，转载需完整注明以上内容。

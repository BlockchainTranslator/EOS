>文章来自：https://docs.google.com/document/d/1P6Oz08vNjrJO1H3HmBkuh4BIVm3-0YAe4nqo-xfT4v0/edit
>
>作者：Scatter Team
>
>译者：区块链中文字幕组 Chuan


RIDL --- Scatter’s Reputation and Identity Layer


Abstract: RIDL tokens are a utility token used for reserving unique Identity names across all networks and to provide an ecosystem for reputation.

 摘要：RIDL代币是一种功能性代币，用于保存跨区块链网络的身份名称，为名誉提供一种生态系统。



### Introduction 介绍

Identities and reputations have become a huge factor in the world today. We carry pieces of our Identities in our pocket, build up our reputation both online and offline. They influence what we can do in the real world and the virtual. If you want to buy a home, a car or get health care you need a proven Identity. If you own a business or take part in social media your reputation is up for grabs by anyone who gets to register your name on a new application before you do.

今天，身份和声誉已经成为这个世界上产生巨大影响力的因素。我们口袋里带着各种身份证明，在线上线下建立自己的声望。它们影响着我们在真实世界和虚拟世界中的言行。如果你想买房子、车或者保险，你得要证明你的身份。如果你有自己的事业或者活跃在社交媒体上，那么你的名声就会被人争夺，别人会你之前在新的应用程序上注册了你的名字。

Our Identities and Reputations have become the central pivot points of revolution in our lives and yet they can be stolen and tampered with by someone who is bored.

我们的身份和名誉已经成为我们的生活会发生重大改变的关键要点，然而，它们会被某个无聊的人窃取并篡改。



### What are Identities in Scatter? Scatter中的身份是什么

There are two types of Identities in the Scatter ecosystem, each behaving differently. Let’s take a look at both of them separately to highlight the differences.

Scatter生态系统中有两种类型的身份，每个具有不同的行为方式。我们来看一看两者之间的差异。

#### User Identities 用户身份

These are Identities that belong to a user and exist inside of the Scatter Web Extension or Mobile Application. They are containers that hold confidential information such as EOS accounts, first and last name, email, phone, date of birth, and multiple addresses. They power the user interaction with decentralized applications and provide a user experience that rivals even the best centralized applications while still keeping every piece of information secure and encrypted. Information inside of an Identity must be manually requested by an application at some point for them to be able to use it. No information is ever just given to an application without the user’s explicit consent.

用户身份属于用户，存在于Scatter Web插件或者手机App上。它们包含秘密信息，比如EOS账户，姓名，邮箱，电话号码，出生日期，多个地址。它们让用户有使用DApp的权利，提供给用户甚至媲美最好的中心化应用的体验，同时保证所有的信息安全并被加密处理。对于应用程序来说，它要使用身份中的信息，得要人工发出请求。没有用户的明确同意，任何信息都不能被提供给应用程序。

Private keys never leave Scatter and only the transaction signatures signed with them are ever provided back to applications.

私钥一直保存在Scatter，只有用它们签了名的交易信息才会被提供给应用程序。

Each Identity has a name that is always provided with it and that can act as that Identity’s unique username on applications. This name can be registered with the RIDL system and will then become unique across all networks and irrevocably linked to the Scatter that reserved it. This allows for User Identities to switch out their EOS account while still holding their reputation. If an application enforces the use of Scatter Identity names then no one will be able to take your name if you own it, even if you aren’t on that application or on that network.

每个身份都有个名称，它的作用可以作为在应用程序中那个身份唯一的用户名。这个名称可以使用RIDL系统进行注册，然后成为跨网的通行证，并被链接到保存它的Scatter中。这使得用户身份从EOS账户中切换出来，同时仍然掌握他们的声誉。如果应用程序强迫使用Scatter身份名称，那么如果你拥有它，就没有人能够使用你的名字，即使你不在那个应用程序或那个网络里。

*Scatter users do not have to register an Identity name with RIDL in order to use Scatter, but until they do they will be using a specific subset of randomly generated Identity names such as the first name you would get on Google’s “Play Games” before you change it, for instance.*

*Scatter用户不必为了使用Scatter而要用RIDL来注册一个身份名称，但是，在注册之前他们可以使用随机产生的身份名称集合中的一个，比如，你在Google的“Play Games”中的名字。*

#### Application Identities 应用程序身份

The Identities for applications differ considerably. There is no form of confidential information store. Instead they have only the ability to register a name with RIDL that links back to a contract on an EOS network. This makes sure that a developer with malicious intent can not copy their codebase onto a new network ( or the same network under another account ) and impersonate that application.

应用程序身份在很大程度上与用户身份不同。它们不存储任何的机密信息。相反，它们只能使用RIDL注册一个名称，这个名称指回到EOS网络上的一个合约。这可以确保恶意的开发者不能把他们的代码库拷贝到新的网络（或者另一个账户下的相同的网络），不能模仿那个应用程序的运行。

#### Unique/Reserved Names 唯一的/保留的名称

User Identities gain the ability start using the Reputation System once they have registered their name with RIDL.

一旦用户使用RIDL注册了他们的名称，用户身份获得开始使用名誉系统的能力。

Application Identities may always be given reputation even if they are not registered but can not repute back or gain tokens until they are registered with RIDL. This allows for users to give applications reputation ( such as bad reputation for scammy applications ) even if they are not registered with RIDL.
Identities can only be registered once every 7 days per EOS account / public key.

应用程序身份可能一直被给予声誉，即使它们没有被注册，但是，在通过RIDL注册之前，它们不能回馈赞誉或者获得代币。这允许用户给予应有程序声誉（比如给恶意的应用程序标明为坏名声），即使他们没有使用RIDL进行注册。

每个EOS账户/公钥每7天只能进行一次身份注册。

#### How can Scatter provide unique names across all networks? Scatter如何提供全网上名称的唯一性？

Identities are validated by referring back to the Scatter Endorsed Network ( the network that the RIDL contract lives on, the mainnet for instance ). Because of this if an application is registered on network A, and then created on network B by another user maliciously, Scatter will instantly be able to warn the user browsing that application that it is an impersonation of a real RIDL registered application.

身份通过回指到Scatter Endorsed Network进行验证，这个网络是RIDL合约依托的所在，就是主网的意思）。由于这个原因，如果一个应用程序在A网络上注册，然后另一个用户恶意地在B网络上创建它，那么Sactter会立即警告浏览这个应用程序的用户，这个应用程序是模仿一个真实的RIDL注册过的应用程序。

When Scatter looks up RIDL information it does so internally, and because Scatter runs locally on a machine/phone it can not be tampered with by outside sources such as applications. Applications may also request RIDL information however they must be a registered Identity and have a good standing.

Scatter检查RIDL信息是在内部完成这个操作的，而且因为Scatter运行在本地（个人电脑或手机上），所以它不会被外部的资源篡改，比如应用程序。应用程序也许也会请求使用RIDL信息，然而，它们必须是个注册过的身份，并且拥有一个好信誉。

### The Reputation System 信誉系统

Reputation can be shared between applications and users who have registered with RIDL. User Reputation is global and travels with Identities to all networks however Application Reputation will always only exist on the network it was originally registered on.

信誉可以在应用程序和使用RIDL注册过的用户之间共享。用户信誉是全局性的，它跟身份绑定在一起存在于全网络上，然而，应用程序信誉会一直存在于它最初注册的网络中。

Reputation allows for applications to gauge a user’s likelihood to commit to certain actions such as paying back loans or posting appropriately on a forum. Conversely it also allows for users to gauge the security and usability of applications, for instance whether an exchange is trustworthy and pays out promptly.

信誉允许应用程序评估用户做出某种行为的可能性，比如偿还贷款或者在论坛上发布的内容是合适的。相反，它也允许用户衡量应用程序的安全性和可用性，比如，交易是否值得信赖，是否立刻被处理。

#### Reputing Identities 给身份以信誉

Identities can only repute ( give reputation to ) another Identity if they are of the opposite type. For instance applications can repute users, but they can not repute other applications.

如果身份类型是相反的，那么一个身份可以给另一个身份以信誉。例如，应用程序身份可以对用户身份给予信誉，但是它们不能对其它的应用程序这样做。

*When an Identity reputes another they must spend 1 RIDL Token to do so.*

*当一个身份给另一个身份以信誉时，它们必须花费1个RIDL代币。*

User Identities can only repute an application once. A repute from a user on an application is an inverse operation in the sense that it can be changed at any point in time by applying another token towards that repute but can only be a +1 or a ­1.aa

用户身份只能对应用程序进行一次赞誉。来自于用户对应用程序的赞誉从某种意义上说是相反的操作，即它迟早会在某个时候被使用另外的代币来进行赞誉而改变，但是只能是a+1或1.aa

Application Identities can repute users as much as they want however there must be a 24 hour delay between reputes and they must have a good standing in order to repute users. If at any time they fall below a good standing their ability to repute users will be revoked.

应用程序身份可以按他们所想的给用户赞誉，但是，在两次赞誉之间必须有24小时的间隔，而且为了能够给用户赞誉，它们必须拥有好名声。如果任何时候他们声望下降，他们赞誉用户的能力就会被废除。

#### Tokens held does not equal Reputation 持有的代币并不等同于声望

RIDL tokens must flow through an Identity and not simply sit there. For every token spent on an Identity the Identity reputed takes that token and gains 1 Reputation ( + or ­ ). Each registered Identity can hold at most 100 tokens at any given time.

RIDL代币必须通过身份才能流动。对花在身份上的每个代币，被赞誉的身份接受这个代币，并获得1个或者1个以上的声誉。在任何时候每个注册过的身份可以持有最多100个代币。

Once reaching the token limit that Identity must then spend/transfer their tokens in order to accumulate any more tokens.

一旦达到代币的上限，为了积累更多的代币，身份必须把代币花掉或转让。

Applications can still receive reputation while holding the maximum token amount in order to avoid reputation locking, but Users can not.

为了避免声望锁定，应用程序在持有最大数量代币的同时仍然能够接收赞誉，但是用户身份却不可以。

This causes there to always be movement in the system with applications reputing users and users reputing applications.

这在系统里产生了这样的趋势：应用程序赞誉用户，用户赞誉应用程序。

#### Reputations are partitioned by context按背景对信誉进行区分

The reputation that is given to an entity cannot be a singular binary representation. As such a RIDL implements a partitioned reputation at it’s core. However, specificity is an issue when it comes to the broader perception of reputation.

一个实体获得的赞誉不能是一个单一的二进制表示。正因如此，RIDL在其核心部分实现一个隔离的赞誉设计。然而，说到对信誉更广泛的认识，具体性就成为一个问题。

In order to define the contexts of useful reputation we must look at what makes up the basic traits on both sides of the scale. Different things define reputation as a whole, and the way we perceive an entity.

为了对信誉背景进行定义，我们必须看看这个Scatter两方面的基本特点是由什么组成的。不同的事物把信誉定义为一个整体以及我们作为一个实体的认知方式。

Applications 用户程序

● Security 安全

● Confidentiality 机密

● Competence 能力

● User­Experience 用户体验

Users 用户

● Solvency 债务清偿能力

● Etiquette 行为规范

Trust itself is built from the culmination of all parts of a reputation.

信任本身来自于声望各方面的积累。

#### Reputation Decay 信誉下降

When we talk about reputation it’s important to note that who we once were is not definitive to who we are at this moment in time. Reputations must degrade over time as more reputation flows in which can change the overall perception of who we are. Just because a person didn’t have the ability to pay their bills on time last year doesn’t mean they don’t this year.

我们在谈论信誉时，重要的是要注意到曾经的我们与当前的我们是不一样的。信誉肯定会随着时间而下降，当更多信誉涌现，这可能改变对我们是谁的整体认知。只因为某个人去年没能准时支付账单，并不意味着他们今年不能。

#### Logistic Reputation Standings 具有逻辑性的信誉级别

RIDL uses a logistic growth/decay algorithm for calculating Reputation Standing. Users and applications are able to quickly be defined within the RIDL as either having a Good Standing or a Bad Standing, something which can change quickly back and forth at the beginning but will be much harder to revert as time passes, especially with applications.

RIDL使用逻辑性的增长/衰减算法来计算信誉级别。用户和应用程序能够迅速地在RIDL内被定义为要么是好名声要么是坏名声，它们是某些在一开始被很快地来回改变的东西，但是当时间流逝，它们就将很难恢复，尤其是对应用程序来说。

This also makes it very hard and costly for a single user, a group of users or an application to negatively or positively impact a single Identity. See the section on Sybil Attacks and Reputation Gaming below for more information.

对单个用户，一组用户或者一个应用程序来说，给单一实体好名声或坏名声也是非常难的，而且成本不低。为了了解更多信息，可以看一下下面的女巫攻击和信誉损失部分。

#### Limitations on Transferring and Reputing 对转让和给予赞誉的限制

Identities have two states that can be changed at the request of the Identity. Trading and Reputing. When the Identity’s state changes it is frozen for 24 hours and can not repute, gain reputation, or trade tokens. Once the 24 hour period is up the Identity can then either trade or repute depending on it’s current state.

身份有两种状态，它们能够在身份的请求下被改变。交易和给予赞誉。当身份的状态改变时，它要被冻结24小时，并且不能被赞誉，获得声望或者交易代币。一旦过了24小时，身份能够交易或者赞誉，取决于它当前的状态。

This makes it so that applications and users can not spend and refill their balances quickly by reputing and transferring tokens between accounts and gaming the system.

这就造成应用程序和用户不能快速地通过给予赞誉、在账户间转让代币以及和信誉损失来花费代币并重新让余额中拥有代币。

No reputation is gained from transferring tokens between Identities, and the maximum 100 token limit still applies meaning you can not transfer 100 tokens from two different Identities to the same Identity or they will overflow and only the first transfer will succeed.

信誉不是从身份之间转让代币获得的，而且最大100个代币的限制仍然适用，这意味着你不能从两个不同的身份中转让100个代币给同一个身份， 要不然它们会溢出，并且只有第一个传输会成功。

#### Sybil Attacks and Reputation Gaming 女巫攻击和信誉损失

By only allowing User Identities to repute once per entity and requiring 1 EOS ( governed price ) for RIDL registration the cost of giving an application a high reputation maliciously is 1 EOS*Reputation wanted.

通过只允许用户身份给每个实体赞誉一次，并要求用1个EOS用于RIDL注册，恶意地给一个应用程序很高声望的成本是1个EOS乘以期望的声望值。

It is harder yet to game a user’s reputation because of the limitation of minimum good standing ( initialized at 100, but governed and set on a sliding scale based on averages ) that an application needs in order to repute users. If a malicious actor wanted to give a User Identity 1000 reputation within a 24 hour period they would need to create 1000 applications and then 100,000 users to repute those applications. The cost of RIDL alone would be 101,000 EOS. For maximum reputation that would require 10,000 applications and 1,000,000 users, equaling 1,010,000 EOS. This does not account for the costs of EOS resource staking. The attacker would also instantly be traceable due to the amount of EOS they are moving from their account into these smaller accounts.

然而，损失用户声望更难，由于应用程序为了给用户赞誉而需要的最少好声望的限制（初始是100，但根据平均值以浮动的方式进行调整）。如果一个恶意的家伙想要在24小时的时间内给一个用户身份1000个信誉，他们需要创建1000个应用，其后10万个用户去赞誉那些应用程序。单单RIDL的成本就是101000个EOS。为了能够达到最大的声望，这就需要1万个应用程序和100万个用户，相当于1010000个EOS。这解释不了所投入的EOS的成本。由于攻击者在从自己的账户中将EOS转移到更小的账户，所以他们也会立即能够被追踪到。

Because the RIDL ledger is publicly visible and reputations are displayed any user can flag an Identity if they notice a large amount of fake reputes towards it. After a threshold the Identity will start losing 1 positive reputation for every flag applied. Flags expire after 7 days and can be reapplied.

由于RIDL账簿公开可见，并且信誉被公开显示，任一个用户都能够标出一个需要注意的身份，如果他们注意到这个身份有大量的假的信誉。在这之后，这个身份将会因为每个标注而开始失去1个积极的信誉。7天后，标注失效，并能够被再次使用。

### Airdrop, Reservations, and Auction 空投、保留和拍卖

Scatter is already a live project with integration into a few applications and demos readily available online. We believe the airdrop philosophy that has been introduced into the EOS ecosystem is a solution to a larger problem. ICOs have made the blockchain space a dangerous playground rampant with scam projects that never reach fruition and simply apply a “grab and run” mentality towards the communities that support them. We do not wish to take part in that or even be associated with it.

Scatter已经是个在运行的项目，也整合到一些应用程序，网上可以看到它的演示。我们相信EOS生态系统里引入的空投这一方式解决了个大问题。ICO让区块链世界变得危险，骗局猖獗，一些项目对支持它们的社区采取了“抢了就跑”的行径。我们不希望参与其中，或者与它有任何关联。

Hence we have elected to airdrop RIDL Tokens to every EOS holder using the genesis snapshot that will be released on June 1st. This means that every EOS holding public key in the snapshot will have 40 RIDL tokens waiting for them after an Identity is registered with RIDL. Every registered Identity also receives 10 RIDL tokens as a starting pool as well, both now and in the future.

因此，使用将在6月1号正式运行的创世快照，我们选择空投RIDL代币给每个持有EOS的人。这意味着，在使用RIDL注册一个身份后，快照中持有公钥的每个EOS将获得40个RIDL。每个注册的身份也收到10个RIDL代币作为一个现在和将来使用的启动池。

Identity names can be reserved before EOS mainnet launch. The Identities will be linked to a user provided EOS public key. Multiple Identity names may be bound to a single public key. During the reservation period reserved Identity names will be transferable using the auction at the owners own discretion. At the end of the reservation period public keys will be locked to their current Identity names and irrevocably bound to the public keys associated with them at the time.

在EOS主网正式运行前，身份名称可以被保留。这些身份将被链接到提供了EOS公钥的一个用户。多个身份名称可以被绑定在一个单一公钥上。在保留期内，被保留的身份名称可以在持有者同意后通过拍卖来转让。保留期结束时，公钥将被锁定到他们当前的身份名称上，并且最终绑定到当时与身份名称相关联的公钥上。

Though applications can and should reserve their Identities in order to make sure they have access to their unique names, they will not be airdropped tokens as this would cause both sides to have max tokens and no tokens would be able to be used to repute.

尽管为了确保它们可以拥有对它们唯一的名称的使用权，应用程序可以并且应该保留它们的身份，但是它们不能被空投代币，因为这会引起两方持有最多的代币，并且没有代币能够用来给予赞誉。

Scatter has set up a website to facilitate the reservation and auctioning of Identitiy names. You may visit it at airdrop.scatter­eos.com

Scatter建立了一个网站，来简化身份名称的保留和拍卖的过程。你可以[访问它](airdrop.scatter­eos.com)。



*Some Identity names will be pre­reserved by the Scatter team for key proponents of the network and early bird dapps such as Scatter, RIDL, EOSEssentials, EOSGo, EOSIO, EOS.IO, EOS, Block1, BlockOne, DanLarimer, BrendanBlumer, Everipedia, Carmel, Chintai, TMN, TheMerchantNetwork, EOSTracker, and WalletEOS.*

*有些身份名称将被Scatter团队预留，提供给这个网络的重要支持者和早期支持者，比如Scattter, RIDL，EOSEssentials, EOSGo, EOSIO, EOS.IO, EOS, Block1, BlockOne, DanLarimer, BrendanBlumer, Everipedia, Carmel, Chintai, TMN, TheMerchantNetwork, EOSTracker, 和 WalletEOS。*

***

##### 区块链中文字幕组
致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号：w1791520555。

[点击查看 GITHUB 及更多的译文](https://github.com/BlockchainTranslator/EOS)

##### 本文译者介绍

Chuan，区块链技术爱好者。欢迎加我的微信：youyuxiaochuan

译文版权所有，转载需完整注明以上内容。

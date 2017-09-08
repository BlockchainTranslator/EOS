EOS.IO Technical White Paper -- EOS 技术白皮书
---------------------------------------------
DRAFT: June 5, 2017
翻译：Harvey老狼、谭智勇、宋承根@OracleChain，梓岑@YOYOW
对照整理：何德林

Abstract: 摘要
--------------

The EOS.IO software introduces a new blockchain architecture designed to enable vertical and horizontal scaling of decentralized applications. This is achieved by creating an operating system-like construct upon which applications can be built. The software provides accounts, authentication, databases, asynchronous communication and the scheduling of applications across hundreds of CPU cores or clusters. The resulting technology is a blockchain architecture that scales to millions of transactions per second, eliminates user fees, and allows for quick and easy deployment of decentralized applications.

EOS.IO软件引入了一种新的块链架构，旨在实现分布式应用的性能扩展。这是通过创建一个可以构建应用程序的类似操作系统的架构来实现的。该软件架构提供帐户，身份验证，数据库，异步通信以及在数以百计的CPU或群集上的程序调度。该技术的最终形式是一个块链体系架构，该区块链每秒可以支持数百万个交易，同时普通用户无需支付使用费用。

1.Background 背景
--------------

Blockchain technology was introduced in 2008 with the launch of the bitcoin currency, and since then entrepreneurs and developers have been attempting to generalize the technology in order to support a wider range of applications on a single blockchain platform.

Blockchain技术源于2008年推出的比特币，自那时以来，企业家和开发人员一直在努力推广该技术，以便在单个块链平台上支持更广泛的应用。

While a number of blockchain platforms have struggled to support functional decentralized applications, application specific blockchains such as the BitShares decentralized exchange (2014) and Steem social media platform (2016) have become heavily used blockchains with tens of thousands of daily active users. They have achieved this by increasing performance to thousands of transactions per second, reducing latency to 1.5 seconds, eliminating fees, and providing a user experience similar to those currently provided by existing centralized services.

虽然一些通用区块链平台还在努力实现第一个能正常运行的区块链应用，针对特定场景的区块链应用诸如BitShares去中心化交易所（2014）和Steem社交媒体平台（2016）已经成为日活跃用户上万的成功应用。 这两个应用成功的把性能提高到每秒数千个交易，延迟降低到1.5秒，降低交易费用，并实现了与中央服务器方案相似的用户体验。

Existing blockchain platforms are burdened by large fees and limited computational capacity that prevent widespread blockchain adoption.

由于现有的块链平台使用费用高昂，性能有限，阻碍了区块链应用的广泛传播。

2.Requirements for Blockchain Applications--区块链应用的要求
---------------------------------------------------------

In order to gain widespread use, applications on the blockchain require a platform that is flexible enough to meet the following requirements:
成为一个成功的区块链应用平台块，应该需要满足以下要求：

Support Millions of Users 支持百万级别用户
----------------------------------------

Disrupting businesses such as Ebay, Uber, AirBnB, and Facebook, require blockchain technology capable of handling tens of millions of active daily users. In certain cases, applications may not work unless a critical mass of users is reached and therefore a platform that can handle mass number of users is paramount.

如Ebay，Uber，AirBnB和Facebook这样的应用，需要能够处理数千万日活跃用户的区块链技术。 在某些情况下，应用程序可能无法正常工作，除非达到了大量用户，因此可以处理大量用户数量的平台至关重要。

Free Usage 免费使用
------------------

Application developers need the flexibility to offer users free services; Users should not have to pay in order to use the platform or benefit from its services. A blockchain platform that is free to use for users will likely gain more widespread adoption. Developers and businesses can then create effective monetization strategies.

有时候应用开发人员需要灵活的为用户提供免费服务; 用户不必为了使用平台而付出费用。可以免费使用的块链平台自然可能会得到更多的关注。有了足够的用户规模，开发者和企业可以创建对应的盈利模式。

Easy Upgrades and Bug Recovery 轻松升级和Bug恢复
-----------------------------------------------

Businesses building blockchain based applications need the flexibility to enhance their applications with new features.

基于块链的应用程序在进行功能迭代的时候自然需要能支持软件升级。

All non-trivial software is subject to bugs, even with the most rigorous of formal verification. The platform must be robust enough to fix bugs when they inevitably occur.

所有软件都有可能受到bug的影响。一个区块链底层平台在遭遇bug的时候，需要能够从bug中修复错误。

Low Latency 低延迟
------------------

A good user experience demands reliable feedback with delay of no more than a few seconds. Longer delays frustrate users and make applications built on a blockchain less competitive with existing non-blockchain alternatives.

及时的反馈是良好用户体验的基础。延迟时间如果超过了几秒钟，会大大影响用户体验，严重降低程序的竞争力。

Sequential Performance 串行性能
------------------------------

There are some applications that just cannot be implemented with parallel algorithms due to sequentially dependent steps. Applications such as exchanges need enough sequential performance to handle high volumes and therefore a platform with fast sequential performance is required.

有些应用程序由于命令执行必须是顺序的，从而无法用并行算法进行实现。诸如交易所之类的应用经常需要处理大量的串行操作，因此一个成功的区块链架构需要具有强大的串行性能。

Parallel Performance 并行性能
----------------------------

Large scale applications need to divide the workload across multiple CPUs and computers.

大规模应用程序需要在多个CPU和计算机之间划分工作负载。

3.Consensus Algorithm (DPOS) 共识算法（DPOS）
-----------------------------------------

EOS.IO software utilizes the only decentralized consensus algorithm capable of meeting the performance requirements of applications on the blockchain, Delegated Proof of Stake (DPOS). Under this algorithm, those who hold tokens on a blockchain may select block producers through a continuous approval voting system and anyone may choose to participate in block production and will be given an opportunity to produce blocks proportional to the total votes they have received relative to all other producers. For private blockchains the management will use the tokens to add and remove IT staff.

EOS.IO软件架构中采用目前为止唯一能够复合上述性能要求的区块链共识算（DPOS）。根据这种算法，全网持有代币的人可以通过投票系统来选择区块生产者，一旦当选任何人都可以参与区块的生产。

The EOS.IO software enables blocks to be produced exactly every 3 seconds and exactly one producer is authorized to produce a block at any given point in time. If the block is not produced at the scheduled time then the block for that time slot is skipped. When one or more blocks are skipped, there is a 6 or more second gap in the blockchain.

EOS.IO里预计每3秒生产一个区块。任何时刻，只有一个生产者被授权产生区块。如果在某个时间内没有成功出块，则跳过该块。

Using the EOS.IO software blocks are produced in rounds of 21. At the start of each round 21 unique block producers are chosen. The top 20 by total approval are automatically chosen every round and the last producer is chosen proportional to their number of votes relative to other producers. The selected producers are shuffled using a pseudorandom number derived from the block time. This shuffling is done to ensure that all producers maintain balanced connectivity to all other producers.

EOS.IO架构中区块产生是以21个区块为一个周期。在每个出块周期开始时，21个区块生产者会被投票选出。前20名出块者首选自动选出，第21个出块者按所得投票数目对应概率选出。所选择的生产者会根据从块时间导出的伪随机数进行混合。以便保证出块者之间的连接尽量平衡。

If a producer misses a block and has not produced any block within the last 24 hours they are removed from consideration until they notify the blockchain of their intention to start producing blocks again. This ensures the network operates smoothly by minimizing the number of blocks missed by not scheduling those who are proven to be unreliable.

如果出块者错过了一个块，并且在最近24小时内没有产生任何块，则这个出块者将被删除。这确保了网络的顺利运行。

Under normal conditions a DPOS blockchain does not experience any forks because the block producers cooperate to produce blocks rather than compete. In the event there is a fork, consensus will automatically switch to the longest chain. This metric works because the rate at which blocks are added to a blockchain chain fork is directly correlated to the percentage of block producers that share the same consensus. In other words, a blockchain fork with more producers on it will grow in length faster than one with fewer producers. Furthermore, no block producer should be producing blocks on two forks at the same time. If a block producer is caught doing this then such block producer will likely be voted out. Cryptographic evidence of such double-production may also be used to automatically remove abusers.

在正常情况下，DPOS块链不会经历任何叉，因为块生产者合作生产区块而不是竞争。如果有区块分叉，共识将自动切换到最长的链条。具有更多生产者的区块链长度将比具有较少生产者的区块链增长速度更快。此外，没有块生产者应该同时在两个区块链分叉上生产块。如果一个块生产者发现这么做了，就可能被投票出局。

Transaction Confirmation 交易确认
--------------------------------

Typical DPOS blockchains have 100% block producer participation. A transaction can be considered confirmed with 99.9% certainty after an average of 1.5 seconds from time of broadcast.

由DPOS共识算法维护的区块链一般出块者都是100％在线的。这就是说一个交易平均1.5秒后，会被写入区块链中，同时被所有出块节点知晓这笔交易。这就意味着只需要1.5秒，一笔交易可以认定为99.9％被区块链接收了。

There are some extraordinary cases where a software bug, Internet congestion, or a malicious block producer will create two or more forks. For absolute certainty that a transaction is irreversible, a node may choose to wait for confirmation by 15 out of the 21 block producers. Based on a typical configuration of the EOS.IO software, this will take an average of 45 seconds under normal circumstances. By default all nodes will consider a block confirmed by 15 of 21 producers irreversible and will not switch to a fork that excludes such a block regardless of length.

有一些非常情况下例如，软件bug，Internet拥塞或恶意出块者出现，区块链可能出现分叉。为了确保一个交易是不可逆转的，可以等待15个区块确认。根据EOS.IO软件的配置，在正常情况下15个区块确认平均需要45秒。

It is possible for a node to warn users that there is a high probability that they are on a minority fork within 9 seconds of the start of a fork. After 2 consecutive missed blocks there is a 95% probability a node is on a minority fork. With 3 consecutive missed blocks there is a 99% certainty of being on a minority fork. It is possible to generate a robust predictive model that will utilize information about which nodes missed, recent participation rates, and other factors to quickly warn operators that something is wrong.

在分叉产生的9秒钟内，出块节点就可能发现这个分叉可能并警告用户。一个节点观察网络的时候如果发现连续2次的丢块事件，这意味着改节点由95%可能性在区块链的分叉分支上。有出现3个连续的丢块以后，该节点有99％的可能性在一条分叉出来的区块链上。可以生成一个预测模型，它将利用节点丢失的信息，最近的参与率以及其他因素来快速地警告用户出现什么问题。

The response to such a warning depends entirely upon the nature of the business transactions, but the simplest response is to wait for 15/21 confirmations until the warning stops.

对这种警告的反应完全取决于业务交易的性质，但最简单的反应是等待15/21确认，直到警告停止。

Transaction as Proof of Stake (TaPoS) 交易证明（TaPoS）
-----------------------------------------------------

The EOS.IO software requires every transaction to include the hash of a recent block header. This hash serves two purposes:

EOS.IO软件要求每个交易都包括最近的区块头的哈西。 这个哈希有两个目的：

1. prevents a replay of a transaction on forks that do not include the referenced block; 

2. and signals the network that a particular user and their stake are on a specific fork.

1.防止分叉区块链上出现大量交易记录;
2.使得系统能感知到用户是否在分叉出来的区块链上

Over time all users end up directly confirming the blockchain which makes it difficult to forge counterfeit chains as the counterfeit would not be able to migrate transactions from the legitimate chain.

随着时间的推移，所有用户最终直接确认块链，这使得难以伪造假冒链，因为假冒将无法从合法链路迁移交易。

4.Accounts 帐户
------------

The EOS.IO software permits all accounts to be referenced by a unique human readable name of 2 to 32 characters in length. The name is chosen by the creator of the account. All accounts must be funded with the minimal account balance at the time they are created to cover the cost of storing account data. Account names also support namespaces such that the owner of account @domain is the only one who can create the account @user.domain.

EOS.IO软件允许使用唯一的长度为2到32个字符的可读的名称来实现对帐户的引用。该名称由帐户的创建者自行选择。所有帐户必须在创建时必须充入最小的帐户余额以支付存储帐户数据的费用。帐户名称还支持命名空间，因此帐户@domain的所有者是唯一可以创建帐户@user.domain的用户。

In a decentralized context, application developers will pay the nominal cost of account creation to sign up a new user. Traditional businesses already spend significant sums of money per customer they acquire in the form of advertizing, free services, etc. The cost of funding a new blockchain account should be insignificant in comparison. Fortunately, there is no need to create accounts for users already signed up by another application.

在去中心化的情况下，应用程序开发人员将支付创建帐户名义上的成本以注册新用户。通常企业已经以广告和免费服务等形式为获取每个客户花费了大量资金。相比之下，创建新的区块链帐户所需的资金成本是微不足道的。并且幸运的是，没有必要为已经由另一个应用程序注册的用户创建帐户。

Messages & Handlers -- 消息和消息处理程序
---------------------------------------

Each account can send structured messages to other accounts and may define scripts to handle messages when they are received. The EOS.IO software gives each account its own private database which can only be accessed by its own message handlers. Message handling scripts can also send messages to other accounts. The combination of messages and automated message handlers is how EOS.IO defines smart contracts.

每个帐户可以将结构化消息发送到其他帐户，并且可以定义消息被接受后的处理脚本。EOS.IO软件为每个帐户提供其自己独有的数据库，只能由自己的消息处理程序访问。消息处理脚本还可以向其他帐户发送消息。消息和自动的消息处理程序的组合正是EOS.IO定义智能合约的方式。

Role Based Permission Management -- 基于角色的权限管理
----------------------------------------------------

Permission management involves determining whether or not a message is properly authorized. The simplest form of permission management is checking that a transaction has the required signatures, but this implies that required signatures are already known. Generally authority is bound to individuals or groups of individuals and is often compartmentalized. The EOS.IO software provides a declarative permission management system that gives accounts fine grained and high level control over who can do what and when.

权限管理主要涉及明确特定的消息是否被正确授权。权限管理的最简单形式是检查事务是否具有所需的签名，但这隐含着所需的签名是已知的。通常权力是与可以分类的个人或个人群组绑定在一起的。EOS.IO软件提供了一个声明式权限管理系统，可以让帐户细粒度和高级别地控制谁在何时能够做什么。

It is critical that authentication and permission management be standardized and separate from the business logic of the application. This enables tools to be developed to manage permissions in a general purpose manner and also provide significant opportunities for performance optimization.

至关重要的是，身份认证和权限管理被标准化实现，并与应用程序的业务逻辑分离。这使得开发某种工具以通用方式管理权限成为可能，并为性能优化提供了巨大的空间。

Every account may be controlled by any weighted combination of other accounts and private keys. This creates a hierarchical authority structure that reflects how permissions are organized in reality, and makes multi-user control over funds easier than ever. Multi-user control is the single biggest contributor to security, and, when used properly, it can greatly eliminate the risk of theft due to hacking.

每个帐户都可以通过其他帐户和私钥的任何加权组合来控制。这种机制创建了一个能够真实反映权限在现实中的组织情况的层次化权限结构，并使得多用户对资金的控制比以往任何时候都更容易。多用户控制是提升安全性的最重要因素，如果能正确地使用，可以极大地消除黑客盗窃的风险。

EOS.IO software allows accounts can define what combination of keys and/or other accounts can send a particular message type to another account. For example, it is possible to have one key for a user's social media account and another for access to the exchange. It is even possible to give other accounts permission to act on behalf of a user's account without assigning them keys.

EOS.IO软件允许帐户可以定义与其他帐户密钥的“and”和“or”的组合，并且把这个组合以将特定类型的消息发送到另一个帐户。例如，可以为用户的社交媒体帐号提供一个密钥，另一个用于交易。甚至用户可以给予其他帐户许可让其代表自己的帐户行事，而无需向其他帐户分配密钥。

Named Permission Levels--命名权限级别
-----------------------------------

Using the EOS.IO software, accounts can define named permission levels each of which can be derived from higher level named permissions. Each named permission level defines an authority; an authority is a threshold multi-signature check consisting of keys and/or named permission levels of other accounts. For example, an account's "Friend" permission level can be set for the account to be controlled equally by any of the account's friends.

使用EOS.IO软件，帐户可以定义命名权限级别，每个权限级别可以从更高级别的命名权限派生。每个命名权限级别定义一个权力，这个权力可以是其他帐户的密钥和(/或)命名权限级别组成的多签名检查的阈值。例如，帐户的“朋友”权限级别可以设置为帐户能被其任何朋友帐户平等地控制。

Another example is the Steem blockchain which has three hard-coded named permission levels: owner, active, and posting. The posting permission can only perform social actions such as voting and posting, while the active permission can do everything except change the owner. The owner permission is meant for cold storage and is able to do everything. EOS.IO generalizes this concept by allowing each account holder to define their own hierarchy as well as the grouping of actions.

另一个例子是Steem区块链，其具有三个硬编码命名的权限别：owner，active和posting。P*osting权限只能执行诸如投票和发布等社交行为，而active权限可以做除了更改所有者的所有事情。owner*权限实质是被保留了起来，它能够做所有一切。EOS.IO通过允许每个帐户持有者定义自己的权限层次结构以及动作的分组来实现类似的管理理念。

Named Message Handler Groups -- 命名消息处理程序组
------------------------------------------------

The EOS.IO software allows each account to organize its own message handlers into named and nested groups. These named message handler groups can be referenced by other accounts when they configure their permission levels.

EOS.IO软件允许每个帐户将自己的消息处理程序以命名嵌套的方式予以组织。这些命名的消息处理程序组可以通过配置其权限级别被其他帐户引用。

The highest level message handler group is the account name and the lowest level is the individual message type being received by the account. These groups can be referenced like so: @accountname.groupa.subgroupb.MessageType.

最高级别的消息处理程序组是处理帐户名称的程序组，最低级别的消息处理程序组是处理该帐户正在接收的单独消息类型的程序组。这些程序组的引用格式为：@accountname.groupa.subgroupb.MessageType。

Under this model it is possible for an exchange contract to group order creation and canceling separately from deposit and withdraw. This grouping by the exchange contract is a convenience for users of the exchange.

在这种模式下，可以将创建和取消订单的交易合约与存取款的交易合约分离。这种交易合约的分组对用户使用交易合约提供了较大便利。

Permission Mapping -- 权限映射
-----------------------------

EOS.IO software allows each account to define a mapping between a Named Message Handler Group of any account and their own Named Permission Level. For example, an account holder could map the account holder's social media application to the account holder's "Friend" permission group. With this mapping, any friend could post as the account holder on the account holder's social media. Even though they would post as the account holder, they would still use their own keys to sign the message. This means it is always possible to identify which friends used the account and in what way.

EOS.IO软件允许每个帐户定义任何帐户的命名消息处理程序组与其自己的命名权限级别之间的映射。例如，账户持有人可以将账户持有人的社交媒体应用程序映射到帐户持有者的“朋友”权限组。通过此映射，帐户的任何朋友都可以和帐户持有者一样，在帐户的社交媒体上发布内容。即使他们将作为帐户持有者发布，他们仍然会使用自己的密钥来签名。这意味着总是可以辨别出来哪些朋友以何种方式使用了其帐户。

Evaluating Permissions 权限评估
------------------------------

When delivering a message of type "Action", from @alice to @bob the EOS.IO software will first check to see if @alice has defined a permission mapping for @bob.groupa.subgroup.Action. If nothing is found then a mapping for @bob.groupa.subgroup then @bob.groupa, and lastly @bob will be checked. If no further match is found, then the assumed mapping will be to the named permission group @alice.active.

当从@alice到@bob传送“Action”类型的消息时，EOS.IO软件将首先检查@alice是否为@bob.groupa.subgroup.Action定义了权限映射。如果没有找到任何结果，那么将会检查@bob.groupa.subgroup，然后是@bob.groupa，最后是@bob的映射。如果此时仍然没有找到匹配的结果，那么假定的映射将是命名的权限组@alice.active。

Once a mapping is identified then signing authority is validated using the threshold multi-signature process and the authority associated with the named permission. If that fails, then it traverses up to the parent permission and ultimately to the owner permission, @alice.owner.

一旦识别出权限映射，则启动多签名阈值校验过程。如果校验成功，所命名的权限将与关联的权限建立关联。如果失败，那么它会遍历父权限，最终遍历到其所有者的权限@alice.owner。

Default Permission Groups 默认权限组
-----------------------------------

The technology also allows all accounts have an "owner" group which can do everything, and an "active" group which can do everything except change the owner group. All other permission groups are derived from "active".

该技术还允许所有帐户都有一个可以做所有事情的“owner”权限组，和一个除了更改所有者组之外可以执行所有操作的“active”权限组。所有其他权限组均派生自“active”权限组。

Parallel Evaluation of Permissions 权限的并行评估
-----------------------------------------------

The permission evaluation process is "read-only" and changes to permissions made by transactions do not take effect until the end of a block. This means that all keys and permission evaluation for all transactions can be executed in parallel. Furthermore, this means that a rapid validation of permission is possible without starting the costly application logic that would have to be rolled back. Lastly, it means that transaction permissions can be evaluated as pending transactions are received and do not need to be re-evaluated as they are applied.

权限评估是个“只读”的过程，即使在事务过程中对权限进行了修改，在运行到区块结尾时这种修改也会失效。首先，这意味着所有事务的所有密钥和权限评估可以并行执行。其次，这种机制意味着可以快速验证权限，而不需要考虑启动可能回滚的昂贵的应用程序逻辑。最后，这意味着当挂起的事务继续执行时，事务权限的评估可以继续执行，而无需重新执行。

All things considered, permission verification represents a significant percentage of the computation required to validate transactions. Making this a read-only and trivially parallelizable process enables a dramatic increase in performance.

这么设计考虑的主要原因，是因为权限验证占据交易验证的很大计算量比例。使之成为一个只读和可并行化的过程，可以显着提高性能。

When replaying the blockchain to regenerate the deterministic state from the log of messages there is no need to evaluate the permissions again. The fact that a transaction is included in a known good block is sufficient to skip this step. This dramatically reduces the computational load associated with replaying an ever growing blockchain.

当区块链消息被重放，来从消息日志中重新生成确定状态时，并不需要再次评估权限。事务被包含在一个已知的状态良好的区块中的事实使其可以跳过这个步骤。这极大地减少了重放之前的区块链数据相关的计算量。

Messages with Mandatory Delay 有强制延迟的消息
--------------------------------------------

Time is a critical component of security. In most cases, it is not possible to know if a private key has been stolen until it has been used. Time based security is even more critical when people have applications that require keys be kept on computers connected to the internet for daily use. The EOS.IO software enables application developers to indicate that certain messages must wait a minimum period of time after being included in a block before they can be applied. During this time they can be canceled.

时间是安全的关键组成部分。在大多数情况下，在私钥被使用前不可能知道其是否已经被盗用。基于时间的安全机制在人们使用一些特殊类型应用程序时更为关键，这些应用程序需要将密钥保存在连接到互联网的人们日常使用的计算机上。EOS.IO软件支持应用程序开发者指定某些消息在包含在区块后，实际应用之前必须等待一段比较小的时间段。在此期间，这些消息可以被取消。

Users can then receive notice via email or text message when one of these messages is broadcast. If they did not authorize it, then they can use the account recovery process to recover their account and retract the message.

当这类消息被广播时，用户可以通过电子邮件或短信收到相应通知。如果他们不授权该消息，那么他们可以登录其帐户来还原帐户数据并撤回消息。

The required delay depends upon how sensitive an operation is. Paying for a coffee can have no delay and be irreversible in seconds, while buying a house may require a 72 hour clearing period. Transferring an entire account to new control may take up to 30 days. The exact delays chosen are up to application developers and users.

所需的延迟取决于操作的重要程度。支付一杯咖啡可以毫不拖延地在几秒钟内确认，而买房子可能需要72小时清算周期。将整个帐户转移到新的控制者手上可能最多需要30天。具体延迟的选择取决于应用程序开发者和用户。

Recovery from Stolen Keys 密钥被盗后的恢复
----------------------------------------

The EOS.IO software provides users a way to restore control of their account when their keys are stolen. An account owner can use any owner key that was active in the last 30 days along with approval from their designated account recovery partner to reset the owner key on their account. The account recovery partner cannot reset control of the account without the help of the owner.

EOS.IO软件为用户提供了一种在密钥被盗时恢复其帐户控制的方法。
帐户所有者可以使用在过去30天内活动的任何其批准的帐户恢复合作伙伴的密钥，在其帐户恢复合作伙伴的允许后，重置其帐户上的所有者密钥。在没有帐户所有者的配合情况下，帐户恢复合作伙伴无法重置其帐户的控制权。

There is nothing for the hacker to gain by attempting to go through the recovery process because they already "control" the account. Furthermore, if they did go through the process, the recovery partner would likely demand identification and multi-factor authentication (phone and email). This would likely compromise the hacker or gain the hacker nothing in the process.

对于攻击帐户的黑客而言，由于其已经“控制”该帐户，因此尝试执行恢复过程没有任何收获。此外，如果他们的确进行恢复的过程，那么恢复合作伙伴可能需要身份认证和多因素认证（如电话和电子邮件）。这或者会暴露黑客的身份，或者黑客在恢复过程中毫无所得。

This process is also very different from a simple multi-signature arrangement. With a multi-signature transaction, there is another company that is party to every transaction that is executed, but with the recovery process the agent is only a party to the recovery process and has no power over the day-to-day transactions. This dramatically reduces costs and legal liabilities for everyone involved.

这个过程与简单的多重签名机制有极大的不同。通过多重签名的交易，会有一个对象会执行并参与每一个交易；而通过恢复过程，恢复过程的操作者仅参与了恢复的过程，并没有权力参与日常的交易。这极大降低了相关参与者的成本和法律责任。

5.Deterministic Parallel Execution of Applications -- 应用程序的确定性并行执行
---------------------------------------------------------------------------

Blockchain consensus depends upon deterministic (reproducible) behavior. This means all parallel execution must be free from the use of mutexes or other locking primitives. Without locks there must be some way to guarantee that all accounts can only read and write their own private database. It also means that each account processes messages sequentially and that parallelism will be at the account level.

区块链共识取决于确定性（可重现）行为。这意味着所有并行执行都能不能使用互斥体或其他锁的原语的情况下正常运行。没有锁，必须有一些方法来保证所有帐户只能读写自己的私有数据库。这也意味着每个帐户会顺序处理其消息，并行性确定在帐户级别。

Using the EOS.IO software, it is the job of the block producer to organize message delivery into independent threads so that they can be evaluated in parallel. The state of each account depends only upon the messages delivered to it. The schedule is the output of a block producer and will be deterministically executed, but the process for generating the schedule need not be deterministic. This means that block producers can utilize parallel algorithms to schedule transactions.

使用EOS.IO软件，区块生成器的工作是将消息传递到独立的线程中，以便它们可以并行地评估。每个帐户的状态只取决于传递给它的消息。调度表是区块生成器的输出，并且将被确定性地执行，但是生成调度的过程不必是确定性的。这意味着区块生成器可以利用并行算法来调度事务。

Part of parallel execution means that when a script generates a new message it does not get delivered immediately, instead it is scheduled to be delivered in the next cycle. The reason it cannot be delivered immediately is because the receiver may be actively modifying its own state in another thread.

并行执行还意味着当脚本生成新消息时，它不会立即发送，而是在下一个周期中发送它。无法立即发送的原因是因为接收方可能会在另一个线程中主动修改自己的状态。

Minimizing Communication Latency 通信延迟优化
--------------------------------------------

Latency is the time it takes for one account to send a message to another account and then receive a response. The goal is to enable two accounts to exchange messages back and forth within a single block without having to wait 3 seconds between each message. To enable this, the EOS.IO software divides each block into cycles. Each cycle is divided into threads and each thread contains a list of transactions. Each transaction contains a set of messages to be delivered. This structure can be visualized as a tree where alternating layers are processed sequentially and in parallel.

延迟时间是一个帐户将消息发送到另一个帐户并收到响应所需的时间。EOS.IO软件的目标是使两个帐户能够在单个区块内来回交换消息，而不必在每个消息之间等待3秒。为了实现这一点，EOS.IO软件将每个区块分为周期（cycle）。每个周期分为线程（thread），每个线程包含事务列表。每个事务包含一组要传递的消息。该结构可以被可视化为树，其中各层依据其特性被顺序或者并行地进行处理。

Block

    Cycles (sequential)

      Threads (parallel)

        Transactions (sequential)

          Messages (sequential)

            Receiver and Notified Accounts (parallel)

区块Block
周期Cycles（顺序）
线程Threads（并行）
交易Transactions（顺序）
消息Messages（顺序）
接收方和通知的帐户Receiver and Notified Accounts（并行）

Transactions generated in one cycle can be delivered in any subsequent cycle or block. Block producers will keep adding cycles to a block until the maximum wall clock time has passed or there are no new generated transactions to deliver.

在一个周期中生成的交易可以在任何后续周期或区块中传送。区块生成器将不断把周期添加到区块中，直到最长的区块时间间隔达到，或者没有新的可传送交易生成。

It is possible to use static analysis of a block to verify that within a given cycle no two threads contain transactions that modify the same account. So long as that invariant is maintained a block can be processed by running all threads in parallel.

可以使用区块的静态分析来验证在给定周期内是否存在两个线程包含修改同一个帐户的事务。只要这种静态分析机制一直起作用，就可以通过并行运行所有线程来处理区块。

Read-Only Message Handlers -- 只读消息处理
-----------------------------------------

Some accounts may be able to process a message on a pass/fail basis without modifying their internal state. If this is the case then these handlers can be executed in parallel so long as only read-only message handlers for a particular account are included in one or more threads within a particular cycle.

部分账户可能会处理一些只需要决定通过与否的消息，而不会改变自己内在状态。这种情形下，只需要有一个或多个进程包含这个特殊账户下的只读消息处理器，这些处理就能并行进行。

Atomic Transactions with Multiple Accounts -- 多账户原子交易
----------------------------------------------------------

Sometimes it is desirable to ensure that messages are delivered to and accepted by multiple accounts atomically. In this case both messages are placed in one transaction and both accounts will be assigned the same thread and the messages applied sequentially. This situation is not ideal for performance and when it comes to "billing" users for usage, they will get billed by the number of unique accounts referenced by a transaction.

有时，我们希望确保消息被多个帐户以原子方式交付和接受。在这种情况下，两个消息被放置在一个交易中，两个帐户将被分配相同的线程和消息按顺序执行。这种情况在性能上并不理想，并且当涉及到“付费”用户的使用时，他们将会被根据交易所涉及的特殊帐户的数量来收费。

For performance and cost reasons it is best to minimize atomic operations involving two or more heavily utilized accounts.
出于性能和费用的考虑，最好将涉及两个或更多帐户的原子操作最小化

Partial Evaluation of Blockchain State -- 部分区块链状态评估
----------------------------------------------------------

Scaling blockchain technology necessitates that components are modular. Everyone should not have to run everything, especially if they only need to use a small subset of the applications.

大规模区块链技术组件应该是模块化的。每个人都不应该运行所有东西，特别是如果他们只需要使用一小部分应用程序的时候。

An exchange application developer runs full nodes for the purpose of displaying the exchange state to its users. This exchange application has no need for the state associated with social media applications. EOS.IO software allows any full node to pick any subset of applications to run. Messages delivered to other applications are safely ignored because an application's state is derived entirely from the messages that are delivered to it.

出于将交易状态显示给用户的目的，交易应用的开发者将维护一个完整的节点。这款交易应用不需要与其他社交媒体应用关联状态。EOS.IO系统允许任何完整的节点选择性的运行任意应用子集。传递给其他应用的消息将被安全地忽略，因为应用的状态完全来自于传递给它的消息。

This has some significant implications on communication with other accounts. Most significantly it cannot be assumed that the state of the other account is accessible on the same machine. It also means that while it is tempting to enable "locks" that allow one account to synchronously call another account, this design pattern breaks down if the other account is not resident in memory.

这对于多帐户之间的通信有一些重要的影响。最重要的是，不能假定另一个帐户的状态在同一台机器上是可访问的。它还意味着，虽然允许一个帐户同步调用另一个帐户的“锁”是一种诱人的设计模式，但如果其他帐户不在内存中，这种设计模式将会崩溃。

All state communication among accounts must be passed via messages included in the blockchain.

因此，所有帐户间的状态通信必须通过区块链上的消息进行传递。

Subjective Best Effort Scheduling -- 自主最优任务安排
---------------------------------------------------

The EOS.IO software cannot obligate block producers to deliver any message to any other account. Each block producer makes their own subjective measurement of the computational complexity and time required to process a transaction. This applies whether a transaction is generated by a user or automatically by a script.

EOS.IO系统不能强制阻止区块生成者向其他帐户发送的任何消息。每个区块的生成者对处理交易的计算复杂度和时间复杂度都有自己的主观度量，无论这个交易是由用户生成的还是由脚本自动生成的。

The EOS.IO software provides that at a network level all transactions are billed a fixed computational bandwidth cost regardless of whether it took .01ms or a full 10 ms to execute it. However, each individual block producer using the software may calculate resource usage using their own algorithm and measurements. When a block producer concludes that a transaction or account has consumed a disproportionate amount of the computational capacity they simply reject the transaction when producing their own block; however, they will still process the transaction if other block producers consider it valid.

在网络层面，EOS.IO系统处理的每一笔交易都有固定的计算带宽成本，不管它是耗费01ms还是10 ms来处理它。但是，使用该系统的每个单独的区块生成者会使用它们自己的算法和度量来衡量资源使用。当一个区块生成者发现一个交易或帐户已经消耗了大量的计算能力时，他们会在生成自己的块时拒绝该交易；但是，如果其他区块生成者认为它是有效的，他们仍然会处理该交易。

In general so long as even 1 block producer considers a transaction as valid and under the resource usage limits then all other block producers will also accept it, but it may take up to 1 minute for the transaction to find that producer.

一般来说，只要一个区块生成者认为一个交易是有效的，并且所消耗的资源是可控的，那么其他所有的区块生成者也会接受它，但可能要花费1分钟才能使该交易传播到这个区块生成者处。

In some cases a producer may create a block that includes transactions that are an order of magnitude outside of acceptable ranges. In this case the next block producer may opt to reject the block and the tie will be broken by the third producer. This is no different than what would happen if a large block caused network propagation delays. The community would notice a pattern of abuse and eventually remove votes from the rogue producer.

在某些情况下，区块生成者可以创建一个区块，其中包括在可接受范围之外的交易。在这种情况下，下一个区块生成者可能会选择拒绝这个区块，而这条线路将会被第三个区块生成者终结。这与一个大区块导致网络传播延迟所引发的情况没有什么不同。社区会注意到这种异常模式，并最终清理该流氓区块生成者的选票。

This subjective evaluation of computational cost frees the blockchain from having to precisely and deterministically measure how long something takes to run. With this design there is no need to precisely count instructions which dramatically increases opportunities for optimization without breaking consensus.

这种对计算、资源成本的主观评估将使区块链不必精确地去度量运行一个任务需要多长时间。有了这个设计，就不需要精确地数指令，这将极大地增加优化的机会，而不会打破共识。

6.Token Model and Resource Usage -- 令牌模型和资源使用
--------------------------------------------------

All blockchains are resource constrained and require a system to prevent abuse. With the EOS.IO software, there are three broad classes of resources that are consumed by applications:

所有的区块链都是资源受限的，并且需要一个系统来防止滥用。在EOS.IO系统中，有三大类资源被应用程序消耗:

Bandwidth and Log Storage (Disk);
Computation and Computational Backlog (CPU); and
State Storage (RAM).

1．带宽和日志存储(磁盘)；
2．计算和计算积压(CPU)；
3．状态存储器(RAM)。

Bandwidth and computation have two components, instantaneous usage and long-term usage. A blockchain maintains a log of all messages and this log is ultimately stored and downloaded by all full nodes. With the log of messages it is possible to reconstruct the state of all applications.

瞬时使用和长期使用的这两类组件都会消耗带宽和计算。区块链系统将维护所有消息的日志，这些日志将会被所有的完整节点下载和存储。通过日志信息，可以重构所有应用程序的状态。

The computational debt is calculations that must be performed to regenerate state from the message log. If the computational debt grows too large then it becomes necessary to take snapshots of the blockchain's state and discard the blockchain's history. If computational debt grows too quickly then it may take 6 months to replay 1 year worth of transactions. It is critical, therefore, that the computational debt be carefully managed.

可计债务是指通过对消息日志重新生成状态的计算消耗。如果可技债务增长太大，就有必要对区块链的当前状态进行拍照，并抛弃区块链的历史状态。如果计算债务增长过快，区块链将使用6个月的时间来重放1年的交易。因此，对可计债务进行精心管理是至关重要的。

Blockchain state storage is information that is accessible from application logic. It includes information such as order books and account balances. If the state is never read by the application then it should not be stored. For example, blog post content and comments are not read by application logic so they should not be stored in the blockchain's state. Meanwhile the existence of a post/comment, the number of votes, and other properties do get stored as part of the blockchain's state.

区块链存储的状态指那些可从应用程序逻辑访问的信息。它包括诸如订单和帐户余额等信息。如果应用程序不读取该状态，则不应该存储它。例如，博客文章的内容和注释不被应用程序逻辑读取，因此它们不应该存储在区块链的状态中。与此同时，邮件或评论的索引、投票数和其他属性将作为区块链状态的一部分被存储起来。

Block producers publish their available capacity for bandwidth, computation, and state. The EOS.IO software allows each account to consume a percentage of the available capacity proportional to the amount of tokens held in a 3-day staking contract. For example, if a blockchain based on the EOS.IO software is launched and if an account holds 1% of the total tokens distributable pursuant to that blockchain, then that account has the potential to utilize 1% of the state storage capacity.

区块生成者可以发布它们可用的带宽、计算资源和状态的容量。EOS.IO系统允许每个帐户在一个3天对赌合约中消耗一定比例的可用容量。例如，假设一个基于EOS.IO系统的区块链应用启动，如果一个帐户持有该区块链提供的总令牌的1%，那么这个帐户就有可利用该区块链1%的状态存储容量。

Using the EOS.IO software, bandwidth and computational capacity are allocated on a fractional reserve basis because they are transient (unused capacity cannot be saved for future use). The algorithm used by EOS.IO is similar to the algorithm used by Steem to rate-limit bandwidth usage.

使用EOS.IO系统，带宽和计算能力将被分配到部分储备基础中，因为它们是短暂的(未使用的容量不能存储下来为将来使用)。EOS. IO系统将使用类似于Steem的算法来限制带宽使用速率。

Objective and Subjective Measurements 目标和主观度量
--------------------------------------------------

As discussed earlier, instrumenting computational usage has a significant impact on performance and optimization; therefore, all resource usage constraints are ultimately subjective and enforcement is done by block producers according to their individual algorithms and estimates.

正如前面所讨论的，可度量计算的使用对性能和优化有很大的影响；因此，所有资源的使用限制最终都是主观的，并且根据各自的算法和估计来执行。

That said, there are certain things that are trivial to measure objectively. The number of messages delivered and the size of the data stored in the internal database are cheap to measure objectively. The EOS.IO software enables block producers to apply the same algorithm over these objective measures but may choose to apply stricter subjective algorithms over subjective measurements.

也就是说，从客观角度来说，有些事情是微不足道的。站在客观的角度，传递的消息数量和存储在内部数据库中的数据的大小都是很便宜的。EOS.IO系统允许区块生成者能够在这些客观度量上应用相同的算法，但是也可以在主观度量上选择更严格的主观算法。

Receiver Pays 接收方支付
-----------------------

Traditionally, it is the business that pays for office space, computational power, and other costs required to run the business. The customer buys specific products from the business and the revenue from those product sales is used to cover the business costs of operation. Similarly, no website obligates its visitors to make micropayments for visiting its website to cover hosting costs. Therefore, decentralized applications should not force its customers to pay the blockchain directly for the use of the blockchain.

传统上，它是用来支付办公空间、计算电力以及运营业务所需的其他费用的业务。客户从该业务中购买特定产品，而这些产品的销售收入将用于支付业务成本。同样，没有任何网站要求访问者为维护服务器而支付小额费用。因此，分散的应用程序不应该强迫它的客户直接为使用区块链支付费用。

The EOS.IO software does not require its users to pay directly to the blockchain for its use and therefore does not constrain or prevent t a business from determining its own monetization strategy for its products.

EOS.IO系统不要求用户直接向区块链支付，因此不限制或阻止企业确定其产品的货币化策略。

Delegating Capacity 授权能力
---------------------------

If a blockchain is launched using the EOS.IO software and tokens are held by a holder who may not have an immediate need to consume all or part of the available bandwidth, such holder can choose to give or rent the unconsumed bandwidth to others; the block producers running EOS.IO software will recognize this delegation of capacity and allocate bandwidth accordingly.

如果一个区块链是使用EOS.IO系统开发的，而其令牌是由一个持票人持有，他可能不需要立即消耗全部或部分可用带宽，这样的持有者可以选择将未消耗的带宽给予或租给他人；使用EOS.IO 系统的区块生成者将识别这样的授权并直接分配相应的带宽。

Separating Transaction costs from Token Value -- 将交易成本与令牌价值分开
-----------------------------------------------------------------------

One of the major benefits of the EOS.IO software is that the amount of bandwidth available to an application is entirely independent of any token price. If an application owner holds a relevant number of tokens, then the application can run indefinitely within a fixed state and bandwidth usage. Developers and users are unaffected from any price volatility in the token market and therefore not reliant on a price feed. The EOS.IO software enables block producers to naturally increase bandwidth, computation, and storage available per token independent of the token's value.

EOS.IO系统的主要优点之一是，应用程序可用的带宽完全独立于任何令牌价格。如果应用程序所有者持有相应数量的令牌，那么应用程序可以在固定的状态和带宽使用中持续运行。开发人员和用户不会受到令牌市场价格波动的影响，因此不会依赖于价格。EOS.IO系统运行区块生成者能够自然地增加带宽、计算资源和每个令牌的可用性，这与令牌的价值无关。

The EOS.IO software awards block producers tokens every time they produce the block. The value of the tokens will impact the amount of bandwidth, storage, and computation a producer can afford to purchase; this model naturally leverages rising token values to increase network performance.

EOS.IO系统将奖励那些生成了区块的区块生成者一定的令牌。令牌的值将影响一个区块生成者能够购买的带宽、存储和计算量；这个模型自然会利用上升的令牌价值来提高网络性能。

State Storage Costs 状态存储成本
------------------------------

While bandwidth and computation can be delegated, storage of application state will require an application developer to hold tokens until that state is deleted. If state is never deleted then the tokens are effectively removed from circulation.

因为带宽和计算资源可以被委托，因此应用程序状态的存储要求应用的开发者持有令牌直到该状态被删除。如果状态不被删除，那么令牌将被有效地从循环中删除。

Every user account requires a certain amount of storage; therefore, every account must maintain a minimum balance. As storage capacity of the network increases this minimum required balance will fall.

每个用户帐户需要一定数量的存储空间；因此，每个帐户必须保持最低余额。随着网络存储容量的增加，最低余额的要求将会下降。

Block Rewards 块奖励
-------------------

EOS.IO software awards new tokens to a block producer every time a block is produced. The number of tokens created is determined by the median of the desired pay published by all block producers. The EOS.IO software may be configured to enforce a cap on producer awards such that the total annual increase in token supply does not exceed 5%.

每次生成一个块时，EOS.IO系统都会奖励该区块生成者一个新的令牌。所创建的令牌数量由所有区块生成者所公布的期望报酬的中位数决定。EOS.IO系统可能被配置为限制区块生成者所得奖励上限，这样，令牌供应的年总增长不超过5%。

Community Benefit Applications 社区福利应用
------------------------------------------

In addition to electing block producers, based on the EOS.IO software, users can elect 3 community benefit applications also known as smart contracts. These 3 applications will receive tokens of up to a configured percent of the token supply per annum minus the tokens that have been paid to block producers. These smart contracts will receive tokens proportional to the votes each application has received from token holders. The elected applications or smart contracts can be replaced by newly elected applications or smart contracts by token holders.

除了加入以EOS.IO系统为基础的区块生成者团队，用户还可以选择3个社区福利应用，也称为智能合约。这3个应用程序最多能按配置的比例接收到每年的令牌配额减去已支付给区块生成者的部分。这些智能合约将根据每个应用程序从令牌持有者收到的选票比例来收取令牌。经选举的应用程序或智能合约可以由新当选的应用程序或令牌持有人的智能合约所替代。

7.Governance 治理
---------------

Governance is the process by which people reach consensus on subjective matters that cannot be captured entirely by software algorithms. The EOS.IO software implements a governance process that efficiently directs the existing influence of block producers. Absent a defined governance process, prior blockchains relied ad hoc, informal, and often controversial governance processes that result in unpredictable outcomes.

治理是人们在主观问题上达成共识的过程，而这些问题不可能完全被软件算法所捕获。EOS.IO系统实现了一个治理过程，有效地影响到现有的区块生产商。在被定义治理流程之外，之前的区块链依赖于临时的、非正式的、经常有争议的治理过程，从而导致不可预知的结果。

The EOS.IO software recognizes that power originates with the token holders who delegate that power to the block producers. The block producers are given limited and checked authority to freeze accounts, update defective applications, and propose hard forking changes to the underlying protocol.

EOS.IO系统认识到，治理权力源来自于将权力代理给区块生成者的令牌持有者。区块的生成者被给予有限的和被监督的权限来冻结帐户，更新有缺陷的应用程序，并提出对底层协议的变更。

Part of the EOS.IO software is the election of block producers. Before any change can be made to the blockchain these block producers must approve it. If the block producers refuse to make changes desired by the token holders then they can be voted out. If the block producers make changes without permission of the token holders then all other non-producing full-node validators (exchanges, etc) will reject the change.

EOS.IO系统的一部分是区块生成者的选举。在对区块链进行任何更改之前，这些区块生成者必须批准它。如果区块生成者拒绝做出让令牌持有人所期望的改变，那么他们可以被投票否决。如果区块生成者未经令牌持有者允许进行更改，那么所有其他非生产的全节点验证器(交换器等)将拒绝更改。

Freezing Accounts 冻结账户
--------------------------

Sometimes a smart contact behaves in an aberrant or unpredictable manner and fails to perform as intended; other times an application or account may discover an exploit that enables it to consume an unreasonable amount of resources. When such issues inevitably occur, the block producers have the power to rectify such situations.

有时，智能合约的行为会发生异常或不可预知，无法按照预期执行；有时应用程序或帐户可能发现一个漏洞，使其消耗不合理的资源。当此类问题不可避免地发生时，区块生成者应当有能力纠正这种情况。

The block producers on all blockchains have the power to select which transactions are included in blocks which gives them the ability to freeze accounts. EOS.IO software formalizes this authority by subjecting the process of freezing an account to a 17/21 vote of active producers. If the producers abuse the power they can be voted out and an account will be unfrozen.

所有区块链的区块生成者有权选择哪些交易被包含在区块中，从而使他们有冻结帐户的能力。EOS.IO系统通过冻结一个帐户到17 / 21活跃区块生成者的投票结论中，使这一授权成为正式结论。如果生成者滥用权力，他们可以被淘汰，账户将被解冻。

Changing Account Code -- 改变帐户代码
------------------------------------

When all else fails and an "unstoppable application" acts in an unpredictable manner, the EOS.IO software allows the block producers to replace the account's code without hard forking the entire blockchain. Similar to the process of freezing an account, this replacement of the code requires a 17/21 vote of elected block producers.

当其他一切都失败了，而“不可阻挡的应用程序”以一种不可预知的方式运行时，EOS.IO系统允许区块生成者在不需要硬分叉整个区块链的情况下替换帐户的代码。与冻结帐户的过程类似，此代码的替换需要17 / 21被选中的区块生成者的投票。

Constitution 宪法
----------------

The EOS.IO software enables blockchains to establish a peer-to-peer terms of service agreement or a binding contract among those users who sign it, referred to as a "constitution". The content of this constitution defines obligations among the users which cannot be entirely enforced by code and facilitates dispute resolution by establishing jurisdiction and choice of law along with other mutually accepted rules. Every transaction broadcast on the network must incorporate the hash of the constitution as part of the signature and thereby explicitly binds the signer to the contract.

EOS操作系统可以用区块链技术在签名用户之间建立P2P服务协议或约束性合约，也就是所谓的“宪法”。宪法内容定义了仅依靠代码无法完全执行的用户间义务，同时结合相互间的公认规则，确立司法权和适用法律。每一个在网络中签名广播的交易，其签名信息中必须包含宪法的哈希值，以明确约束合约签名者。

The constitution also defines the human-readable intent of the source code protocol. This intent is used to identify the difference between a bug and a feature when errors occur and guides the community on what fixes are proper or improper.

宪法还定义了源代码协议的人类可读性intent（意图）。当出现系统错误时，intent（意图）可用来区分这个错误是bug还是系统特性，并且判断社区对此的修复措施是否正确。

Upgrading the Protocol & Constitution -- 升级协议和宪法
-----------------------------------------------------

The EOS.IO software define a process by which the protocol as defined by the canonical source code and its constitution, can be updated using the following process:

EOS操作系统使用源代码定义宪法和协议，同时也定义了宪法及协议的更新方法。对宪法或协议进行变更，需要完成以下步骤：

Block producers propose a change to the constitution and obtains 17/21 approval.
Block producers maintain 17/21 approval for 30 consecutive days.
All users are required to sign transactions using the hash of the new constitution.
Block producers adopt changes to the source code to reflect the change in the constitution and propose it to the blockchain using the hash of a git commit.
Block producers maintain 17/21 approval for 30 consecutive days.
Changes to the code take effect 7 days later, giving all full nodes 1 week to upgrade after ratification of the source code.
All nodes that do not upgrade to the new code shut down automatically.

区块生产者（译注：miner/delegate/witness，因此没有译作矿工）提交一个宪法变更动议，并获得17/21以上的赞成票；
区块生产者将17/21以上的赞成票维持连续30天；
要求所有用户都使用新宪法的哈希值确认交易；
区块生产者采用修改源代码的方式反映宪法变更，使用git提交的哈希值将变更提交到区块链上；
区块生产者继续将17/21以上的赞成票维持连续30天；
变更的代码7天后生效，源代码修改通过后，将有1周的时间来对所有节点的进行升级；
所有没有升级为新代码的节点将自动关闭。

By default configuration of the EOS.IO software, the process of updating the blockchain to add new features takes 2 to 3 months, while updates to fix non-critical bugs that do not require changes to the constitution can take 1 to 2 months.

根据EOS操作系统的默认配置，更新区块链来添加新功能这一进程需要2到3个月时间，而修复那些不需要更改宪法的非关键性漏洞需要1到2个月时间。

Emergency Changes 紧急变更
-------------------------

The block producers may accelerate the process if a software change is required to fix a harmful bug or security exploit that is actively harming users. Generally speaking it could be against the constitution for accelerated updates to introduce new features or fix harmless bugs.

面临一个损害用户利益的有害漏洞或安全漏洞时，区块生产者可以加速宪法变更过程。一般来说，加速新特性更新过程或修复无害漏洞，都是违反宪法的行为。

8.Scripts & Virtual Machines 脚本&虚拟机
-------------------------------------

The EOS.IO software will be first and foremost a platform for coordinating the delivery of authenticated messages to accounts. The details of scripting language and virtual machine are implementation specific details that are mostly independent from the design of the EOS.IO technology. Any language or virtual machine that is deterministic and properly sandboxed with sufficient performance can be integrated with the EOS.IO software API.

EOS操作系统将首先作为一个传递账户间已认证信息的平台。脚本语言和虚拟机的实现将独立于EOS操作系统技术，任何开发语言或虚拟机，只要有适当的、性能足够的沙箱，都可以通过API与EOS集成在一起。

Schema Defined Messages --模式定义的消息
---------------------------------------

All messages sent between accounts are defined by a schema which is part of the blockchain consensus state. This schema allows seamless conversion between binary and JSON representation of the messages.

在账户之间发送的所有消息都是由区块链共识状态的一个模式定义的，该架构允许消息在二进制和JSON格式之间的无缝转换。

Schema Defined Database -- 模式定义的数据库
------------------------------------------

Database state is also defined using a similar schema. This ensures that all data stored by all applications is in a format that can be interpreted as human readable JSON but stored and manipulated with the efficiency of binary.

数据库状态也使用类似的模式定义，这确保所有应用程序存储的数据都以一种格式呈现，同时具备JSON的人类可读性，以及二进制格式的高效率存储和易操作性。

Separating Authentication from Application - 将身份验证与应用程序分离
-------------------------------------------------------------------

To maximize parallelization opportunities and minimize the computational debt associated with regenerating application state from the transaction log, EOS.IO separates validation logic into three sections:

为了最大化并行运算，同时将从程序日志中重新生成应用程序状态的计算任务降至最低，EOS操作系统将验证逻辑分为三个部分:

Validating that a message is internally consistent;
Validating that all preconditions are valid; and
Modifying the application state.

确认消息在内部是一致的;
确认所有的前置条件都是有效的;
修改应用程序状态。

Validating the internal consistency of a message is read-only and requires no access to blockchain state. This means that it can be performed with maximum parallelism. Validating preconditions, such as required balance, is read-only and therefore can also benefit from parallelism. Only modification of application state requires write access and must be processed sequentially for each application.

验证消息的内部一致性是只读的，不需要访问区块链状态，这意味着它可以最大化并行运算来执行。验证前置条件（例如需求平衡）也是只读的，因此也可以从并行运算中获益。只有对应用程序状态进行修改才需要写访问，并且需要按顺序对每个应用程序进行处理。

Authentication is the read-only process of verifying that a message can be applied. Application is actually doing the work. In real time both calculations are required to be performed, however once a transaction is included in the blockchain it is no longer necessary to perform the authentication operations.

身份验证是验证消息是否可以应用的只读过程，应用程序实际上就是在做这项工作。实时的计算都需要执行，但交易一旦被包含在区块链中，就不再需要执行身份验证操作了。

Virtual Machine Independent Architecture -- 虚拟机独立架构
---------------------------------------------------------

It is the intention of the EOS.IO software that multiple virtual machines can be supported and new virtual machines added over time as necessary. For this reason, this paper will not discuss the details of any particular language or virtual machine. That said, there are two virtual machines that are currently being evaluated for use within EOS.IO.

这是EOS操作系统软件的目的是可以支持多种虚拟机，同时可以随着时间推移持续按需求增加新的虚拟机。出于这个原因，本文不会讨论任何特定语言或虚拟机的细节，但即便如此，目前也已经有三种虚拟机正在评估接入EOS系统。

Web Assembly (WASM)  Web组件(WASM)
---------------------------------

Web Assembly is an emerging web standard for building high performance web applications. With a few small modifications Web Assembly can be made deterministic and sandboxed. The benefit of Web Assembly is the widespread support from industry and that it enables contracts to be developed in familiar languages such as C or C++.

WASM是构建高性能Web应用程序的新兴Web标准，通过少量适配就可以被明确定义和沙箱化。WASM的好处在于业界广泛支持，因此可以用熟悉的语言开发开发智能合约，例如C或C++。

Ethereum developers have already begun modifying Web Assembly to provide suitable sandboxing and determinism in with their Ethereum flavored Web Assembly (WASM). This approach can be easily adapted and integrated with EOS.IO software.

以太发人员已经开始适配WASM，以提供适当的沙箱并使用以太坊WASM定义(https://github.com/ewasm/design)。这种方法很容易改编后用于EOS系统软件集成。

Ethereum Virtual Machine (EVM) 以太虚拟机(EVM)
---------------------------------------------

This virtual machine has been used for most existing smart contracts and could be adapted to work within an EOS.IO blockchain. It is conceivable that EVM contracts could be run within their own sandbox inside an EOS.IO blockchain and that with some adaptation EVM contracts could communicate with other EOS.IO blockchain applications.

这个虚拟机已经被用于大多数现有的智能合约，并且可以在EOS系统区块链上使用。可以想象，在EOS操作系统区块链上，EVM合约可以在内部沙箱中运行，只需要少量适配就可以与其他EOS应用程序交互。

9.Inter Blockchain Communication 跨链交互
--------------------------------------

EOS.IO software is designed to facilitate inter-blockchain communication. This is achieved by making it easy to generate proof of message existence and proof of message sequence. These proofs combined with an application architecture designed around message passing enables the details of inter-blockchain communication and proof validation to be hidden from application developers.

EOS操作系统旨在促进区块链间的跨链交互，这是通过简化消息存在证明和消息序列证明来实现的。这些证明与围绕信息传送的应用架构设计相结合，同时可以隐藏跨链交互和验证的细节，避免向应用程序开发人员公开。

Merkle Proofs for Light Client Validation (LCV) --用于轻客户端验证的默克尔证明(LCV)
--------------------------------------------------------------------------------

Integrating with other blockchains is much easier if clients do not need to process all transactions. After all, an exchange only cares about transfers in and out of the exchange and nothing more. It would also be ideal if the exchange chain could utilize lightweight merkle proofs of deposit rather than having to trust its own block producers entirely. At the very least a chain's block producers would like to maintain the smallest possible overhead when synchronizing with another blockchain.

要更容易地与其他区块链集成，对于客户端而言最好是不需要处理全部的交易。毕竟，一个交易所关心的不过只是入账和出账操作。更进一步而言，一个更加理想的状态是，对于交易所自身所维持的链来说，如果可以将轻量级的默克尔存款证明应用其中，那么就不必完全依赖全节点矿工，全节点矿工同步时也能维持尽可能小的开销。

The goal of LCV is to enable the generation of relatively light-weight proof of existence that can be validated by anyone tracking a relatively light-weight data set. In this case the objective is to prove that a particular transaction was included in a particular block and that the block is included in the verified history of a particular blockchain. 
 
LCV的目标是能产生相对轻量级的交易存在证明，并且该证明能被其他人通过跟踪一个轻量级数据集进行验证。既然如此，目的就是证明一个特定的交易是被一个特定的区块包含其中，并且这个区块是被包含在已经验证的特定区块链历史中。

Bitcoin supports validation of transactions assuming all nodes have access to the full history of block headers which amounts to 4MB of block headers per year. At 10 transactions per second, a valid proof requires about 512 bytes. This works well for a blockchain with a 10 minute block interval, but is no longer "light" for blockchains with a 3 second block interval.  

比特币的轻量级验证方式是，假设所有节点都有读取区块头数据完整记录的能力。而区块头数据每年增长4MB， 假设每秒产生10笔交易，一个有效的证明需要512 bytes，这对于一个出块时间为10分钟的区块链来说是可行的。但对于一个出块时间为3秒的区块链来说则远远不够。

The EOS.IO software enables lightweight proofs for anyone who has any irreversible block header after the point in which the transaction was included. Using the hash-linked structure shown below it is possible to prove the existence of any transaction with a proof less than 1024 bytes in size.  If it is assumed that validating nodes are keeping up with all block headers in the past day (2 MB of data), then proving these transactions will only require proofs 200 bytes long.

EOS操作系统的轻量级证明只需要验证包含某个特定的不可逆交易之后的区块头数据，使用哈希链表架构（如下图），数据集可以保持在1024 bytes内，即可证明任何一个交易是否存在。这是基于验证节点保留着前一天的所有区块头数据（2 MB大小)，然后证明这些交易只需要200 bytes大小的证明数据。

There is little incremental overhead associated with producing blocks with the proper hash-linking to enable these proofs which means there is no reason not to generate blocks this way.

当生成区块时候使用合适的哈希链表时，使用这种方法只会带来很小的增量开销，这意味着没有理由不以这种方式去生成区块。

When it comes time to validate proofs on other chains there are a wide variety of time/ space/ bandwidth optimizations that can be made. Tracking all block headers (420 MB/year) will keep proof sizes small.  Tracking only recent headers can offer a trade off between minimal long-term storage and proof size. Alternatively, a blockchain can use a lazy evaluation approach where it remembers intermediate hashes of past proofs. New proofs only have to include links to the known sparse tree. The exact approach used will necessarily depend upon the percentage of foreign blocks that include transactions referenced by merkle proof.

当与其他链验证证明的时候，时间、空间和带宽都有很大的优化空间。跟踪所有区块头数据(420 MB/年)可以使证明体积尽可能小。只跟踪最近的区块头可以使得在持久区块头数据保存体积以及证明体积之间获得平衡。同样的一个区块链可以“懒惰地”只记录过去数据的哈希值作为之前数据的证据，新证明只需要保留已知的sparse tree（稀疏树）结构，具体的方法会视乎于外部区块所占的默克尔证明所包含的交易比例。

After a certain density of interconnectedness it becomes more efficient to simply have one chain contain the entire block history of another chain and eliminate the need for proofs all together. For performance reasons, it is ideal to minimize the frequency of inter-chain proofs.

在链与链之间经过一定密度的相互关联之后。他们将会变得越来越高效。一条链可能会包含另外一条链的全部历史记录，那么就不再需要互相证明。从性能的角度来说，这将极大地减少链间互相证明操作的频率。

Latency of Interchain Communication 跨链通信延迟
-----------------------------------------------

When communicating with another outside blockchain, block producers must wait until there is 100% certainty that a transaction has been irreversibly confirmed by the other blockchain before accepting it as a valid input. Using EOS.IO software and DPOS with 3 second blocks and 21 producers, this takes approximately 45 seconds. If a chain's block producers do not wait for irreversibility it would be like an exchange accepting a deposit that was later reversed and could impact the validity of the a chain's consensus.

与其他区块链通信的时候，矿工必须等待其他区块链不可逆地确认之后才会接受其为有效的输入。使用EOS系统软件，凭借出块时间为秒的委任权益证明以及21个矿工，这大概只需要45秒的确认时间。如果某个链上的矿工不等到交易确认，就像一个交易所接受了一笔存款而后又撤销这笔操作，这会影响这条链共识的有效性。

Proof of Completeness -- 完成证明
--------------------------------

When using merkle proofs from outside blockchains, there is a significant difference between knowing that all transactions processed are valid and knowing that no transactions have been skipped or omitted. While it is impossible to prove that all of the most recent transactions are known, it is possible to prove that there have been no gaps in the transaction history. The EOS.IO software facilitates this by assigning a sequence number to every message delivered to every account. A user can use these sequence numbers to prove that all messages intended for a particular account have been processed and that they were processed in order.

使用外部区块链的默克尔证明时，知道所有已处理的交易是有效的和知道有没有交易被忽略，这两者之间有巨大的不同。因为不可能证明所有最近交易是已知的，但有可能证明历史交易数据之间没有缺失。EOS操作系统通过分配一个顺序的标识编号给每一笔到达账户的信息来完成这个功能，用户可以使用这些标号来证明所有给这个账号的消息已经被处理并且是被按顺序处理的。

10.Conclusion 结论
--------------

The EOS.IO software is designed from experience with proven concepts and best practices, and represents fundamental advancements in blockchain technology. The software is part of a holistic blueprint for a globally scalable blockchain society in which decentralized applications can be easily deployed and governed.

EOS操作系统是基于经过普遍证实、并通过长期实践考验的概念来设计的，代表着区块链技术的根本性进步。它是可扩展的全球性区块链社会的宏伟蓝图的一部分 ，分布式应用程序可以轻松地以此为环境开发和管理。

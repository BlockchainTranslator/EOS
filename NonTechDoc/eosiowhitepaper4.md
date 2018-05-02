# Token Model and Resource Usage 代币模型和资源使用

**PLEASE NOTE: CRYPTOGRAPHIC TOKENS REFERRED TO IN THIS WHITE PAPER REFER TO CRYPTOGRAPHIC TOKENS ON A LAUNCHED BLOCKCHAIN THAT ADOPTS THE EOS.IO SOFTWARE. THEY DO NOT REFER TO THE ERC-20 COMPATIBLE TOKENS BEING DISTRIBUTED ON THE ETHEREUM BLOCKCHAIN IN CONNECTION WITH THE EOS TOKEN DISTRIBUTION.**

请注意：这份白皮书中提到的加密代币指的是采用EOS.IO软件的区块链的加密代币。它们并不是指分发于以太坊区块链上的兼容ERC-20的代币。

All blockchains are resource constrained and require a system to prevent abuse. With a blockchain that uses EOS.IO software, there are three broad classes of resources that are consumed by applications:

所有的区块链都是资源有限的，要求系统能够防止资源的滥用。对于使用EOS.IO软件的区块链，有三种重要的、被应用程序消耗的资源：

1. Bandwidth and Log Storage (Disk); 带宽和日志存储（磁盘）
2. Computation and Computational Backlog (CPU); and 计算能力和计算量的积压（CPU）
3. State Storage (RAM). 状态存储（RAM）

Bandwidth and computation have two components, instantaneous usage and long-term usage. A blockchain maintains a log of all Actions and this log is ultimately stored and downloaded by all full nodes. With the log of Actions, it is possible to reconstruct the state of all applications.

带宽和计算能力包括两部分，及时使用和长期使用。区块链保存一个所有操作的日志，这个日志最终被所有的全节点存储并下载。利用这个操作日志，能够重构所有应用程序的状态。

The computational debt is calculations that must be performed to regenerate state from the Action log. If the computational debt grows too large then, it becomes necessary to take snapshots of the blockchain's state and discard the blockchain's history. If computational debt grows too quickly then it may take 6 months to replay 1 year worth of transactions. It is critical, therefore, that the computational debt be carefully managed.

算力负债指的是那些必须被执行用来从操作日志中重新产生状态的运算。如果算力负债增长地太大，就有必要对区块链的状态执行快照，放弃保存区块链的历史记录。如果算力负债增长地太快，那么可能需要6个月的时间来重放相当于1年的交易。因此，算力负债应该被仔细地管理是至关重要的。

Blockchain state storage is information that is accessible from application logic. It includes information such as order books and account balances. If the state is never read by the application, then it should not be stored. For example, blog post content and comments are not read by application logic, so they should not be stored in the blockchain's state. Meanwhile the existence of a post/comment, the number of votes, and other properties do get stored as part of the blockchain's state.

区块链状态存储指的是一些可以从应用逻辑层获取的信息。它包含如图书订单和账户余额的信息。如果这个状态从来没有被应用程序读取过，那么它就不应该被存储。例如，应用逻辑不读取博客文章的内容和评论，所以这些内容就不应该存储在区块链的状态中。同时，文章或评论的存在，投票，以及其他的属性要被存储为区块链状态的一部分。

Block producers publish their available capacity for bandwidth, computation, and state. The EOS.IO software allows each account to consume a percentage of the available capacity proportional to the amount of tokens held in a 3-day staking contract. For example, if a blockchain based on the EOS.IO software is launched and if an account holds 1% of the total tokens distributable pursuant to that blockchain, then that account has the potential to utilize 1% of the state storage capacity.

区块生产者发布它们在带宽、算力和状态方面的可用量情况。EOS.IO软件允许每个账户消耗一定比例的可用量，这个用量与3日数字协议中包含的代币量是成比例的。例如，如果以EOS.IO软件为基础的区块链正式运行，一个账户持有分发的代币总量的1%，那么这个账户有潜力利用到状态存储容量的1%。

Adopting the EOS.IO software on a launched blockchain means bandwidth and computational capacity are allocated on a fractional reserve basis because they are transient (unused capacity cannot be saved for future use). The algorithm used by EOS.IO software is similar to the algorithm used by Steem to rate-limit bandwidth usage.

在落地的区块链应用中采用EOS.IO软件，意味着带宽和算力的大小被分配在少量的预留基础上，因为它们是转瞬即逝的（没有被使用的并不会保存下来待用）。EOS.IO软件使用的算法类似于Steem使用的算法，它采用了等级限制的带宽使用方法。

## Objective and Subjective Measurements 客观评估和主观评估

As discussed earlier, instrumenting computational usage has a significant impact on performance and optimization; therefore, all resource usage constraints are ultimately subjective, and enforcement is done by block producers according to their individual algorithms and estimates. These would typically be implemented by a block producer via the writing of a custom plugin.

正如之前的讨论，计算能力对性能和优化有非常重要的影响；因此，所有的资源使用受限最终都是主观的，并且根据区块生产者自己的算法和估计由他们来强制执行。这些一般通过定制的插件由区块生产者来实现。

That said, there are certain things that are trivial to measure objectively. The number of Actions delivered, and the size of the data stored in the internal database are cheap to measure objectively. The EOS.IO software enables block producers to apply the same algorithm over these objective measures but may choose to apply stricter subjective algorithms over subjective measurements.

这就是说，有一些东西对做出客观地评估是无足轻重的。提交的操作指令数量，存储在内部数据库的数据大小对客观评估都是可以忽略的。EOS.IO软件让区块生产者运用相同的算法来进行客观评估，但是也可能选择使用更严格的主观算法来做出主观的评估。

## Receiver Pays 接收方付费

Traditionally, it is the business that pays for office space, computational power, and other costs required to run the business. The customer buys specific products from the business and the revenue from those product sales is used to cover the business costs of operation. Similarly, no website obligates its visitors to make micropayments for visiting its website to cover hosting costs. Therefore, decentralized applications should not force its customers to pay the blockchain directly for the use of the blockchain.

传统上，企业要为办公场地、计算能力和其它所需的运营成本付费。顾客从企业那里购买具体的商品，从这些商品中获得的收入用来支付企业运营成本。同样地，没有网站强迫游客为浏览它们的网站付一点钱来抵消运行网站的成本。因此，去中心化的应用不应该强迫用户要为使用区块链而为区块链付费。

A launched blockchain that uses the EOS.IO software does not require its users to pay the blockchain directly for its use and therefore does not constrain or prevent a business from determining its own monetization strategy for its products.

一个使用EOS.IO软件的正式运行的区块链不会要求它的用户因为使用区块链而为区块链付费，因此，它也不能限制或阻碍企业为自己的商品确定创收策略。

While it is true that the receiver can pay, EOS.IO enables the sender to pay for bandwidth, computation, and storage. This empowers application developers to pick the method that is best for their application. In many cases sender-pays significantly reduces complexity for application developers who do not want to implement their own rationing system. Application developers can delegate bandwidth and computation to their users and then let the “sender pays” model enforce the usage. From the perspective of the end user it is free, but from the perspective of the blockchain it is sender-pays.

尽管是接收方付费，但是EOS.IO让发送方要为带宽、算力和存储付费。这让应用开发人员选择最适合他们应用程序的方法。在许多情况下，发送方付费的方式为应用开发人员极大地降低复杂度，他们不想自己来实现资源配给系统。应用开发人员能够分配带宽和算力给他们的用户，然后让“发送方付费”模型强制执行这一使用。从终端用户的角度来看，它是免费的，但是，从区块链的角度来看，这是发送方付费。

## Delegating Capacity 出租可用资源

A holder of tokens on a blockchain launched adopting the EOS.IO software who may not have an immediate need to consume all or part of the available bandwidth, can delegate or rent such unconsumed bandwidth to others; the block producers running EOS.IO software on such blockchain will recognize this delegation of capacity and allocate bandwidth accordingly.

采用EOS.IO软件的区块链，它的代币持有者可能并不需要立刻消耗所有或部分的可用带宽，他可以分配或者出租没有消耗的带宽给其他人；运行EOS.IO软件的区块生产者将认清这些资源的委托情况，并相应地分配带宽。

## Separating Transaction costs from Token Value 从代币价值中分离交易成本

One of the major benefits of the EOS.IO software is that the amount of bandwidth available to an application is entirely independent of any token price. If an application owner holds a relevant number of tokens on a blockchain adopting EOS.IO software, then the application can run indefinitely within a fixed state and bandwidth usage. In such case, developers and users are unaffected from any price volatility in the token market and therefore not reliant on a price feed. In other words, a blockchain that adopts the EOS.IO software enables block producers to naturally increase bandwidth, computation, and storage available per token independent of the token's value.

EOS.IO软件主要的优势之一是：应用程序可用的带宽大小完全独立于代币的价格。如果应用程序所有者持有相关的一些代币，那么这个应用能够在固定的状态和固定的带宽下无限地运行。这样的话，开发人员和用户不受代币价格波动影响，因此不用依赖代币的价格。换句话说，采用EOS.IO软件的区块链人区块生产者自然而然地增加每个代币可用的带宽、算力和存储大小，而不用考虑代币的价值。

A blockchain using EOS.IO software also awards block producers tokens every time they produce a block. The value of the tokens will impact the amount of bandwidth, storage, and computation a producer can afford to purchase; this model naturally leverages rising token values to increase network performance.

使用EOS.IO软件的区块链也奖励那些产生区块的区块生产者。代币的价值将影响生产者能够买得起的带宽、存储和算力的数量；这个模型自然地平衡上涨的代币价格来增加网络性能。

## State Storage Costs 状态存储成本

While bandwidth and computation can be delegated, storage of application state will require an application developer to hold tokens until that state is deleted. If state is never deleted, then the tokens are effectively removed from circulation.

尽管带宽和算力能够被委托（出租），应用程序状态的存储需要应用开发人员持有代币，直到状态被删除。如果状态从未被删除，那么这些代币就在流通中被丢弃。

## Block Rewards 区块奖励

A blockchain that adopts the EOS.IO software will award new tokens to a block producer every time a block is produced. In these circumstances, the number of tokens created is determined by the median of the desired pay published by all block producers. The EOS.IO software may be configured to enforce a cap on producer awards such that the total annual increase in token supply does not exceed 5%.

采用EOS.IO软件的区块链每当一个区块被挖出时就奖励给区块生产者新的代币。在这样的环境下，产生的代币数量被所有区块生产者发布的所期望的费用的中位数来决定。EOS.IO软件也许能够进行某些配置来对区块生产者的奖励设定上限，这样的话，代币供应量的年增长不会超过5%。






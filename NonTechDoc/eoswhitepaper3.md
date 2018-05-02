
>文章来自：https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md
>
>译者：区块链中文字幕组 Chuan

## EOS.IO 白皮书

### Deterministic Parallel Execution of Applications 不可逆转的并行执行

Blockchain consensus depends upon deterministic (reproducible) behavior. This means all parallel execution must be free from the use of mutexes or other locking primitives. Without locks there must be some way to guarantee that transactions that may be executed in parallel do not create non-deterministic results.

区块链共识依赖于不可逆转的操作。这意味着所有的并行执行必须不受互斥锁或者其它锁定原语的的限制。没有锁定，就必须有某种方法来保证可能被并行执行的交易不能创建可逆转的结果。

The June 2018 release of EOS.IO software will run single threaded, yet it contains the data structures necessary for future multithreaded, parallel execution.

2018年6月上线的EOS.IO软件将以单线程运行，但是它包含了为未来的多线程、并行执行所需的数据结构。

In an EOS.IO software-based blockchain, once parallel operation is enabled, it will be the job of the block producer to organize Action delivery into independent shards so that they can be evaluated in parallel. The schedule is the output of a block producer and will be deterministically executed, but the process for generating the schedule need not be deterministic. This means that block producers can utilize parallel algorithms to schedule transactions.

在基于EOS.IO软件的区块链中，一旦并行执行并允许，把指令的传递打包到独立的分片中就是区块生产者所做的事，这样，这些独立的分片能够被并行地评估。区块生产者的执行结果就是一个计划安排表，它将被不可逆转地执行，但是对产生这个计划安排表的过程并不是不可逆的。这意味着区块生产者能够实现并行算法来安排交易什么时候执行。

Part of parallel execution means that when a script generates a new Action it does not get delivered immediately, instead it is scheduled to be delivered in the next cycle. The reason it cannot be delivered immediately is because the receiver may be actively modifying its own state in another shard.

部分的并行执行表明，当一个脚本产生一个新的指令，它并不会立即被传递，而是被排定到计划表中在下一个循环中被传递。这样安排的原因在于接收者可能实际上在修改他自己在另一个分片中的状态。

#### Minimizing Communication Latency 最小化通信延迟

Latency is the time it takes for one account to send an Action to another account and then receive a response. The goal is to enable two accounts to exchange Actions back and forth within a single block without having to wait 0.5 seconds between each Action. To enable this, the EOS.IO software divides each block into cycles. Each cycle is divided into shards and each shard contains a list of transactions. Each transaction contains a set of Actions to be delivered. This structure can be visualized as a tree where alternating layers are processed sequentially and in parallel.

延迟指的是，一个账户发送指令到另一个账户，然后接收到响应所需的时间。目的是使两个账户在一个块内来回交换指令，无需在每个指令之间等待0.5秒。为做到这一点，EOS.IO软件把每个块划分成循环周期。每个循环周期被划分成分片，每个片包含一组交易。每个交易包含一组要被发送的指令。这个结构可以用树来表示，每一层轮流地按照顺序并行地处理。

Block 区块

Region 区域

Cycles (sequential) 循环（有序的）

Shards (parallel) 分片 (并行的)

Transactions (sequential) 交易 (有序的)

Actions (sequential) 指令 (有序的)

Receiver and Notified Accounts (parallel) 接收者和被通知的账户（并行的）

Transactions generated in one cycle can be delivered in any subsequent cycle or block. Block producers will keep adding cycles to a block until the maximum wall clock time has passed or there are no new generated transactions to deliver.

在一个循环周期里产生的交易可以在任一个随后的循环周期或块中被提交。区块生产者将持续地把循环周期添加到块中，直到经过了最大运行时间，或者不再有新的交易需要提交。

It is possible to use static analysis of a block to verify that within a given cycle no two shards contain transactions that modify the same account. So long as that invariant is maintained a block can be processed by running all shards in parallel.

对一个区块进行统计分析来验证在一个指定的循环周期内没有两个分片包含修改相同账户的交易是可行的。只要保持这一常态，一个区块就能够通过并行地运行所有的分片来进行处理。

#### Read-Only Action Handlers 只读的指令操作程序

Some accounts may be able to process an Action on a pass/fail basis without modifying their internal state. If this is the case, then these handlers can be executed in parallel so long as only read-only Action handlers for a particular account are included in one or more shards within a particular cycle.

一些账户也许能够在通过/没通过的基础上处理一条指令，无需修改他们的内在状态。如果发生这样的情况，只要把一个特定账户的只读指令操作程序包含在一个指定的循环里的一个或多个分片中，这些操作程序就能够被并行执行。



#### Atomic Transactions with Multiple Accounts 多账户的基本交易

Sometimes it is desirable to ensure that Actions are delivered to and accepted by multiple accounts atomically. In this case both Actions are placed in one transaction and both accounts will be assigned the same shard and the Actions applied sequentially.

有时候，能够保证指令被多个账户传递并接受是值得期待的。这种情况下，两个指令都放在一笔交易里，两个账户将被分配相同的片，指令按序执行。

#### Partial Evaluation of Blockchain State 区块链状态的不完全评估

Scaling blockchain technology necessitates that components are modular. Everyone should not have to run everything, especially if they only need to use a small subset of the applications.

扩容区块链技术必要条件是组件要模块化。每个人不应该得要运行所有的东西，尤其如果他们只需要使用一小部分应用的话。

An exchange application developer runs full nodes for the purpose of displaying the exchange state to its users. This exchange application has no need for the state associated with social media applications. EOS.IO software allows any full node to pick any subset of applications to run. Actions delivered to other applications are safely ignored if your application never depends upon the state of another contract.

一个交易所应用的开发人员为了能够把交易状态显示给用户需要运行全节点。这种交易所应用程序不需要把交易状态与社交媒体应用关联。EOS.IO软件允许任意一个全节点来挑选任意数量的应用程序来运行。如果你的应用从来不依赖其他合约的状态，那么传递给其他应用程序的指令可以被安全地忽略。

#### Subjective Best Effort Scheduling 自主最优调度

The EOS.IO software cannot obligate block producers to deliver any Action to any other account. Each block producer makes their own subjective measurement of the computational complexity and time required to process a transaction. This applies whether a transaction is generated by a user or automatically by a smart contract.

EOS.IO软件不能指使区块生产者提交任一条指令给任何其他账户。每个区块生产者对计算复杂度和处理一笔交易所需的时间做出自己的主观评估。这适用于一笔交易无论是由用户还是智能合约发起。

On a launched blockchain adopting the EOS.IO software, at a network level all transactions are billed a computational bandwidth cost based on the number of WASM instructions executed. However, each individual block producer using the software may calculate resource usage using their own algorithm and measurements. When a block producer concludes that a transaction or account has consumed a disproportionate amount of the computational capacity they simply reject the transaction when producing their own block; however, they will still process the transaction if other block producers consider it valid.

在采用EOS.IO软件实现的区块链中，在网络层上所有交易的费用是基于被执行的WASM指令数量的计算带宽成本。可是，使用EOS.IO软件的每个独立的区块生产者也许使用自己的算法和评估方法来计算资源的使用情况。当一个区块生产者得出结论说，一个交易或账户消耗了不成比例的算力时，在产生自己的区块时他们可以拒绝这个交易。可是，如果其他区块认为它有效的话，他们仍旧会处理这个交易。

In general, so long as even 1 block producer considers a transaction as valid and under the resource usage limits then all other block producers will also accept it, but it may take up to 1 minute for the transaction to find that producer.

一般来说，只要一个区块生产者认为一笔交易是有效的，并且消耗的资源在范围之内，那么其他所有的区块生产者也就接受它，但是对这笔交易来说，这也许要花上多达1分钟的时间来找到那个区块生产者。

In some cases, a producer may create a block that includes transactions that are an order of magnitude outside of acceptable ranges. In this case the next block producer may opt to reject the block and the tie will be broken by the third producer. This is no different than what would happen if a large block caused network propagation delays. The community would notice a pattern of abuse and eventually remove votes from the rogue producer.

有些情况下，区块生产者也许创建了一个区块，它包含的交易是在可接受范围外按照重要性的顺序排列。这样的话，下一个区块生产者也许选择拒绝这个块，这一连接将被第三个区块生产者打破。这跟一个大的区块引起网络广播延迟而产生的情况没有什么不同。社区会注意到滥用的模式，并最终去掉恶意生产者的选票。

This subjective evaluation of computational cost frees the blockchain from having to precisely and deterministically measure how long something takes to run. With this design there is no need to precisely count instructions which dramatically increases opportunities for optimization without breaking consensus.

计算成本的主观评估使区块链不必精确地评估需要运行多长时间。通过这样的设计，就没有必要对指令计数，这可以显著地增加优化机会，而不必违反共识。

#### Deferred Transactions 延迟交易

EOS.IO Software supports deferred transactions that are scheduled to execute in the future. This enables computation to move to different shards and/or the creation of long-running processes that continuously schedule a continuance transaction.

EOS.IO软件支持延迟交易，让它们在之后的某个时间被执行。这能够把计算放到不同的分片中，并且/或者创建长时间运行的进程来持续地安排一个不间断的交易。

#### Context Free Actions 上下文无关的指令

A Context Free Action involves computations that depend only on transaction data, but not upon the blockchain state. Signature verification, for example, is a computation that requires only the transaction data and a signature to determine the public key that signed the transaction. This is one of the most expensive individual computations a blockchain must perform, but because this computation is context free it can be performed in parallel.

上下文无关的指令包含仅依赖交易数据，而不依赖区块链状态的计算。比如说，签名验证这种计算，只需要交易数据和一个签名来确定对交易签名的公钥。在区块链必须执行的单一计算中，这是最昂贵的一种，然而由于这种计算是上下文无关的，所以它可以被并行执行。

Context Free Actions are like other user Actions, except they lack access to the blockchain state to perform validation. Not only does this enable EOS.IO to process all Context Free Actions such as signature verification in parallel, but more importantly, this enables generalized signature verification.

上下文无关的指令和其他的用户指令类似，除了它们不能访问区块链状态来执行验证。这不仅使得 EOS.IO 软件能够并行地处理所有上下文无关的操作，比如签名验证，更重要的是，这还能够做到通用签名验证。

With support for Context Free Actions, scalability techniques such as Sharding, Raiden, Plasma, State Channels, and others become much more parallelizable and practical. This development enables efficient inter-blockchain communication and potentially unlimited scalability.

通过支持上下文无关的操作，Sharding，Raiden，Plasma，State Channels 等扩容技术变得更加可并行和实用。这一技术的发展技术使得高效的链间通信和潜在的无限扩容性成为可能。

***

##### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。
如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号：w1791520555。

[点击查看 GITHUB 及更多的译文](https://github.com/BlockchainTranslator/EOS)

##### 本文译者介绍

Chuan，区块链技术爱好者。欢迎加我的微信：youyuxiaochuan

译文版权所有，转载需完整注明以上内容。

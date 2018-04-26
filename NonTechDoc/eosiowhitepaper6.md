# Scripts & Virtual Machines 脚本和虚拟机

The EOS.IO software will be first and foremost a platform for coordinating the delivery of authenticated messages (called Actions) to accounts. The details of scripting language and virtual machine are implementation specific details that are mostly independent from the design of the EOS.IO technology. Any language or virtual machine that is deterministic and properly sandboxed with sufficient performance can be integrated with the EOS.IO software API.

EOS.IO软件首要的是作为一个平台用来协调把验证过的消息（称为Action）发送给账户。脚本语言和虚拟机的细节很大程度上是独立于EOS.IO技术设计的特有的细节。任何一种确定性的、具备沙盒安全技术的语言或者虚拟机，都能够使用EOS.IO软件的API进行整合。

## Schema Defined Actions模式定义的Action

All Actions sent between accounts are defined by a schema which is part of the blockchain consensus state. This schema allows seamless conversion between binary and JSON representation of the Actions.

账户之间发送的所有Action通过一份属于区块链共识状态的模式来定义。这种模式允许在Action的二进制和JSON格式之间的无缝转换。

## Schema Defined Database模式定义的数据库

Database state is also defined using a similar schema. This ensures that all data stored by all applications is in a format that can be interpreted as human readable JSON but stored and manipulated with the efficiency of binary.

数据库状态也使用相似的模式来定义。这保证所有应用程序存储的数据以一种能够让人可读的JSON格式来解释，但是又使用二进制的高效性来存储并进行管理。

## Generic Multi Index Database API 通用多索引数据库API

Developing smart contracts requires a defined database schema to track, store, and find data. Developers commonly need the same data sorted or indexed by multiple fields and to maintain consistency among all the indices.

开发智能合约需要一个定义好的数据库模式来跟踪、存储和寻找数据。开发人员通常需要按照多个字段存储或索引的相同数据，并维持在所有索引中的一致性。

## Separating Authentication from Application 从应用中分离验证过程

To maximize parallelization opportunities and minimize the computational debt associated with regenerating application state from the transaction log, EOS.IO software separates validation logic into three sections:

为了最大化并行处理效果，并且把从交易日志中重生应用状态相关联的计算负债降到最低，EOS.IO软件把验证逻辑分成三个部分：

1. Validating that an Action is internally consistent; 验证Action的内在是前后一致的。
2. Validating that all preconditions are valid; and 验证所有的前提条件是有效的。
3. Modifying the application state. 修改应用程序的状态。

Validating the internal consistency of a Action is read-only and requires no access to blockchain state. This means that it can be performed with maximum parallelism. Validating preconditions, such as required balance, is read-only and therefore can also benefit from parallelism. Only modification of application state requires write access and must be processed sequentially for each application.

验证Action的内在一致性是只读的，不需要访问区块链状态。这意味着它可以做到最大化并行处理。验证前提条件，比如所需的余额，也是只读的，因此也能从并行处理中获益。只有应用程序状态的修改需要写入操作，以及对每个应用程序必须按序处理。

Authentication is the read-only process of verifying that an Action can be applied. Application is actually doing the work. In real time both calculations are required to be performed, however once a transaction is included in the blockchain it is no longer necessary to perform the authentication operations.

验证是校验一个Action可以被应用的只读过程。应用程序实际上做了这一工作。这两个计算过程都被要求实时被执行，可是，一旦交易被放进区块链，就没有必要来执行验证操作。

# Inter Blockchain Communication 跨链通信

EOS.IO software is designed to facilitate inter-blockchain communication. This is achieved by making it easy to generate proof of Action existence and proof of Action sequence. These proofs combined with an application architecture designed around Action passing enables the details of inter-blockchain communication and proof validation to be hidden from application developers, enabling high level abstractions to be presented to developers.

EOS.IO软件被设计用来使跨链通信变得容易。这是通过产生Action存在证明和Action顺序证明来实现的。这些证明与围绕Action传递而设计的应用结构相结合，Action传递使得跨链通信的细节和证据的验证对应用开发人员不可见，通过高阶的抽象形式来呈现给开发人员。

## Merkle Proofs for Light Client Validation (LCV)用于轻客户端验证的默克尔证明

Integrating with other blockchains is much easier if clients do not need to process all transactions. After all, an exchange only cares about transfers in and out of the exchange and nothing more. It would also be ideal if the exchange chain could utilize lightweight merkle proofs of deposit rather than having to trust its own block producers entirely. At the very least a chain's block producers would like to maintain the smallest possible overhead when synchronizing with another blockchain.

如果客户端不需要处理所有的交易，和其它区块链进行整合更加容易。毕竟，交易所只关心从交易所转进转出，不处理别的事务。如果交易所链能够对转入的交易实现轻量默克尔证明，而不是非得完全信任它自己的区块生产者，那么这将是一种理想的情况。至少，当和另一个区块链同步时，一个链的区块生产者想要维持最小的开支。

The goal of LCV is to enable the generation of relatively light-weight proof of existence that can be validated by anyone tracking a relatively light-weight data set. In this case the objective is to prove that a particular transaction was included in a particular block and that the block is included in the verified history of a particular blockchain.

轻客户端验证的目标是能够产生相对轻量级的存在证明，这一证明能够被任一个跟踪相对轻量级的数据集来进行验证。在这种情况下，目标就是证实：特定的交易被放进特定的区块，并且这个区块被包含在特定的区块链的被校验过的历史记录中。

Bitcoin supports validation of transactions assuming all nodes have access to the full history of block headers which amounts to 4MB of block headers per year. At 10 transactions per second, a valid proof requires about 512 bytes. This works well for a blockchain with a 10 minute block interval, but is no longer "light" for blockchains with a 0.5 second block interval.

比特币支持交易验证，假设所有的节点可以访问区块头的全部历史记录，这个历史记录每年的大小有4M。每秒10笔交易，一个有效的证明需要512字节。对于一个10分钟出块的区块链来说，这可以的，但是，对于出块间隔为0.5秒的区块链，这就不再是“轻量级的”数据了。

The EOS.IO software enables lightweight proofs for anyone who has any irreversible block header after the point in which the transaction was included. Using the hash-linked structure shown it is possible to prove the existence of any transaction with a proof less than 1024 bytes in size.

在交易被放进区块链后，拥有了不可逆转的区块头的人来说，EOS.IO使得轻量级证明成为可能。使用哈希链接结构，能够证实任何一笔交易使用的证据大小不超过1024个字节。

Given any block id for a block in the blockchain, and the headers a trusted irreversible block. It is possible to prove that the block is included in the blockchain. This proof takes ceil(log2(N)) digests for its path, where N is the number of blocks in the chain. Given a digest method of SHA256, you can prove the existence of any block in a chain which contains 100 million blocks in 864 bytes.

考虑到区块链中每个区块有个ID以及区块头。能够证实区块被放进区块链之中。这一证明需要的时间复杂度是它的路径的ceil(log2(N))，其中N是链上的区块数。考虑到SHA256摘要算法，你可以证实任一个区块存在于区块链中，这个链包含1亿个大小为864字节的区块。

There is little incremental overhead associated with producing blocks with the proper hash-linking to enable these proofs which means there is no reason not to generate blocks this way.

伴随着产生那些使用合适的哈希值相连的区块，并没有增加多少费用，这使得这些证明是可行的。所以，就没有理由不使用这种方式来产生区块。

When it comes time to validate proofs on other chains there are a wide variety of time/ space/ bandwidth optimizations that can be made. Tracking all block headers (420 MB/year) will keep proof sizes small. Tracking only recent headers can offer a trade off between minimal long-term storage and proof size. Alternatively, a blockchain can use a lazy evaluation approach where it remembers intermediate hashes of past proofs. New proofs only have to include links to the known sparse tree. The exact approach used will necessarily depend upon the percentage of foreign blocks that include transactions referenced by merkle proof.

说到验证其它链上的证据时，可以在时间/空间/带宽等方面作出各种优化。跟踪所有区块头（每年420兆字节）将减少证据大小。只跟踪最近的区块头能够在最低的长期存储量和证据大小之间达到平衡。或者，区块链可以使用偷懒的评估方法，它只记住过去证据的中间哈希值。新证据只要包含指向已知稀疏树的链接。选择的精确方法必须依赖外部区块的比例，这些区块包含由默尔克证明引用的交易。

After a certain density of interconnectedness, it becomes more efficient to simply have one chain contain the entire block history of another chain and eliminate the need for proofs all together. For performance reasons, it is ideal to minimize the frequency of inter-chain proofs.

在经过一定程度的互联后，只要让一个链包含另一个链的完整区块历史，并且不再需要所有的证据，这样做带来的效率更高。出于性能原因的考虑，理想的情况是让链与链之间的证明次数最小化。

## Latency of Interchain Communication 链内通信的延迟性

When communicating with another outside blockchain, block producers must wait until there is 100% certainty that a transaction has been irreversibly confirmed by the other blockchain before accepting it as a valid input. Using an EOS.IO software-based blockchain and DPOS with 0.5 second blocks and the addition of Byzantine Fault Tolerant irreversibility, this takes approximately 0.5 second. If any chain's block producers do not wait for irreversibility it would be like an exchange crediting a deposit that was later reversed and could impact the validity of the blockchain's consensus. The EOS.IO Software uses both DPOS and aBFT to provide rapid irreversibility.

当和外部区块链进行通信的时候，区块生产者必须要 100% 确信一笔交易已经被不可逆转地被这个外部区块链确认后，才可以将其当作合法输入。基于EOS.IO软件的区块链，0.5秒出块的 DPOS 共识算法，以及拜占庭容错的不可逆转性，这一确认过程大概需要 0.5 秒。如果任一区块生产者没有等待这种不可逆转性，那么将影响区块链的共识的有效性。EOS.IO 软件使用 DPOS 算法和拜占庭容错机制来快速地实现交易的不可逆转性。

## Proof of Completeness 完整性证明

When using merkle proofs from outside blockchains, there is a significant difference between knowing that all transactions processed are valid and knowing that no transactions have been skipped or omitted. While it is impossible to prove that all of the most recent transactions are known, it is possible to prove that there have been no gaps in the transaction history. The EOS.IO software facilitates this by assigning a sequence number to every Action delivered to every account. A user can use these sequence numbers to prove that all Actions intended for a particular account have been processed and that they were processed in order.

当使用来自于外部区块链的默克尔证明时，知道处理的全部交易是有效的，明显不同于知道没有交易被跳过或省略。尽管不太可能证实最近所有的交易是已经知晓的，但是，还是有可能证明在这个交易历史中没有被跳过或省略的交易。EOS.IO 软件通过给发送到每个账户的每个Action一个顺序编号来做到这一点。用户可以使用这些顺序编号来证实用于某个特定账户的所有Action都已经被处理，并且是按照顺序来处理的。

## Segregated Witness 隔离见证

The concept of Segregated Witness (SegWit) is that transaction signatures are not relevant after a transaction is immutably included in the blockchain. Once it is immutable the signature data can be pruned and everyone else can still derive the current state. Since signatures represent a large percentage of most transactions, SegWit represents a significant savings in disk usage and syncing time.

隔离见证（SegWit）是指一笔交易被打包进不可变更的区块链之后，交易的签名就变得无关紧要了。一旦交易不可变更，签名数据就可以被删除，其他人仍然能获得当前状态。由于签名构成了大多数交易的很大部分，隔离见证在磁盘使用和同步时间方面可以节省很多资源。

This same concept can apply to merkle proofs used for inter-blockchain communication. Once a proof is accepted and irreversibly logged into the blockchain, the 2KB of sha256 hashes used by the proof are no longer necessary to derive the proper blockchain state. In the case of inter-blockchain communication, this savings is 32x greater than the savings on normal signatures.

这一概念可以应用于对跨链通信采用默克尔证明。一旦一个证明被接受并被不可逆地记录进区块链，那么这个证明所用的 2KB 大小的 sha256 哈希值对于获得区块链的状态就不再是必须的。在这种跨链通信情况下，这样的节省要比使用普通签名高出32倍。。

Another example of SegWit would be for Steem blog posts. Under this model a post would contain only the sha256(blog content) and the blog content would be in the segregated witness data. The block producer would verify that the content exists and has the given hash, but the blog content would not need to be stored in order to recover the current state from the blockchain log. This enables proof that the content was once known without having to store said content forever.

隔离见证应用的另一个例子是用于 Steem 的博客文章。在这种模式下，一篇文章只包含sha256哈希值（博客内容），博客内容将放在隔离见证数据中。区块生产者会验证内容的存在以及对应的哈希值，但是，为了从区块链日志中恢复当前状态，博客内容并不需要被存储。这使得博客内容只要被看过一次，而不必永久地储存这个内容。

# Conclusion 结束语

The EOS.IO software is designed from experience with proven concepts and best practices, and represents fundamental advancements in blockchain technology. The software is part of a holistic blueprint for a globally scalable blockchain society in which decentralized applications can be easily deployed and governed.

EOS.IO 软件的设计来自于已被证实的概念和最佳实践，代表了区块链技术的根本性进步。这个软件是全球性的可变化的区块链团体的宏伟蓝图的一部分，在这个团体中，去中心化的应用能够轻松地部署和管理。




# Inter-blockchain Communication via Merkle Proofs with EOS.IO | 通过默克尔证明实现EOS.IO跨链通讯

> 本文翻译自：https://steemit.com/eos/@dan/inter-blockchain-communication-via-merkle-proofs-with-eos-io
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)   何德林    Xuming Meng
> 
> 翻译时间：2017-12-17

----------------------------------------------------

Merkle trees are used to enable proofs of user actions to light weight clients. Light weight clients are the foundation of inter-blockchain communication where one blockchain acts as a light-client to another blockchain.

默克尔树用来为轻量级客户提供用户操作的证明。轻量级客户端是区块链跨链通信的基础，即一链作为另一个链的轻客户端。

Every user action can be viewed as someone writing a check which gets processed by the bank (blockchain) and if accepted logged. Inter Blockchain communication is about generating proofs that a particular check was accepted and the order of its acceptance relative to other checks written by the same sender or receiver.

每个用户操作都可以被看作是一个人开了一张由银行(区块链)来处理的支票，如果被接受的话。在跨链通信中，是关于生成一个特定的支票被接受的证明，以及它接受的顺序，相对于同一发送方或接收方所写的其他支票。

Chain A can receive messages from Chain B by following Chain B’s block headers and processing action proofs. Each action proof has one or more sequence numbers which Chain A uses to make sure there are no gaps in processing.

链A可以通过链B的块头和处理操作证明接收链B的消息，通过跟随链B的块头和处理证明。每个动作证明都有一个或多个序列号，该序列号链用于确保Chain A在处理过程中没有遗漏。

Where as other chains generate a merkle tree over state (account balances), EOS.IO generates a merkle tree over sequenced actions. A light client can derive the balance of a single account by processing all sequenced actions for that account without having to process the actions for other accounts.

当其他链在状态(帐户余额)上生成一棵默克尔树时，EOS.IO生成一棵“默克尔树”，用于排序操作。一个轻客户端可以通过处理该帐户的所有顺序操作来获得单个帐户的余额，而不必处理其他帐户的操作。

In many cases it is not necessary to know the balance of an account, instead all the light client needs to do is verify payment. This can be verified with the proof of a single action.

在许多情况下，不需要知道帐户的余额，所有的轻客户端需要做的只是验证付款。这可以通过单个动作的证明来验证。

Blockchains are built on top of deterministic state machines; therefore, inter blockchain communication is most effective when guarantees of completeness and order can be provided. The EOS.IO protocol creates a TCP like communication channel between chains. This means that missing or out of order proofs can be detected.

区块链建立在确定性状态机之上；因此，在保证完整性和顺序的前提下，跨链通信是最有效的。 EOS.IO 协议创建了类似于TCP通信通道，在不同的链之间。这意味着可以检测到丢失或顺序不对，可以被监测到。

While you can generates proofs to guarantee no actions are skipped, it is not possible to prove that you have all actions up to the present moment. To prove completeness to the present moment one must generate a transaction, have it included, then generate a proof that the most recent transaction was confirmed with the proper sequence number.

虽然您可以生成证据以确保没有跳过任何操作，但不可能证明您已经完成了，截止到当前时刻，所有的操作。为了证明当前时刻的完整性，必须生成一个事务，把它包含进来，然后生成一个证明，证明最近的事务，用正确的顺序号，得到了确认。

Target Audience 目标用户

This post is for those curious over the cryptographic design of EOS.IO inter-blockchain communication. With this information you can design and build light weight wallets or integrate with your own blockchain. This text was originally drafted for internal documentation, but we are providing it here for community review and inspection by the curious.

这篇文章是为了那些对 EOS.IO跨链通讯加密设计的感兴趣人。有了这些信息，你就可以设计和建造轻便的钱包，或者与你自己的区块链整合。这篇文章最初是为内部文件起草的，但我们在这里提供，以便社区和感兴趣的人查看。

Canonical Trees and Proofs

All of the merkle calculations in EOS.IO share a few conventions that disambiguate entries in a proof without requiring additional space. Given two leaves with respective digests of Da and Db. Their shared parent node in a basic merkle tree would be the digest of the concatenation of Da and Db (Da|Db). However, unless the chosen digest calculation is commutative, Da|Db is not the same as Db|Da. This means that a proof, in the form of a “path” from a leaf to the root of a Merkle tree (sometimes referred to as a “log proof”) must indicate whether the entries in the “path” represent left or right concatenation.

在 EOS.IO中，所有默克尔计算都共享一些，可以在不需要额外空间的情况下消除歧义的约定。给定两个叶，分别是Da和Db的摘要。它们在一个基本的默克尔树中，他们的共享父节点将是Da和Db(Da | Db)的连接的摘要。然而，除非选择的摘要计算是可交换的，否则Da | Db与Db | Da不一样。这意味着，从叶子到默克尔根节点(有时被称为“日志证明”)的“路径”形式中，必须表明“路径”中的条目是否代表左或右连接。

To avoid this extra “path” data in the proof, EOS.IO applies a transform to the leaf digests before concatenating them for the new digest. This transform, indicates whether the digest is on the left or right side of the concatenation. The proof “path” then includes pre-transformed digests making the correct concatenation operation easy to infer.

为了避免这种额外的“路径”数据，EOS.IO 在将它们连接到新摘要之前，将对叶子摘要进行转换。这个转换，表示摘要是在连接的左边还是右边。“路径”证明包括预先转换的摘要，使正确的连接操作容易推断。

More precisely, EOS.IO enforces that the first bit of the leaf digest is 0 for “left” digests and 1 for “right” digests. When reading a proof path entry (Dp) and applying it to a given digest (Dn) if the first bit of Dp is 0 then the resulting digest is hash(Dp|Dn) otherwise it is hash(Dn|Dp)

更准确地说,EOS.IO强制“左”摘要的第一个位是0，“右”的摘要第一个位是1。当读取一个证明路径条目(Dp)并将其应用到给定摘要(Dn)时，如果Dp第一位是0，那么得到的摘要就是哈希(Dp | Dn)，否则它就是哈希(Dn |Dp)

C_HASH(left,right)
LET canonical_left := CLEAR_FIRST_BIT(left),
LET canonical_right := SET_FIRST_BIT(right),
LET data := CONCATENATE(canonical_left,canonical_right),
HASH_FN(data);

(pseudocode for generating a hash form a left and right leaf)

生成哈希的伪代码

In addition, should construction of a merkle tree require hashing a node with an unknown value, for example in a balanced tree of 3 nodes, the resulting digest is the concatenation of the digest with itself.

另外，默克尔树的构建需要哈希一个具有未知值的节点，例如在一个3个节点平衡树的中，摘要结果是对自身的摘要的连接。

Root:

Dabcc
/ \
Dab Dcc <- Dc concatenates with itself
/ \ /
Da Db Dc

The Block Merkle 区块默克尔树
For any Block N, its header includes the root of a balanced merkle tree where the leaves are the block ids for all preceding blocks 0..N-1: the Block Root. This serves as a commitment to the contents of the blockchain, from genesis on, by each new block.

对于任何块N，它的头包含一个平衡的默克尔树的根，所有叶子节点是所有前面块的id。这是对区块链内容的确认，从创世记到每个新区块。

Given any block id for a block in the blockchain, and the headers a trusted irreversible block. It is possible to prove that the block is included in the blockchain. This proof takes ceil(log2(N)) digests for its path, where N is the number of blocks in the chain. Given a digest method of SHA256, you can prove the existence of any block in a chain which contains 100 million blocks in 864 bytes.

在区块链中给定一个块id,，以及一个可信不可逆的块头，可以证明该块包含在区块链中。这个证明包含了ceil(log2(N))对其路径的摘要，其中N为链中的区块数。给定一个SHA256的摘要方法，您可以证明一个链中任何块的存在，它包含1亿个块，以864字节为单位。

The Action Merkle 操作默克尔树
For any Block N, the headers include the root of a nearly-balanced merkle tree where the leaves are commitments to data generated while processing actions: the Action Root. This can be used to prove existence and, ordering of actions. Additionally, it can be used to prove completeness of transcripts of actions that affect a given scope.

对于任何块N，头都包含了一棵接近平衡的默克尔树的根，此树的叶子是对在处理动作时生成数据的确认。这可以用来证明操作的存在he和操作的顺序。此外，它还可以用来证明给定范围内操作记录的完整性。

The data committed to for each action, or Action Commitment, is:

为每项操作确认的数据为:

receiver: the account name whose contract received the given action
scope: the scope where this action is defined
name: The name of the action (eg: ‘transfer’)
data: the binary encoded data payload delivered to the contract
data_access: an array of sequence numbers for scopes accessed during the processing of this action

This can be used to prove complete transcripts by providing actions and proofs for the sequence numbers between two given actions

这可以用来证明操作记录的完整性，通过提供操作以及两个给定操作之间的顺序号证明。

Sequence numbers always increment on write operations and never on reads. There will be exactly one action with a write for a given

顺序号总是在写操作上增加，而从不在读取上增加。一个操作会有一个给定的写操作。

(sequence, scope, receiver)
region_id: the region this action was processed in
cycle_index: the cycle this action was processed in

This can be used to prove ordering constraints Shards inside a cycle can execute in parallel; there is no deterministic ordering between actions in the same cycle but different shards.

这可以用来证明排序约束

一个循环中的分片可以并行执行;在同一循环中，不同的分片之间没有确定的排序。

(Example Action Commitment)
{
receiver:inite,
scope:eosio,
name:transfer,
data:{
"from":"inite",
"to":"inita",
"amount":10000,
"memo":"memo"
},
data_access:[
{"type":"write","scope":"inite","sequence":1},
{"type":"write","scope":"inita","sequence":0}
],
region:0,
cycle:0
}
For each shard (a unit of parallelizable execution in a cycle) a balanced merkle tree is constructed of these action commitments to generate a temporary shared merkle root. This is done for speed of parallel computation. The block header contains the root of a balanced merkle tree whose leaves are the roots of these individual shard merkle trees. This means that the resulting merkle tree represented by the Action Root is not guaranteed to be a perfectly balanced merkle tree, however, it should be very close in most cases.

对于每个分片(一个循环中的并行执行单元)，平衡的默克尔树是由各操作确认构建，以生成一个临时共享的默克尔根。这是为了加快并行计算。区块的头部包含了一个平衡默克儿树的根，它的叶子是各个单独的分片默克尔树的根。这意味着，由操作树根代表的结果默克尔树不能保证是一个完美平衡的merkle树，然而，在大多数情况下它应该非常接近。

Given an action, somewhere in the blockchain, it is possible to succinctly prove the retirement of that action by first proving that it was committed to by a block’s Action Root, and then that the given block was committed to by a trusted irreversible block header’s Block Root. These two proofs are referred to as the “Action Path” and the “Block Path” respectively.

给定一个操作，在区块链的某个地方，有可能简洁地证明该操作的结束，通过第一次证明它是由一个块的操作根节点提交的，然后这个给定的块是由一个可信的不可逆块头的区块根节点提交。这两种证明分别称为“操作路径”和“区块路径”。

The Action Path consists of all the data (sibling digests from the merkle tree) necessary to recalculate the root of a merkle tree with respect to a single Action Commitment. That merkle tree’s root should exactly match the Action Root committed to by the header of the block that retired the action.

操作路径由所有的数据(来自merkle树的各摘要节点)组成，它们需要重新计算默克尔树的根，就一个单独的操作确认。这棵默克尔树的根节点应该完全匹配，区块头部提交的查找根节点。

The Block Path consists of all the data necessary to recalculate the root of a merkle tree with respect to a single Block ID. That merkle tree’s root should exactly match the Block Root committed to by the header of a trusted irreversible block.

区块路径包含重新计算默克尔树的根，就单个区块ID所必需的所有数据。该默克尔树的根节点，应该完全匹配区块的根节点，由信任的不可逆块的区块头所提交的。

For example, 例如，

Given the action above, retired in a block with the ID:

给定上面的操作，在区块中有ID:
00000033e4f902358b1d43918d197652fc01baaf0e6ca8ee38cda2e8780b7dbd

Whose Action Root was:

它的操作根：

067ed979eeff38064f10bd77dcd3630ce104ae2685b5d6c2500552b0172e4c57
And trusted irreversible block whose Block Root is:

1ae092ea41e70982b56b9673f990346876ba535595df16dc1094740c144aaae6
That proof data looks like this:

该证明数据看起来如下：

Action Path:

操作路径:
9b75773cc9e2d8d186c408c3f5cdc55cde5b23addb6f25aa924bd3279bd0ca91
9cb66ff0d78991662c4784afac391a0e5f7104164daed36ba1fd4c6cc4907067
C65abe772ecb192105cd627bcb170eff8ec8f707a5d68d5c8060fee0236b4167
4cf39dfbe8a0fdc2540c8f0b68037484051a20d6ca00b891bbfc66d826503677
A8773db30f3733063352d1abec5fea265115bdf646a69d21545746a4f7cff3f3

Block Path:

区块路径:
8000003418a608c3704f80cdfed2793a055cc13993eea67ccdd018d9df027101
2351ee036c6a4052e18c9ded8d35c1b1dfb330531e163039847797d38e9babd2
De1996e5c23c73fa212abaaf423b9038e289fc7a19be5a7f395c7727a5266168
Ccd7c6e10b398fd27cfc4d29f339806593d614c736ae1af8a47908e44d2fe924
1e95b55e98d329bda8f2c79d1f969650716207a03f13f540931ab5a6a80f4d0b
369d86219b35e493a4fda3649c9f3a546809add40462c4b5ddca185f75cfe05c
9067c63043027831fbc7ba046d5bd7d9a0c23e1baa6fe0ac16a911ff7c3acd74

To verify this proof, first serialize the claimed Action Commitment to EOS.IO’s standard binary format. That results in the following binary representation (in hex):

为验证此证明，首先序列化声明的操作确认成标准二进制格式。以下是二进制表示的结果(以十六进制表示):

000000000095dd740000000000ea3055000000572d3ccdcd1d000000000095dd74000000000093dd741027000000000000046d656d6f0000000000000000020100000000000000000000000095dd7401000000000000000100000000000000000000000093dd740000000000000000
EOS.IO currently uses SHA256 for its digest method(HASH_FN), so the leaf digest is the SHA256 of the above binary representation:

EOS.IO目前使用SHA256作为其摘要生成方法(HASH_FN)，因此，叶子摘要是上述二进制表示形式的SHA256:

1b75773cc9e2d8d186c408c3f5cdc55cde5b23addb6f25aa924bd3279bd0ca91

Using that leaf digest, apply the Block Path, referring to the section on canonical paths and signatures to determine if an entry in the path requires left or right concatenation. After applying the complete path, the resulting root digest should be exactly equal to the Action Root in the header of the block that retired the action:

使用该叶子摘要，应用区块路径，引用其中标准路径和签名的部分，以确定路径中的条目是否需要左或右连接。在应用完整的路径后，得到的根节点摘要，应该正好等于该操作的区块头部的操作根节点:

C_HASH(
1b75773cc9e2d8d186c408c3f5cdc55cde5b23addb6f25aa924bd3279bd0ca91,
9b75773cc9e2d8d186c408c3f5cdc55cde5b23addb6f25aa924bd3279bd0ca91)
=> 1cb66ff0d78991662c4784afac391a0e5f7104164daed36ba1fd4c6cc4907067

C_HASH(
1cb66ff0d78991662c4784afac391a0e5f7104164daed36ba1fd4c6cc4907067,
9cb66ff0d78991662c4784afac391a0e5f7104164daed36ba1fd4c6cc4907067)
=> 465abe772ecb192105cd627bcb170eff8ec8f707a5d68d5c8060fee0236b4167

C_HASH(
465abe772ecb192105cd627bcb170eff8ec8f707a5d68d5c8060fee0236b4167,
C65abe772ecb192105cd627bcb170eff8ec8f707a5d68d5c8060fee0236b4167)
=> dd205c37e3de758120f50060b052736ba903382904a445fae3a371cfb29820ab

C_HASH(
4cf39dfbe8a0fdc2540c8f0b68037484051a20d6ca00b891bbfc66d826503677,
dd205c37e3de758120f50060b052736ba903382904a445fae3a371cfb29820ab)
=> ecce9664089221e351aaedafd967a9e19e25ad03d82949b3953de53f8b3b1996

C_HASH(
ecce9664089221e351aaedafd967a9e19e25ad03d82949b3953de53f8b3b1996,
a8773db30f3733063352d1abec5fea265115bdf646a69d21545746a4f7cff3f3)
=> 067ed979eeff38064f10bd77dcd3630ce104ae2685b5d6c2500552b0172e4c57

Once we have verified that the block has a commitment retiring the action as described, we must also verify that the retiring block is included in the blockchain using the Block Path and the retiring block’s id. After applying the complete path, the resulting root digest should be exactly equal to the Block Root in the header of the trusted irreversible block:

一旦我们确认，该区块已有一个操作的确认，我们还必须校验该区块包含在区块链中，使用块路径和区块的id。应用完整路径，根摘要应该等于区块的根，在信任不可逆的区块头中:

C_HASH(
00000033e4f902358b1d43918d197652fc01baaf0e6ca8ee38cda2e8780b7dbd,
8000003418a608c3704f80cdfed2793a055cc13993eea67ccdd018d9df027101)
=> da16dd856cbb888545c0ed248f2acbbed57037cf407e258849d4600c8f074739

C_HASH(
2351ee036c6a4052e18c9ded8d35c1b1dfb330531e163039847797d38e9babd2,
da16dd856cbb888545c0ed248f2acbbed57037cf407e258849d4600c8f074739)
=> da1a4326c7d83cc86f1154e76000ae94a7579833e75d9378972c6f034e044c11

C_HASH(
da1a4326c7d83cc86f1154e76000ae94a7579833e75d9378972c6f034e044c11,
de1996e5c23c73fa212abaaf423b9038e289fc7a19be5a7f395c7727a5266168)
=> d2d0abf4e6d8b771f8de27413ce7c9ca9e443c89fd10c4d42cb37bcc47cb3598

C_HASH(
d2d0abf4e6d8b771f8de27413ce7c9ca9e443c89fd10c4d42cb37bcc47cb3598,
ccd7c6e10b398fd27cfc4d29f339806593d614c736ae1af8a47908e44d2fe924)
=> c36045ffee9c98eb419077aa356d65fb6a928914c40ec88aadcf634781e56c23

C_HASH(
1e95b55e98d329bda8f2c79d1f969650716207a03f13f540931ab5a6a80f4d0b,
c36045ffee9c98eb419077aa356d65fb6a928914c40ec88aadcf634781e56c23)
=> 4432bce7431f676ed704f2d3367cb33407898b70f51fea2dfa014b97ac37a97b

C_HASH(
369d86219b35e493a4fda3649c9f3a546809add40462c4b5ddca185f75cfe05c,
4432bce7431f676ed704f2d3367cb33407898b70f51fea2dfa014b97ac37a97b)
=> 94f5ba720b886515ada9c0f73ab393dffc43beaeac7be6f7f86bce808834dfde

C_HASH(
94f5ba720b886515ada9c0f73ab393dffc43beaeac7be6f7f86bce808834dfde,
9067c63043027831fbc7ba046d5bd7d9a0c23e1baa6fe0ac16a911ff7c3acd74)
=> 1ae092ea41e70982b56b9673f990346876ba535595df16dc1094740c144aaae6

Thanks  致谢
I would like to thank Bart W. for his help in writing this post and implementing this protocol in the eos-noon branch of our github repository.

我要感谢Bart W. ，他为本文的撰写以及eos - noon分支中实现该协议，提供了帮助。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介
何德林 区块链技术爱好者，热衷于区块链业务创新研究与分析，欢迎加微信号:tongxwl

抖抖，在读博士，专注区块链技术研究与行业分析，区块链项目私募基金，微信 jonas-meng

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

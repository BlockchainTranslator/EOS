> 本文翻译自：https://github.com/EOSIO/eos/wiki
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)
>
> 翻译时间：2017-12-31
>
> 本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

### 词汇表

| Taxonomy Term 分类术语  | Synonym 同义词        | block.one Definition block.one 的定义|
|-----------------|----------------|----------------------|
| Account	      | 			   | An on-chain identifier made up of native and/or custom permissions that are assigned one or more keys or accounts. |
| 帐户 | |由本地和/或自定义权限组成的链上标识符，分配有一个或多个密钥或帐户。|
| Authority		  |          	   | An abstract of permissions that represent how permissions are organized in reality that are bound to an individual or groups of individuals |
| 授权 | |		权限摘要，表示事实上权限是如何组织，这些权限绑定到个人或由个人组成的组|
| Block           | Blk            | A confirmable unit of the Blockchain. Each block contains zero or more Transactions, as well as a cryptographic connection to all prior blocks. When a block becomes "irreversibly confirmed" it's because a supermajority of Block Producers have agreed that the given Block contains correct Transactions. Once a Block is irreversibly confirmed, it becomes a permanent part of the immutable Blockchain. |
| 块	| Blk	| 区块链上的可被确认的单位。每个块包含零个或多个交易，以及与所有先前块的加密连接。当一个块被“不可逆转地确认”时，意味着绝大多数的块生产者已经认可给定的块上包含正确的交易。一旦一个块被不可逆转地确认，它就成为不可变的区块链中永恒的一部分。|
| DAC             |                | Decentralized Autonomous Collective, or Decentralized Autonomous Corporation. Described in detail here (need link). |
| DAC	| | 去中心化的自治集体或去中心化的的自治公司。点这里有详细的介绍 (链接尚未提供)|
| DAO             |                | Decentralized Autonomous Organization. |
| DAO | |		去中心化的自治组织。|
| DPoS            |                | Delegated Proof of Stake. Also, "Democracy as Proof of Stake." DPoS is one of a collection of consensus algorithms, i.e. methods by which block producers can agree (reach consensus) on which transactions and which blocks are "real" and should be confirmed and treated as irreversible. |
| DPoS	| |	委托权益证明。也称 “民主权益证明”。 DPoS 是共识算法集合中的一种，它规定了哪个块生产者可以同意（达成共识）哪些交易和哪些块是“真实的”并且应该被确认和被视为不可逆的方法。 |
| Key pair		  | keys		   | A public key and its corresponding private key |
| 密钥对 |	密钥 |	公钥其及相对应的私钥 |
| larimer         |                | 1/1000 of an EOS (token) `0.0001 EOS` |
| 拉里默	|	| 1/1000 个 EOS (即 0.0001 EOS) |
| Master Password | 			   | The password used to to unlock (decrypt) a wallet file |
| 主密码 | |		用于解锁（解密）钱包文件的密码 |
| Message         | Msg            | A change to the Blockchain. One or more messages make up a Transaction. |   
| 信息	| Msg |	用来改变区块链。交易由一条或多条消息组成。|
| Oracle          |                | "An oracle, in the context of blockchains and smart contracts, is an agent that finds and verifies real-world occurrences and submits this information to a blockchain to be used by smart contracts." *[Source](https://blockchainhub.net/blockchain-oracles/)* |
| Oracle | |		“在区块链和智能合约的背景下，oracle 是一个代理，负责发现并验证真实世界的事件，并将这些信息提交给区块链，以供智能合约使用。” *[来源](https://blockchainhub.net/blockchain-oracles/)* |
| Permission      |				   | A weighted security mechanism that determines whether or not a message is properly authorized by evaluating its signature(s) authority |
| 权限 | |		一个加权的安全机制，通过评估其签名来确定一个消息是否被正确授权 |
| Private Key	  |    			   | A secret key used to sign transactions |
| 私钥 | | 		用于签署交易的密钥 |
| Public Key	  | pub key		   | A publicly available key that is transmitted alongside a transaction |
| 公钥 | 	pub key | 	与交易一起发送的公开的密钥 |
| Smart Contract  |                | A smart contract is a computer protocol intended to facilitate, verify, or enforce the negotiation or performance of a contract. |
| 智能合约 | |		智能合约是旨在促进，验证或执行谈判或履行合同的计算机协议。 |
| Transaction     | Tx, Txn        | A complete all-or-nothing change to the Blockchain. A combination of one or more Messages. Usually, the execution of a Smart Contract.
| 事务 |	Tx，Txn |	使区块链进行全面更改或完全没有更改。一个或多个消息的组合。通常，如智能合约的执行。|
| Wallet		  |  			   | An encrypted file generated and/or managed by a client (for example, `eosc`) that manages private keys and facilitates the signing of transactions in a secure manner. Wallets may be in a locked or unlocked state. |
| 钱包 | | 		由客户端（例如eosc）生成和/或管理的加密文件，用于管理私钥并便于以安全方式签署交易。钱包可处于锁定或解锁状态。 |
| Witness         | block producer | The node that is currently taking its turn producing the "right now" block for the blockchain. Or, a member of the group of nodes who have been elected to take such turns. Synonymous with 'block producer' |
| 见证人 |	块生产者 |	目前轮流到可以生成区块链当前区块的节点。或者，此轮被推选出的节点组中的成员。与'块生产者'同义 |                               


----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

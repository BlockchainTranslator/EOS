### EOSIO Dawn 3.0 Now Available 
---

>本文翻译自：https://medium.com/eosio/eosio-dawn-3-0-now-available-49a3b99242d7
>
>作者：Danial Larimer ,  CTO at Block.One
>
>译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [JohnnyJ](https://github.com/BlockchainTranslator/EOS)
>
>翻译时间：2018-4-11

***

Block.one is excited to announce the first feature-complete pre-release of EOSIO, Dawn 3.0. This pre-release represents a major milestone on the road to EOSIO 1.0 targeted for release in June 2018. Our world wide team of developers have been working around the clock to make EOSIO the most powerful platform for building blockchain applications. It has been four months since we released EOSIO Dawn 2.0 and we have a lot to show for it. 

Block.one 公司很高兴地宣布：具备完整特性的EOSIO 软件先行版本Dawn 3.0首发。这个先行版本是通往2018年6月EOSIO 1.0版本发布之路上的重要里程碑。我们全球的开发者团队一直都在日以继夜地工作，志在让EOSIO 软件成为开发区块链应用最强大的平台。自EOSIO Dawn 2.0的发布以来，已经过去了4个月，今天，我们有很多内容要展示给大家。

Building state of the art blockchain architectures is a process where designs change as we learn. Many of the features we have completed in Dawn 3.0 were not even contemplated in the original EOSIO White Paper, but were discovered in the process of building a platform that is performant, flexible, and easy to develop on.

最先进的区块链架构的建立是一个过程，在我们学习的过程中个，设计也发生了一些变化。Dawn 3.0 中已经完成的很多特性，我们在最初的EOSIO 白皮书中甚至都没有想到，这些特性是在创建一个高性能、灵活且易于开发的平台过程中被发现的。

### Scalability Features | 可扩展性

Scalability means the ability to scale to meet market demand. At every step our team has factored future scaling needs into the design. That said, Dawn 3.0 only implements a fraction of the potential optimizations that will allow EOSIO to scale. We have designed EOSIO so that future implementations can utilize parallel computation to accelerate throughput without hard forking changes.

可扩展性是指满足市场需求的扩展能力。在软件开发过程中的每一步，我们团队都将未来扩展的需求作为设计考虑因素。即便如此，Dawn 3.0 也仅仅实现了可以让EOSIO 软件具备扩展能力的一小部分潜在优化方案。在不进行硬分叉的情况下，EOSIO 软件未来可以通过并行计算快速提高交易量。

### Inter-Blockchain Communication | 跨链通信

Inter-blockchain communication is the ultimate scalability feature — the holy grail — that the industry has been searching for with proposals such as side-chains, plasma, and sharding. Inter-blockchain communication enables one blockchain to verify the authenticity of an event on another blockchain in a provably secure manner. The goal is for inter-blockchain communication to be as secure as intra-chain communication between smart contracts and we think we have achieved that goal.

业内人士一直在寻找可以解决可扩展性问题的“圣杯”，比如：侧链、plasma、分片。跨链通信才是最终的可扩展性解决方案。通过可验证的、安全的方式，跨链通信技术使得一条链验证另一条链上所发生的交易的真实性成为可能。目标是要让跨链通信达到和链内智能合约通信一样的安全级别，我认为我们已经达成了这个目标。

From our perspective, inter-blockchain communication is nothing more than having the ability to implement a light client as a smart contract. A light client is able to validate transactions from a blockchain without having to process the entire blockchain. This in turn means building a proof-of-stake blockchain with efficient and secure light-client validation. Light-client validation must therefore be factored into the protocol design, as it is almost impossible to implement after the fact.

在我们看来，跨链通信所需的技术和将一个轻量级客户端作为智能合约来运行所需的技能没什么差别。在不同步整条链数据的情况下，一个轻量级客户端可以验证链上的交易。这意味着我们要建立一个有效、安全且具备轻客户端验证功能的授权股份权益区块链系统。因此，在协议设计中必须考虑轻客户端验证，因为，事后很难实现这一功能。

### Sparse Header Verification | 稀疏区块头验证

Traditional light clients are expected to process every block header and then validate proofs relative to those block headers. Now that EOSIO can generate two blocks every second, a blockchain would require at least 2 transactions-per-second to process every block header. This does not scale for scenarios where there is relatively infrequent inter-blockchain communication. To solve this problem, we created the first blockchain with byzantine fault-tolerant sparse-header validation. Specifically, it requires more than 2/3 (e.g. 15+ out of 21) of the block producers to be corrupt in order to attempt to deceive a light client. Furthermore, light clients only need to process block headers where the set of active block producers changes and those that include relevant inter-blockchain messages. This dramatically reduces the overhead in maintaining a byzantine fault-tolerant light client, and dramatically increases the efficiency of inter-blockchain communication.

传统的轻客户端需要处理每一个区块头，然后验证和区块头相关的证据。现在，EOSIO 软件每秒可以产生2个区块，要求至少以每秒2笔交易的速度处理每一个区块头。在目前还不常见的跨链通信场景中，这是无法扩展的。为了解决这个问题，我们首创采用了具有拜占庭容错稀疏区块头验证特性的区块链。具体来讲，试图蒙骗一个轻客户端需要有超过三分之二（比如：21个BP中超过15个BP）的区块生产者是腐败的。另外，轻客户端只需要处理那些活跃区块生产者更改的区块头，以及那些包括相关跨链信息的区块头。这很大程度上减少了维护一个具备拜占庭容错特性轻客户端所需要的工作量，同时，也大幅提高了跨链通信的效率。

### Context Free Actions | 上下文无关动作

Context free actions are one of the key features that enable efficient inter-blockchain communication. They are special actions in that they can be included in a transaction yet do not depend upon blockchain state, hence they are “context-free”. An example of a context free action is the validation of a merkle proof or signature. Because these computations are context-free they can be trivially validated in parallel and the computation can be pruned from replay.

上下文无关动作是实现高效跨链通信的核心特性之一。这些动作是非常特殊的，不依赖于区跨链状态，这些动作就可以被包含在一个交易中，因此，被称为“上下文无关”。上下文无关动作的一个例子是：默克尔证明或者签名的验证。这些计算是和上下文无关的，可以被并行验证，这些计算可以通过重放删除。

Every context-free action can also reference a special prunable data section of a transaction. This means that large merkle proofs can be pruned and their expensive computation skipped during blockchain replay.

每一个上下文无关动作都可以参考一个交易中一段特殊的可编辑数据段。这意味着大量的默克尔证明内容可以被删除，并且在区块链重放过程中，验证这些默克尔证明所需的昂贵计算过程可以被跳过。

Context free actions enable us to parallelize the vast majority of the overhead associated with inter-blockchain communication. They also enable us to parallelize and prune the overhead of computationally expensive privacy techniques such as confidential transactions, bullet proofs, and zkSNARKs.

上下文无关动作让绝大多数与跨链通信有关的资源开销并行化成为可能。同样，这也使得需要昂贵计算资源开销的保密技术的计算并行和计算资源消耗减少成为可能，比如：机密交易、bullet proofs（一种零知识证明技术）、zkSNARKs（ZCash的零知识证明技术）。

In order to incentivize the use of context free actions, block producers will only charge users a fraction of the CPU usage when a calculation is performed as part of a context free action instead as part of a traditional transaction.

为了激励上下文无关动作的使用，当用户执行上下文无关动作的计算而不是传统的交易计算时，区块生产者只会对用户收取很小一部分的CPU使用费用。

### Context-Free Inline Actions as Events | 上下文无关内联动作作为事件

One of the features EOSIO Dawn 2.0 developers were looking for was an efficient way to generate events that get processed by outside sources. In Ethereum these events are used to report structured information about the internal operation of a contract. With the addition of context-free actions, we also have the potential to do context-free inline actions. An inline action is one that is generated by contract code and executed as part of the current transaction. A context-free inline action can be processed cheaply and in parallel. Because all inline actions are also included in the merkle root, it is possible to use these actions as provable notifications to outside services and other blockchains.

开发者希望 EOSIO Dawn 2.0 提供的特性之一就是：通过有效的方式生成由外部资源处理过的事件。在以太坊区块链网络中，这些事件用于播报智能合约内部操作的结构化信息。增加了上下文无关动作后，我们也有可能执行上下文无关内联动作。一个内联动作由合约代码生成，也是当前合约执行内容的一部分。上下文无关内联动作的处理成本非常低，而且可以并行执行。由于所有的内联动作都包含在默克尔根中，所以，可以将这些动作作为可证明的通知用到链外服务和其他区块链上。

### Transaction Compression | 交易压缩

There are many transactions that have a lot of compressible data. One of the most unavoidable examples of this is the contract WebAssembly code itself. Other examples include the ABI specification and the Ricardian contract associated with an account/contract. Some applications, such as social media, may also want to include compressible user generated content in the blockchain.

很多交易中包含了大量可压缩的数据。最无法回避的情况之一就是智能合约使用的 WebAssembly 代码本身。其他的情况包括ABI 规范和与账户、合约相关的 Ricardian 合约。有一些应用，比如社交媒体，也许也需要在区块链中保存压缩过的由用户产生的内容。

By utilizing transaction compression the blockchain can more efficiently store and transmit large numbers of transactions and bill users less for transactions with compressible data than transactions with incompressible data.

和未经数据压缩的交易相比，利用交易数据压缩的区块链在有效存储和传输大量交易的同时，对使用数据压缩交易的用户收取更少的费用。

### Interpreter & Just-In-Time Compilation | 解释器和JIT编译器

One of the biggest changes from Dawn 2.0 is the abstraction of our WebAssembly runtime environment. Dawn 3.0 now utilizes the Binaryen WebAssembly interpreter by default rather than the faster Just-in-Time (JIT) compiler. This decision reduces performance but increases stability and standards conformance while allowing us to trivially swap in the higher performant JIT environment when desired. The interpreter also solved one of the biggest challenges we faced with Dawn 2.0: the delay caused by compiling a contract. In the future we can use the interpreter to get a slower, but lower-latency, execution of freshly deployed contracts while we compile and optimize the contract in the background. This double-implementation means all of our unit tests are tested against both compiled and interpreted code, so we can discover potential non-deterministic or non-standards-conforming behavior before we deploy the hybrid approach.

和 Dawan 2.0相比，Dawan 3.0最大的改变之一是 WebAssembly 运行环境的抽象化。Dawan 3.0默认使用了二进制的 WebAssembly 解释器，而不是速度更快的JIT 编译器。这个决定降低了系统的性能表现，但是提高了系统的稳定性和标准的一致性，同时，也允许我们在需要的时候，方便地切换到高性能的JIT 环境。解释器的使用也解决了我们在 Dawn 2.0 中面临的一个最大挑战：编译合约导致的延迟。将来，当我们在后端编译和优化合约时，我们可以用解释器来执行最新部署的合约，虽然速度更慢了，但是延迟更低。这样的双重部署意味着所有的单元测试都可以用编译器代码和解释器代码来测试，因此，在部署这种混合方式之前，我们可以发现潜在的非最终状态的交易或者非标准确认格式的交易。

### Resource Metering Rate Limiting | 资源使用比例限制

With Dawn 3.0 we now have an entirely new resource rate limiting system. Perhaps the biggest change is the introduction of an objective instruction-counting algorithm. When we set out to build EOSIO, we had a goal to use entirely subjective rate limiting and enforcement. What we discovered was that the cost of subjective enforcement was almost identical to a more objective approach. We now utilize a hybrid solution where users are billed for objective use, but block producers place subjective wall-clock time limits on contracts as well. These subjective limits prevent abuse of variance in the objective billing.

在 Dawn 3.0 版本中，我们建立了一个全新的资源使用比例限制系统。其中最大的变化是引入了一套客观指令数算法。当初在我们刚开始创建 EOSIO 软件时，我们的目标是使用完全主观的资源使用比例和执行系统。后来我们发现主观执行系统的成本几乎和客观系统相当。现在，我们采用了这种混合方案，这样用户就可根据客观的使用量付费，但是区块生产者还是会将主观的挂钟时间限制植入在合约代码中。这些主观的资源限制是为了防止客观资源使用账单中的差异被滥用。

One of the major reasons we adopted this approach was to allow individual transactions to perform many more calculations than was previously possible. It is now theoretically possible for a block to include a single transaction that takes 100 ms to run, whereas under the old model every transaction had to run in under 1 ms.

我们采用这个方案的一个主要原因是：让单个事务和之前相比可以完成更多的计算。从理论上讲，一个区块可以包含一个需要100 毫秒运行的交易，而在老的模型中，每笔交易都必须在1 毫秒以内运行。

Another change to rate limiting is the separation of limits from the need to define a token. This allows EOSIO to be used in private, permissioned blockchains without any use of tokens. The public blockchain can adopt a system contract which implements the limits via staking, and the community can dynamically upgrade how resources are allocated independently from how the allocation is enforced.

另一个针对资源使用比例限制的更改是：将区块链系统中定义的通证和系统资源使用限制分离。如此，在不使用通证的情况下，EOSIO软件可以被当作私有链使用。公有链可以采用实现了资源锁定限制方式的系统合约，同时，社区会根据通证抵押分配执行情况，动态调整系统资源的独立分配。

### 500 ms Block Interval & BFT DPOS | 500毫秒块间隔和 BFT DPOS

With Dawn 3.0 we have moved from a 3 second block interval to a 0.5 second interval. This dramatically reduces the latency until confirmation. When combined with BFT DPOS, transactions can be irreversibly confirmed in under 1 second. The latency until irreversibility has major implications for inter-blockchain communication, because another blockchain must wait for irreversibility before incorporating a proof from a foreign chain. Two EOSIO-based blockchains should be able to perform a round-trip communication in under 3 seconds. A similar communication pattern on Ethereum would take 9 minutes, and on Bitcoin would take 3+ hours.

在 Dawn 3.0 中，我们将原先的3秒块间隔提升到了0.5秒，大幅降低了区块达到确认状态所发生的延迟。结合 BFT DPOS 共识机制，交易可以在1秒内达到不可逆的确认状态。达到不可逆状态所发生的延迟对跨链通信有重要意义，因为，跨链通信中的一条链在采用外部链的验证结果之前，必须等到外部链上的区块达到不可逆状态。两条基于 EOSIO 软件的区块链应该可以在3秒内完成一次来回的跨链通信。以太坊网络上类似的通信模式要花9分钟，比特币网络上类似的通信模式要花超过3小时。

BFT DPOS has not yet been implemented as it is a non-hard-forking optimization. We will be implementing BFT DPOS prior to releasing EOSIO 1.0.

BFT DPOS共识机制是一种非硬分叉优化方案，目前在 Dawn 3.0中还没有使用，我们会在 EOSIO 1.0 软件发布之前采用BFT DPOS共识机制。

### BIOS Architecture | BIOS 架构

The BIOS architecture is one of the biggest architectural changes from EOSIO Dawn 2.0. Under EOSIO Dawn 3.0, the vast majority of the blockchain business logic has moved into a smart contract which can be dynamically updated by the community without a hard fork. A bare-bones EOSIO blockchain is now a single producer without any tokens, voting, or delegated proof-of-stake. The only thing implemented in the core blockchain code is the permission system which includes the ability to create accounts, deploy contracts, and enforce resource quotas. Everything that makes the blockchain Delegated Proof of Stake including the token, voting, staking, and resource allocation is now defined by the Web Assembly based system contract.

自从EOSIO Dawn 2.0发布以来，最大的一个架构更改就是 BIOS 架构。在 EOSIO Dawn 3.0中，绝大多数的业务逻辑已经被写入智能合约，这些智能合约可以在不进行硬分叉的情况下，由社区通过投票进行动态更新。极简版的 EOSIO 软件就像一个没有通证、没有投票、没有授权股份权益证明机制的单个生产者，唯一写入核心区块链代码的是一个权限系统，这个系统包含创建账户、部署合约和实施资源分配的功能。一个具有授权股份权益证明共识机制的区块链系统需要的通证、投票、资源锁定和资源分配这些特性，现在都被定义在基于Web Assembly 代码的系统合约这一层。

With this new architecture, we have been able to focus development on the static non-WebAssembly portions of the blockchain. These are the portions that are most critical for stability — and most difficult to upgrade. Between the release of EOSIO Dawn 3.0 and EOSIO 1.0 we will be working out the final details of the system contract, staking, and voting.

基于这一新的架构，我们可以专注于静态的、非WebAssembly 部分的区块链软件开发，这部分开发对系统的稳定性最为重要，同时，这部分开发在未来也是最难升级的部分。从现在开始到EOSIO 1.0 发布这段时间内，我们会完成系统合约、资源锁定、投票这些特性的最终执行细节。

### Security Features | 安全特性

Security is crucial for any computing system, and we have designed EOSIO to be the most secure blockchain on the market. Security is a multi-dimensional problem that must factor in the risk of hacking, hardware failure, lost hardware, and lost passwords. Hardware wallets are good at protecting against hacking, but could nevertheless lock you out of your account if they fail. Furthermore, paper backups of hardware wallets can be lost or stolen.

安全对任何计算机系统来说都是至关重要的，我们设计的 EOSIO 软件系统是目前市场上最安全的区块链系统。安全性是一个多维度的问题，必须将黑客攻击风险、硬件故障、硬件丢失、密码丢失这些因素考虑进去。硬件钱包在防止黑客攻击方面是非常好的选择，但是，硬件钱包故障时，也可能让你无法使用你的钱包账户，而且，硬件钱包的纸质备份也可能被盗或者丢失。

### Security Delayed Transactions | 安全的延时交易

One of the most significant features of EOSIO Dawn 3.0 is the addition of a user-configurable delay for different actions. With this delay, a transaction must be broadcast to the blockchain for a number of hours or days before it can be applied. During this delay period the user can take measures to reset their account with higher-permission levels and then cancel the transaction. This is a significant improvement over other blockchains where you don’t know you have been hacked until it is too late to do anything about it.

EOSIO Dawn 3.0 最为显著的特性之一是：针对不同的操作，用户自己可以配置延迟执行。有了这样的延迟执行功能，在交易被真正执行之前，可以提前几小时或者几天被广播到区块链网络，在延迟时间段内，用户可以通过更高阶的账户权限重新设置他们的账户，然后取消之前的延迟交易。和其他区块链相比，这是非常明显的改进。在其他区块链上，直到发生了无法挽回的损失后，你才会知道账户被黑客攻击了。

### Lost Password Recovery | 密码丢失恢复

Every account has at least two permission levels: “owner” and “active”. The owner permission level should be a N of M multisig where there is no N that doesn’t include the owner’s key(s). The owner permission level can reset the active permission any time the active key is lost or stolen.

每一个账户至少有两种权限： Owner 和 Active 。Owner权限是一个需要M个签名中的N个签名才会生效的多签设置，N个签名中必须包含 Owner 自己的一个或多个私钥。当 Active 权限的私钥丢失或者被盗时，Owner 权限在任何时候都可以重置 Active 权限私钥。

If you lose the owner key or your multisig partners are being uncooperative, then the account active permission can request a reset of owner permission after 30 days of owner permission inactivity. The owner authority then has 7 days to challenge the request by updating the active authority.

如果Owner权限私钥丢失或者多签伙伴不配合，同时Owner 权限账户连续30天没有交易，处于静止状态，那么账户的 Active 权限可以请求重置Owner权限私钥。

Under this model, an account owner permission controlled by one or more hardware wallets will be secure against hacking and device failure. If the device were an Apple iPhone with hardware and Fingerprint/Face ID secured private keys, then the attacker would require compromising your multisig partners, physically stealing your phone, and stealing your fingerprint or face. Ideally your multisig partners are also using biometrically secure hardware devices.

在这种模式下，由一个或者多个硬件钱包控制的 Owner权限账户可以抵御黑客攻击和设备失效带来的风险。如果这个设备是一个带有指纹识别或者脸部ID 识别的苹果手机，那么，攻击者就必须同时获得多签伙伴的私钥、偷到你的手机和获得你的指纹或者脸部。在理想情况下，你的多签伙伴也会使用带有生物安全识别系统的硬件装置。

### Transaction Proposal System | 交易提案系统

Multisig is made easier when users can add and remove their permissions independently in their own time, rather than having to gather all the signatures during the limited expiration window of traditional transactions. With the proposal system, anyone can propose a transaction and the parties involved in the transaction can simply approve it. At any time between adding your approval and getting the necessary threshold, your approval can be removed.

多签设置让用户独立地增加和取消账户权限变得更容易，而且用户随时可以操作，不需要像传统的交易那样要求在有限的时间窗口内收集齐所有的签名。结合这个提案系统，任何人都可以提交一个交易，和交易相关的各方都可以方便地批准交易。在你的批准之后和获得必要的threshold函数阀值之间的任何时候，你的批准都可以被取消。

To implement this system, we added new APIs that allow contracts to evaluate whether a set of account permissions is sufficient to authorize a transaction. This allows us to upgrade the multisig process by deploying new WebAssembly rather than requiring a hardfork.

为了实现这个系统，我们新增了很多API，使得合约可以评估一组账户权限是否足以授权一个交易。通过部署新的 WebAssembly 代码而不是硬分叉的方式，我们可以更新多签流程。

### Simplified Contract Development | 简化的合约开发

One of our many goals with EOSIO is to make contract development as simple and painless as possible. If a developer knows how to write a C++ class with methods, then they should be able to write a smart contract with as little boilerplate complexity as possible.

EOSIO 软件的众多目标之一是让合约开发变得尽可能简单和轻松。如果一个开发者知道编写C++ 类语言的方法，那么，他就能够用尽可能小的样板文件编写智能合约。

We are pleased to have simplified our “hello world” contract down to a few simple lines of code. Our toolchain has automated the process of generating contract ABI and dispatching user actions to the methods defined on your class. Developing contracts has never been easier.

我们很高兴已经把我们的“hello world” 这个合约简化成了一些简单的代码行。我们的工具链已经把生成合约ABI的过程自动化，同时，按照你自己定义类的方法调度用户操作。开发合约从未如此简单。

### Floating Point Support | 浮点支持

Part of simplifying smart contract development is making it easier to implement the mathematical algorithms developers need. One of the most difficult aspects of blockchain development has been the lack of floating point math and related power, root, and trig functions. Many algorithms, such as Bancor, are much easier to implement in terms of floating point rather than forcing all computations into error-prone and memory intensive fixed point.

简化智能合约开发的部分目标是为了让智能合约更容易实现开发者所需要的数学算法。区块链开发最难的一个方面是缺少浮点数和相关的幂、根和三角函数。很多算法，比如班科算法，在浮点数方面更容易实现，而不是将所有的计算都强加到容易错误且消耗内存的不动点。

We solved the non-deterministic nature of hardware floating point by integrating a software-floating point library that is used transparently by the WebAssembly contracts. With software floating point we get the benefits of determinism and ease of development at a cost not much greater than fixed point in complex cases. In many cases, fixed point is either more error prone or more memory intensive than the deterministic floating point representation.

我们通过集成一个软件浮点库来解决硬件浮点数的不确定性特质，由 WebAssembly 合约公开透明地使用这个库。有了软件浮点数，我们就可以受益于确定性和开发的便利性，花费的成本并不比复杂情况中不动点的成本高。大多数情况中，和确定性浮点数的表现相比，不动点要么更容易出错，要么更消耗内存。

### C++ Standard Template Library Support | C++ 标准模板库支持

For EOSIO Dawn 3.0, we put significant effort into adding support for the majority of the C++ standard template library. This means developers can use the tools, libraries, and algorithms they are familiar with, while eliminating the potential for bugs caused by non-standard implementations of these algorithms.

在EOSIO Dawn 3.0中，我们付出了极大的努力让系统支持大多数的C++ 标准模板库。这意味着开发者可以使用他们所熟悉的工具、函数库和算法，同时，减少了因使用非标准算法而导致的潜在漏洞。

### Scheduled Transactions | 定时交易

With scheduled transactions, developers can now write contracts that operate forever — provided the contract has sufficient staked bandwidth. Other platforms require off-chain solutions to wake a contract at an appropriate time. With scheduled transactions, we gain efficiency and ease of use without requiring developers to host their own servers to keep a contract running.

有了定时交易，假如合约锁定了充足的带宽，那么，开发者可以编写永久运行的合约。其他的区块链平台需要链外解决方案以便在适当的时候激活一个合约。有了定时交易，为了让一个合约持续运行，开发者就不需要搭建自己的服务器了，这一特性让EOSIO 软件变得高效且易于使用。

### Automatic Scope Detection | 自动域检测

Under EOSIO Dawn 2.0, every transaction was required to declare which data ranges it would access. This was error prone and verbose for developers. Under Dawn 3.0, the block producers are responsible for determining which data ranges are accessed and to deconflict them. This makes all transactions smaller and moves the scheduling overhead to the block producer rather than pushing it back on the user, developer, or full nodes.

在EOSIO Dawn 2.0中，每个交易都必须表明它需要访问的数据范围，这样做很容易出错，同时会让开发者感到繁琐。在Dawn 3.0中，区块生产者负责确定被访问的数据范围，同时化解数据范围冲突。这会让所有的交易变得更小，同时，将资源调度的开销转移到区块生产者那里，而不是加到用户、开发者或者全节点头上。

### MultiIndex Database API | 多重索引数据库 API

EOSIO Dawn 3.0 introduces a new database API that mirrors the boost::multi_index_container. With this API, it is trivial to support database tables that are sorted by multiple keys, find items, use lower/upper bound, and iterate forward and backward over the database. This new API uses an iterator interface which dramatically improves performance for scanning through a table.

EOSIO Dawn 3.0 引入了一种新的数据库API ,这个数据库API映射了boost库：multi_index_container。有了这个API，就可以很方便地支持多个键排列的数据库表、查找条目、lower/upper bound算法的使用、数据库的向前和向后迭代。这个新的API使用了迭代器界面，大幅改进了扫描一个数据表的性能表现。

It is also now possible to have indices on 64 bit, 128 bit, 256 bit, and 512 bit integers as well as 64 bit floating point (doubles). Support for string indices will be added before EOSIO 1.0 is released. This is is a significant improvement in flexibility and ease of development as it is now possible to have almost unlimited number of indexed fields on the same table.

现在也可以有针对64位、128位、256位、512位整数以及64位浮点数（双精度数）的索引。对字符串索引的支持将会在EOSIO 1.0 发布前实现。这是在灵活性和易于开发性方面取得的巨大改进，因为，现在可以在同一数据表中拥有几乎无限数量的索引字段。

### Performance | 性能

Real-world performance is something our team has been monitoring closely, and we are very happy with the results at this time. We have benchmarked our software in several different configurations to understand the lower and upper bound of performance as we enable future optimizations. All of these tests are assuming token transfers to be apples-to-apples comparable to Bitcoin or Ethereum ERC20 token transfers in terms of computational complexity.

现实中的实际性能表现是我们团队一直以来都在密切监测的，目前来看，我们对性能表现的实际结果还是非常满意的。在几种不同的配置情况下，我们已经对软件进行了基准测试，了解了性能表现的上下边界，这让我们能够在未来对性能进行优化。我们假设我们所做的通证转账测试，在计算复杂性方面，是可以和比特币或者以太坊 ERC20 通证转账对应比较的。

### Worst Case — 1000 TPS | 最坏情况 1000 TPS

This is our baseline performance without any optimizations. We are able to sustain over 1000 TPS using a multi-node network running the interpreter with single-threaded signature verification.

1000 TPS是在没有进行任何优化情况下的最差性能表现。在一个运行单线程签名验证解释器的多节点网络中，我们的软件可以支持超过1000 TPS。

### Average Case — 3000 TPS | 一般情况 3000 TPS

Once we turn on the JIT compiler we can sustain 3000 TPS using a multi-node network running the interpreter with single-threaded signature verification.

一旦启用JIT编译器，在一个运行单线程签名验证解释器的多节点网络中，我们的软件可以支持3000 TPS。

### Best Case — 6,000 TPS | 最优情况 6000 TPS

Once we implement parallel signature verification, we can assume the wall-clock-time per-signature will approach 0 as the level of parallelism and the number of signatures increase. We can simulate this environment by disabling signature verification. Under this model we can hit 6,000 TPS on a multi-node network with the JIT compiler.

一旦我们的软件启用并行签名验证，我们可以假定，随着并行度的提高和签名数量的增加，每个签名的挂钟时间会接近于0。我们可以通过禁用签名验证的方式来模拟这样的运行环境，在这种模式下，使用JIT 编译器的多节点网络的TPS可以达到6000。

### Theoretical Case — 8,000 TPS | 理论情况 8000 TPS

If we remove the networking code from the equation and focus only on what the CPU is capable of doing with signature verification turned off and using the JIT, then we can hit 8,000 single-threaded transactions-per-second. To go higher than this on a single chain would require implementing parallel execution of the WebAssembly, and a more advanced scheduler. In this same scenario, using the interpreter rather than the JIT, we can see 2700 TPS. This suggests that the relatively simple change of enabling the JIT will give us about 3x performance increase for transfers. These measurements were made on a MacBook 2.8Ghz i7.

如果我们从方程式中删除网络代码，仅仅专注于CPU的处理能力，在禁用签名验证的同时使用JIT编译器的情况下，单线程版本软件的TPS可以达到8000。在一条单链上想要超过 8000 TPS，需要实现WebAssembly 环境中的并行执行，同时，需要一个更高级的调度器。在同样的场景中，使用解释器而不是JIT编译器，TPS可以达到2700。这意味着做一个简单的更改，从而启用JIT编译器，转账性能可以提高3倍。这些测试是在一台MacBook 2.8Ghz i7的电脑上完成的。

### Unlimited Transactions Per Second | 无限TPS

The definition of a “transaction per second” is often an apples to oranges comparison. With inter blockchain communication we can divide the workload between as many blockchains as we want. Tokens can reliably and securely be transferred between different chains. With 1000 chains operated in parallel by the same (or different) block producers we could see millions of transactions per second. This represents a practical realization of the theoretical scaling proposals presented by other blockchains.

TPS 这个数据通常被人们用在不同的场景中进行比较。在跨链通信的场景中，我们可以根据我们的意愿将交易量分配到尽可能多的链中。在不同的链间，通证可以被安全可靠地转账。如果由相同（或者不同）的区块生产者并行运行着1000条链，那么，我们可以看到百万TPS。这意味着其他区块链项目提出的理论上的扩展性能提案可以在实际应用场景中实现了。

We strongly encourage block producers of EOSIO based public networks to operate as many chains as necessary to meet user demand. All chains could use the same token as the basis for staking and resource allocation. This will create the maximum possible network effect around a single token and leverage the trust and security of economic incentives created by high-market capitalization tokens.

我们强烈建议EOSIO 公共网络上的区块生产者到尽可能多的侧链上生产区块，以满足用户的需求。所有的侧链都可以使用同一种通证作为资源锁定和资源分配的工具。这样可以最大化单一通证的网络效应，同时，也可以获得高市值通证带来的可信任且安全的经济奖励。

Applications like exchanges, currencies, and social media can trivially balance their loads across many parallel chains.

交易所、货币和社交媒体这些应用可以很方便地通过使用并行侧链的方式平衡他们的交易负载量。

### The Road Ahead | 未来之路

With EOSIO Dawn 3.0 the focus was on stability of the core platform. Over the next month we will be preparing the final system contract which implements all of the staking, voting, and governance mechanics. We will also be finalizing our token standard.

EOSIO Dawn 3.0专注于核心软件平台的稳定性。接下来的几个月中，我们将准备最终的系统合约，这个系统合约会实现资源锁定、投票和治理机制这些特性，同时，软件系统中的通证标准也会最终确定。

Once the system contract has matured to our satisfaction we will launch a new public test network. Until then we have greatly simplified the process for starting your own test network and developing your own applications. We are shutting down the current public test network for the next couple of weeks while we prepare the new test network to minimize developer confusion.

一旦我们对系统合约的成熟度感到满意，我们会发布新的公开测试网络。在此之前，我们已经大大简化了启动测试网络和开发应用的流程。接下来几周，我们会关闭目前的公开测试网络，同时，我们也会充分准备好新的测试网络，以减少因切换测试网络对开发人员造成的困扰。

### Summary | 总结

EOSIO Dawn 3.0 is a developer release designed to be “feature complete” with stable APIs. We believe the platform is now stable enough for serious application developers to start building their applications. EOSIO has become far more powerful and easy to develop for than we had conceived a year ago.

EOSIO Dawn 3.0是一个开发者版本，它的设计目的是成为一个提供稳定API、特性完备的软件平台。我们认为这个平台现在已经足够稳定，可以让应用开发者开始在上面创建他们的各种应用。和一年前我们构想的平台相比，现在的EOSIO 平台更强大，也更易于开发应用。

Our team is growing and development is occurring at record pace. Our repository has been one of the top 10 most active C++ repositories in all of github for the past month. Everything is on track for a high quality public release of EOSIO 1.0 in June!

我们的团队在以创纪录的速度成长和发展。我们的资源库是过去一个月 GitHub上所有资源库中10个最活跃的C++ 资源库之一。一切都在按计划进行，目标是为了在6月发布高质量的EOSIO 1.0 软件版本。

***

**区块链中文字幕组**

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

**本文译者简介**

金强（JohnnyJ ) 区块链爱好者、投资者，微信：john82king，公众号：时间的朋友时间的力量。

本文源自新闻媒体Medium，如果侵权，请与译者联系删除。

译文版权所有，转载需完整注明以上内容。

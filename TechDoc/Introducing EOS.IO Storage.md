Introducing EOS.IO Storage--EOS.IO 存储简介
--------------------------------------------------

> 本文翻译自：https://github.com/EOSIO/Documentation/raw/master/EOS.IO%20Storage.pdf
> 
> 译者：区块链中文字幕组 [Haoshi hu](https://github.com/huhaoshi10000)
> 
> 翻译时间：2017-09-20

---------------------------
Abstract: ​EOS.IO Storage is a proposed decentralized file system designed to
give everyone the ability to permanently store and host files accessible by any
web browser. Unlike some other proposed alternatives, there would be no
upfront fee or ongoing charge for storage or bandwidth on EOS.IO Storage
aside from a completely refundable deposit. Users must hold tokens while they
need storage and bandwidth and may sell tokens when storage and bandwidth
is no longer required. Built on the InterPlanetary File System (IPFS) and the
EOS.IO software, EOS.IO Storage will be a service provided by block producers
for those who hold tokens on a blockchain that adopts the EOS.IO software. The
block producers would be incentivized to replicate and host these files, allowing
anyone with an Internet browser to access them.

摘要：EOS.IO存储是一种建议的去中心化的文件系统，旨在为每个人提供永久存储和托管任何网页浏览器可访问的文件的能力。
与其他建议的替代方案不同，除了完全可退还的存款之外，EOS.IO存储上的存储或带宽将不会产生预付费用或固定费用。用户可以在需要存储和带宽的时候持有代币，并且在不需要存储和带宽的时候出售代币。
基于星际间文件系统（IPFS）和EOS.IO软件，EOS.IO存储服务将由区块生产者提供，并且为那些持有基于EOS.IO软件的区块链的令牌的人提供服务。区块生产者被激励去复制和托管那些允许任何人通过Internet浏览器的访问的文件。

Background--背景
----------

IPFS
----

IPFS is an emerging standard for storing content addressable files. Content-addressable
storage is a mechanism for storing information that can be retrieved based on its content rather
than its location. Stated another way, all files stored using IPFS are given names derived from
the hash of their content.

IPFS是用于存储内容可寻址文件的新兴标准。内容可寻址存储是一种基于其内容而不是其位置来检索的信息的存储机制。换句话说，使用IPFS存储的所有文件的名称都是从其内容的散列中生成。

What this means is that the same file will have the same name on every computer, and the
contents of that file can never change without also changing the name of the file. It also means
that when you download a file from a server you can verify that it is the exact file you requested
by recalculating the name based on the content provided by the server.

这意味着同一个文件在每台计算机上都具有相同的名称，并且更改文件内容会导致文件名称的更改。这也意味着当您从服务器下载一个文件夹时，您可以根据服务器提供的内容重新计算文件名称来验证文件是否为您请求的文件。

IPFS also provides a peer to peer (P2P) network layer that allows computers to discover and
share files based on their deterministic names. However, this P2P network layer does not
provide or guarantee storage, hosting, or bandwidth. As it is currently structured, the IPFS
network expects users to provide their own servers and related infrastructure.

IPFS还提供P2P网络层，允许计算机根据其唯一的名称发现和共享文件。然而，该P2P网络层不提供或保证存储，托管或带宽。根据目前的结构，IPFS网络希望用户能够提供自己的服务器和相关的基础架构。

EOS.IO
------

EOS.IO is software designed to allow anyone to create and launch their own smart contract
platform. A smart contract is self-executing computer code that automatically enforces its terms
and validates user actions. Blockchains are secured by reaching consensus on the order of
valid user actions and then applying their deterministic state machine to derive the current
application state.

EOS.IO是一款允许任何人创建并启动智能合约的软件平台。智能合约是一段自动执行条款并验证用户操作的计算机代码。区块链通过在有效的用户操作顺序上达成共识来确保安全，然后应用其确定性状态机来获取当前应用状态。

Because the security of a blockchain is highly dependent upon it being heavily replicated and
100% available, it is not suitable for storing large, potentially prunable, files. For example, a high
performance blockchain processing 1 million transactions per second will grow at over 100 MB
per second, assuming 100 bytes per transaction. To remain practical, these blockchains may
periodically truncate their transaction history and take snapshots of the state. Furthermore, the
blockchain ledger is replicated to every node which creates an unnecessary level of replication
overhead. Storing bulk data in either the transaction log or the blockchain state is neither a
practical nor a scalable solution to decentralized file storage.

因为区块链的安全性很大程度上取决于它被大量复制并且100％可用，不适合存储大型的可能被修改的文件。例如，假定每个事务为100个字节，一个每秒可以处理100万笔交易的高性能区块链会以超过100MB/s的速度增长。为了保持实用性，这些块链可能定期截断其交易并且记录区块链状态快照。除此以外，区块链分类账簿会被复制每一个节点从而导致不必要的备份开销。在事务日志或区块链状态中存储批量数据是一个既不实用的也不可扩展的分散文件存储解决方案。

To address this problem, some blockchain applications have opted to store the IPFS file names.
This process ensures that the smart contracts are referring to specific and incorruptible files, but
makes no guarantees about the availability of those files.


为了解决这个问题，一些块链应用程序选择存储IPFS文件名。这个过程确保了智能合同是引用确定和不可破坏的文件，但是不保证这些文件的可用性。

IPFS does not guarantee the availability of files; a file may disappear if nodes decline to make it
available. An inaccessible file may ultimately break the utility and purpose of a smart contract as
parties are no longer able to verify the meaning of the file. For example, consider a smart
contract that references a will by its IPFS name. That contract may fail if the file containing the
will is unavailable, which could happen if someone forgets to pay for ongoing file hosting, or if
the deceased person’s estate fails to arrange to pay for file hosting. Smart contracts cannot
simply store IPFS filenames and be confident that the file will always exist and be accessible
when needed.

IPFS不保证文件的可用性;如果节点拒绝使自己可用，那么文件可能会消失。一个无法访问的文件可能最终会破坏智能合同的效用和目的，因为各参与方无法验证文件的含义。例如，考虑一个通过其IPFS名称引用遗嘱的合同。可能由于忘记支付进行中的文件托管服务或者死者的财产未能安排支付档案托管，导致包含遗嘱的文件不可用，从而引起合约失败。智能合同不能只需存储IPFS文件名，并确信文件将始终存在并在需要时可访问。

Filecoin, Maidsafe, Siacoin, and Storj
--------------------------------------

Filecoin is a decentralized storage network created by the team behind IPFS for the purpose of
incentivising the storage of files on IPFS. This protocol creates a blockchain that utilizes the
latest advancements in cryptographic proofs to generate trustless proof-of-storage and
proof-of-replication. The protocol then incentivises individuals to run auditors that spot-check
storage providers.

Filecoin是一个由IPFS后面的团队创建去中心化的存储网络，用于激励在IPFS上存储文件。根据加密证明的最新发展，此协议创建一个无信任存储证明\(proof-of-storage\)和备份证明\(proof-of-replication\)。然后该协议激励个人运行审核员来抽查存储提供者。

Filecoin is the currency that storage providers are paid when someone wishes to store or fetch a
file from the network. The underlying idea is that there are vast quantities of unused storage
sitting on home computers and servers around the globe. Filecoin aims to enable the owners of
this unused storage to monetize it, while eliminating any need for 3rd parties to trust the storage
providers, or vice versa.

当有人想从该网络中存储或者获取一份文件时，存储提供者会收到Filecoin代币。其基本思想是存在大量未使用的存储空间存在在全球的家用电脑和服务器上。Filecoin旨在使拥有未使用存储空间的所有者从中获利，同时减少对第三方对存储提供者的信任需求，反之亦然。

The model adopted by Filecoin is similar to other decentralized storage solutions such as
Maidsafe, Storj, and Siacoin. They all attempt to collect micropayments for both the storage
and retrieval of data, and they all create their own dedicated currency. Furthermore, all of these
products target home computer storage providers renting out space located behind slow internet
connections. Lastly, they all require users to continually purchase cryptocurrency to pay for
storage and bandwidth. This means the files may not be available for the general public to
access for free via their browser.

Filecoin采用的模式与其他分散式存储解决方案Maidsafe，Storj和Siacoin类似。他们都试图收集用于存储和数据检索的小额支付，并且他们都创建自己的专用货币。除此之外，所有这些产品的目标都是出租位于低速网络连接下的存储空间的家庭电脑存储提供者。最后，他们都要求用户不断购买加密货币来支付存储和带宽。这意味着这些文件可能不适用于大众通过浏览器免费访问。

The cost of storage and bandwidth on these networks may be higher than that offered by cloud
service providers such as Amazon S3. For example, at the time of this writing, Storj charges
$0.05 per GB of download whereas Amazon charges $0.01 per GB downloaded. Storj charges
$0.015 per GB per month whereas Amazon charges $0.0125 per GB per month for infrequently
accessed storage (Glacier).

这些网络上的存储和带宽成本可能高于使用云服务提供商如Amazon S3的成本。例如，在撰写本文时，Storj收费每GB下载$0.05，而亚马逊每GB下载$0.01，Storj收费每月每GB$0.015，而亚马逊每月每GB收取0.0125美元非频繁访问存储。

It is not clear that the designs of Filecoin, Maidsafe, Siacoin or Storj scale up to many users
and many accesses. As the number of users and files grows, the number of recurring payments
will also grow. This will place increasing stress on their single-threaded blockchains as the base
transaction load grows just to maintain the status quo. Users wanting to store files will need to
set up their own server to make automatic crypto payments or they will have to log in every
month to do it manually. The overhead of zero-knowledge proofs and spot checks consume
bandwidth and CPU resources whose cost may be greater than the actual cost of the storage
and bandwidth being managed.

尚不清楚Filecoin，Maidsafe，Siacoin或Storj的设计是否可以扩展适用于大量用户和大量访问。随着用户和文件的数量的增加，定期付款的数量也将增长。随着基础事务负载的增长，光是维持现状就会不断给基于单线程的区块链造成压力。需要存储文件的用户甚至需要设置自己的服务器以进行自动加密付款或者他们将不得不每月登录手动执行付款。零知识证明和抽查会消耗带宽和CPU资源，其成本可能大于存储的实际成本并管理带宽。

DropBox, Mega, GoogleDrive, and iCloud
--------------------------------------

These services provide users 2GB to 50GB of free storage and some bandwidth. These
services are freemium products used to upsell their paid products. Unfortunately, these
services do not have a common file naming system, like IPFS, nor do they integrate with an
open P2P network, nor are they decentralized. Each is entirely controlled by its respective
single legal entity, and it is not uncommon for one of these services to have some down time or
to change their pricing model.

这些服务为用户提供2GB至50GB的免费存储空间和一些带宽服务。这些服务是出售加价付费产品的免费增值服务。不幸的是这些服务既没有公共文件命名系统，如IPFS，也不集成一个开放的P2P网络，也不是去中心化的。每个都完全受到各自的控制单一法律实体，并且停机时间或改变他们的定价模式不是一个罕见的情况。

The Design of EOS.IO Storage--EOS.IO存储设计
-------------------------------------------

For the purpose of this paper we will assume someone has deployed an EOS.IO based
blockchain with native tokens called TOK. A filesystem smart contract, @storage, is deployed
to the TOK blockchain, this smart contract allows every user to define a directory structure
where all files are links to an IPFS file.

为了本文的目的，我们假设有人部署了基于EOS.IO一个名为TOK的本地代币的区块链。在TOK区块链上部署了一个文件系统智能契约@storage，这个智能契约允许每个用户定义一个目录结构其中所有文件都是指向IPFS文件的链接。

A user creates a link to an IPFS file by signing a transaction that is broadcast to the TOK
blockchain. The transaction includes the path relative to the user’s “home directory”, the
corresponding IPFS file name, and the size of the file. The user also specifies whether they
want the file be stored and hosted by the TOK block producers.


用户通过签署一个事务并且在TOK链上广播来创建到IPFS文件的链接。该事务包括相对于用户的“主目录”的路径，对应的IPFS文件名和文件大小。用户还可以指定它们希望文件由TOK区块生产者存储和托管。

The user will then upload the file to one of the block producers via standardized REST
Application Programming Interfaces (APIs) defined by the EOS.IO Storage software. Once the
producer verifies the file has the size and the IPFS name indicated by the user, the producer will
broadcast a transaction to the TOK blockchain indicating the file has been received. The other
block producers will then replicate the file over an IPFS network.

然后，用户将通过由EOS.IO存储软件定义的标准化REST应用程序编程接口（API）将文件上传到其中一个区块生产者。生产者验证文件具有由用户指定的大小和IPFS名称，即制作者会在TOK区块链上广播一个事务，表示该文件已被接收。其他区块生产者将通过IPFS网络复制该文件。

Storage Quota--存储配额
----------------------

Collectively, the block producers vote on how much total storage capacity they would like to
offer. The median value of the producer votes is the expected capacity that all producers will
have to provide. Block producers are incentivised to increase capacity as they compete for
votes from TOK holders. A grace period may be offered during which those below the mean can
increase their available capacity.

总的来说，区块生产者投票表示他们想要的总存储容量。生产者投票的中位数是所有生产者必须提供的预期容量。生产者会被激励去提高存储容量来竞争TOK持有人的投票。在宽限期中，那些提供的存储空间低于平均值的生产者可以增加其可用容量。

In order for a user to utilize storage, they must first reserve it by locking TOKs in the @storage
smart contract - essentially a fully refundable security deposit. A user may unlock their TOKs by
releasing the block producers from the requirement to store and host the files, although these
files may still be available via other IPFS hosts. Assuming the price of TOK is constant, the
ongoing cost of storage and bandwidth is 0. The market value of TOK may rise or fall while
one’s files are stored. Either way, an individual will pay 0 net TOK for their storage and
bandwidth usage.

为了使用户能够使用存储，他们必须首先通过在@storage智能合合约锁定TOK来预定它- 基本上是一笔完全可退还的押金。用户可以通过解除对区块生产者存储和托管文件的要求来解锁他们的TOK，尽管这些文件仍然可以通过其他IPFS主机可用。假设TOK的价格是恒定的，该持续的存储和带宽成本为0。当某人的文件被存储期间，TOK的市场价值可能会上涨或下降。无论哪种方式，一个人无需为其存储和带宽使用支付任何TOK。


The amount of storage available per TOK token is determined using the Bancor algorithm that
maintains a Constant Reserve Ratio (CRR) of 10. A CRR means that the storage will never be
completely consumed, as the price (locked TOK per megabyte) will rise as free capacity shrinks.
A CRR of 10 is based on the fact that most TOK holders will not demand access to all of their
storage, which therefore minimizes the cost of over-provisioning the network.

每个TOK令牌可用的存储量是由Bancor算法确定，该算法维持恒定储备比率（CRR）为10。CRR意味着存储容量永远不会被用完，因为对应的开销（每兆字节锁定的TOK）将随着空闲容量的缩小而上升。基于大多数TOK持有人不要求访问他们所有的存储的事实，CRR被设定为10来最小化网络过度配置的成本。

The equation to the right defines Balance as the total
amount of storage consumed by all parties. Supply is the
total amount of storage the block producers physically
have, and CCR is the constant reserve ratio.

下面的方程将Balance定义为所有各方消耗的储存量的总数。Supply是供应量区块生产者的实际拥有的存储总量，而CCR是恒定的准备金率。

![image](https://github.com/BlockchainTranslator/EOS/blob/master/TechDoc/pics/Introducing%20EOS.IO%20Storage-Price.jpg)

Collectively the block producers may adjust the CRR (up or down), or adjust the total storage
supply (up or down), but may never decrease the storage supply below what has already been
claimed (balance).

总体上来说，生产者可以调整CRR（向上或向下）或调整总存储量供应（向上或向下），但将存储供应绝不可能低于已经声明的存储空间。

Objectionable Data--不良数据
---------------------------

EOS.IO software is designed to combine smart contracts with legally binding arbitration. In
addition to having code, these contracts can also impose subjective requirements on the
parties. Block producers and storage users enter into a smart contract paired with a legal
contract that agrees block producers may be responsible for controlling objectionable content.
Pursuant to the arbitration dispute resolution mechanism provided by the network, anyone can
seek a ruling that any stored file is objectionable and should be deleted if its storage and hosting
is in violation of laws or other contracts.


EOS.IO软件旨在将智能合约与具有法律约束力的仲裁结合起来。除了有代码之外，这些合约也可以强加主观要求到各个参与方。区块生产者和存储用户签订智能合同协议的同时，也附带签订一个法律合约允许区块生产者负责控制不良数据内容。根据网络提供的仲裁争议解决机制，任何人都可以发起判定任意存储文件是非法的裁定，并且该文件将被删除如果对应的存储和托管违反法律或其他合同。

The EOS.IO Storage protocol will allow a block producer to delete any file where required by
law or arbitration. Not all block producers will be subject to the same laws and regulations;
therefore, it will be up to the community of TOK holders to determine whether block producers
are deleting files fairly and reasonably. Misbehaving producers can be voted out and/or brought
before arbitration under the blockchain’s constitution.

EOS.IO存储协议将允许块生产者删除任何法律或仲裁要求删除的文件。不是所有的块生产者都要遵守相同的法律法规;因此，由TOK持有者的社区决定区块生产者是否在正确合理地删除文件。有不正当行为的生产者可以在区块链宪法的仲裁之前被投票否决。

It is important to understand that the use of the IPFS network places fundamental limits on the
ability of EOS.IO Storage to censor data. While the block producers may no longer store or
serve a particular file, the file may still be available if someone else hosts it on the IPFS network.
The identifier remains an accurate descriptor of the file, and any independent full node may also
employ an independent IPFS node to access the file. An individual may choose to host it
themselves or pay someone else to host the file on their behalf. In this case the individual or
their service provider will assume the liability for hosting and serving the file.

重要的是使用IPFS网络从根本上限制了EOS.IO存储器检查数据的能力。如果其他人将文件托管IPFS网络，即使当块生产者不再存储或提供一个特定的文件，该文件可能仍然可用。标识符仍然是文件的准确描述符，任何独立的完整节点也可以使用独立的IPFS节点访问文件。个人可以选择自己托管它或付款给他人来代替他们托管文件。在这种情况下，个人或他们的服务提供商将承担托管和提供文件的责任。

Privacy--隐私
-------------

EOS.IO Storage is a platform for hosting public data. Users who need privacy may apply an
encryption algorithm prior to uploading their files. While the content of the encrypted file will be
private, the identity of the blockchain account that uploads the file will still be visible to everyone.
Decentralization and Replication


EOS.IO存储是托管公共数据的平台。需要隐私的用户可以在上传文件之前对其应用加密算法。尽管加密文件的内容将是私人，但是上传文件的区块链帐户的身份仍然可以被所有人看到。

去中心化和复制

The core of EOS.IO Storage will be IPFS, which provides a decentralized network where
anyone can host files that are discoverable by their address. The block producers represent 20
or more unique and independent individuals or organizations each of which could replicate and
host the data in different jurisdictions around the globe. These producers could already be
located in data centers capable of supporting high-throughput EOS.IO transaction volume. As
long as at least 1 of the 20 block producers is online and makes the document available, then
the file will be available to everyone.

EOS.IO存储的核心将是IPFS，它提供了一个去中心化的网络，在这个网络上任何人都可以托管通过其地址识别的文件。区块生产者代表20或更独特和独立的个人或组织，每个人或组织都可以在全球不同的司法管辖区复制和托管数据。这些生产者可以是位于能够支持高吞吐量EOS.IO交易量的数据中心。只要20个块生产者中至少有一个在线并提供文档，该文件对所有人都是可用的。

This approach will provide a level of replication and bandwidth availability that is significantly
greater than other decentralized solutions which use a lower level of replication. The reliability of
the service will also be significantly greater because block producers need to maintain uptime to
keep their votes and get paid for producing blocks.

通过这种方法提供的复制和带宽可用性将显著大于使用较低级别复制的其他分散式解决方案。由于区块生产者需要维持正常运行时间保留他们的投票并获得生产块的报酬，该服务的可靠性也将大大增加

According to the proposed storage smart contract and corresponding legal obligations, block
producers who are not in the top 25 by total votes will not be obligated to offer the EOS.IO
Storage service; however, they should indicate their ability to enable the service quickly once
they are voted into the top 25.

根据提出的存储智能合同和相应的法律义务，不在总票数前25名的生产者将无法提供EOS.IO存储服务;但是，在被选入前25名后，它们应该表明他们能够快速启用服务的能力。

Economics of EOS.IO Storage--EOS.IO存储的经济学
----------------------------------------------

There is no such thing as a free lunch, so who is actually paying for the storage and bandwidth
provided by the block producers? Existing decentralized solutions all rely on monthly
micropayments, but this is likely not sustainable as it creates an ever-growing base load of
transfers and is difficult to automate without trusting a 3rd party with ability to make payments
on your behalf. Furthermore, micropayments create transactional friction which discourages
adoption. In practice we typically see strong consumer resistance to micropayments in favor of
flat fee or one-time payments .

天下没有一个免费的午餐，所以是谁实际在支付由区块生产商提供的存储空间和带宽？现有的去中心化解决方案都依赖于每月小额支付，但这是不可持续的，因为它创造了不断增长的基本转账负载，并且很难在不信任具有付款能力的第三方的情况下进行自动化。小额支付创造了不利于大规模采纳的交易阻力。我们通常看到消费者对支付小额贷款的抵制并且偏爱固定费用或一次性付款[^1]。

1
Storage Economics--储存经济学
---------------------------

With EOS.IO Storage all TOK holders will be paying for this via a portion of the 5% EOS.IO
annual inflation. More specifically, those who will be storing files are exposed to this supply
inflation as they are unable to sell their TOK until they delete their files. Those who require
permanent storage effectively burn their TOK. As long as the rate of new storage requests is
locking up TOK faster than the TOK inflation rate, then the TOK currency will undergo effective
monetary deflation. This will in turn increase the value of the TOK paid to block producers and
enables them to expand the supply of storage.

使用EOS.IO存储的所有TOK持有人将通过EOS.IO每年5％的通货膨胀的部分来支付该费用。更具体来说，在已存储文档的用户删除文档之前，由于无法出售TOK，他们面临这种供应通货膨胀。那些需要永久存储的用户将经济有效地消耗他们的TOK。只要新存储请求锁定TOK的速率比TOK通货膨胀率快，那么TOK货币将会有效货币通货紧缩。这将反过来增加向区块生产者支付的TOK的价值使他们能够扩大存储供应。

In the event that there is a significant reduction in storage demand, unlocked TOK may enter the
market causing effective price inflation in excess of the natural inflation. In other words, the price
of TOKs may fall and the amount of storage block producers can afford to maintain will
decrease. Fortunately, due to the lower demand, producers can simply decommission drives to
cut costs and reduce the available capacity. Alternatively, they could lower the reserve ratio
used to calculate the number of TOKs that must be locked up to reserve storage capacity.

如果存储需求大幅度减少，解锁的TOK可能进入市场导致有效价格通胀超过自然通胀。换句话说，价格的TOK可能会下降，区块生产商可以维持的存储容量也会下降。幸运的是，由于需求下降，生产者可以简单地减少驱动器数量降低成本也从而降低可用空间。不然，他们也可以降低用于计算锁定的TOK数量的恒定储备比率（CRR）来预留存储容量。

The bottom line is that those who require storage pay for it via the time-value of money. This
should result in no micropayments, no transactional friction, and no surprise fees.

底线是那些需要存储的人通过金钱的时间价值来支付费用。从而取消小额支付，交易阻力，和惊喜费用。

Bandwidth Economics--带宽经济学
-----------------------------

A person who uploads and stores a file is likely very different from the individual who would
download the file. Consider the example of a decentralized variant of YouTube. In this example
someone uploads a home movie which is then viewed by millions of people. The publisher of
the video does not want to or is unable to pay for the bandwidth consumption of a million
viewers.

上传和存储文件的人可能与下载该文件的个人有很大的不同。请假设YouTube的去中心化版本，有人上传了一部家庭电影，然后被数百万人观看。发布视频的人不想或无法支付百万观众带来的带宽消耗。

In this situation, it would be ideal for each individual to pay for their own bandwidth. Once again
this is a situation where micropayments are not a viable solution because the cost of the
1 See for example http://www.dtc.umn.edu/~odlyzko/doc/price.war.pdf page 5.

在这种情况下，每个人为自己的带宽付费是理想的。这又是一个小额支付不是可行的情况，因为它的成本交易（心理和网络）成为有效妨碍大规模采用的收费墙。也就是说，所有用户永远锁定足够的TOK来合理的满足每个人的平均带宽需求，而不用感觉每次观看他们都被收取费用。

transaction (mental and network) becomes an effective paywall that will hinder adoption. That
being said, it should be entirely reasonable for all users to lock up enough TOK to permanently
cover all of their average individual bandwidth needs without feeling like they are being charged
per view.


In addition to giving all users with TOK bandwidth, the block producers can offer a freemium
service to all internet users that is subsidized by the TOK holders via inflation. It would be up to
each block producer to determine how much free service it will offer to anonymous internet
browsers, and it would be up to TOK holders to determine which block producers to vote for and
how much to pay them.

除了给所有用户提供TOK带宽外，区块生产者可以提供免费增值服务给所有由TOK持有人通过通货膨胀补贴的互联网用户。每个区块制造商自主决定将向匿名互联网浏览器提供多少免费服务。由TOK持有者决定向哪个区块生产商投票和支付金额。

In addition, the individual who uploads the file may choose to subsidize the bandwidth of those
downloading it, e.g. a film studio distributing a movie trailer.

此外，上传文件的个人可以选择提供那些下载它的带宽费用，例如分发电影预告片的电影制片厂。

Conclusion--结论
---------------

EOS.IO Storage has the potential to fundamentally change the decentralized storage market by
revolutionizing the economic model. Eliminating the overhead of micropayments and the
perception of cost will enable innovative applications, such as decentralized video hosting,
which were not previously viable. For the first time, a decentralized, cryptographically-secured
platform may be able to offer a hosting service competitive to the current freemium, centralized,
providers.

通过彻底改变经济模式，EOS.IO存储有潜力从根本上改变去中心化存储市场。消除小额贷款的开销和对成本的新理解将促进应用程序的创新，如从前不可行的去中心化的视频托管。这是史上第一次，一个由分布式加密保护的平台提供托管服务，可以媲美由中心化供应商提供的免费增值服务的托管服务。

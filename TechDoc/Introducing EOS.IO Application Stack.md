Introducing EOS.IO Application Stack--EOS.IO 应用程序栈
------------------------------------------------------

> 本文翻译自：https://steemit.com/eos/@eosio/introducing-eos-io-application-stack
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)  [Xuming Meng](https://github.com/jonas-meng)
>
> 翻译时间：2017-10-11

---------------------------
After three years of experience with BitShares and Steem, it has become abundantly clear that developing decentralized applications requires much more than a fast blockchain. It also requires infrastructure capable of offering a usable experience to millions of concurrent users. In the early days of steemit.com, users were expected to provide their own image hosting. This made the interface difficult to use and prone to broken images.

在 BitShares 和 Steem 的三年经验之后，开发去中心化的应用程序需要的不仅仅需要一个高速的区块链，它还需要能够为数百万并发用户提供可用体验的基础设施。在 steemit.com 的早期，用户期望提供自己(链上)的图像托管。这使得界面难以使用，容易出现图像破损。

![image](https://github.com/BlockchainTranslator/EOS/blob/master/TechDoc/pics/introducing-eos.io-application-stack.png)

With the EOS.IO software, we, at block.one, envision a world where block producers provide general purpose infrastructure that allows developers to build and deploy their applications without having to run any servers themselves. This includes applications as complex as [steemit](https://steemit.com/), [DTube](https://dtube.video/), and [decentralized exchanges](https://bitshares.org/).

使用 EOS.IO 软件，我们在 block.one 设想了一个世界，其中区块生产者提供通用基础架构，允许开发人员在无需运行任何服务器的情况下构建和部署应用程序。 这包括像 [steemit](https://steemit.com/)，[DTube](https://dtube.video/) 和 [decentralized exchanges](https://bitshares.org/) (去中心化交易所) 这样复杂的应用程序。

EOS.IO Storage--EOS.IO 存储
---------------------------
EOS.IO Storage is a decentralized file system designed to give everyone in the world with Internet access the ability to permanently store and host legal files which are accessible by any browser. Unlike current alternatives, there are no fees for storage or bandwidth on EOS.IO Storage. Built on IPFS, EOS.IO Storage is a service provided by block producers for those who hold a blockchain’s native tokens. EOS.IO block producers will replicate and host token-holders’ files on the IPFS network as well as provide https endpoints allowing anyone with a browser to access the files.

EOS.IO 存储是一种去中心化的文件系统，旨在为世界各地的互联网用户提供永久存储和托管任何浏览器可访问的合法文件的能力。与目前的替代方案不同，EOS.IO 存储没有存储或带宽费用。基于 IPFS，EOS.IO 存储是由区块生产者为持有该区块链的原生代币的用户提供的服务。EOS.IO 区块生产者将在 IPFS 网络上复制和托管代币持有者的文件，并提供允许任何人通过浏览器访问这些文件的 https 端点。

Collectively the producers will reach consensus on how much storage they are willing to provide in exchange for their compensation (block rewards). Block producers who offer more storage for the same reward are likely to earn more votes from token holders.

生产者们将共同就他们愿意提供多少储存以换取他们的补偿（区块奖励）达成共识。 为相同奖励提供更多储存空间的区块生产者可能会从代币持有者那里获得更多的投票。

More information on EOS.IO Storage will be provided in a future update.

有关 EOS.IO 存储的更多信息将在未来的更新中提供。

EOS.IO Query Services--EOS.IO 查询服务
-------------------------------------
In addition to hosting files, block producers will be expected to run API nodes that are able to query the blockchain database state on behalf of applications. These APIs will likely be a combination of Graph QL and custom Web Assembly based queries. This makes it trivial for applications to get the information they need without having to run and maintain their own scalable hosting services.

除了托管文件外，区块生产者还将运行能够代理应用程序去查询区块链数据库状态的 API 节点。这些 API 可能是基于 Graph QL 和 自定义 Web 组件查询的组合。这使得应用程序无需运行和维护自己的可扩展托管服务就可以获得所需的信息。

block.one will design and publish open source micro-services that block producers can deploy to map the blockchain database state into more traditional databases for the purpose of scaling read access, maintainability, and additional indexing. This software will facilitate application developers and block producers to build web applications that interact with traditional database APIs.

block.one将设计和发布开源微服务，区块生产者可以部署该微服务将区块链接数据库状态映射到更传统的数据库中，其目的是为了扩展读访问能力，可维护性和附加索引。该软件将帮助应用程序开发人员和区块生产者构建与传统数据库 API 进行交互的Web应用程序。

Resource Limits--资源限制
------------------------
Applications consume bandwidth, computation, and storage both on the blockchain and for the interface. Block producers will necessarily have to rate limit access to prevent abuse. This is accomplished for file downloading and API queries the same way bandwidth and CPU time is measured for blockchain updates. Users who hold a small amount of native tokens in a staking contract should be able to have a reasonable level of free access to most applications.

应用程序在区块链和接口上都占用带宽，计算和存储。区块生产者必须通过访问限制来防止滥用。对于文件下载和 API 查询的访问限制是通过与测量区块链更新的带宽和CPU时间相同的方式来实现的。在股权合约中持有少量原生代币的用户应该在合理级别上享有对大多数应用程序免费访问的能力。

The usage model will support balancing resource usage billing to either the individual users downloading the file or to the individual who uploaded it in the first place. This mirrors the model where websites pay to provide hosting but adds the flexibility of transparently moving the bill and rate limiting to the users who ultimately have control over their consumption. This is critical for bandwidth intensive applications like dtube.com .

资源使用模型将支持在下载文件的个人用户和上传文件的用户之间平衡资源使用量的费用。这个模式复制了网站付费提供托管的模式，但增加了将账单和资源限制透明地转移到控制消费的用户的灵活性。这对于像 dtube.com 这样的带宽密集型应用程序至关重要。

Custom Application Infrastructure--定制应用基础架构
------------------------------------------------
block.one recognizes that there are limits to what kind of applications can be built using the general purpose infrastructure provided by block producers. Specifically, applications that require server-side rendering (e.g., steemit) or that require custom database indices maintained by custom micro-services (e.g., market history) may require custom server infrastructure hosted by the application developer or other parties. Developers of these applications can benefit from the same scalable architecture used by block producers to deploy their own customized API and Query Services. This will help developers rapidly bring scalable application infrastructure to market.

block.one 认识到在区块生成者提供的通用基础架构上构建应用程序的局限性。具体来说，需要服务端渲染（如，steemit）或需要由定制微服务维护的自定义数据库索引（例如，市场历史）的应用程序可能需要由应用程序开发人员或其他托管方来定制服务器基础架构。这些应用程序的开发人员可以从被区块生产者用来部署自己的定制 API 查询服务的相同的可扩展架构中获益。这将有助于开发人员快速地将可扩展应用程序基础架构推向市场。

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

抖抖，在读博士，专注区块链技术研究与行业分析，欢迎加微信号:jonas-meng

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

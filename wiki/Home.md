
### **EOS Wiki Navigation**  **维基导航**

> 本文翻译自：https://github.com/EOSIO/eos/wiki
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)
>
> 翻译时间：2017-12-24
>
> 本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

Welcome to the EOS.IO wiki. This resource is intended as a guide for developers looking to interact directly with EOS.IO software. For a higher level explanation of EOS.IO software, please go to the main [README](https://github.com/EOSIO/eos), or the [Documentation Repo](https://github.com/EOSIO/Documentation). Suggestions and contributions are welcome.

欢迎来到EOS.IO wiki。本资源旨在为希望直接与EOS.IO软件交互的开发人员提供指导。有关EOS.IO软件的更高级别解释，请查看 [ README ](https://github.com/EOSIO/eos)及[ EOS 文档](https://github.com/EOSIO/Documentation)。欢迎提供建议或贡献代码。

注：章节前标记为 √ 的为已经翻译

- √ [Glossary | 词汇表](Glossary) 鱼 何德林
- √ [Public Testnet: Dawn 2.0  | 公共测试网：黎明 2.0](Testnet%3A%20Public) 何德林 鱼   
  * [Overview  | 概观](Testnet%3A%20Public#overview)
  * [Nodes  | 节点](Testnet%3A%20Public#nodes)
  * [Public Testnet Endpoints  | 公共测试网络端点](Testnet%3A%20Public#public-testnet-endpoints)
  * [Connecting Local EOSD with Public Testnet  | 连接本地 EOSD 与公共测试网](Testnet%3A%20Public#connecting-local-eosd-with-public-testnet)
  * [Connecting Local EOSC with Public Testnet |  连接本地 EOSC 与公共测试网](Testnet%3A%20Public#connecting-local-eosc-with-public-testnet)

  * [Testnet Accounts  | Testnet 帐户](Testnet%3A%20Public#accounts-on-testnet)
- √ [Programs & Tools |  程序和工具](Programs-&-Tools) 胡亮 陈伟
  * [eosd](Programs-&-Tools#eosd)
  * [eosc](Programs-&-Tools#eosc)
  * [eos-walletd](Programs-&-Tools#eos-walletd)
  * [launcher |  启动器](Programs-&-Tools#launcher)
  * [snapshot  | 快照](Programs-&-Tools#snapshot)
  * [eoscpp](Programs-&-Tools#eoscpp)
- √ [Local Environment  | 本地环境](Local-Environment) 陈伟 胡亮
  * [Getting the code  | 获取代码](Local-Environment#1-getting-the-code)
  * [Building EOS  | 构建 EOS](Local-Environment#2-building-eos)
  * [Docker](Local-Environment#3-docker)

  * [Creating and Launching a Single Node Testnet |  创建和启动单个 Testnet 节点](Local-Environment#4-creating-and-launching-a-single-node-testnet)
  * [Troubleshooting Guide  | 故障排除指南](Local-Environment#5-troubleshooting-guide)
- √ [Accounts & Permissions  | 帐户和权限](Accounts%20%26%20Permissions) 林炜鑫 AMY
  * [Wallets |  钱包](Accounts%20%26%20Permissions#1-wallets)
  * [Accounts |  帐号](Accounts%20%26%20Permissions#2-accounts)
  * [Authorities and Permissions  | 授权和权限](Accounts%20%26%20Permissions#3-authorities-and-permissions)
  * [Putting it all Together  | 组合在一起](Accounts%20%26%20Permissions#4-putting-it-all-together)
- √ [CLI Wallet  | CLI 钱包](CLI%20Wallet) 鱼 Haoshi Hu
  * [Overview  | 概观](CLI%20Wallet#1-overview)
  * [Purpose  | 目的](CLI%20Wallet#2-purpose)
  * [How to run the Wallet  | 如何运行钱包](CLI%20Wallet#3-how-to-run-the-wallet)
  - [Available Commands |  可用的命令](CLI%20Wallet#4-available-commands)
- √ [Database Schema  | 数据库模式](Database%20Schema) 小丹 抖抖
  * [Primary Schema Relationships  | 主要模式关系](Database%20Schema#1-primary-schema-relationships)
  * [Blocks  | 区块](Database%20Schema#2-blocks)

  * [Transactions  | 交易](Database%20Schema#3-transaction)
  * [Messages  | 消息](Database%20Schema#4-message)
  * [Accounts  | 帐号](Database%20Schema#5-accounts-collection)
- √ [[Database API  | 数据库 API](Database%20API) 抖抖 小丹
  * [Overview  | 概观](Database%20API#1-overview)
  * [Modules  | 模块](Database%20API#2-modules)
  * [Indexes  | 索引](Database%20API#3-indexes)
- √ [Smart Contracts  | 智能合约](Smart%20Contract) 张奎 王明华
  * [Introduction to EOS Smart Contract  | EOS 智能合约介绍](Smart%20Contract#1-introduction-to-eos-smart-contract)
  * [Smart Contract Files  | 智能合约文件](Smart%20Contract#2-smart-contract-files)
  * [Checklist  | 清单](Smart%20Contract#3-checklist)
  * [Interacting with Smart Contract Examples  | 与智能合约的交互示例](Smart%20Contract#4-interacting-with-smart-contract-examples)
  * [Writing your first EOS Smart Contract  | 编写您的第一个 EOS 智能合约](Smart%20Contract#5-writing-your-first-eos-smart-contract)
  * [Deploy and update Smart Contract  | 部署和更新智能合约](Smart%20Contract#6-deploy-and-update-smart-contract)
  * [Command Summary |  命令摘要](Smart%20Contract#7-command-summary)
  * [Debugging Smart Contracts  | 调试智能合约](Smart%20Contract#8-debugging-smart-contract)
- √ [[Tutorials |  教程](Tutorials) 王明华 张奎
  * [Accounts & Wallets  | 账户和钱包](Tutorials#1-accounts--wallets)

  * [Currency Contract Walkthrough  | 合约演练](Tutorials#2-currency-contract-walkthrough)
  * [Smart Contract "Hello World" |  智能合约最简实例](Tutorials#3-smart-contract-hello-world)
  * [Tic-Tac-Toe  | 示例：井字棋游戏](Tutorials#4-tic-tac-toe)
- √ [Testnet: Private Testnet： | 测试网络：私有测试网络](Testnet%3A%20Private) 凯风自南 张奎
  * [Testnet Nodes, Networks, and Topology  | 测试网络的节点，网络和拓扑](Testnet%3A%20Private#testnet-nodes-networks-and-topology)
  * [Localhost Networks  | 本地主机网络](Testnet%3A%20Private#localhost-networks)
  * [Network Topology |  网络拓扑结构](Testnet%3A%20Private#network-topology)
  * [The Launcher Application  | 启动程序](Testnet%3A%20Private#the-launcher-application)
- Core Development (Coming Soon)  | 核心开发（即将推出）
  * Code Standards  | 代码标准
  * Github Contribution  | Github 贡献
  * Testing/Debugging  | 测试/调试
  * Benchmarking 基准测试
- Block Producers (Coming Soon)  | 块生产者（即将推出）
  * Prerequisites  | 先决条件
  * Installation  | 安装
  * Configuration  | 配置
  * Tuning  | 调优
- Community Resources (Coming Soon)  | 社区资源（即将推出）
  * Software  | 软件
  * Guides  | 指南
- √ [Command Reference  | 命令参考](Command%20Reference) 楷书 龙心小台
- √ [Doxygen Guidelines  | Doxygen 指南](Doxygen%20Guidelines) 龙心小台 楷书
- [Releases  | 版本发布](Releases)

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

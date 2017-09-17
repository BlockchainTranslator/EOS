# EOS.IO Dawn v1.0 - Pre-Release

@thomasbcox thomasbcox released this 2 days ago · 6 commits to master since this release

# EOS.IO 破晓 v1.0 - 预览版


EOS.IO Dawn 1.0 is the first pre-release of the EOS.IO SDK (Software Development Kit).

The Dawn series of EOS.IO software releases represent early alpha-quality software suitable for use by those looking to get a head start on the EOS.IO ecosystem.


EOS.IO 破晓 1.0 版是 EOS.IO SDK (软件开发工具包) 的首个预览版。

EOS.IO 破晓系列产品代表了早期的 `alpha-quality` 软件，适合那些希望在EOS.IO系统上进行早期开发的人员。


## Table of Contents
---
* Who This Release is For
* Phase 1 Features Included in this Release
* Phase 2 Features Included in this Release

    Phase 2 Features Not Included in this Release

* Known Open Issues

    Benchmarking

* History of Issues

## 目录
---

* 此版本使用人员

* 此版本中包含的第一阶段的功能

* 此版本中包含的第二阶段的功能

    此版本中不包含在第二阶段的功能

* 已知的问题

    性能

* 问题日志


## Who This Release is For
---
Whether you are an experienced C++ developer interested in blockchain or a seasoned blockchain expert you are welcome to experiment with the first pre-release. Some familiarity with Linux/C++ helps.

If you are unfamiliar with both Linux and C++, please wait for a more end-user friendly release. The current release is for experienced developers.

Currently EOS.IO has been tested on Ubuntu 16.10 and Mac OS Sierra. EOS.IO nodes should be able to run on a minimum hardware requirement of Core i7 CPU, 16GB RAM.

## 此版本的使用人员
---
Whether you are an experienced C++ developer interested in blockchain or a seasoned blockchain expert you are welcome to experiment with the first pre-release. Some familiarity with Linux/C++ helps.

If you are unfamiliar with both Linux and C++, please wait for a more end-user friendly release. The current release is for experienced developers.

Currently EOS.IO has been tested on Ubuntu 16.10 and Mac OS Sierra. EOS.IO nodes should be able to run on a minimum hardware requirement of Core i7 CPU, 16GB RAM.


无论您是有经验的并且对区块链开发感兴趣的 `C++` 开发者还是经验丰富的区块链专家，都欢迎你尝试使用我们的第一个预发行版。
如果你熟悉`Linux/C++` 将对你的开发有所帮助。

如果您不熟悉 `Linux` 和 `C++`，请等待我们以后更多的用户友好版本。目前的版本只是为经验丰富的开发人员所准备。

目前EOS.IO已经在`Ubuntu 16.10`和`Mac OS Sierra`上测试过。EOS.IO节点运行的最低硬件要求是`Core i7 CPU，16GB RAM`。


## Phase 1 Features Included in this Release
## 此版本中包含的第一阶段功能
---
Per the EOS.IO Roadmap, this release represents Phase 1, the Minimal Viable Testing Environment.

根据EOS.IO路线图，此版本代表第一阶段功能，最小的开发测试环境。

### Programs

* a standalone node eosd that produces blocks and adds them to the blockchain
* a client eosc that provides a command line interface
* eos-walletd provides a client wallet server
* a utility launcher that creates a local testnet

### 程式

* `eosd` 一个独立运行的节点，生成区块并将它们添加到块链
* `eosc` 一个提供命令行界面的客户端
* `eos-walletd` 提供客户端钱包服务
* 一个创建本地测试网络的实用程序启动器

### Scripts

* build.sh to install dependencies and build eos
* eoscpp for smart contract developers to build contracts

### 脚本

* `build.sh` 安装依赖项并构建eos
* `eoscpp` 为智能合同开发者创建合同


### Example Contracts 智能合约示例
---
#### native contracts,
* native currency
* staking
* producer voting
* code updating
* permission updating

#### 本土合同，
* 本身代币
* 绑架
* 生产者投票
* 代码更新
* 权限更新

#### example contracts 示例合同
* dice
* exchange 交换
* simpledb
* social 社会

### Documentation
---
virtual machine API
deferred / inline messaging
user-local storage for contracts
3 built in database types
basic developer documentation
installation and setup
build and deployment
tutorial for trying out blockchain commands
Doxygen based API reference


### 文档
---
* 虚拟机API
* 延迟/内联消息传递
* 用户本地存储的合同
* 3内置数据库类型
* 基本开发人员文档
* 安装和设置
* 构建和部署
* 块链接命令使用教程
* 基于Doxygen的API参考

## Phase 2 Features Included in this Release
---
In addition, we are releasing these features of Phase 2 ahead of schedule:

functional distributed networks and
first complete rewrite of networking code since BitShares 1.0
virtual machine sandboxing
contracts are limited to about 10 ms execution time
contracts are rejected if they contain floating point operations
contracts are restricted to 64KB of RAM
contracts are restricted to reading database tables in scope

## 本版本中包含的第2阶段功能
---
此外，我们提前发布了第二阶段的这些功能：

* 分布式网络功能和

  首次完成自BitShares 1.0以来的网络代码重写

* 虚拟机沙箱
* 合约的执行时间限制约为10 ms
* 如果合约包含浮点运算，将被拒绝
* 合约限制最大64KB的内存
* 合同限制只在范围内读取数据库表


### Phase 2 Features Not Included in this Release
---
Not included in this release are these features of Phase 2:

* resource usage and rate limiting (Dawn 1.2)
* genesis snapshot of ERC20 (Dawn 1.1)
* inter blockchain communication (Dawn 2.0)
* these native contracts:

    * producer proxy voting (Dawn 1.2)
    * EOS.IO Storage (Dawn 2.0)
    * feature upgrade voting (hard forks) . (Dawn 1.2)
    * stake delegation (renting) (Dawn 2.0)

### 本版本不包括第2阶段功能
---

本新闻稿不包括第2阶段的这些功能：

* 资源使用率和速率限制（Dawn 1.2）
* ERC20的起源快照（Dawn 1.1）
* 块间通信（Dawn 2.0）
* 这些本地合约：

    * 生产者代理投票（Dawn 1.2）
    * EOS.IO存储（Dawn 2.0）
    * 功能升级投票（硬叉）。（黎明1.2）
    * 利益代理（租赁）（Dawn 2.0）


## Known Open Issues
---
APIs incomplete

The APIs are known to be incomplete and are not expected to be stable throughout the 1.x releases.

In v1.0 there is no API exposed for Accounts.
P2P code may become unstable when stressed due to lack of rate limiting
a. work around - keep all producers on a single node

## 已知的开放问题
---
API 尚末完整

已知API是不完整的，预计在整个1.x版本中都不会稳定。

在v1.0中，没有关有帐户的API。
由于缺乏速率限制，P2P代码可能会变得不稳定
a.解决问题 - 将所有生产者保留在单个节点上



## Benchmarking
---
We have tools that have enabled us to benchmark the code at over 10,000 TPS per second under certain controlled conditions, but it remains too early for anyone to reliably reproduce benchmarks and/or interpret the results for a number of reasons:

you must operate a multi-node network and push transactions to multiple different nodes
block production algorithm does not currently time-bound generation which means benchmarks do not properly capture "backlog" or generation bottlenecks
the HTTP interface is currently a bottleneck in submitting transactions to the network
the signature verification is not yet multi-threaded
This release is designed to help developers build their applications. It does not provide a benchmarking toolkit.

## 性能
---

我们已经有一些工具，使我们能够在某些受控条件下以每秒超过10,000 TPS的速度对代码进行基准测试，但是基于以下多种原因，可靠地再现基准和得到一致的结果仍然为时过早：

* 您必须操作多节点网络并将事务推送到多个不同的节点
* 块生产算法当前没有时间限制生成，这意味着基准不能正确捕获“积压”或生成瓶颈
* HTTP接口当前是向网络提交事务的瓶颈
* 签名验证还没有多线程

此版本旨在帮助开发人员构建其应用程序。它不提供基准测试工具包。


## Disclaimer
---
block.one is a software company and is producing the EOS.IO software as free, open source software. This software may enable those who deploy it to launch a blockchain or decentralized applications with the features described above. block.one will not be launching a public blockchain based on the EOS.IO software. It will be the sole responsibility of third parties and the community and those who wish to become block producers to implement the features and/or provide the services described above as they see fit. block.one does not guarantee that anyone will implement such features or provide such services or that the EOS.IO software will be adopted and deployed in any way.

All statements in this document, other than statements of historical facts, including any statements regarding block.one’s business strategy, plans, prospects, developments and objectives are forward looking statements. These statements are only predictions and reflect block.one’s current beliefs and expectations with respect to future events and are based on assumptions and are subject to risk, uncertainties and change at any time. We operate in a rapidly changing environment. New risks emerge from time to time. Given these risks and uncertainties, you are cautioned not to rely on these forward-looking statements. Actual results, performance or events may differ materially from those contained in the forward-looking statements. Some of the factors that could cause actual results, performance or events to differ materially from the forward-looking statements contained herein include, without limitation: market volatility; continued availability of capital, financing and personnel; product acceptance; the commercial success of any new products or technologies; competition; government regulation and laws; and general economic, market or business conditions. Any forward-looking statement made by block.one speaks only as of the date on which it is made and block.one is under no obligation to, and expressly disclaims any obligation to, update or alter its forward-looking statements, whether as a result of new information, subsequent events or otherwise.

## Downloads 下载
---
Source code (zip)
Source code (tar.gz)
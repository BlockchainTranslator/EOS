# EOS.IO Dawn v1.0 - Pre-Release    EOS.IO 破晓 v1.0 - 预览版

本文翻译自：https://github.com/EOSIO/eos/releases

译者：区块链中文字幕组 鱼

翻译时间：2017-09-20

EOS.IO Dawn 1.0 is the first pre-release of the EOS.IO SDK (Software Development Kit).

EOS.IO 破晓 1.0 版是 EOS.IO SDK (软件开发工具包) 的首个预发布版。

The Dawn series of EOS.IO software releases represent early alpha-quality software suitable for use by those looking to get a head start on the EOS.IO ecosystem.

EOS.IO 破晓系列产品代表早期的 alpha 版本，适合那些希望在EOS.IO系统上进行早期开发的人员。


## Table of Contents  

* Who This Release is For
* Phase 1 Features Included in this Release
* Phase 2 Features Included in this Release

    Phase 2 Features Not Included in this Release

* Known Open Issues

    Benchmarking

* History of Issues

## 目录

* 使用人员

* 第一阶段的功能

* 第二阶段的功能

    不包含在第二阶段的功能

* 存在的问题说明

    性能测试

* 问题日志


## Who This Release is For  使用人员

Whether you are an experienced C++ developer interested in blockchain or a seasoned blockchain expert you are welcome to experiment with the first pre-release. Some familiarity with Linux/C++ helps.

无论您是对区块链开发感兴趣的有经验的 `C++` 开发者还是经验丰富的区块链专家，都欢迎你尝试使用我们的第一个预发行版。
熟悉`Linux/C++` 将有助于您的开发。

If you are unfamiliar with both Linux and C++, please wait for a more end-user friendly release. The current release is for experienced developers.

如果您不熟悉 `Linux` 和 `C++`，请等待我们以后更多的用户友好版本。目前的版本只是为经验丰富的开发人员准备。

Currently EOS.IO has been tested on Ubuntu 16.10 and Mac OS Sierra. EOS.IO nodes should be able to run on a minimum hardware requirement of Core i7 CPU, 16GB RAM.

目前EOS.IO已经在`Ubuntu 16.10`和`Mac OS Sierra`上测试通过。EOS.IO节点运行的最低硬件要求是`Core i7 CPU，16GB RAM`。

## Phase 1 Features Included in this Release 第一阶段功能

Per the EOS.IO Roadmap, this release represents Phase 1, the Minimal Viable Testing Environment.

根据EOS.IO路线图，此版本拥有第一阶段的功能，最小的开发测试环境。

### Programs 

* a standalone node eosd that produces blocks and adds them to the blockchain
* a client eosc that provides a command line interface
* eos-walletd provides a client wallet server
* a utility launcher that creates a local testnet

### 应用程序

* `eosd` 一个独立运行的节点，具有生成区块并将它们添加到块链的功能
* `eosc` 一个提供命令行界面的客户端
* `eos-walletd` 提供客户端钱包服务
* 一个创建本地测试网络的实用程序启动器

### Scripts 脚本

* build.sh to install dependencies and build eos
* eoscpp for smart contract developers to build contracts

* `build.sh` 用于安装依赖项并自动构建eos
* `eoscpp` 为智能合约开发者创建合约

### Example Contracts 智能合约示例
--- 
#### native contracts 
* native currency
* staking
* producer voting
* code updating
* permission updating
#### 原生智能合约
* 原生虚拟货币
* 对赌合约
* 生产者投票
* 代码更新
* 权限更新

#### example contracts 示例合约
* dice 底册
* exchange 交换
* simpledb
* social 社会

### Documentation
---
* virtual machine API
* deferred / inline messaging
* user-local storage for contracts
* 3 built in database types
* basic developer documentation
* installation and setup
* build and deployment
* tutorial for trying out blockchain commands
* Doxygen based API reference
### 文档
* 虚拟机API
* 延迟/内联消息传递
* 用户本地存储的合约
* 3内置数据库类型
* 基本开发人员文档
* 安装和设置
* 构建和部署
* 块链接命令使用教程
* 基于Doxygen的API参考

## Phase 2 Features Included in this Release 第2阶段功能

In addition, we are releasing these features of Phase 2 ahead of schedule:

functional distributed networks and
first complete rewrite of networking code since BitShares 1.0
virtual machine sandboxing
contracts are limited to about 10 ms execution time
contracts are rejected if they contain floating point operations
contracts are restricted to 64KB of RAM
contracts are restricted to reading database tables in scope

此外，我们提前发布了第二阶段的这些功能：

* 分布式网络功能和

  首次完成了自BitShares 1.0以来的网络代码重写

* 虚拟机沙箱
* 限制合约的执行时间约为10 ms
* 拒绝包含浮点运算的合约
* 合约内存限制为最大64KB
* 合约限制只能在范围内读取数据库表


### Phase 2 Features Not Included in this Release 本版本不包括的第2阶段功能
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

本新闻稿不包括第2阶段的这些功能：

* 资源使用率和速率限制（Dawn 1.2）
* ERC20的起源快照（Dawn 1.1）
* 块间通信（Dawn 2.0）
* 这些本地合约：

    * 生产者代理投票（Dawn 1.2）
    * EOS.IO存储（Dawn 2.0）
    * 功能升级投票（硬分叉）。（破晓1.2）
    * 利益代理（租赁）（破晓 2.0）

## Known Open Issues 存在的问题说明

APIs incomplete  API 尚末完整

The APIs are known to be incomplete and are not expected to be stable throughout the 1.x releases.

API尚不完整，预计在整个1.x版本中都不会稳定。

In v1.0 there is no API exposed for Accounts.
P2P code may become unstable when stressed due to lack of rate limiting
a. work around - keep all producers on a single node

在v1.0中，没有有关帐户功能的API。
由于缺乏速率限制，P2P代码可能会变得不稳定
a.解决问题 - 将所有生产者保留在单个节点上

## Benchmarking 性能测试

We have tools that have enabled us to benchmark the code at over 10,000 TPS per second under certain controlled conditions, but it remains too early for anyone to reliably reproduce benchmarks and/or interpret the results for a number of reasons:

you must operate a multi-node network and push transactions to multiple different nodes
block production algorithm does not currently time-bound generation which means benchmarks do not properly capture "backlog" or generation bottlenecks
the HTTP interface is currently a bottleneck in submitting transactions to the network
the signature verification is not yet multi-threaded
This release is designed to help developers build their applications. It does not provide a benchmarking toolkit.

我们已经有一些工具，让我们能够在某些受控条件下以每秒超过10,000 TPS的速度对代码进行基准测试，但是基于以下多种原因，能够可靠地再现测试和得到一致的结果仍然为时过早：

* 您必须操作多节点网络并将事务推送到多个不同的节点
* 块生成算法当前没有时间限制，意味着测试不能正确形成“积压”效果或生成瓶颈
* HTTP接口当前是向网络提交事务的瓶颈
* 签名验证功能还没有实现多线程

此版本旨在帮助开发人员构建其应用程序。它不提供基准测试工具包。

## Downloads 下载

* Source code (zip)
* Source code (tar.gz)

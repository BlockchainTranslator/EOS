> 本文翻译自：https://github.com/EOSIO/eos/wiki
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS)
>
> 翻译时间：2018-1-1
>
> 本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

# 钱包的命令行操作

- [1. Overview 概述](#1-overview)
- [2. Purpose 目的](#2-purpose)
- [3. How to run the Wallet 如何运行钱包](#3-how-to-run-the-wallet)
- [4. Available Commands 可用的命令](#4-available-commands)

## 1. Overview | 概述

Program: eos-walletd

Path: eos/build/programs/eos-walletd

程序：eos-walletd

路径：eos/build/programs/eos-walletd

## 2. Purpose | 目的

To store private keys that will be used to sign transactions sent to the block chain. Please note that this is a local process running on your local machine and that it also stores your private keys locally.

用于保存私钥，此私钥用来签署发送到区块链的交易。注意，这是运行在你本地机器上的一个本地进程，因此它也会将您的私钥存储在本地。

## 3. How to run the Wallet | 如何运行钱包

Start eos-walletd process on your local instance as follows:

使用如下命令在本地实例上启动 eos-walletd ：

```
$ eos-walletd
```

You will notice that it creates a folder called data-dir and contains a config.ini file. The configuration file contains the http server endpoint for incoming http connections and other parameters for cross origin resource sharing.

The default parameters should be sufficient for running a local instance of wallet process.

此命令会创建一个名为 data-dir 的文件目录并包含 config.ini 配置文件。此配置文件包含用于配置服务于接入连接的 http 服务器的功能接口，以及用于跨源资源共享的其他参数。

对于运行钱包进程的一个本地实例来说，缺省的参数配置应该已经足够。

## 4. Available Commands | 可用的命令


The command line tool to interact with eos-walletd is called “eosc”. It is found in eos/build/programs/eosc folder.

It provides the following commands to interact with eos-walletd:

可以跟 eos-walletd 进行交互的命令行工具称为 “eosc” 。它位于 eos/build/programs/eosc 文件夹中。

它提供了以下命令来与 eos-walletd 进行交互：

### Create | 创建钱包

```
$ eosc wallet create ${options}
```

Options:

  -n,--name TEXT=default      The name of the new wallet

If you don’t provide an optional name it creates a default wallet.

选项：

  -n,--name TEXT=default      新钱包的名称

如果您没有提供可选名称，则会创建一个默认钱包。

### Open | 打开钱包

Open an already created wallet. You need to open a wallet (if you are not on default wallet) to operate on it.

为了打开一个已经创建的钱包。您需要先使用打开钱包命令（如果您不在默认钱包上）才能对其进行操作。

```
$ eosc wallet open ${options}
```

Options:

  -n,--name TEXT              The name of the wallet to open

选项：

  -n,--name TEXT              要打开的钱包的名称


### Lock | 锁定钱包

Locks a wallet.

锁定一个钱包。

```
$ eosc wallet lock ${options}
```

Options:

  -n,--name TEXT              The name of the wallet to lock

选项：

  -n,--name TEXT              要锁定的钱包的名称


### Unlock wallet | 解锁钱包

```
$ eosc wallet unlock ${options}
```

Options:

  -n,--name TEXT              The name of the wallet to unlock
  --password TEXT             The password returned by wallet create

  选项：

  -n,--name TEXT              需要解锁的钱包名
  --password TEXT             创建钱包时返回的密码


### Import private key into wallet | 将私钥导入钱包

```
$ eosc wallet import ${options} key
```

Positionals:

  key TEXT                    Private key in WIF format to import

Options:

  -n,--name TEXT              The name of the wallet to import key into

位置参数：

  key TEXT                    用来导入的 WIF 格式的文本私钥

选项：

  -n,--name TEXT              要导入密钥的钱包的名称  


### List | 列出钱包

List opened wallets, * = unlocked

列出打开的钱包，标示为 * 的表示已解锁的钱包

```
$ eosc wallet list
```

### Keys | 私钥列表

List of private keys from all unlocked wallets in wif format.

以 wif 格式显示所有解锁钱包中的私钥列表

```
$ eosc wallet keys
```

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

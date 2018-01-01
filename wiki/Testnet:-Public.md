# Testnet: Public  | 公共测试网络


> 本文翻译自：https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [何德林](https://github.com/BlockchainTranslator/EOS)
> 
> 翻译时间：2017-12-24

## Overview | 概述

The Public Testnet exists to support developers and testers who are already working with their own standalone (private) testnet and who want to test their code on a public net, but without the issues and restrictions of working on a public production net ("mainnet").

公共测试网是为了已经在使用自己的独立(私有)测试网的开发人员和测试人员准备的，他们希望在公共网上测试他们的代码，没有公共生产网(主网)上工作的问题和限制。

The Public Testnet allows developers to work with free test tokens, provided during signup. Access the signup page [here](https://docs.google.com/forms/d/e/1FAIpQLSel3HVFb22zYaAJfUtu_IzFgIJ4OATb0jQ3H2FV-HbwnJ090g/viewform).

公共测试网允许开发人员使用免费的测试代币，注册时提供的。[在这里访问注册页面](https://docs.google.com/forms/d/e/1FAIpQLSel3HVFb22zYaAJfUtu_IzFgIJ4OATb0jQ3H2FV-HbwnJ090g/viewform)。

## Differences between Testnet and Mainnet | 测试网和主网的区别

There are several differences between the Public Testnet and the public Mainnet. As of this writing, they include:

公共测试网和公共主网之间有一些区别。在撰写本文时，它们包括:

* Existence. The public mainnet doesn't exist yet, and the public testnet does.

* 存在性。 公共主网还不存在，但公共测试网已存在。

* Genesis block. The mainnet genesis block is different from the testnet genesis block. The Testnet genesis block includes a faucet account and several "initx" accounts (inita - initu) used by the core development team during testing. At least some of these initx accounts are also present in the provided genesis block of standalone private testnets.

*  创世区块。 主网的创世区块与测试网的创世区块不同。测试网的创世区块包含一个faucet帐户和几个“initx”帐户(inita - initu)，在测试期间由核心开发团队使用。其中一些initx帐户也出现在，私有测试网络的创世区块中。

* Resets. The Testnet is subject to resets as needed to support testing.

* 重置。 测试网络需要重置以支持测试。

* Versions. The Testnet can actually include multiple testnets with different addresses and different reset cycles, depending on the needs and desires of the development community.

* 版本。 测试网络实际上可以包含多个测试网络，具有不同地址和不同复位周期，具体取决于开发社区的需求。

* Hosting. The Testnet is currently configured such that block-producing nodes will only be run on hosts set up and operated by the core developers. The Mainnet's block producing nodes will run on hosts selected by a vote of the token holders.

* 主机 测试网络目前已经配置好，区块生成节点只能在核心开发人员设置和操作的主机上运行。主网的块产生节点将运行在由令牌持有者投票选择的主机上。

## Nodes | 节点

The Testnet consists of block-producing nodes and non-producing nodes.

测试网络由区块生成节点和非生成节点组成。

## Public Testnet Endpoints | 公共测试网络的接入点

The following is the list of currently available Public Testnets:
以下是目前可用的公共测试网列表:

Testnet1

HTTP Endpoint: testnet1.eos.io

P2P Endpoint: p2p-testnet1.eos.io:9876

Web Wallet Endpoint: t1wallet.eos.io, t1api.eos.io, t1readonly.eos.io

You can test the connection using curl

你可以用curl进行连接测试。

    $ curl testnet1.eos.io/v1/chain/get_info

## Connecting Local EOSD with Public Testnet | 连接本地EOSD到公共测试网络

In order to connect your local eosd to the public testnet, ensure your machine's clock is accurate and you need to modify your config.ini as the following:

为将您的本地eosd连接到公共测试网络，须确保您的机器时钟是准确的，且需要修改您的config.ini如下:

    Add p2p-peer-address field with one of the valid public testnet p2p endpoint

将公共测试网络的p2p接入点增加到 p2p-peer-address

    p2p-peer-address = p2p-testnet1.eos.io

Modify block-interval-seconds to match the testnet, which is 2. Otherwise, your local eosd node won't be able to sync with the public testnet.

修改block -interval- seconds为2，以匹配网络。否则，本地的eosd节点将无法与公共测试网同步。

    block-interval-seconds = 2

## Connecting Local EOSC with Public Testnet | 连接本地EOSC到公共测试网络

You can connect your local eosc with public testnet by using the http endpoint as the hostname and port 80:

您可以连接本地eosc和公共testnet，通过使用http端点作为主机名，端口为80:

    $ eosc -H ${http_endpoint} -p 80 ${options} ${subcommand}

Furthermore, public testnet does not provide any wallet functionality. In order to be able to sign transaction/ push transaction/ wallet operation, you will need to connect your local wallet with eosc when you are connecting to public testnet. To do so, ensure that you have your local wallet running.

此外，公共测试网络不提供任何钱包功能。为了能够签署交易/推送交易/钱包操作，当你连接到公共测试时，你需要将你的本地钱包与eosc连接起来。要做到这一点，你要确保你的本地钱包在运行。

    $ eos-walletd

    # this will create a data-dir folder inside your current working directory, this data-dir folder will contain your private keys encrypted with the wallet password

    这将在当前工作目录中创建一个data dir文件夹，data dir文件夹将包含你的私匙，使用钱包密码加密过的

Then specify your local wallet endpoint and port when using eosc, unless you override it, wallet_endpoint will be localhost and wallet_port will be 8888.

然后指定你的本地钱包端点和端口，在使用eosc时，除非您重写它。钱包端点是localhost,钱包端口是8888。

$ eosc -H ${http_endpoint} -p 80 ${options} --wallet-host ${wallet_endpoint} --wallet-port ${wallet_port} ${subcommand}

## Accounts on Testnet  | 测试网络帐户

Before you begin first you'll need your account name and EOS public key handy.
在开始之前，您需要获得你的帐户名和EOS公钥。

Discover your account name
获取你的帐户名

Find your account name(s) assigned in genesis by entering the ETH address or EOS Public Key you believe is included in the snapshot into the Account Name Lookup tool

找到您的帐户名，在创世区块中，输入你的ETH地址或者EOS公钥。

If your address is not included in the snapshot, apply for a faucet account

如果您的地址不包含在快照中，请申请一个faucet帐户

Get your EOS public key ready
获取你的EOS公钥

If you're in the snapshot, your EOS Public Key is the key you registered with the EOSCrowdsale contract

如果你在快照中，你的EOS公钥就是你登记在EOS代币销售合约中的KEY。

If you applied for an account through the faucet, your EOS public key is the key you submitted in the faucet account application

如果你通过faucet申请了帐户，你的EOS公钥即是你在faucet帐户中提交的KEY。

Once you have your account name, you can choose how you would like to interact with EOS.

一旦你有的帐户名，你可以选择如何喜欢的方式与EOS交互。

## Web Wallet (End Users) | Web钱包（终端用户）

1. Visit the Testnet Web Wallet. 访问测试网网页钱包

2. Create an account. 创建一个帐户

3. Login.  登陆

4. Click on 'Accounts' in the sidebar. 点击工具栏中的 'Accounts'

5. In the Account input enter the account you acquired in the previous steps.  在'Accounts'中，输入你的账号，通过前面的步骤获取的。

6. In the EOS Active Key and Owner Key fields enter your EOS public key(s). 在'EOS Active Key and Owner Key'中，输入你的EOS公钥。

7. Click "Add Account".  点击 "Add Account"

## Command Line (Developers) | 命令行(开发人员)

You'll need the eos-walletd and eosc binary from recent eosd build, see Local Environment

你需要 eos-walletd 和 eosc binary 从最近的EOS构建中，参加本地环境。

Connect to Public Testnet

连接公共测试网

Import your private key to the wallet with eosc

导入你的私钥到钱包，通过eosc

Learn how to use eosc by either figuring it out yourself with the command reference or with a comprehensive tutorial.

学习如何使用eosc，通过使用命令参考自己搞定或者通过全面的培训。


© 2017 GitHub, Inc.

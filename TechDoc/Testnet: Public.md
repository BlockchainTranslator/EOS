Overview 概述
The Public Testnet exists to support developers and testers who are already working with their own standalone (private) testnet and who want to test their code on a public net, but without the issues and restrictions of working on a public production net ("mainnet").

公共Testnet的存在是为了支持已经在使用自己的独立(私有)Testnet的开发人员和测试人员，他们希望在公共网络上测试他们的代码，但是没有在公共生产网络上工作的问题和限制(“mainnet”)。

The Public Testnet allows developers to work with free test tokens, provided during signup. Access the signup page here.
公共Testnet允许开发人员在注册期间提供免费的测试令牌。在这里访问注册页面。

Differences between Testnet and Mainnet
There are several differences between the Public Testnet and the public Mainnet. As of this writing, they include:
公共测试网和公共主机之间有一些区别。在撰写本文时，它们包括:

Existence. The public mainnet doesn't exist yet, and the public testnet does.
的存在。公共主网络还不存在，公共测试网也不存在。

Genesis block. The mainnet genesis block is different from the testnet genesis block. The Testnet genesis block includes a faucet account and several "initx" accounts (inita - initu) used by the core development team during testing. At least some of these initx accounts are also present in the provided genesis block of standalone private testnets.

《创世纪》。主网络发生块与testnet genesis块不同。Testnet genesis模块包含一个faucet帐户和几个“initx”帐户(inita - initu)，在测试期间由核心开发团队使用。至少其中一些initx帐户也出现在提供的独立的私有testnets的起源块中。

Resets. The Testnet is subject to resets as needed to support testing.

重置。Testnet需要重新设置以支持测试。

Versions. The Testnet can actually include multiple testnets with different addresses and different reset cycles, depending on the needs and desires of the development community.

版本。Testnet实际上可以包含多个具有不同地址和不同复位周期的Testnet，具体取决于开发社区的需求和需求。

Hosting. The Testnet is currently configured such that block-producing nodes will only be run on hosts set up and operated by the core developers. The Mainnet's block producing nodes will run on hosts selected by a vote of the token holders.

托管。Testnet目前已经配置好，这样块生成节点只能在核心开发人员设置和操作的主机上运行。主网络的块产生节点将运行在由令牌持有者投票选择的主机上。

Nodes

The Testnet consists of block-producing nodes and non-producing nodes.
Testnet由块生成节点和非生成节点组成。

Public Testnet Endpoints
The following is the list of currently available Public Testnets:
以下是目前可用的公共测试网的列表:

Testnet1
HTTP Endpoint: testnet1.eos.io
P2P Endpoint: p2p-testnet1.eos.io:9876
Web Wallet Endpoint: t1wallet.eos.io, t1api.eos.io, t1readonly.eos.io
You can test the connection using curl

$ curl testnet1.eos.io/v1/chain/get_info
Connecting Local EOSD with Public Testnet
In order to connect your local eosd to the public testnet, ensure your machine's clock is accurate and you need to modify your config.ini as the following:

为了将您的本地eosd连接到公共testnet，确保您的机器的时钟是准确的，您需要修改您的配置。ini如下:

Add p2p-peer-address field with one of the valid public testnet p2p endpoint
p2p-peer-address = p2p-testnet1.eos.io

Modify block-interval-seconds to match the testnet, which is 2. Otherwise, your local eosd node won't be able to sync with the public testnet.

修改block -interval- seconds以匹配testnet，即2。否则，本地的eosd节点将无法与公共testnet同步。

block-interval-seconds = 2
Connecting Local EOSC with Public Testnet
You can connect your local eosc with public testnet by using the http endpoint as the hostname and port 80:

您可以通过使用http端点作为主机名和端口80来连接本地eosc和公共testnet:

$ eosc -H ${http_endpoint} -p 80 ${options} ${subcommand}
Furthermore, public testnet does not provide any wallet functionality. In order to be able to sign transaction/ push transaction/ wallet operation, you will need to connect your local wallet with eosc when you are connecting to public testnet. To do so, ensure that you have your local wallet running.

此外，public testnet不提供任何钱包功能。为了能够签署交易/推动交易/钱包操作，当你连接到公共测试网时，你需要将你的本地钱包与eosc连接起来。要做到这一点，你要确保你的钱包在当地运行。

$ eos-walletd
# this will create a data-dir folder inside your current working directory, this data-dir folder will contain your private keys encrypted with the wallet password

这将在当前工作目录中创建一个data dir文件夹，这个data dir文件夹将包含使用钱包密码加密的私有密匙

Then specify your local wallet endpoint and port when using eosc, unless you override it, wallet_endpoint will be localhost and wallet_port will be 8888.

然后在使用eosc时指定您的本地钱包端点和端口，除非您重写它，wallet_endpoint将是localhost,wallet_port将是8888。

$ eosc -H ${http_endpoint} -p 80 ${options} --wallet-host ${wallet_endpoint} --wallet-port ${wallet_port} ${subcommand}
Accounts on Testnet
Before you begin first you'll need your account name and EOS public key handy.
在您开始之前，您需要您的帐户名和EOS公钥方便。

Discover your account name

Find your account name(s) assigned in genesis by entering the ETH address or EOS Public Key you believe is included in the snapshot into the Account Name Lookup tool
If your address is not included in the snapshot, apply for a faucet account
Get your EOS public key ready
If you're in the snapshot, your EOS Public Key is the key you registered with the EOSCrowdsale contract
If you applied for an account through the faucet, your EOS public key is the key you submitted in the faucet account application
Once you have your account name, you can choose how you would like to interact with EOS.

Web Wallet (End Users)
Visit the Testnet Web Wallet
Create an account
Login
Click on 'Accounts' in the sidebar
In the Account input enter the account you acquired in the previous steps.
In the EOS Active Key and Owner Key fields enter your EOS public key(s)
Click "Add Account"
Command Line (Developers)
You'll need the eos-walletd and eosc binary from recent eosd build, see Local Environment
Connect to Public Testnet
Import your private key to the wallet with eosc
Learn how to use eosc by either figuring it out yourself with the command reference or with a comprehensive tutorial.
© 2017 GitHub, Inc.

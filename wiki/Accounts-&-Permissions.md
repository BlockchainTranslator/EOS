# Accounts & Permissions
# 账户和权限


> 本文翻译自：https://github.com/EOSIO/eos/wiki/Accounts%20%26%20Permissions
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [林炜鑫](https://github.com/weixin1993)
> 
> 翻译时间：2017-12-31


 - [1.Wallets 钱包](#wallets)
 - [2.Accounts 账号](#accounts)
 - [3.Authorities and Permissions 许可和权限](#permissions)
 - [4.Putting it all Together 把它们放在一起](#together)
-- [4.1 Default Account Configuration (Single-Sig) 默认账户配置（单机）](#4-Putting-it-all-Together)
-- [4.2 Multi-sig Account & Custom Permissions]()

An account is a human-readable identifier that is stored on the blockchain. Every transaction has its permissions evaluated under the configured authority of an account. Each named permission has a threshold that must be met for a transaction signed under that authority to be considered valid. Transactions are signed by utilizing a client that has a loaded and unlocked wallet. A wallet is software that protects and makes use of your keys. These keys may or maybe not be permissioned to an account authority on the blockchain.

帐户是一种人类可读的、存储在区块链中的标识符。每一笔交易都有其权限，这个权限是在一个配置好的账户许可下进行评估的。每个指定的权限都有一个阈值，该阈值必须满足在该许可认为是有效的且签署好的交易。交易的签署是通过使用一个已装载并解锁的钱包的客户端来签署的。钱包是一种保护和使用你的密钥的软件。这些密钥可能、也可能不会授权给区块链上的一个账户许可。

<a name="wallets">
## 1. Wallets | 钱包
Wallets are clients that store keys that may or may not be associated with the permissions of one or more accounts. Ideally a wallet has a locked (encrypted) and unlocked (decrypted) state that is protected by a high entropy password. The EOSIO/eos repository comes bundled with a command line interface client called eosc that includes a wallet as part of its functionality.

钱包是存储密钥的客户端，而这些密钥可能或者可能不会与一个或多个帐户的权限相关联。理想状况下，钱包有一个锁定（加密）和解锁（解密）的状态，该状态由高熵密码保护。
钱包是存储密钥的客户端，这些密钥可能与一个或多个帐户的权限相关联。理想情况下，钱包有一个锁定(加密)和解锁(解密)的状态，该状态由高熵密码保护。EOSIO/eos存储库绑定了一个名为eosc的命令行接口客户端，该客户端包含一个钱包作为其功能的一部分。
</a>

<a name="accounts">
## 2.Accounts | 账号
An account is a human-readable name that is stored on the blockchain. It can be owned by an individual or group of individuals depending on permissions configuration. An account is required to transfer or otherwise push a transaction to the blockchain.

一个帐户是一个人类可读的、存储在区块链的名字。它可以由个人或群体拥有，这取决于权限配置。一个账户被要求转移或将一个交易推到区块链。
</a>

<a name="permissions">
## 3. Authorities and Permissions | 许可和权限

Authorities determine whether or not any given message is properly authorized.

许可决定是否给予适当的授权。

Every account has two native named permissions.

每个账户都有两种本地指定权限。


- `owner` authority symbolizes ownership of an account. There are only a few transactions that require this authority, but most notably, are messages that make any kind of change to the owner authority. Generally, it is suggested that owner is kept in cold storage and not shared with anyone. `owner` can be used to recover another permission that may have been compromised.

- `所有者`许可象征着一个账户的所有权。只有很少的交易需要这个许可，但最值得注意的是，消息是指对所有者许可进行任何更改的消息。一般情况下，建议所有者用冷钱包的方式储存并不与任何人分享。`所有者`可以被用来恢复另一个可能已经被破坏的权限。

- `active` authority is used for transferring funds, voting for producers and making other high-level account changes.

- `活跃者`的许可用来转账、为生产者投票以及使其他高等级账户改变。

In addition to the native permissions, an account can possess custom named permissions that are available to further extend account management. Custom permissions are incredibly flexible and address numerous possible use cases when implemented. Much of this is up to the developer community in how they are employed, and what conventions if any, are adopted.

除了本机权限之外，帐户还可以拥有用于进一步扩展帐户管理的自定义权限。自定义权限非常灵活，并在实现时能够处理大量可能发生的用例。这在很大程度上取决于开发人员如何使用他们，以及采用了什么约定。

Permission for any given authority can be assigned to one or multiple `public keys` or a valid `account name`.

任何授权的权限都可以分配给一个或多个`公钥`或一个有效的帐户名。

</a>

<a name="together">
## 4. Putting it all Together | 把他们放在一起

Below is the combination of all the above concepts and some loose examples of how they might be practically employed.

下面是所有上述概念的组合，以及一些关于如何实际使用它们的简单示例。
</a>

<a name="default">
### 4.1 Default Account Configuration (Single-Sig)
### 4.1 默认账户配置（单机）

This is how an account is configured after it has been created, it has a single key for both the **owner** and **active** permissions, both keys with a weight of 1 and permissions both with a threshold of 1. The default configuration requires a single signature to authorize a message for the native permissions.

这是介绍创建账户后如何配置账户的方式，它有一个用于 **所有者** 和 **活跃账户** 权限的密钥，这两个密钥的权值以及权限阈值都为1。默认配置需要一个签名来授权给本机权限的消息。
</a>


----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

林炜鑫，在读硕士，专注区块链技术研究与行业分析，欢迎加微信号:wxlinzju，微信名：艾米·哈伯

本文由币乎社区（bihu.com）内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------





# Accounts & Permissions
# 账户和权限


> 本文翻译自：https://github.com/EOSIO/eos/wiki/Accounts%20%26%20Permissions
> 
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [林炜鑫](https://github.com/weixin1993) 
       [AMY](https://github.com/lindasayer)
> 
> 翻译时间：2017-12-31


 - [1.Wallets 钱包](#wallets)
 - [2.Accounts 账号](#accounts)
 - [3.Authorities and Permissions 许可和权限](#permissions)
 - [4.Putting it all Together 把它们放在一起](#together)
 - [4.1 Default Account Configuration (Single-Sig) 默认账户配置（单机）](#default)
 - [4.2 Multi-sig Account & Custom Permissions  多重签名账户和自定义权限](#Multi)

An account is a human-readable identifier that is stored on the blockchain. Every transaction has its permissions evaluated under the configured authority of an account. Each named permission has a threshold that must be met for a transaction signed under that authority to be considered valid. Transactions are signed by utilizing a client that has a loaded and unlocked wallet. A wallet is software that protects and makes use of your keys. These keys may or maybe not be permissioned to an account authority on the blockchain.

帐户是一种人类可读的、存储在区块链中的标识符。每一笔交易都有其权限，这个权限是在一个配置好的账户许可下进行评估的。每个指定的权限都有一个阈值，该阈值必须满足在该许可认为是有效的且签署好的交易。交易的签署是通过使用一个已装载并解锁的钱包的客户端来签署的。钱包是一种保护和使用你的密钥的软件。这些密钥可能会、也可能不会授权给区块链上的一个账户许可。


## 1. Wallets | 钱包
<a name="wallets">
Wallets are clients that store keys that may or may not be associated with the permissions of one or more accounts. Ideally a wallet has a locked (encrypted) and unlocked (decrypted) state that is protected by a high entropy password. The EOSIO/eos repository comes bundled with a command line interface client called eosc that includes a wallet as part of its functionality.

钱包是存储密钥的客户端，而这些密钥可能或者可能不会与一个或多个帐户的权限相关联。理想状况下，钱包有一个锁定（加密）和解锁（解密）的状态，该状态由高熵密码保护。
钱包是存储密钥的客户端，这些密钥可能与一个或多个帐户的权限相关联。理想情况下，钱包有一个锁定(加密)和解锁(解密)的状态，该状态由高熵密码保护。EOSIO/eos存储库绑定了一个名为eosc的命令行接口客户端，该客户端包含一个钱包作为其功能的一部分。
</a>


## 2.Accounts | 账号
<a name="accounts">
An account is a human-readable name that is stored on the blockchain. It can be owned by an individual or group of individuals depending on permissions configuration. An account is required to transfer or otherwise push a transaction to the blockchain.

一个帐户是一个人类可读的、存储在区块链的名字。它可以由个人或群体拥有，这取决于权限配置。一个账户被要求转移或将一个交易推到区块链。
</a>


## 3. Authorities and Permissions | 许可和权限
<a name="permissions">
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


## 4. Putting it all Together | 把他们放在一起
<a name="together">
Below is the combination of all the above concepts and some loose examples of how they might be practically employed.

下面是所有上述概念的组合，以及一些关于如何实际使用它们的简单示例。
</a>


### 4.1 Default Account Configuration (Single-Sig)
### 4.1 默认账户配置（单机）
<a name="default">
This is how an account is configured after it has been created, it has a single key for both the `owner`  and `active` permissions, both keys with a weight of 1 and permissions both with a threshold of 1. The default configuration requires a single signature to authorize a message for the native permissions.

这是介绍创建账户后如何配置账户的方式，它有一个用于 `所有者` 和 `活跃者` 权限的密钥，这两个密钥的权值以及权限阈值都为1。默认配置需要一个签名来授权给本机权限的消息。
</a>

@bob account authorities

| Permission        | Account   |  Weight        | Threshold  |
| :-----:   | :-----:   | :-----:   | :-----:   | 
|owner        |       |         |    1     |   
|        | EOS5EzTZZQQxdrDaJAPD9pDzGJZ5bj34HaAb8yuvjFHGWzqV25Dch     |  1      |        |     
| active       |       |         |     1    |   
|        | OS61chK8GbH4ukWcbom8HgK95AeUfP8MBPn7XRq8FeMBYYTgwmcX    |   1    |         |  

@bob账户授权

| 权限        | 账户   |  权重       | 阈值  |
| :-----:   | :-----:   | :-----:   | :-----:   | 
|owner        |       |         |    1     |   
|        | EOS5EzTZZQQxdrDaJAPD9pDzGJZ5bj34HaAb8yuvjFHGWzqV25Dch     |  1      |        |     
| active       |       |         |     1    |   
|        | OS61chK8GbH4ukWcbom8HgK95AeUfP8MBPn7XRq8FeMBYYTgwmcX    |   1    |         |  



In the @bob account example, this table shows that @bob's owner key has a permissioned weight of 1, and the required threshold to push a transaction under that authority is 1.

在 @bob 这个账户的例子中，这个表格展示了@bob 的 `所有者`密钥的权重为1，在这个权限下产生一次交易需要的阈值为1。

To push a transaction under the owner authority, only @bob needs to sign the transaction with his owner key for the transaction to be eligible for validation. This key would be stored in a wallet, and then processed using eosc.

若想在 `所有者`权限下产生一次交易，只需 @bob 用他的 `所有者`密匙对交易进行签名以保证交易通过验证，这个密匙将保存在钱包中，进而利用eosc处理。



### 4.2 Multi-sig Account & Custom Permissions
<a name="Multi">
The below examples are authorities for a fictional account named @multisig. In this scenario, two users are authoritized to both the owner and active permissions of a fictional @multisig account, with three users permissioned to a custom publish permission with varying weight.
</a>

### 4.2多重签名账户和自定义权限

以下的示例是一个名为 @multisig 的虚拟账户的权限。在这个脚本中，两个用户分别被授予虚拟账户@multisig 的 `所有者`和 `活跃者`权限，三个用户分别根据不同的权重授予一个定义的publish 权限。

@multisig account authorities

| Permission        | Account   |  Weight        | Threshold  |
| :-----:   | :-----:   | :-----:   | :-----:   | 
|owner        |       |         |    2     |   
|        | @bob    |  1      |        |     
|        | @stacy    |  1      |        |     
|active        |       |         |    1     |   
|        | @bob    |  1      |        |     
|        | @stacy    |  1      |        |   
|pulish       |       |         |    2     |   
|        | @bob    |  2     |        |     
|        | @stacy    |  2     |        |   
|        | @stacyEOS7Hnv4iBWo1pcEpP8JyFYCJLRUzYcXSqtQBcEnysYDFTEbUpi6y	    |  1      |        |

@多账户权限

| 权限        | 账户   |  权重        | 阈值 |
| :-----:   | :-----:   | :-----:   | :-----:   | 
|owner        |       |         |    2     |   
|        | @bob    |  1      |        |     
|        | @stacy    |  1      |        |     
|active        |       |         |    1     |   
|        | @bob    |  1      |        |     
|        | @stacy    |  1      |        |   
|pulish       |       |         |    2     |   
|        | @bob    |  2     |        |     
|        | @stacy    |  2     |        |   
|        | @stacyEOS7Hnv4iBWo1pcEpP8JyFYCJLRUzYcXSqtQBcEnysYDFTEbUpi6y	    |  1      |        |




In this scenario, a weight threshold of 2 is required to make changes to the owner permission level, which means that because all parties have a weight of 1, all users are required to sign the transaction for it to be fully authorized.

在这个脚本中，改变 `所有者`权限水平需要的权重阙值为2，这意味着因为所有的参与方权重都为1，为了一个交易被完整授权，所有的用户都需要签名这个交易。


To send a transaction which requires the active authority, the threshold is set to 1. This implies that only 1 signature is required authorize a message from the active authority of the account.

该账户的 `活跃者`权限中发送一笔交易，阙值设置为1。这说明只需要1个用户的签名来授权一个信息。

There's also a third custom named permission called publish. For the sake of this example, the publish permission is used to publish posts to the @multisig's blog using a theoretical blog dApp. The publish permission has a threshold of 2, @bob@* and @stacy both have a weight of 2, and a public key has a weight of 1. This implies that both @bob and @stacy can publish without an additional signature, whereas the public key requires an additional signature in order for a message under the public permission to be authorized.

其中也有第三个名为publish的自定义权限。这个示例中，publish权限是用一个假想的博客dApp在@multisig的博客上发帖子。publish权限阙值为2，@bob和@stacy权重均为2，及一个公钥的权重为1.这说明@bob和@stacy都可以独自发布而不需要额外的签名，但是为了一个信息被授权，则那个公钥需要一个额外的签名。


Thus the above permissions table implies that @bob and @stacy, as owners of the account, have elevated priviledges similar to a moderator or editor. While this primitive example has limitations particularly with scalability and is not necessarily a good design, it does adequately demonstrate the flexible nature of the EOS permissions system.

因此以上权限表格说明，作为这个账户的所有者，@bob和@stacy提升的特权类似于一个审核者或编辑。虽然这个原始示例有局限性，特别是可扩展性方面，并且不一定是一个好的设计，但它确实充分展示了EOS权限系统的灵活性。


Also, notice in the above table, we've permissions using both an account name and a key. At first glance this may seem trivial, however it does suggest some added dimensions of flexibility.

另外，请注意上面的表格，我们有同时使用账户名和密匙的权限。乍看起来，这似乎微不足道，但它确实表现了一些额外的灵活性。


Observations
• @bob and @stacy can be explicitly identified as the owners of this account
• @bob and @stacy have elevated privileges for the the publish permissions.

注意
• @bob和@stacy可以明确地标识为该帐户的所有者。
• @bob和@stacy为publish 权限增加了特权。



----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

林炜鑫，在读硕士，专注区块链技术研究与行业分析，欢迎加微信号:wxlinzju，微信名：艾米·哈伯

AMY,区块链爱好者和行业新动向研究者，欢迎加微信号：Amyrenlin, 微信名：AMY

本文由币乎社区（bihu.com）内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------


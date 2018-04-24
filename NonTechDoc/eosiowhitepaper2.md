
>文章来自：https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md
>
>译者：区块链中文字幕组 Chuan


## Accounts 账户

The [EOS.IO](http://EOS.IO) software permits all accounts to be referenced by a unique human readable name of up to 12 characters in length. The name is chosen by the creator of the account. The account creator must reserve the RAM required to store the new account until the new account stakes tokens to reserve its own RAM.

[EOS.IO](http://EOS.IO) 软件允许账户由一个唯一的、最长12个字符的名称来引用。这个名称由账户的创建者来选定。账户创建者必须预留所需的RAM来储存新账户，直到新账户押上代币来预留自己的RAM。

In a decentralized context, application developers will pay the nominal cost of account creation to sign up a new user. Traditional businesses already spend significant sums of money per customer they acquire in the form of advertising, free services, etc. The cost of funding a new blockchain account should be insignificant in comparison. Fortunately, there is no need to create accounts for users already signed up by another application.

在去中心化的背景下，应用程序开发者将象征性地支付创建账户费用来注册新用户。传统企业已经以广告、免费服务等形式花费大量资金在获得的每个顾客身上。相比而言，为一个区块链账户花的钱应该说是微不足道。幸运的是，不需要为已经通过另一个应用程序注册的用户创建账户。

## Actions & Handlers 指令&操作者

Each account can send structured Actions to other accounts and may define scripts to handle Actions when they are received. The [EOS.IO](http://EOS.IO) software gives each account its own private database which can only be accessed by its own action handlers. Action handling scripts can also send Actions to other accounts. The combination of Actions and automated action handlers is how [EOS.IO](http://EOS.IO) defines smart contracts.

每个账户可以发送结构化的指令给其它账户，并且可以定义脚本来处理接收到的指令。EOS.IO软件为每个账户提供私有的数据库，它只能被它自己的指令操作者访问。指令操作脚本也可以发送指令给其他账户。指令和自动化的指令操作者相结合就是EOS.IO 定义智能合约的方式。

To support parallel execution, each account can also define any number of scopes within their database. The block producers will schedule transaction in such a way that there is no conflict over memory access to scopes and therefore they can be executed in parallel.

为了支持并行处理，每个账户也可以在他们的数据库内定义任意数量的作用域。区块生产者按照既定的安排处理交易，这种处理方式对作用域的内存访问不会有冲突，因此交易可以被并行处理。

## Role Based Permission Management基于角色的权限管理

Permission management involves determining whether or not an Action is properly authorized. The simplest form of permission management is checking that a transaction has the required signatures, but this implies that required signatures are already known. Generally, authority is bound to individuals or groups of individuals and is often compartmentalized. The [EOS.IO](http://EOS.IO) software provides a declarative permission management system that gives accounts fine grained and high-level control over who can do what and when.

权限管理包含确定一个指令是否被合理地授权。最简单的权限管理形式是检查一笔交易是否拥有所需的签名，但是这意味着所需的签名是已知的。一般来说，权力是与个人或者团体相连的，并且经常被分成不同的类别。EOS.IO软件提供一个声明性权限管理系统，为账户对谁能做什么以及什么时候做提供细致的、高级别的控制。

It is critical that authentication and permission management be standardized and separated from the business logic of the application. This enables tools to be developed to manage permissions in a general-purpose manner and also provide significant opportunities for performance optimization.

重要的是，身份验证和权限管理应该做到标准化，并从应用程序的业务逻辑中分离出来。这使得能够开发一些工具以多样化的的方式来管理权限，也能够为性能优化提供重要的机会。

Every account may be controlled by any weighted combination of other accounts and private keys. This creates a hierarchical authority structure that reflects how permissions are organized in reality and makes multi-user control over accounts easier than ever. Multi-user control is the single biggest contributor to security, and, when used properly, it can greatly reduce the risk of theft due to hacking.

每个账户也许可以被其它账户和私钥的任意权重组合来控制。这创建一个层级权限结构，反映出权限在现实中如何被组织，以及使得对账户的多用户控制比以往更加容易。多用户控制是对安全最大的促进因素，而且，使用得当的话，它可以极大地降低因攻击引起的被盗风险。

[EOS.IO](http://EOS.IO) software allows accounts to define what combination of keys and/or accounts can send a particular Action type to another account. For example, it is possible to have one key for a user's social media account and another for access to the exchange. It is even possible to give other accounts permission to act on behalf of a user's account without assigning them keys.

[EOS.IO](http://EOS.IO) 软件允许帐户定义密钥和账户的组合方式把特定的指令类型发送到另一个账户。例如，可以使用一个密钥访问用户的社交媒体帐户，另一个密钥用于访问交易所。甚至可以授权其他帐户来代表该用户账户进行操作，而无需为他们分配密钥。

### Named Permission Levels 命名权限级别

Using the [EOS.IO](http://EOS.IO) software, accounts can define named permission levels each of which can be derived from higher level named permissions. Each named permission level defines an authority; an authority is a threshold multi-signature check consisting of keys and/or named permission levels of other accounts. For example, an account's "Friend" permission level can be set for an Action on the account to be controlled equally by any of the account's friends.

利用EOS.IO软件，账户能够定义命名权限级别，每一层都可以派生于高一层的命名权限。每个命名权限级别定义一种权限；权限是一种入门级的多签名检查，这个检查由密钥和其它账户的命名权限级别组成。例如，一个账户的“朋友”权限级别可以被设置为对这个账户的一个指令，这个账户的朋友对它拥有相同的控制权。

Another example is the Steem blockchain which has three hard-coded named permission levels: owner, active, and posting. The posting permission can only perform social actions such as voting and posting, while the active permission can do everything except change the owner. The owner permission is meant for cold storage and is able to do everything. The [EOS.IO](http://EOS.IO) software generalizes this concept by allowing each account holder to define their own hierarchy as well as the grouping of actions.

另一个例子是Steem区块链，它有3个硬编码的命名权限级别：所有者(owner)，活跃状态(active)和发布(posting)；发布权限只能执行一些社交化的行为如投票和发文，而活跃权限能够做任何事情，除了变更所有者外。所有者权限是为冷存储设计的，能够做任何事情。EOS.IO软件通过允许每个账户持有者来定义自己的权限结构以及指令分组使得这些概念能被普遍使用。

### Permission Mapping 权限映射

[EOS.IO](http://EOS.IO) software allows each account to define a mapping between a contract/action or contract of any other account and their own Named Permission Level. For example, an account holder could map the account holder's social media application to the account holder's "Friend" permission group. With this mapping, any friend could post as the account holder on the account holder's social media. Even though they would post as the account holder, they would still use their own keys to sign the Action. This means it is always possible to identify which friends used the account and in what way.

EOS.IO软件允许每个账户来定义一个一个合约/指令或者任一个其它账户的合约与他们自身的命名权限级别之间的映射。例如，一个账户持有人可以映射这个账户持有人的社交媒体应用来这个账户持有人的“朋友”权限组。通过这种映射，任意一个朋友能够作为账户持有人在这个账户持有人的社交媒体上发布消息。即使他们都作为账户持有人来发布消息，但是他们仍旧使用自己的密钥来对这个指令进行签名。这意味着总是能够知道哪个朋友以及通过什么方式使用了这个账户。

### Evaluating Permissions 评估权限

When delivering an Action of type "Action", from @alice to @bob the [EOS.IO](http://EOS.IO) software will first check to see if @alice has defined a permission mapping for @bob.groupa.subgroup.Action. If nothing is found then a mapping for @bob.groupa.subgroup then @bob.groupa, and lastly @bob will be checked. If no further match is found, then the assumed mapping will be to the named permission group @alice.active.

当从爱丽丝@alice发送一个“动作”类型的指令到鲍伯@bob时，EOS.IO软件首先进行检查来看爱丽丝是否定义了一个对@bob.groupa.subgroup.Action的权限映射。如果没有，那么看是否定义了@bob.groupa.subgrou的映射，依次类推，然后是@bob.groupa，最后是检查@bob。如果没有发现任何的匹配，那么这个假设的映射将作为@alice.active命名权限组。

Once a mapping is identified then signing authority is validated using the threshold multi-signature process and the authority associated with the named permission. If that fails, then it traverses up to the parent permission and ultimately to the owner permission, @alice.owner.

一旦找到这样的映射，那么签名权就使用入门的多签名过程和与命名权限相关联的权限来验证。如果验证失败，那么它向上移动到父一级的级别权限，最终到所有者权限@alice.owner。

#### Default Permission Groups默认权限组

The [EOS.IO](http://EOS.IO) technology also allows all accounts to have an "owner" group which can do everything, and an "active" group which can do everything except change the owner group. All other permission groups are derived from "active".

EOS.IO也允许所有的账户拥有一个“所有者”组，它可以做任何事情，以及一个“活跃”组，它可以做任何事情，除了不能变更所有者组。所有其它的权限组都派生于“活跃”组。

#### Parallel Evaluation of Permissions并行权限评估

The permission evaluation process is "read-only" and changes to permissions made by transactions do not take effect until the end of a block. This means that all keys and permission evaluation for all transactions can be executed in parallel. Furthermore, this means that a rapid validation of permission is possible without starting costly application logic that would have to be rolled back. Lastly, it means that transaction permissions can be evaluated as pending transactions are received and do not need to be re-evaluated as they are applied.

权限评估过程是“只读的”，并且对由交易引起的权限变化不会发生效果，直到把交易打包成块。这意味着所有的密钥和对所有交易的权限评估可以被并行执行。此外，这表示对权限的快速验证是可以做到的，而不需要启动代价太大、可能得要回滚的应用层逻辑。最后，这表明交易权限能够被评估，并且当接收到待定交易，并且在它们被处理时，这些交易不需要重新评估。

All things considered, permission verification represents a significant percentage of the computation required to validate transactions. Making this a read-only and trivially parallelizable process enables a dramatic increase in performance.

从整体来看，权限验证表示需要相当多的计算来验证交易。使它成为“只读”以及可并行的过程能够使得性能获得显著的提升。

When replaying the blockchain to regenerate the deterministic state from the log of Actions there is no need to evaluate the permissions again. The fact that a transaction is included in a known good block is sufficient to skip this step. This dramatically reduces the computational load associated with replaying an ever growing blockchain.

当重放区块链来从行为日志重新产生不可逆转的状态时，不需要再评估这个权限。一笔交易被包含在一个已知的好区块中这一事实足够用来跳过评估这一步骤。这极大地减少重放一个不断增长的区块链的计算负荷。

## Actions with Mandatory Delay 带强制延迟的指令

Time is a critical component of security. In most cases, it is not possible to know if a private key has been stolen until it has been used. Time based security is even more critical when people have applications that require keys be kept on computers connected to the internet for daily use. The [EOS.IO](http://EOS.IO) software enables application developers to indicate that certain Actions must wait a minimum period of time after being included in a block before they can be applied. During this time, they can be cancelled.

时机是安全考虑的一个重要因素。大多数情况下，不太可能知道一个私钥是否被偷，直到它被人使用。当人们有一些应用需要密钥被保存在连网的电脑上时，以时机为考量的安全甚至更加重要。EOS.IO软件使得应用开发人员能够指明，某些指令必须要在被打包到块里后等上一段最短时间才能被执行。在这段时间内，它们可以被取消。

Users can then receive notice via email or text message when one of these Actions is broadcast. If they did not authorize it, then they can use the account recovery process to recover their account and retract the Action.

当一个这样的指令被广播时，用户可以接收来自邮件或者文本消息的提醒。如果他们没有对这个指令授权，那么他们可以使用账户恢复过程来恢复账户并撤回这个指令。

The required delay depends upon how sensitive an operation is. Paying for a coffee might have no delay and be irreversible in seconds, while buying a house may require a 72 hour clearing period. Transferring an entire account to new control may take up to 30 days. The exact delays are chosen by application developers and users.

这个需要的延迟时间取决于一个操作的敏感性如何。付钱买一杯咖啡也许不需要延迟，在几秒内就不能撤消，而买一套房子可能需要72小时结算时间。转移一个账户到新的控制方可能需要多达30天。具体的延迟时间由应用开发人员和用户来决定。


***

区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号：w1791520555。

[点击查看 GITHUB 及更多的译文](https://github.com/BlockchainTranslator/EOS)

本文译者介绍

Chuan，区块链技术爱好者。欢迎加我的微信：youyuxiaochuan

译文版权所有，转载需完整注明以上内容。

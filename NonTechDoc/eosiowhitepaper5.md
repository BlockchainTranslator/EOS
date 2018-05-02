### Governance 管理

Governance is the process by which people in a community:

管理是指人们在社区中进行以下活动所遵守的过程。

1. Reach consensus on subjective matters of collective action that cannot be captured entirely by software algorithms;对那些不能被算法完全理解的集体性的行为在主观方面达成共识。

2. Carry out the decisions they reach; and执行他们做出的决定

3. Alter the governance rules themselves via Constitutional amendments.通过宪法修正案来变更管理规则。

An EOS.IO software-based blockchain implements a governance process that efficiently directs the existing influence of block producers. Absent a defined governance process, prior blockchains relied ad hoc, informal, and often controversial governance processes that result in unpredictable outcomes.

基于EOS.IO软件的区块链实现这一管理过程，它有效地指导区块生产者的现有影响力。由于缺乏一个清晰的管理过程，之前的区块链依赖临时安排的、非正式的、常有争议的管理过程，从而导致不可预测的后果。

A blockchain based on the EOS.IO software recognizes that power originates with the token holders who delegate that power to the block producers. The block producers are given limited and checked authority to freeze accounts, update defective applications, and propose hard forking changes to the underlying protocol.

基于EOS.IO软件的区块链认识到，权利来自于持币者，他们把权利委托给区块生产者。区块生产者获得有限的且审核过的权利，他们可以冻结账户，更新有缺陷的应用程序，提议对底层协议实行硬分叉。

Embedded into the EOS.IO software is the election of block producers. Before any change can be made to the blockchain these block producers must approve it. If the block producers refuse to make changes desired by the token holders then they can be voted out. If the block producers make changes without permission of the token holders then all other non-producing full-node validators (exchanges, etc) will reject the change.

区块生产者的选举内嵌于EOS.IO软件之中。在对区块链作出任何改变之前，这些区块生产者必须接受它。如果区块生产者拒绝执行持币者期望的改变，那么他们就可以被投票淘汰出局。如果区块生产者未经持币者的允许对区块链进行更改，那么所有其他的非产块的全节点验证者（交易所等）将拒绝这一更改。

#### Freezing Accounts冻结账户

Sometimes a smart contact behaves in an aberrant or unpredictable manner and fails to perform as intended; other times an application or account may discover an exploit that enables it to consume an unreasonable amount of resources. When such issues inevitably occur, the block producers have the power to rectify such situations.

有时候，智能合约以反常或不可预测的方式运行，没有按预期执行。其他时候，应用程序或账户可能发现一个行为，让它消耗不合理的资源使用量。当这样的问题不可避免地发生时，区块生产者有权修正这样的状态。

The block producers on all blockchains have the power to select which transactions are included in blocks which gives them the ability to freeze accounts. A blockchain using EOS.IO software formalizes this authority by subjecting the process of freezing an account to a 15/21 vote of active producers. If the producers abuse the power they can be voted out and an account will be unfrozen.

所有区块链上的区块生产者有权选择哪些交易被打包放进块中，这给予他们拥有冻结账户的权利。使用EOS.IO软件的区块链使这一权利得以实现的方式在于：把冻结账户的这个过程交给21个区块节点中的15个同意即可。如果区块生产者滥用权利，他们可以被投票淘汰出局，账户就可以被解冻。

#### Changing Account Code修改账户代码

When all else fails and an "unstoppable application" acts in an unpredictable manner, a blockchain using EOS.IO software allows the block producers to replace the account's code without hard forking the entire blockchain. Similar to the process of freezing an account, this replacement of the code requires a 15/21 vote of elected block producers.

当所有的修正都于事无补，“无法停止的应用”以不可预测的方式运行时，使用EOS.IO软件的区块链允许区块生产者替换账户代码，无需对整个区块链进行硬分叉。与冻结账户的过程相似，替换代码也需要21个区块节点中15个以上的同意。

#### Constitution 宪法

The EOS.IO software enables blockchains to establish a peer-to-peer terms of service agreement or a binding contract among those users who sign it, referred to as a "constitution". The content of this constitution defines obligations among the users which cannot be entirely enforced by code and facilitates dispute resolution by establishing jurisdiction and choice of law along with other mutually accepted rules. Every transaction broadcast on the network must incorporate the hash of the constitution as part of the signature and thereby explicitly binds the signer to the contract.

EOS.IO软件使得区块链在那些签了名的用户当中建立起点对点的服务协议或者约束性合约，我们将之称为“宪法”。宪法的内容确定了用户需要遵守的那些不能完全由代码执行的责任，通过确立司法权和法律以及其它相互接受的规则，促进争端的解决。网络上的每一个交易广播必须把宪法的哈希纳入到签名的一部分，从而明确地把签名人与合约绑定在一起。

The constitution also defines the human-readable intent of the source code protocol. This intent is used to identify the difference between a bug and a feature when errors occur and guides the community on what fixes are proper or improper.

宪法也明确源代码协议的人可读的意图。这一意图被用来界定错误和错误出现时的特征之间的差异，并指导社区什么样的修复办法才是合理的。

#### Upgrading the Protocol & Constitution 升级协议和宪法

The EOS.IO software defines the following process by which the protocol, as defined by the canonical source code and its constitution, can be updated:

EOS.IO软件定义了以下过程，根据这些过程，由源代码和宪法确定的协议能够被升级。

1. Block producers propose a change to the constitution and obtains 15/21 approval.区块生产者提议对宪法作出修改，获得21个区块节点中15个的同意。

2. Block producers maintain 15/21 approval of the new constitution for 30 consecutive days. 区块生产者连续30天维持对新宪法的15/21的同意率。

3. All users are required to indicate acceptance of the new constitution as a condition of future transactions being processed.所有用户被要求对新宪法的接受作为未来交易被处理的条件。

4. Block producers adopt changes to the source code to reflect the change in the constitution and propose it to the blockchain using the hash of the new constitution.区块生产者接受对源代码的修改来反映宪法的变化，并使用新宪法的哈希值把这一变化提交给区块链。

5. Block producers maintain 15/21 approval of the new code for 30 consecutive days.区块生产者连续30天维持对新代码的15/21的同意率。

6. Changes to the code take effect 7 days later, giving all non-producing full nodes 1 week to upgrade after ratification of the source code 对代码的更改7天后生效，在认可源代码后所有非出块的全节点有1周的时间来升级.

7. All nodes that do not upgrade to the new code shut down automatically. 所有没升级到新代码的节点自动停止运行。

By default, configuration of the EOS.IO software, the process of updating the blockchain to add new features takes 2 to 3 months, while updates to fix non-critical bugs that do not require changes to the constitution can take 1 to 2 months.

根据EOS.IO软件的默认配置，区块链加入新特征的这一更新过程需要2到3个月，而修复那些并不会要求对宪法作出修改的非重大错误可能需要1到2个月。

#### Emergency Changes 应急变更

The block producers may accelerate the process if a software change is required to fix a harmful bug or security exploit that is actively harming users. Generally speaking it could be against the constitution for accelerated updates to introduce new features or fix harmless bugs.

如果要求对软件进行修改来修复重大的错误或影响用户的安全问题，区块生产者可以加速这个过程。一般来说，对于加快更新来引入新特征或修复不是大问题的错误可能是对宪法不利的。


The Message Is The Medium  信息即媒介
-----------------------------------

> 本文翻译自：https://steemit.com/eos/@iang/the-message-is-the-medium

> 原文作者: [iang](https://steemit.com/@iang)

> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [荆凯(shuke0327)](https://github.com/shuke0327)
>
> 翻译时间：2017-10-22

## A Preliminary Message　预备信息

This post introduces what I think is a fundamental flaw in almost all blockchain designs. In brief, it is the emphasis on state as the ‘atomic element’, when we could also build using messages instead. The implications of this are quite severe, but also quite hard to understand because the computer science concepts are a bit inaccessible to the non-CS world.

在这篇文章中介绍了我认为的几乎所有的 blockchain 设计中都存在的一个基础缺陷。简言之，这缺陷在于太过强调状态( state )作为（区块链的）"原子因素"，而我们也可以改用信息( message )来构建。 这一缺陷的影响很严重，但也很难理解，因为计算机科学的概念对于计算机科学世界以外的人来说，有些难以触及。

What follows is a very informal, non-rigourous description to try and explain the difference between messaging and state to the non-technical audience. I’ve tried to get the simple message across but if you find yourself in a state of confusion, there is another way to understand it and that is to watch this space - we’re going to build it, so then the message will be put to the medium. Enough bad analogies, let’s forge on.

下文是非常不正式、不严格的描述，我尝试对非技术型的读者解释清楚信息和状态之间的区别。我尝试尽量简单的传达信息，但如果你仍然感到困惑，还有另外一种方式去理解，即，观察此处的空间 - 我们要创建它，从而信息会发送至媒介。这类比够烂的，让我们继续前进吧。

## What’s a State Machine, anyway?　状态机是什么？



A state machine is a [computer science invention][1] to capture the reliable, deterministic machine. In words, it is a software “machine” that given some set of inputs and memory, always delivers the same outputs.

状态机是一个[计算机科学发明的一个概念][1]，用来描述具有可靠性、 确定性的机器。换句话说，它是一台软件"机器"，给定一组输入和存储，会始终产生相同的输出。

![Figure 1 - The State Machine.png](https://steemitimages.com/DQmaHQSpoii8AMJsdfynqbiRdpM1nT5hn7Q8ie587D5RM8g/Figure%201%20-%20The%20State%20Machine.png)

Think about a vending machine, and the software inside, which has to simulate the hardware machine so as to figure out what to do next. In words, “if we are in State 1, wait for coin. If a coin turns up, enter State 2\. If in State 2, wait for button push. If a button push turns up, deliver drink, go to State 1.” In essence then, our machine consists of some code to handle that algorithm, some state (memory) to recall where we are, and an ability to read incoming messages (coins, buttons) and write out some instructions as messages (drink!).

设想一台自动售货机和其中的软件用于模拟硬件机器，以决定下一步做什么。换句话说，"如果我们处于状态 1，等待投币。如果硬币出现，进入状态 2。如果在状态 2中，等待按钮按下。 如果按下按钮，提供饮料，转到状态 1。” 在本质上，我们的机器包含处理算法的代码，记录位置的状态(存储)，读取输入信息（硬币，按钮）和将指令作为信息(饮料)输出的能力。

![Figure 2 - a coke machine .png](https://steemitimages.com/0x0/https://steemitimages.com/DQmNa2UbPMh9eirxS9bTt192aKqdR4QNEBdHxdKCjJPSjmY/Figure%202%20-%20a%20coke%20machine%20.png)

We can also construct bigger state machines out of smaller ones - a database is essentially an enormous state machine, made up many little machines for each SQL table, each row and each cell. A protocol is a small state machine made of two state machines - one for each end. A blockchain is another enormous state machine, made of thousands of “full node” state machines with lots of hangers-on called SPV clients. While the essence of the design of a state machine is pretty simple, using them is as much an art as a science because we don’t have a great view on how to compose small state machines into large state machines. But we’ll leave aside that complexity for now.

我们也可以用小的状态机构造出大的状态机-数据库本质上就是一台庞大的状态机，由每个 SQL 表，每一行和每个单元格的小状态机组成。 协议也是一个小的状态机，由分布在协议两端的两个状态机组成。 Blockchain 是另一个巨大的状态机，由数以千计的"完整节点"状态机，以及大量叫做 SPV 客户端的附属节点组成。虽然状态机设计的本质很简单，但使用起来却既是一门艺术也是一门科学，因为对于如何将小的状态机组成大型状态机，我们并没有很好的见解。不过我们暂时先忽略这种复杂性。

## Choice　选择

It turns out that there are two fundamental approaches to building a state machine.

构建一个状态机，有两种基本方法。

Note, what follows is a very stylised viewpoint, not a rigorous one. We ignore the code above, and just assume it is referenced wherever needed. We also ignore the output messages, for simplicity. Our goal is to get you to a state of understanding the message, not to impress CS geeks.

注意，以下是非常具有个人色彩的观点，并非严格表述。我们忽略了上面提到的代码，只要假设在需要的地方它被引用到了。为了简单起见，我们也忽略掉输出信息。我们的目标是让你能够理解信息，而非为了讨好电脑geeks.

![Figure 3 - timeline of transitions .png](https://steemitimages.com/DQmVzThtGykmgAQoi3GA7a87cuakCd2DqfRxdc5X4Dyfuj6/Figure%203%20-%20timeline%20of%20transitions%20.png)

We normally model the state machine as above - it starts out in State One, and then Message 1 arrives. The processing of this message causes a transition from State One to State Two. On transitioning to State 1, the machine sends out messages, although that is strictly optional - it depends on the machine’s needs at that transition.

通常我们对状态机的建模如上所示 -- 从状态一开始， 然后信息1 到达。 处理信息，会从状态1转变为状态2。在转变过程中，状态机发出信息，是否发送信息是可选的 - 取决于状态机在状态变化时的需要。

Our job in building the state machine is to write the code to store and transition all states for all known messages. It turns out that, in doing this job, there are two fundamentally different ways in which to write the machine, and the choice of which colours our thinking, our design and eventually our capabilities.

构建状态机时，我们的工作是编写代码来存储所有的状态，以及根据所有的已知信息来变更全部的状态。结果是，在做这件事的时候，有两种从根本上不同的方法去写状态机，选择哪种方法，会影响到我们的思考，我们的设计，最终影响到我们的能力(capabilities)。

> First Way: Thinking of it as a machine of states. In this view, we store State One. Then, when the message arrives, the machine turns over to State Two, and we store that new state. Repeat! Think of the states as the Blue Circles above, and you can ignore any other view of the world.

> 第一种方式: 将其视作一台状态机。在这一观点中，我们存储状态1。 当信息到达时，状态机切换到状态2，我们存储新的状态。重复上述过程！将状态看作是上图中的蓝色的圆圈，你可以忽略掉世上所有其它不同的观点。

> Second Way: Thinking of it as a machine of messages. In this alternate view, we record the messages. We always start the machine at State One. Then we pump all of the incoming messages (Red Pills above) into the machine (and out pops any new messages). We store the messages, but don’t bother with the state, because we can calculate it any time.

> 第二种方式: 将其视作一台信息的机器。在这一替代观点中，我们把信息记录下来。 我们仍然从状态1开始状态机。然后把所有输入的信息(上图中红色的标签)传入到机器中（并且将所有的新信息传出）。 我们存储信息，而不用为状态分神，因为我们可以随时计算出。

These views are mostly equivalent in theory, and the trick to understanding this is that the machine is deterministic. Once we’ve established the machine as being exact and unforgiving in its actions, we know that for example M1 on State1 always results in State2 (and M2 out).

这些观点在理论上是大致等效的，要理解这一点关键在于知晓状态机是具有确定性的。一旦我们确立了机器的运行是精确无差错的，我们就可以知道，例如，状态1 叠加信息 M1 总是会得到 State2的结果（并输出信息M2）。

Then, if we have the machine, and we have the set of messages, we can always roll it again to get the states. OR, if we have recorded the states, we can always walk the chain of states to reproduce the action, although we don’t necessarily know what messages caused that journey. If you like your graphs, you could think of the distinction as storing the nodes OR storing the edges.

然后，如果我们有这台机器和一组给定的消息，我们总是可以运行机器，得到相同的状态。或者，如果我们记录了状态，我们总是可以按照状态的链条运行，重现状态机的动作，虽然我们没有必要知道这一过程是由什么信息导致的。如果你喜欢图（graphs），那么可以将（状态和信息的）这种区别看作是存储图的节点或者存储边界的区别。

We have a choice about how we think about things. And, depending on our desires and assumptions, we are likely to prefer one way or the other: databases are seen as machines of state, as is a light switch - it knows whether it is on or off, but doesn’t know how it got to where it is now. Whereas protocols are typically thought of more as machines of messages; consider an email exchange in which the last message doesn’t tell you all the story, and if it’s been a while you might have to scan all the previous messages in thread to work out what’s happening.

我们可以选择思考事物的方式。并且根据我们的愿望和设想，我们有可能青睐一种方式或其他： 数据库被视作状态机，正如电灯的开关-它知道是否它是打开还是关闭，但不知道它是如何成为现在的状态的。而协议则更经常被认为是信息的机器；思考一下在邮件交流中的情形，最后一条消息不会告诉你所有的故事，需要花费时间去查看之前的所有信息，才能知道发生了什么事情。

![photo.png](https://steemitimages.com/0x0/https://steemitimages.com/DQmPHQnxJ6XLRRsCKGJL3BTZWpPvL7SKr95pFUNEd83wqn4/photo.png)

### wheretofore the machinery of blockchain?
### 当前区块链的机制是什么？

That’s in theory - practice can be different. Your online bank account is presented as a machine of state, with balance being told to you. But inside the bank, use of double entry accounting makes it more a machine of messages.

这是就理论而言 — — 实践可能有所不同。你的网上银行账户表现得像一台状态机，会告知你账户的余额。但在银行内部，对复式记帐会计法的使用让它更像一台信息机。

What should blockchain do?

区块链该如何做？

For reasons that might be historical, or maybe because it’s more typical for designers to think this way, blockchains are seen as machines of state, and not as machines of messages:

可能由于历史原因，或者可能因为这种方式对设计者而言更为典型，区块链被视作是一台状态机，而非信息机:

> … The goal of a blockchain is to represent a single state being concurrently edited. In order to avoid conflicts between concurrent edits, it represents the state as a ledger, that is as a series of transformations applied to an initial state. These transformations are the “blocks” of the blockchain, and — in the case of Bitcoin — the state is mostly the set of unspent outputs.(my emphasis) LM Goodman, “Tezos: A Self-Amending Crypto-Ledger Position Paper”, 2013

> ......区块链 的目标是表现一个正在被并行编辑的单一状态。 为了避免并行编辑中的冲突，它将状态表述为分类总账，即作用在初始状态上的一系列变化。 这些变化是区块链上的"块"，在比特币中，状态主要是未花费的输出的集合(这段强调是我加的）LM Goodman, “Tezos: A Self-Amending Crypto-Ledger Position Paper”, 2013

Or, from a recent Ethereum replacement project:

或者，在最近的一个旨在取代 Ethereum 的项目中的表述：

> How do transaction semantics fit into our description of contracts? From the process level, a transaction is an acknowledgment that a message has been “witnessed” at a channel.Messages themselves are virtual objects, but the pre-state and post-state of a contract, referring to the states before and after a message is sent by one agent and witnessed by another, are recorded and timestamped in storage, also known (in a moral sense) as the “blockchain”.Message passing is an atomic operation. Either a message is witnessed, or it is not, and only the successful witnessing of a message qualifies as a verifiable transaction that can be included in a block.(author’s emphasis in bold, my emphasis in italics) anon?, “RChain Architecture - Contract Design”, 2017 RChain Cooperative

> 描述交易的语义学表述如何与我们对合约的描述相结合？从处理的层面看，交易是对消息在某个渠道已被"见证"的确认。消息本身是虚拟对象。某个代理发送信息，由另外的代理见证信息，信息打上时间戳记录在存储系统中-- 即为人们所知的”区块链“上，这一过程前后的状态，就是合约的前状态和后状态。信息的传递是原子操作。无论信息是否得到见证，只有对信息的成功见证才有资格作为可信的交易被记录到区块中。（原作者的重点强调以粗体显示，我的重点用斜体表示）匿名？，“RChain Architecture - Contract Design”, 2017 RChain Cooperative

Note how the author above has established everything we need to store the message as transaction, and then fallen back to blockchain canon of state.

请注意上述作者的观点，（他们认为）我们需要做的所有事情是将信息作为交易存储，然后回到区块链上，记录状态。

If we look at the Bitcoin state machine in Figure 4 below for another example, we can see this state view writ large in the UTXO model, which groups transactions as collections of Unspent Transaction Outputs(“UTXO”). The transaction is a record of state that includes the input, andthe output. Comparing to Figure 3 above, think of both of the blue circles in each record, but none of the messages. Normally each UTXO transaction is represented as a box with a column of inputs on the left, and outputs on the right, Figure 4:

我们来看另一个例子，在下面图4中的比特币状态机器，我们可以在 UTXO 的模型之中可以很明显的见到这一关于状态的设计观点，UTXO模型将交易归类为未消费的交易输出("UTXO") 的集合。交易记录了包含了输入和输出的状态。与上面图 3比较，思考一下两张图中的存在于每条记录之中的蓝色框，不用考虑信息。通常每个 UTXO 交易表示为一个盒子模型，左边列出输入，右边列出输出，如图4：

![Figure 4 - the UTXO or Unspent Transaction Outputs model .png](https://steemitimages.com/DQmWr7y9f3P8zKUANhdB9EuF82ZfFwsZRvavmo7UrwifsZU/Figure%204%20-%20the%20UTXO%20or%20Unspent%20Transaction%20Outputs%20model%20.png)

On the input (left) side of each transaction is a list of references to prior outputs or “coins”, by which presence they are then spent, and on the output (right) side is another matching list of new coins, by which presence they are now created and spendable in the future. Above, “Transaction 1” creates a 0.5BTC coin as an output, and “Transaction 2” spends the 0.5BTC coin by citing it as an input.

每笔交易的输入侧（左侧）是对之前的输出或"币"的引用列表，表示它们已经花费了，输出侧（右侧）是另外一个相匹配的新币列表，表示新币已经创建，可以用于未来消费。在上面图中，"交易 1"创建了 0.5BTC 作为输出，"交易 2"引用这个输出作为它的输入，花掉 0.5BTC .

The Bitcoin transaction record, as a record of both inputs and outputs, is like a miniature balance sheet; the inputs match the outputs. For the visually minded, each of these transaction records is also like lego blocks in that new ones must plug onto old ones, and provide for newer ones to plug into them in the future.

比特币交易记录，同时记录了输入和输出，就像一个微型的资产负债表一样; 输入与输出相匹配。对视觉思考者来说，可以把每个交易记录视作乐高块，每个新的乐高块必须插到旧的块上，并且让更新的乐高块能够插到它上面。

## The Brittleness of the UTXO（UTXO 的脆弱性）

Now, it has been observed before, but it is worth repeating: the Bitcoin design is of an extraordinary design, but one of its facets is that all of the components are strongly linked to each other in a very dependent way. As it says:

在前面你已经看过了，但现在仍值得重复: 比特币的设计非同凡响，但是有一点，即比特币中所有的组块都以一种依赖性很强的方式彼此链接。 正如白皮书中所说：

> “A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without going through a financial institution.”Satoshi Nakamoto, “Bitcoin: A Peer-to-Peer Electronic Cash System,” 2008.

>
“纯粹的点对点的电子现金实现版本，允许在线支付，无须经过金融机构，直接从一方发送到另一方"。中本聪，"比特币:-点对点电子现金系统，"2008年。

The mission was the money, but the money is also the driver for the security model, by means of paying miners to compete to validate. This powerful facet of intra-dependency does have one weakness - it is brittle in architectural terms. By this, I do not mean that Bitcoin is about to fall apart at any moment, but rather, if we change one design element, it threatens the sanctity of the entire architecture.

比特币的使命是成为金钱，钱也是安全模型的驱动力，借助给矿工支付的方式使矿工竞争挖矿，以完成交易的验证。内部依赖性这一强大的特性存在一个弱点 -- 用建筑学术语来讲叫做脆弱性（brittle）。我这样讲并不是指比特币会随时崩溃，而是，如果我们更改其中一个设计元素，就会威胁到整个架构的神圣性。

And so it is with the UTXO. As mentioned, the mission of Bitcoin was a money. Every (full) node needs to have each record of the money available for it, so it can validate every incoming transaction, and proceed to distribute the transactions into its proposed block for mining. In contrast, SPV or remote clients need to have an easy way of proving just their component of incoming coins, without dragging in the whole chain.

UTXO 也是如此。 如上所述，比特币的使命是成为货币。 每个（完全）节点需要有可用的比特币的所有记录，因此可以验证每笔传入的交易，并继续分发到备用区块中供挖矿计算。 相反，SPV 或远程客户端需要有简单的方法，只需要证明他们接收的那部分币，而不需要将整个区块链都拖下来。

These two requirements are in conflict. Because there are a lot of records in a big chain like Bitcoin, the UTXO layout is an elegant design that meets both those requirements with a reasonable efficiency given its other impacts. It is very good at providing the proof that a client needs at a point in time.

这两项要求有冲突。在像比特币这样的大型区块链上，存在大量的记录， UTXO 的布局设计优雅，虽然有其它影响，但是能够以一种合理的效率满足两者的要求。它非常善于提供给客户端在某个时间点上所需要的交易证明。

## An Order Book　交易委托账本

But what happens to the UTXO when the requirements change? Let’s say we want to do trading. For various reasons, the best way to do this is to bring everyone together, construct an order book - a list of bids to buy versus a list of offers to sell - and then run an auction clearing process to find the best price for all traders. There are other ways of course, but this is both the time-tested way and the way imposed by exchanges. Figure 5.

但如果要求变化了，UTXO 会发生什么？ 假设我们想进行交易。由于种种原因，最好的办法是把所有人集中，构建委托账本-包含竞价买单列表和一个卖单报价列表，然后运行拍卖清算过程，为所有的交易者找出最合适的价格。 当然，还有其他方法，但这才是经过时间检验，也是交易所在用的方法。

![Figure 5 - the Blue Pill Trading Book of State .png](https://steemitimages.com/0x0/https://steemitimages.com/DQmUwEnvb2VpmszQsXycXZmkT5yFatfFsEcCSsv6eT9zNeM/Figure%205%20-%20the%20Blue%20Pill%20Trading%20Book%20of%20State%20.png)

In coming together in a UTXO state machine, an unknown number of people want to bid for positions on the buy side, as do an unknown number of people on the sell side. The UTXO design cannot easily facilitate this design for two reasons: 1\. the interaction of many unknowns competing for one result does not scale because the entire layout needs to be negotiated on the fly - inputs, outputs and prices! - between the competing traders; and 2\. trading is information sensitive - if there is a way to pull out of the negotiation and collapse it, traders will do that once they’ve spotted your position. This is a fundamental contradiction!

在 UTXO 状态机的撮合交易中，在买入侧有未知数量的买家出价竞争，在卖出侧，卖家的数量也是未知的。UTXO 设计不能轻易简化这种设计有两个原因: 1\. 诸多未知的参与者相互竞争得到一个结果，这种互动难以规模化，因为总体布局需要运行时协商决定 - 输入，输出以及价格！ -在竞争的贸易者之间; 和 ２\. 交易是信息敏感的 — 如果有方法可以退出谈判让谈判崩溃，交易者一旦确认了你的位置，就会这么做。这是个基本矛盾。

A messaging flow can handle this conundrum easily. If the blockchain intermediator (the miner in a PoW design, or the producer in DPOS) receives a steady series of messages for bids and offers, he simply collects them up in order and hands them to the “book contract” which internally constructs the book, decides on the swap price, and sends new messages out confirming the contract’s outcome.

消息流可以轻松处理这个难题。如果区块链的中间人（在 PoW 设计中的矿工，或者 DPOS 机制之中的区块生产者），收到稳定的出价和要价信息，他只需要按顺序收集信息，将其传递给 "交易委托账本合约"，在合约内部构建委托账本，确定掉期价格，发送新的信息，确认合约的结果。

![Figure 6 - the Red Pill Trading Book of Messages.png](https://steemitimages.com/0x0/https://steemitimages.com/DQmNzTscBAsyDuG1p4wPdg4TbzhpuvPDzttjDyxcVHcCKcv/Figure%206%20-%20the%20Red%20Pill%20Trading%20Book%20of%20Messages.png)

The messages are logged, but the state (e.g., UTXO) is implied, which means it is constructed by the computer internally, and then (can be) thrown away. As long as the blockchain has decided on the strict set of messages - both which messages and in what order - the result is deterministic because every other node runs the same contract for each set of the same input messages, and concurs on the output messages.

消息会被记录，但状态 (例如，UTXO) 只是隐含其中，意味着它在计算机内部构造，然后（可以）被丢弃。只要区块链决定了严格的信息集合 -- 包括有哪些信息，以及信息的顺序 - 结果就是确定的，因为任何其他节点对每一组相同的输入消息运行同一合约，都会得到同样的输出信息。

Two more advantages: if any incoming trades are dropped in this block they can simply be deferred to the next block. That’s because the incoming messages are independent intents to trade whenever, whereas the inputs and outputs making the UTXO state are more constrained to being parts of their dependent collection that should happen now, inside that very transaction.

两个额外的好处： 如果任何传入的交易在此区块中被丢弃，可以仅仅将它们推迟到下一个区块中就可以了。 因为输入的信息是独立于交易的，然而任何时候组成 UTXO状态的输入和输出更受限制，必须是所属的特定交易之中的依赖性集合的一部分。

Secondly. This construct captures much more of the problem of the trading book. That is, when you want to trade with me, or I with you, we both write our bid/offer as a message and send it in. The hard part is done inside the contract, and the smart contract author has covered that in her design. In contrast, with the UTXO construct, it is you and I that have to lay out the blue box in Figure 5, agree on everything, sign off and then submit it for consensus. UTXO leaves the hard part to us the traders, and the easy part - logging the fact - to the chain.

第二, 这一结构更能够捕获到更多交易账簿的问题。就是说，如果你想与我交易，或者我与你交易，我们都需要将自己的投标作为信息发送。 困难的部分在合同内部完成，智能合约的作者在设计时候就已经覆盖了这一情况了。 与此相反的是，UTXO 的结构中，我们必须按照图片五的蓝色盒子那样，就所有的一切达成一致，签名，然后提交达成共识。 UTXO把困难的部分留给我们交易者，而把容易的部分 - 记录事实 - 交给区块链。

As an exercise, you might like to examine how you would handle fees in both designs.

给你留个练习，你可以试试看在两种设计中如何处理交易费用。

## Slight Demurral　小的反驳

It’s not all one way - the state model has the benefit of trapping bugs more quickly. Every transaction has to be perfectly in agreement in its recorded state, not just the messages that got us there. This ability to trap errors quickly could be seen as a major advantage in reconciliation of trades, which the banking sector is looking at for cost and operational risk reduction.But even this could be a choice of risks - when a bug turns up in a blockchain, the chain quickly breaks and forks.

不是只有一种方法 — — 状态模型的优点是捕获 bug 的更快。每一笔交易都需要完美的达成共识记录状态，而不只是让我们达成状态的信息。 交易要达成一致，捕获错误的能力可以被视作主要的优势，银行业正在寻求降低运行成本和业务风险的方式。但是即使这种选择也是有风险的- 当错误出现在区块链上时候，区块链会迅速的断裂和分叉。

Everything stops while nodes argue and hash. When a bug hits a message-model chain, the bug is implicit, and for the most part generates a dispute between parties over the meaning of the messages. Persons impacted can take it offline; including, we could develop the proofs to watch the issue offline, or ex-chain.

当bug出现在信息模型下的区块链时，bug是隐性的，大多数情况下在各方之间就信息的意义产生分歧。受影响的人可以脱机处理；包括，我们可以开发出证明机制，可以在脱机状态或者链外观察所涉事项。

## Conclusion　结论

The messaging model is for many reasons superior to the state model for the purpose of building broadly capable blockchains. It’s not all one way - the state model has the benefit of trapping breaks more quickly.

就构建能力更强的区块链这一目的而言，信息模型出于诸多原因，比状态模型要更有优势。不是只有一种办法 - 状态模型在更快捕获异常方面具有优势。

A fuller post would list all the pros and cons, but for now, we’ll just call out one major pro. Other than the flexibility of the above example, messaging chains can reach much higher performance. For example, Bitshares and Steem by [@danthemamn][2] were all built on this model, and show 1000s of transactions per second. As was my Ricardo system, albeit non-blockchain, but it explains why it is so easy for me to like :-)

一个完整的帖子会列出来所有利弊，但是暂时我们只列出了一个主要的优势。除了上面例子之中的灵活性之外，信息链可以得到好得多的表现。 例如，由[@dantheman][2]创建的Bitshares和Steem，都是构建在信息模型之上，可以每秒处理1000多次交易。就我所创建的Ricardo 系统而言，尽管非区块链，但是可以解释为何它如此容易，如此讨我喜欢：）

On paper at least, this approach promises much higher performance, and you can possible see a hint that EOS will be built this way too! Indeed, it was the need for speed in those systems that led designer [@dantheman][2]and myself to the discovery that, with apologies to Marshall McLuhan,

至少在论文之中，这一路径承诺了更好的性能，你可以看到可能EOS也会按照这种方式来构造。实际上，正是出于对系统速度的要求，让 EOS　的设计者[@dantheman][3]和我能够发现（对不住了，Marshall McLuhan）：

> the message is the medium.

> 信息即媒介

---------------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

荆凯，程序员，坚信区块链将会改变潮水的方向。欢迎加微信: shuke0327，或者关注公众号: 增长之道

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------
[1]:https://en.wikipedia.org/wiki/Finite-state_machine
[2]:https://steemit.com/@dantheman

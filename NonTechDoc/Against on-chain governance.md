Against on-chain governance

反对链上治理

Refuting (and rebuking) Fred Ehrsam’s governance blog

驳斥Ehrsam有关治理的博客。

I’ve been thinking about blockchain governance for a long time, and recently my understanding of the process has become (I think) a lot more clear.

I was (and still am) working on a blog post titled “Blockchain Governance 101”, which I hope will share some basic language for reasoning about governance.

Before I managed to finish (the research is ongoing, and it’s not my top priority), Fred Ehrsam published a blog post “Blockchain Governance: Programming Our Future”, framing the discussion as a primarily design problem.

I really don’t think blockchain governance (or governance in general) can be understood as a design problem. I think it’s almost always a mistake to imagine that you can design and institute a governance process, especially for an existing blockchain community with existing processes, and especially without adequate knowledge of the existing governance processes.

This blog post is not an introduction to blockchain governance (that is still in the pipeline) and won’t give an overview of key concepts, issues or questions. Nor will it provide any blockchain governance solutions or suggestions. It is instead refutation of core positions that Fred takes in his blog, along with a warning about the dangers of suggesting that people should try to institute their favorite formalized governance model without clear regard for the existing blockchain governance processes.

I think that Fred’s intentions are good, and the views he expressed in his blog post are understandable. But I also I think the blog is missing important concepts and context to the point that I consider it harmful, warranting a long-form response (i.e. a response outside of Tweet storms).

Blockchain governance is not a design problem
Fred and I agree that blockchain governance is extremely important. I think it’s the second (rather than first) most important factor that will determine whether blockchains end up being a public good, or a menace to the public. Second only after the shared purpose of the blockchain community (a purpose that legitimate governance presumably is supposed to bear out).

There is no question that governance decisions matter, and big time. And the structure of a blockchain governance process can dramatically effect governance outcomes. However, this does not make blockchain governance a design problem.

Governance is a process. It involves players who participate in that process to produce decisions that affect the governed resources. These decisions can have a lasting impacts on many stakeholders.

The participants coordinate around this process, and they build knowledge about the governance processes, about each other, about their incentives and about their states of knowledge. This knowledge can be tacit or formal, it can be local knowledge or it can be common knowledge. Participants can develop strong norms (e.g. no contentious hard forks).

The information and incentives of participants constrains their participation, and they need to be understood in the context of the underlying culture, as well as their individual contexts. The information and incentives of participants can change over time, but they don’t change instantly, nor do they change independently of each other’s incentives and states of knowledge. The process of changing the way that something is governed is not magic, and in our case it’s also very human.

So even if it was possible to come up with an ideal solution to “the governance design problem”, it might not be possible for the participants to adopt it. There are pre-existing constraints on participants’ ability to coordinate to adopt any proposed governance solutions. And these constraints can even be entirely in their heads, in the form of local or tacit knowledge, or norms and common knowledge.

So when you make a governance proposal, the participants in the current governance process are going to ask themselves “is this a significant improvement over the process we are using now?”, “Will the other participants in the process think so, too?”, “What will it take to switch from our current process to this one?”, and “Is it worth the disruption to existing processes?”

Even if you somehow come up with an ideal governance design, you haven’t “solved governance” for anyone until it is successfully adopted.

Fred seems to have missed the fact that information is just as important of a “critical component of governance” as incentives or “mechanisms for coordination” (which is a subset of a broader “critical component” called “governance structure”, from my point of view). Not a huge deal!

Look at the system before you call for revolution
When you propose an alternative governance process, and especially when you suggest that we need an alternative process, you’re proclaiming “the existing governance processes are not good enough” and you’re begging the question of “are the existing processes legitimate?”. You’re a stone’s throw away from advocating for revolution; a replacement of the existing governance processes.

Revolution isn’t easy or risk-free, and forking means that you will leave some of your peers behind. When you are advocating for revolution, you had better be sure that the revolution will succeed, and that the new process will be effective and legitimate

Fred’s blog post showed no almost acknowledgement of the existence of functoning blockchain governance processes in either Bitcoin or Ethereum. He dismissed them out-of-hand with little consideration, perhaps because Fred knows that the reader likely already assumes that Bitcoin governance is broken and that Vitalik controls Ethereum governance.

He showed very little knowledge about how the Ethereum governence process works. That’s fair enough, because the Ethereum governance process are not very well documented, and it’s hard to understand them without actively participating in them. They evolved over time, and are not an institutionalization of a formal model, and therefore have no inherent reason to be easy to identify or communicate.

No one has full information about the structure of the processes involved. Partly because documenting reality is hard work, and so is communication and education. Partly because the processes are still evolving. And also partly because people only inevitably learn about the processes that they participate in themselves. Most observers don’t participate, and can’t be expected to understand the process, at least until clear documentation is available.

To clear up some of the misinformation about Ethereum governance shared in Fred’s blog: Proof-of-stake will not change the Ethereum governance processes at all, and miners *do not* have a significant influence on the governance process today. Moreover, Vitalik does not have nearly the amount of power to influence governance outcomes that Fred (and lots of other people) assume that he does. The structure of the governance processes limit Vitalik’s power, just as it limits everyone’s power.

Unfortunately for the curious reader, documenting the Ethereum governance process is out of scope for this blog. Stay patient! :)

Against on-chain governance
“On-chain governance” refers to the idea that the blockchain nodes automatically upgrade when an on-chain governance process decides on an upgrade and that it’s time to install it. No hard forks required.

Adopting on-chain governance is incredibly risky because it always represents a revolution. It’s not necessarily a revolt against the governance processes that merge code into software repositories (as those could conceivably be encoded on-chain, though this notably isn’t normally what is proposed), but a revolution that overthrows the processes that govern full nodes.

With off-chain governance (the current norm), a node operator has to consciously decide whether to install a hard fork to have his node be consensus-compatible with the nodes of operators who also decided to install that hard fork.

With off-chain blockchain governance, node operators’ decision processes are absolutely necessary parts of blockchain governance, and therefore node operators are necessary participants in blockchain governance.

On-chain governance makes node operator participation in governance completely unnecessary. It makes it so that a node operator, making no decision, follows the decisions made by the on-chain process. Defaults are incredibly powerful: The more nodes follow the default, the less feasible it is for a concerned node operator to refuse to install a hard fork. (Technically, it’s not actually a hard fork or a soft fork, though the upgrade would have been a hard or soft fork in an off-chain governance model.)

Why is this a big deal? Well, the protocol doesn’t have an anti-Sybil measure on node operators (or on their users). This means that node operators (and therefore users) will necessarily be robbed of their participation in governance, by any on-chain governance proposal.

The role of full nodes in off-chain governance provides an important check to balance against the power of processes that make changes to software. On-chain governance removes that check, and the balance it provides.

Unless there are governance processes that get Sybil-resistant input from node operators, on-chain governance therefore has always has the potential to disenfranchise node operators (and users) of the blockchain. If you are a blockchain node operator (or user), or if you care about blockchain node operators (or users), then I hope you will learn to regard on-chain governance proposals with extreme apprehension.

Against plutocracy and all of its infinite variants
Coin holder interests and user interest are not naturally aligned. Users have to buy coins from coin holders to use the blockchain. Coin holders would prefer if users had to pay more. While users would prefer if they had to pay less.

It is critical to recognize that “user” and “coin holder” are roles that have distinct incentives corresponding to their roles. Just because you’re both a user and a coin holder, or even if most users today are also coin holders, does not mean that we should design our blockchain protocol or our blockchain governance processes to favour coin holder interests over user interests.

The market between blockchains is absolutely not perfectly competitive. It is highly oligopolistic because blockchains have strong network effects (obviously because they are p2p protocols, and more subtly because different blockchain communities have different cultures). So it’s very risky to assume that coin holders want what’s good for users because the price of coins will go down as a result. That will only happen if the users bear sufficient cost. And that cost might be high, and even if it isn’t, any cost is something I wouldn’t wish on all of the users of the blockchain.

If on-chain governance is a big risk to node operators and users, then plutocratic on-chain governance is at least as risky. And any on-chain governance proposal that is driven by coin holder votes has this problem. Yes, even if it’s based on prediction markets (futarchy), and even if the coins are locked up.

Not only is on-chain coin-based governance inconsistent with user interests, it is also antithetical to the ethos of public blockchains. The blockchain is for the public, to serve the public interest. It isn’t for cryptocurrency whales to get more rich. Cyptocurrency holdings (like wealth in global society) is highly concentrated in the hands of a very small number of people. The blockchain isn’t supposed to be owned by anyone… nevermind by a small group of superrich individuals.

Blockchain governance is too important for us to let a small handful of cryptocurrency whales make arbitrary decisions.

Caveats
I agree with Fred that the blockchain itself is a tremendously valuable tool for experimenting with governance tools and processes. I am a fan (in theory) of on-chain tools that are in smart contracts but aren’t part of the blockchain protocol. And I think we should experiment with that. I also agree that off-chain tools can be extremely valuable as a way for participants to signal to each other.

These kinds of tools can provide a signal to node operators that actually helps them make a decision, as opposed to on-chain processes that make their decision unnecessary. These tools can also help participants in the governance processes that affect changes to software repositories.

If we find that we can build useful blockchain governance tools using the blockchain, that’s great! However, overthrowing the processes that govern the software implementations of the blockchain, or the processes that govern full nodes is most probably not well-advised.

Last words (Conclusion)
Blockchain governance is not an abstract design problem. It’s an applied social problem. It’s a problem that is defined in the context of existing governance structure, and in the context of the current information and incentives of today’s participants in today’s governance processes.

We need to look very carefully at the blockchain governance processes that we already have before we declare that they don’t exist, are illegitimate, propose alternatives, fork, or advocate for revolution.

It is your right to propose the institutionalization of your favorite formal governance model as a replacement to the existing structure of governance, of course.

However, consider that insodoing you may be sabotaging the legitimacy of the existing governance process. The existing process may have evolved over time and may not be well understood or documented. Replacing something you don’t understand with something you do has obvious appeal, but it is reckless. So maybe hold off until recklessness is the only tenable option?

Please be careful. The effectiveness and legitimacy of our blockchain governance processes are critically important. Don’t needlessly put them at risk! Treat your articulation of governance problems and proposals as a loaded weapon and don’t shoot in the dark.

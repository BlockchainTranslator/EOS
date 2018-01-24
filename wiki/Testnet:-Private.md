>本文翻译自：https://github.com/EOSIO/eos/wiki/Testnet%3A%20Private
>
>译者：区块链中文字幕组 荆凯
>
>翻译时间：2017-12-30

## Testnet: Private | 私有测试网络

To date, all work done to experiment with the EOS blockchain has been performed using a single instance of eosd hosting all 21 block producers. While this is a perfectly valid solution for validating features of the blockchain, developing new contracts, or whatever, it does not scale. Nor does it expose the sort of issues raised when contract and block data must be shared across multiple instances. Providing the ability to scale involves deploying multiple eosd nodes across many hosts and lining then into a peer-to-peer (p2p) network. Composing this network involves tailoring and distributing configuration files, coordinating starts and stops and other tasks.

目前为止，所有使用EOS区块链进行实验的工作都是使用eosd的单个实例来执行的，在这单个eosd实例上，托管了所有的21个区块生产者。对于验证区块链的特性，开发新的智能合约或者其它东西而言，这是个完全有效的解决方案，但是它没有扩展。它也不会暴露出当智能合约和区块数据必须跨多个实例共享时所引发的问题。想要提供扩展的能力，涉及到跨越多个服务器来部署多个eosd节点，将他们连接为点对点(p2p)网络。组成该网络包括裁剪和分配配置文件，协调启动和停止和其他任务。

Doing this manually is a tedious task and easily error prone. Fortunately a solution is provided, in the form of the Launcher application, described below.

手动执行这一任务是繁琐枯燥，而且容易出错。幸运的是，已经以启动程序的形式提供了一个解决方案，描述如下。

* [Testnet nodes, networks, and topology - 测试节点，网络和拓扑结构](#testnet-nodes-networks-and-topology)
* [Localhost networks - 本地网络](#localhost-networks)
  - [Distributed networks - 分布式网络](#distributed-networks)
* [Network Topology - 网络拓扑](#network-topology)
  - [Star network - 星形网络](#star-network)
  - [Mesh network -  Mesh 网络](#mesh-network)
  - [Custom network shape - 自定义网络形态](#custom-network-shape)
* [The Launcher Application - 启动程序](#the-launcher-application)
  - [Running the Launcher application - 运行启动程序](#running-the-launcher-application)
  - [Launcher command line arguments - 启动程序的命令行参数](#launcher-command-line-arguments)
  - [The Generated Multihost Testnet Configuration File - 生成的多主机测试网络配置文件](#the-generated-multihost-testnet-configuration-file)
  - [Runtime Artifacts - 运行时构件](#runtime-artifacts)



# Testnet nodes, networks, and topology | 测试网络节点，网络，以及拓扑
Before getting into the details of the EOS testnet, lets clarify some terms. In this document I use the terms "host" and "machine" fairly interchangeably. A host generally boils down to a single IP address, although in practice it could have more.

在了解EOS testnet的详细信息之前，先澄清一些术语。在本文档中，我使用了“主机”和“机器”这两个可以互换的术语。主机一般可以归结为一个IP地址，但实际上它可以有更多的IP地址。

The next term is "node." A node is an instance of the eosd executable configured to serve as 0 or more producers. There is not a one-to-one mapping between nodes and hosts, a host may serve more than one node, but one node cannot span more than one host.

下一个术语是“节点”。“节点是eosd可执行文件的一个实例，它被配置为0或更多的生产者。节点和主机之间没有一对一的映射，主机可以提供多个节点，但是一个节点不能跨越多个主机。

I use "local network" to refer to any group of nodes, whether on a single host or several, are all close in that access does not have to leave a secure network environment.

我使用“本地网络”表示任何一组节点，无论是在单个主机还是多个主机上，这些节点都很接近，不需要离开安全的网络环境。

Finally there is the idea of distributed networks that involve remote hosts. These may be hosts on which you may not have direct access for starting and stopping eosd instances, but with whom you may wish to collaborate for setting up a decentralized testnet.

最后是分布式网络的概念，涉及到远程主机。可能有些你无法直接访问来启动和停止eosd实例的主机，但是你可能希望与之合作建立一个分散的测试网络。

# Localhost networks | 本地网络
Running a testnet on a single machine is the quickest way to get started. As you will see below, this is the default mode for the Launcher application. You can set up a localhost network immediately by simply telling the launcher how many producing or non-producing nodes to activate, and perhaps what type of network topology to use.

在一台机器上运行一个测试网络是启动的最快方法。如下所示，这是启动程序应用程序的默认模式。通过简单地告诉启动程序激活多少个生产节点或非生产节点，以及可能使用哪种类型的网络拓扑，您可以立即设置一个本地网络。

The downside is that you need a lot of hardware when running many nodes on a single host. Also the multiple nodes will contend with each other in terms of CPU cycles, limiting true concurrency, and also localhost network performance is much different from inter-host performance, even with very high speed lans.

缺点是在单个主机上运行多个节点时需要大量硬件。此外，多个节点将在CPU周期方面相互竞争，限制真正的并发性，而且本地主机的网络性能与跨主机间的网络性能差别很大，即使是非常高速的lan。

## Distributed networks | 分布式网络

The most representative model of the live net is to spread the eosd nodes across many hosts. The Launcher app is able to start distributed nodes by the use of bash scripts pushed through ssh. In this case additional configuration is required to replace configured references to "localhost" or "127.0.0.1" with the actual host name or ip addresses of the various peer machines.

live net的最具代表性的模型是在许多主机上分布eosd节点。启动程序可以使用通过ssh推送bash脚本来启动分布式节点。在这种情况下，需要额外的配置，将参考的配置从"localhost" 或 "127.0.0.1" 改为多台主机的真实主机名或者ip地址。

Launching a distributed testnet requires the operator to have ssh access to all the remote machines configured to authenticate without the need for a user entered password. This configuration is described in detail below.

启动一个分布式测试网络需要操作者在所有的远程机器上拥有ssh访问权限，不需要输入密码就可以进行身份验证。配置的细节下面会有描述。

In cases where a testnet spans multiple remote networks, a common launcher defined configuration file may be shared externally between distributed operators, each being responsible for launching his or her own local network.

Note that the Launcher will not push instances of eosd to the remote hosts, you must prepare the various test network hosts separately.

在一个测试网络跨越多个远程网络的情况下，一个共用的启动器定义配置文件可以在分布的操作者中内部共享，每个操作者负责启动他/她自己的本地网络。

注意，启动器不会将eosd实例推送到远程主机上，你必须单独为每一台测试网络中的主机配置好。

# Network Topology | 网络拓扑
Network topology or "shape" describes how the nodes are connected in order to share transaction and block data, and requests for the same. The idea for varying network topology is that there is a trade off between the number of times a node must send a message reporting a new transaction or block, vs the number of times that message must be repeated to ensure all nodes know of it.

The Launcher has definitions of two basic different network "shapes" based on inter-nodal connections, which can be selected by a command line option. If you wish to create your own custom network topology, you can do so by supplying a json formatted file. This file is typically the edited version of the template created by the launcher in "output" mode.

网络拓扑或者“shape”描述了节点如何连接，以共享交易和区块数据，和请求相同的数据。之所以设计了可变的网络拓扑，是想在两者之间进行权衡： 一方面是一个节点发送信息报告一笔新交易或者区块的次数，另外一方面，为了让所有的节点都能够知晓，信息需要重复的次数。

启动器定义了基于节点间连接的两个基本不同的网络“形状”，可由命令行选项选择。
如果你想要创建自定义的网络拓扑，可以通过提供一个json格式的文件来实现。该文件通常是由启动程序在“输出”模式中创建的模板的编辑版本。

## Star network | 星形网络
![](https://github.com/EOSIO/eos/raw/master/star.png)
A "star" is intended to support a larger number of nodes in the testnet. In this case the number of peers connected to a node and the distribution of those nodes varies based on the number of nodes in the network.

星形的设计是用于在测试网络中支持更大数量的节点。连接到某个节点的对等节点的数量以及这些节点的分布根据网络中节点的数量变化而变化。

## Mesh network
![](https://github.com/EOSIO/eos/raw/master/mesh.png)
In a "mesh" network, each node is connected to as many peer nodes as possible.

在mesh网络中，每个节点都连接到尽可能多的对等节点。

## Custom network shape 自定义网络形态
![](custom.png)
This is an example of a custom deployment where clusters of nodes are isolated except through a single crosslink.

这是一个自定义部署的示例，其中，除了通过单个交叉链接，集群节点都是单独的。

# The Launcher Application 启动器程序
To address the complexity implied by distributing multiple eosd nodes across a LAN or a wider network, the launcher application was created.

Based on a handful of command line arguments the Launcher is able to compose per-node configuration files, distribute these files securely amongst the peer hosts, then start up the multiple instances of eosd.

Eosd instances started this way have their output logged in individual text files. Finally the launcher application is also able to shut down some or all of the test network.

为了解决在LAN或更广泛的网络中分布多个eosd节点的复杂性，创建了启动应用程序。

基于少量的命令行参数，启动程序可以编写每个节点的配置文件，在对等主机之间安全地分发这些文件，然后启动eosd的多个实例。

以这种方式启动的Eosd实例将其输出记录在单独的文本文件中。最后，启动程序还可以关闭部分或全部的测试网络。

## Running the Launcher application 运行启动程序

The launcher program is used to configure and deploy producing and non-producing eosd nodes that talk to each other using configured routes. The configuration for each node is stored in separate directories, permitting multiple nodes to be active on the same host, assuming the machine has sufficient memory and disk space for multiple eosd instances. The launcher makes use of multiple configuration sources in order to deploy a testnet. A handful of command line arguments can be used to set up simple local networks.

启动程序用于配置和部署eosd区块生产节点和非生产节点，它们使用配置的路由彼此通信。每个节点的配置存储在单独的目录中，假如机器有足够的内存和磁盘空间用于多个eosd实例，可以允许多个节点在同一个主机上活动。启动程序使用多个配置源来部署一个testnet。可以使用少量命令行参数设置简单的本地网络。

To support deploying distributed networks, the launcher will read more detailed configuration from a JSON file. You can use the launcher to create a default JSON file based on the command line options you supply. Edit that file to substitute actual hostnames and other details
as needed, then rerun the launcher supplying this file.

为了支持分布式网络的部署，启动程序将从JSON文件中读取更详细的配置。你可以基于你所提供的命令行选项，使用这个启动器来创建一个默认JSON文件。编辑该文件，替换为实际的主机名和其他需要的细节，然后重新运行提供该文件的启动程序。

For the moment the launcher only activates platform-native nodes, dockerized nodes will be added later. It should be straight forward to use the generated configuration files with dockerized nodes.

目前，启动程序只会激活平台的原生节点，稍后将添加dockerized节点。应该直接使用dockerized节点所生成的配置文件。

## Launcher command line arguments 启动程序的命令行参数
Here is the current list of command line arguments recognized by the launcher.

下面是当前启动程序可识别的命令行参数的列表。

```
launcher command line arguments:
  -n [ --nodes ] arg (=1)               total number of nodes to configure and
                                        launch
  -p [ --pnodes ] arg (=1)              number of nodes that are producers
  -d [ --delay ] arg (=0)               number of seconds to wait before starting the next node. Used to simulate a person keying in a series of individual eosd startup command lines.
  -s [ --shape ] arg (=star)            network topology, use "star"
                                        "mesh" or give a filename for custom
  -g [ --genesis ] arg (="./genesis.json")
                                        set the path to genesis.json
  -o [ --output ] arg                   save a copy of the generated topology
                                        in this file
  --skip-signature                      EOSD does not require transaction
                                        signatures.
  -i [ --timestamp ] arg                set the timestamp for the first block.
                                        Use "now" to indicate the current time
  -l [ --launch ] arg                   select a subset of nodes to launch.
                                        Currently may be "all", "none", or
                                        "local". If not set, the default is to
                                        launch all unless an output file is
                                        named, in which case it starts none.
  -k [ --kill ] arg                     The launcher retrieves the previously
                                        started process ids and signals each with the specified signum. Use 15 for a sigterm and 9 for sigkill.                              
  -h [ --help ]                         print this list
```
Note that if a testnet.json file is supplied as the `--shape` argument, then the `--nodes`, `--pnodes`, and `--genesis` arguments are all ignored.

## The Generated Multihost Testnet Configuration File 生成的多主机测试网络的配置文件
This is the file generated by running the following command:

这是运行如下命令所生成的文件:

 `launcher --output <filename> [other options]`

In this mode, the launcher does not activate any eosd instances, it produces a file of the given filename. This file is a JSON formatted template that provides an easy means of

在这种模式下，启动程序不会激活任何eosd实例，它会生成一个给定文件名的文件。该文件是一个JSON格式的模板，提供了一种简单的方式。

The object described in this file is composed of a helper for using ssl, and a collection of testnet node descriptors. The node descriptors are listed as name, value pairs. Note that the names serve a dual purpose acting as both the key in a map of node descriptors and as an alias for the node in the peer lists. For example:

这个文件中描述的对象由一个使用ssl的helper和一个测试网络节点的描述符组成。节点描述符作为名字-值的对的形式列出。请注意，这些名称有双重用途，既作为描述符map的键，也作为对等列表中的节点的别名。例如:

```
{
  "ssh_helper": {
    "ssh_cmd": "/usr/bin/ssh",
    "scp_cmd": "/usr/bin/scp",
    "ssh_identity": "phil",
    "ssh_args": "-i ~phil/.ssh/id-sample"
  },
```
The ssh helper fields are paths to ssh and scp, an identity if necessary, and any optional arguments.

ssh helper 字段是ssh和scp的路径、必要时的标识和任何可选参数。

```
  "nodes": [[
      "testnet_0",{
        "genesis": "./genesis.json",
        "remote": true,
        "ssh_identity": "",
        "ssh_args": "",
        "eos_root_dir": "/home/phil/blockchain/eos",
        "data_dir": "tn_data_0",
        "hostname": "remoteserv",
        "public_name": "remoteserv",
        "p2p_port": 9876,
        "http_port": 8888,
        "filesize": 8192,
        "keys": [{
            "public_key": "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
            "wif_private_key": "5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"
          }
        ],
        "peers": [
          "testnet_1",
          "testnet_2",
          "testnet_3",
          "testnet_4",
          "testnet_5"
        ],
        "producers": [
          "inita",
          "initg",
          "initm",
          "inits"
        ]
      }
    ],[
      "testnet_1",{

```

The rest of the testnet.json file is the collection of node descriptors. The fragment shown above was created with the command line `programs/launcher/launcher -p6 -s mesh -o testnet.json` and then edited to refer to a remote host named "remoteserv."

testnet.json的其余部分是节点描述符的集合。上面显示的片段是用如下命令行创建的
`programs/launcher/launcher -p6 -s mesh -o testnet.json`
然后编辑该文件，表示一个名为“remoteserv”的远程主机。

### Elements Of The JSON File JSON文件的元素
This table describes all of the key/value pairs used in the testnet.json file.

|Value          | Description
| :------------ | :-----------
| ssh_helper    | a set of values used to facilitate the use of SSH and SCP
| nodes         | a collection of descriptors defining the eosd instances used to assemble this testnet. The names used as keys in this collection are also aliases used within as placeholders for peer nodes.

|值	|说明
| :------------ | :-----------
|ssh_helper	|一组值，供SSH和SCP使用
|nodes	|一组描述符，用于定义组成此测试网络的eosd实例。在此集合中用作键的名称，也用作对等节点的占位符。

|ssh_helper elements | Description
| :----------        | :------------
| ssh_cmd            | path to the local ssh command
| scp_cmd            | path to the local scp command
| ssh_args           | any additional command line arguments needed to successfully connect to remote peers
| ssh_identity       | The user name to use when accessing the remote hosts

|ssh_helper元素	|描述
| :----------        | :------------
|ssh_cmd	|本地ssh命令的路径
|scp_cmd	|到本地scp命令的路径
|ssh_args	|功连接到远程节点所需要的其它额外的命令行参数
|ssh_identity	|在访问远程主机时使用的用户名

|node elements       | Description
| :--------          | :----------
| genesis            | path to the genesis.json file. This should be the same file for all members of the testnet.
| remote             | specifies whether this node is in the local network or not. This flag ties in with the launch mode command line option (-l) to determine if the local launcher instance will attempt to start this node.
| ssh_identity       | a per-node override of the general ssh_identity defined above.
| ssh_args           | a per-node override of the general ssh_args
| eos_root_dir       | specifies the directory into which all eosd artifacts are based. This is required for any hosts that are not the local host.
| data_dir           | the root for the remaining node-specific settings below.
| hostname           | the domain name for the server, or its IP address.
| public_name        | possibly different from the hostname, this name will get substituted for the aliases when creating the per-node config.ini file's peer list.
| p2p_port           | combined with the public name to identify the endpoint listed on for peer connections. When multiple nodes share a host, the p2p_port is automatically incremented for each node.
| http_port          | defines the listen endpoint for the client API services
| filesize           | sets the capacity in megabytes for the size of the blockchain backing store file.
| keys               | specify the authentication tokens for this node.
| peers              | this list indicates the other nodes in the network to which this one actively connects. Since this file may be edited to alter the hostname, public name, or p2p port values, the peers list here holds aliases for the actual endpoints eventually written to the individual config.ini files.
| producers          | this list identifies which of the producers from the genesis.json file are held by this node. Note that the launcher uses a round-robin algorithm to spread the producer instances across the producing nodes.

|节点元素	|描述
| :--------          | :----------
|genesis	|genesis.json文件的路径。这对于testnet的所有成员应该是相同的文件
|remote	|指定该节点是否在本地网络中。此标志与启动模式命令行选项(- l)连接，以确定本地启动程序实例是否将尝试启动此节点。
|ssh_identity	|每个节点中的定义，会覆盖上面所定义的一般ssh_identity。
|ssh_args	|每个节点中的定义，会覆盖通用的ssh_args
|eos_root_dir	|指定所有eosd工件都基于的目录。这对于任何非本地主机都是必需的。
|data_dir	|节点其余配置的根目录
|hostname	|服务器的域名，或其IP地址。
|public_name	|可能与主机名不同，在创建每个节点的config.init文件的peer list时，这个名称将被替换为别名
|p2p_port	|与公共名称结合，以标识用于对等连接的端点。当多个节点共享一个主机时，每个节点都会自动增加p2p_port
|http_port	|定义了客户端API服务的监听端点
|filesize	|为区块链备份存储设置的文件大小, 单位是Mb
|keys	|为该节点指定身份验证token
|peers	|这个列表显示了网络中这个节点所连接的其它活跃节点。由于可以编辑该文件来更改主机名、公共名称或p2p端口值，所以这里的peer列表为最终写入到单独config.init文件中的实际终端节点(endpoints)的别名
|producers	|此列表标识了 genesis.json 文件中的哪些生产者在当前的节点上。注意，启动程序使用 round-robin 算法在生产节点上分布生产者的实例。


### Provisioning Distributed Servers 提供分布式服务器
The ssh_helper section of the testnet.json file contains the ssh elements necessary to connect and issue commands to other servers. In addition to the ssh_helper section which provides access to global configuration settings, the per-node configuration may provide overriding identity and connection arguments.

testnet.json文件中的ssh_helper部分包含连接和发出命令到其他服务器所需的ssh元素。除了提供全局配置设定访问的ssh_helper部分之外，每个节点的配置可能提供覆盖的身份和连接参数。

It is also necessary to provision the server by at least copying the eosd executable, and the genesis.json files to their appropriate locations relative to some named EOS root directory. For example, I defined the EOS root to be `/home/phil/blockchain/eos`. When run, the launcher will run through a variety of shell commands using ssh and finally using scp to copy a config.ini file to the appropriate data directory on the remote.

另外，还至少需要提供给服务器, 复制eosd可执行文件和genesis.json文件到相对于某个名为EOS的根目录的恰当的位置。例如，我定义EOS根目录为
/home/phil/blockchain/eos. 运行时，启动程序将使用ssh运行各种shell命令，最后使用scp来复制config.ini文件到远程服务器上的恰当的data目录下。


## Runtime Artifacts 运行时构件
The launcher app creates a separate date and configuration directory for each node instance. This directory is named `tn_data_<n>` with n ranging from 0 to the number of nodes being launched.

启动应用程序为每个节点实例创建一个单独的日期和配置目录。这个目录名为`tn_data_<n>` n的范围是从0到启动节点的数量。

| Per-Node File | Description
| :------------ | :----------
| config.ini    | The eosd configuration file.
| eosd.pid      | The process ID of the running eosd instance.
| blockchain/*  | The blockchain backing store
| blocks/*      | The blockchain log store
| stderr.txt    | The cerr output from eosd.
| stdout.txt    | The cout output from eosd.

A file called "last_run.json" contains hints for a later instance of the launcher to be able to kill local and remote nodes when run with -k 15.

名为"last_run.json"的一个文件为之后运行的启动程序节点的提示，可以带参数-k 15来运行该节点，杀死本地和远程的节点。

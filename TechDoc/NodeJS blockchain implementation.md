# 用NodeJS实现区块链

> 本文翻译自：[NodeJS blockchain implementation: BrewChain: Chain+WebSockets+HTTP Server](http://www.darrenbeck.co.uk/blockchain/nodejs/nodejscrypto/)
>
> 译者：[区块链中文字幕组](https://github.com/BlockchainTranslator/EOS) [咪咪](https://github.com/mimizhang)
>
> 翻译时间：2018-02-22

-------------

I am going to create BrewChain. A verifiable chain of which member of the team made a brew and when. Protecting the history of events from any swindlers who may attempt to claim they have made more brews than they actually did.

我们将创建一个名为BrewChain的区块链，用于验证团队中的什么人在什么时间制茶，防止一些骗子可能试图声称他们的生产出的茶比他们实际的产出更多。

Our application will consist of the following:

- Our block and blockchain
- A Node which will run on team members machines, listening for new blocks broadcast and also broadcasting new blocks and updating the chain.
- An HTTP server and web interface for interacting with brew activities, the log and other data

我们的应用包含了一下几个部分：

- 区块和区块链
- 运行在团队成员机器中的节点，这个节点将负责监听新区块的产生，并且向全网广播生产出新的区块以及更新区块链
- 用于与制茶活动，日志和其他数据进行交互的HTTP服务器和Web界面

## Blockchain(区块链)

Blockchain is essentially a linked list in which each item contains a hash of the previous item.

区块链本质上是一个链接列表，其中每个区块包含前一个区块的哈希值。

The fundamental element in this chain is the block. Each block contains data, and a hash of the previous block. This hashed pointer maintains the integrity of the data and makes the list immutable.

链条上的基本元素是区块。每个区块包含了数据以及上一个区块的哈希值。这个哈希指针维持了数据的完整性，并使得整个列表不可篡改。

To start with we need to determine the essential elements of our block.

- timestamp
- index (optional)
- data - whatever we wish to store in the block
- hash - (a hash of the timestamp,index,data and previous hash)
- previous hash - the hash of the previous block

首先，我们需要确定区块的基本要素：

- 时间戳
- 索引（可选）
- 数据——存储在区块中的任何数据
- 哈希——时间戳、索引、数据以及上一个区块哈希的哈希值
- 上一个哈希——上一个区块的哈希值

```js
const createBlock = (lastBlock, data) =>{
	let newBlock = {
	    timestamp: new Date().getTime()
	  , data: data
	  , index: lastBlock.index+1
	  , previousHash: lastBlock.hash
	};

	newBlock.hash = createHash(newBlock);

	return newBlock;
}
```

Given the last block and the new data, the function will create and return a new block.

给定上一个区块以及新数据，上面的函数将创建并返回一个新区块。

We’d then need a genesis block to begin our chain at element 0.

然后，我们需要在第0个元素位置创建一个创世区块来作为区块链的开端：

```js
const genesisBlock = { 
	index: 0
  , timestamp: new Date().getTime()
  , data: 'Our genesis data'
  , previousHash: "-1"
};

genesisBlock.hash = createHash(genesisBlock);
addToChain(genesisBlock);
```

We can then create our blocks, adding them to the chain.

这样我们就可以创建新的区块，并把他们加入到链中了。

## BrewChain

Taking the above and building a chain, we get the following:

通过以上步骤我们就可以创建一条链了：

```js
const BrewChain = function() {
    let chain = [];
    let currentBlock = {};
    let genesisBlock = {};

    function init(){
        genesisBlock = { 
            index: 0
          , timestamp: new Date().getTime()
          , data: 'our genesis data'
          , previousHash: "-1"
        };

        genesisBlock.hash = createHash(genesisBlock);
        chain.push(genesisBlock);
        currentBlock = genesisBlock; 	
    }

    function createHash({ timestamp, data, index, previousHash }) {
        return Crypto.createHash('SHA256').update(timestamp+data+index+previousHash).digest('hex');
    }

    function addToChain(block){
        if(checkNewBlockIsValid(block, currentBlock)){	
            chain.push(block);
            currentBlock = block; 
            return true;
        }

        return false;    
    }

    function createBlock(data){
        let newBlock = {
            timestamp: new Date().getTime()
          , data: data
          , index: currentBlock.index+1
          , previousHash: currentBlock.hash
        };

        newBlock.hash = createHash(newBlock);
  
        return newBlock;
    }

    function getLatestBlock(){
        return currentBlock;
    }

    function getTotalBlocks(){
        return chain.length;
    }

    function getChain(){
        return chain;
    }

    function checkNewBlockIsValid(block, previousBlock){
        if(previousBlock.index + 1 !== block.index){
            //Invalid index
            return false;
        }else if (previousBlock.hash !== block.previousHash){
            //The previous hash is incorrect
            return false;
        }else if(!hashIsValid(block)){
            //The hash isn't correct
            return false;
        }
		
        return true;
    }	

    function hashIsValid(block){
        return (createHash(block) == block.hash);
    }

    return {
        init,
        createBlock,
        addToChain,
        checkNewBlockIsValid,
        getLatestBlock,
        getTotalBlocks,
        getChain
    }
};    

let myBrew = new BrewChain();
myBrew.init();

myBrew.addToChain(myBrew.createBlock('The 1st block'));
myBrew.addToChain(myBrew.createBlock('The 2nd block'));

...
```

This will setup our chain object, creating a genesis block and adding it to the chain.

这样我们就设置了一个链对象，该对象创建了一个创世区块，并将它加入到链中。

Our Brewchain contains the ability to create new blocks, add new blocks to our chain and also check the validity of a block.

Brewchain可以创建新的区块，将新区块添加到链中，并且可以验证区块的合法性。

The test code at the end adds two blocks and then outputs the chain to check that the blocks are successfully being created.

上面测试代码的末尾添加了两个区块到链中，然后输出链来确认是否成功创建了区块。

We’ll now begin building our P2P brewNode server..

接下来我们就可以开始创建我们的P2P brewNode服务。

## Brew节点P2P网络

Each BrewNode server will have a chain, a web socket server, and an http server for controlling it

每个BrewNode服务都将有一个链，一个web socket服务和一个http服务来控制它。

We’ll start by creating our node using web sockets..

我们将使用web sockets来创建节点。

```js
const BrewNode = function(port){
    let brewSockets = [];
    let brewServer;
    let _port = port
    let chain = new BrewChain();

    function init(){

        chain.init();
		
        brewServer = new WebSocket.Server({ port: _port });
		
        brewServer.on('connection', (connection) => {
            console.log('connection in');
            initConnection(connection);
        });		
    }

    const messageHandler = (connection) =>{
        connection.on('message', (data) => {
            console.log('Message In:');
            const msg = JSON.parse(data);

            console.log(msg.event);
        });
        console.log('message handler setup');
    }

    const broadcastMessage = (message) => {
        console.log('sending to all '+message)
        brewSockets.forEach(node => node.send(JSON.stringify({event: message})))
    }

    const closeConnection = (connection) => {
        console.log('closing connection');
        brewSockets.splice(brewSockets.indexOf(connection),1);
    }

    const initConnection = (connection) => {
        console.log('init connection');

        messageHandler(connection);
		
        brewSockets.push(connection);

        connection.on('error', () => closeConnection(connection));
        connection.on('close', () => closeConnection(connection));
    }

    const createBlock = (teammember) => {
        let newBlock = chain.createBlock(teammember)
        chain.addToChain(newBlock);
    }

    const getStats = () => {
        return {
            blocks: chain.getTotalBlocks()
        }
    }

    const addPeer = (host, port) => {
        let connection = new WebSocket(`ws://${host}:${port}`);

        connection.on('error', (error) =>{
            console.log(error);
        });

        connection.on('open', (msg) =>{
            initConnection(connection);
        });
    }

    return {
        init,
        broadcastMessage,
        addPeer,
        createBlock,
        getStats
    }

}
```

On init our server sets up a listening socket server, we add a handler for incoming messages and add the incoming connection to an array of socket connections.

在init方法中，我们创建了一个socket监听服务，我们也为传入的消息添加了一个处理器，并且将新链接添加到socket链接数组中。

We also add some methods for adding a new peer, broadcasting messages to connected peers and removing disconnected peers from our collection of sockets.

我们也创建了一些方法来添加新的节点，向新的节点广播消息以及将断开的节点从socket集合中删除。

The node also contains our BrewChain, a method which will create a block based on a teammembers name and add it to the chain.

节点上也有BrewChain，BrewChain将根据团队成员的名字创建区块，并将区块添加到链中。

Next we’ll add an HTTP server for sending commands to our server , which will also be used by our future UI interface.

接下来我们将添加一个HTTP服务用于像我们的服务发送指令，这个服务也将在今后的UI界面中使用。

```js
const http_port = 3000

let BrewHTTP = function (){
    const app = new express();

    app.use(bodyParser.json());

    app.get('/broadcast', (req, res)=>{
        console.log('broadcasting '+req.query.message)
        node1.broadcastMessage(req.query.message)
        res.send();
    })

    // For testing purposes currently only uses localhost
    app.get('/addNode/:port', (req, res)=>{
        console.log('adding localhost host: '+req.params.port)
        node1.addPeer('localhost', req.params.port)

        res.send();
    })

    app.get('/spawnBrew/:teammember', (req, res)=>{
        let newBlock = node1.createBlock(req.params.teammember);
		
        console.log('block created');

        console.log(node1.getStats())

        res.send();
    })

    app.listen(http_port, () => {
        console.log(`http server up.. ${http_port}`);
    })
}

let httpserver = new BrewHTTP();
```

So we now have an HTTP server for invoking actions on our node via the browser.

所以我们现在就有了一个可以在浏览器上调用节点的HTTP服务。

running the following requests in the browser:

在浏览器上运行下面三个请求：

- <http://localhost:3000/spawnBrew/terry> 
- <http://localhost:3000/spawnBrew/barry> 
- <http://localhost:3000/spawnBrew/bob>

Results in:

结果是：

![](http://www.darrenbeck.co.uk/assets/part1/brewnode.png)

The next stage of development is to begin communication between our nodes, distributing the chain

开发的下一步是要在节点之间进行通信。

Each node needs to do the following:

- Generate new chain blocks
- When it connects to a new node, request the latest block
- If we have no blocks, request the entire chain
- On receiving a new block with an index greater than ours from another node, determine if it is valid - if it is , and it is the next in the chain, add it. If it isn’t the next in the chain , we must have missed a few so lets request a full chain

每个节点都需要做到：

- 产生新的区块
- 当节点与新的节点连接时，要请求最新的区块
- 如果没有新的区块，请求整条链
- 在从另一个节点接收到大于当前区块索引的新区块时，确认它是否有效 - 如果是，并且新区快是链中的下一个区块时，则添加新区块。如果这个新区块不是下一个区块，那么肯定是错过了一些区块，就要请求整条链

To do this, lets begin by having it so that when a node generates a block it will dispatch it to all connected nodes.

为了做到这一点，我们首先让节点生成一个区块，然后将它广播给所有连接的节点。

```js
const BrewNode = function(port){
....
    const messageHandler = (connection) =>{
        connection.on('message', (data) => {
            const msg = JSON.parse(data);
            switch(msg.event){
                case "block":
                    console.log('Block recieved');
                    console.log(msg.message);
                    break;  
                default:  
                    console.log('Unknown message');
            }
        });
    }
....
    const broadcastMessage = (event, message) => {
        brewSockets.forEach(node => node.send(JSON.stringify({ event, message})))
    }
....
    const createBlock = (teammember) => {
        let newBlock = chain.createBlock(teammember)
        chain.addToChain(newBlock);

        broadcastMessage('block', newBlock);

    }
....
```

To test this is happening, lets load up two brew nodes on different ports.

为了测试这种情况，让我们在不同的端口上加载两个brew节点。

![](http://www.darrenbeck.co.uk/assets/part1/2nodes.png)

I’ll then run the following url to connect node 2 to node 1

运行下面的URL，将节点2连接到节点1：

![](http://www.darrenbeck.co.uk/assets/part1/2nodes2.png)

Running ‘<http://localhost:3004/spawnBrew/barry>’ should create a block and dispatch it to the connected node

运行 `http://localhost:3004/spawnBrew/barry`将创建一个区块，并将其广播到相连的节点

![](http://www.darrenbeck.co.uk/assets/part1/2nodes3.png)

That now works, with node 1 recieving the barry brew block

现在，节点1就接收到了barry brew区块

A quick alteration we must make here is to fix our genesis block to be the same across our nodes.

我们必须快速修改一下创世区块，使得所有节点的创世区块都是相同的：

```js
const BrewChain = function() 
...
    const genesisBlock = { 
        index: 0
      , timestamp: 1511818270000
      , data: 'our genesis data'
      , previousHash: "-1"
    };
```

Now we are going to process the recieved block(s) and create a consensus between our nodes.

现在我们要处理接收到的块，并在节点之间建立一个共识。

We’ll add some constants for our events and then setup the block processor

我们将为事件添加一些常量，然后设置区块处理器：

```js
...
    const BLOCK = "BLOCK";
    const REQUEST_CHAIN = "REQUEST_CHAIN";
...	

    const messageHandler = (connection) =>{
        connection.on('message', (data) => {
            const msg = JSON.parse(data);
            switch(msg.event){
                case BLOCK:
                    processedRecievedBlock(msg.message);
                    break;  
                default:  
                    console.log('Unknown message');
            }
        });
    }
...
    const processedRecievedBlock = (block) => {

        let currentTopBlock = chain.getLatestBlock();

        // Is the same or older?
        if(block.index <= currentTopBlock.index){
        	console.log('No update needed');
        	return;
        }

        //Is claiming to be the next in the chain
        if(block.previousHash == currentTopBlock.hash){
        	//Attempt the top block to our chain
        	chain.addToChain(block);

        	console.log('New block added');
        	console.log(chain.getLatestBlock());
        }else{
        	// It is ahead.. we are therefore a few behind, request the whole chain
        	console.log('requesting chain');
        	broadcastMessage(REQUEST_CHAIN,"");
        }
    }
```

Reloading up our two test nodes on different ports and running the following on node 1

在不同的端口上重载两个测试节点，然后在节点1上运行下面链接：

- <http://localhost:3003/spawnBrew/barry> 
- <http://localhost:3003/spawnBrew/bob>

Node 2 successfully recieves the new blocks and adds them to it’s chain

节点2成功的接收到两个区块，并把它加入到链中。

![](http://www.darrenbeck.co.uk/assets/part1/2nodes4.png)

Next we will add in our request chain functionality

接下来我们将添加请求链功能：

```js
...
	const CHAIN = "CHAIN";
...
    const messageHandler = (connection) =>{
        connection.on('message', (data) => {
            const msg = JSON.parse(data);
            switch(msg.event){
            	case REQUEST_CHAIN:
                    connection.send(JSON.stringify({ event: CHAIN, message: chain.getChain()}));
                    break;                  
                case BLOCK:
                    processedRecievedBlock(msg.message);
                    break;  
                case CHAIN:
                    processedRecievedChain(msg.message);
                    break;  
...
    const processedRecievedChain = (blocks) => {
        let sortedBlocks = blocks.sort((block1, block2) => (block1.index - block2.index))

        //Is the chain valid
        console.log('recieved a chain');
        console.log(sortedBlocks);
    }
```

Our server now recieves the requested chain, sorted. Before replacing our own chain for this one, we to verify it is a valid chain…

我们的服务现在接收到排序过的请求链。在替换我们自己的链之前，我们需要验证它是否是一个有效的链。

Before we do that though, I am going to implement a basic Proof of Work (for the sake of it)

在这么做之前，我们需要实现一个工作量证明。

## 工作量证明

In replacing our chain with the have the issue of consensus and knowing which chain is the ‘truth’. With blockchain, one way of helping do this is to add in the concept of ‘proof of work’. This requires a computational task to be carried out in order to generate (mine) a new block, the proof of this computation (called a nonce) is then stored in the block.

替换链就要涉及到共识问题以及要知道哪个链是真的。区块链中的“工作量证明”概念可以帮助我们知道哪一个链是有效的。这需要执行计算任务以生成（挖掘）一个新区块，然后将该计算的证明（称为随机数）存储在区块中。

The purpose of this is to add a time(energy) consuming element/puzzle into the process of creation, which is easy for others to verify as correct.

这样做的目的是在创建区块过程中添加一个耗时（耗能），并且其他人易于验证的元素（难题）。

Without this, it would be possible to spam the chain by creating a lot of blocks quickly and attempt to replace it with a chain that is longer.

如果不这么做，就可以在链上制造大量垃圾区块，并尝试用更长的链取代原有的链。

The inputs to this computational task are the based on the data of the previous block/block to be formed, and an integer which is our ‘guess’.

这个计算任务的输入是基于上一个区块的数据以及一个我们猜测的整数。

A common way of doing this is to iterate, incrementing an integer x. In each iteration we hash our block together with x. The computation is successful when the trailing characters of the resulting hash string have 3 zeroes (or more to increase the difficulty).

通常的做法是迭代，递增一个整数`x`。在每次迭代中，通过区块和整数`x`计算哈希。当结果的哈希值的末尾是3个（或者更多）零，计算成功。

Ok, to implement this we’ll begin by adding the nonce property to our genesis block

为了实现这一点，我们首先将nonce属性添加到我们的创世区块中：

```js
genesisBlock = { 
            index: 0
          , timestamp: 1511818270000
          , data: 'our genesis data'
          , previousHash: "-1"
          , nonce: 0
        };
```

We’ll also alter our create hash function to take into account the nonce

修改创建哈希函数，将nonce考虑进来：

```js
function createHash({ timestamp, data, index, previousHash, nonce }) {
        return Crypto.createHash('SHA256').update(timestamp+data+index+previousHash+nonce).digest('hex');
    }
```

Next we will alter our create block method to include a default nonce of 0. We’ll then add a new method proofOfWork, this is going to create a hash of the block. It will then examine to see if the last 3 characters of the blocks hash have 3 trailing zeroes, if not it will increment the nonce within the block and try again until it is successful before finally returning the block.

接下来，我们将改变我们的创建区块的方法，使其包含为0的默认nonce。然后，我们将添加一个新的方法`proofOfWork`，用于产生区块的哈希值。它将检查区块的哈希值的最后三个字符是否为三个0，如果不是，则会增加区块内的nonce，然后再次尝试，直到最终返回正确的区块。

```js
const BrewChain = function() {
...
    function createBlock(data){
        let newBlock = {
            timestamp: new Date().getTime()
          , data: data
          , index: currentBlock.index+1
          , previousHash: currentBlock.hash
          , nonce: 0
        };

        newBlock = proofOfWork(newBlock);
		
        return newBlock;
    }

    function proofOfWork(block){

        while(true){
            block.hash = createHash(block);
            if(block.hash.slice(-3) === "000"){	
                return block;
            }else{
                block.nonce++;
            }
        }
    }
...    
```

We can always know that the work has been done by examining that the contents of the block are valid and that the hash of the contents ends with 3 trailing zeroes.

通过检查区块的内容是否有效以及内容的散列是否以三个0结束，我们总是可以知道已经完成了工作量。

Now we will continue on with our p2p network, checking to see if our recieved chain is valid.

现在我们将继续使用我们的P2P网络，检查我们的接收到的链是否有效。

To do this we will add a method to our chain which takes a new chain array. If the first element is our genesis we then iterate over each block in the chain, checking to see that it’s contents are valid and that the hash indicates proof of work took place.

为了做到这一点，我们将在链中添加一个方法，该方法使用了一个新的链数组。如果第一个元素是创世区块，那么就要遍历链中的每个区块，检查是否有内容是有效的，以及哈希值是否通过了工作量证明。

We’ll also add a method for replacing the chain.

同时也要添加一个替换链的方法。

```js
...
    function checkNewChainIsValid(newChain){
        if(createHash(newChain[0]) !== genesisBlock.hash ){
            return false;
        }

        let previousBlock = newChain[0];
        let blockIndex = 1;

        while(blockIndex < newChain.length){
            let block = newChain[blockIndex];

            if(block.previousHash !== createHash(previousBlock)){
                return false;
            }

            if(block.hash.slice(-3) !== "000"){	
                return false;
            }

            previousBlock = block;
            blockIndex++;
        }

        return true;
    }
...	
    function replaceChain(newChain){
        chain = newChain;
        currentBlock = chain[chain.length-1];
    }
... 
```

We’ll now invoke these methods in the brew node. The consensus rule in our brew node is the longest valid chain is the ‘truth’. We’ll therefore do a check to see if new chain is longer than our own and is valid, and if it is, replace our chain with it

在brew节点中调用这些方法。共识原则是节点中的最长的有效链为真。因此，我们会检查一下，看看新的链条是否比我们自己的链条长并且有效，如果是，用它替换我们的链。

```js
...
    const processedRecievedChain = (blocks) => {
        let newChain = blocks.sort((block1, block2) => (block1.index - block2.index))

        if(newChain.length > chain.getTotalBlocks() && chain.checkNewChainIsValid(newChain)){
            chain.replaceChain(newChain);
            console.log('Chain replaced');
        }
    }
...    
```

The final step is to have a brew node request the chain on startup and on connecting to a new brew node, request the nodes latest block.

最后一步是在启动时让一个新的brew节点请求链，并在连接到一个新的brew节点时，请求最新的区块。

```js
...
    const REQUEST_BLOCK = "REQUEST_BLOCK";
...
    case REQUEST_BLOCK:
        requestLatestBlock(connection);    
...
    const requestLatestBlock = (connection) => {
        connection.send(JSON.stringify({ event: BLOCK, message: chain.getLatestBlock()}))   
    }
...
    const initConnection = (connection) => {
        console.log('init connection');

        messageHandler(connection);
        
        requestLatestBlock(connection);

        brewSockets.push(connection);

        connection.on('error', () => closeConnection(connection));
        connection.on('close', () => closeConnection(connection));
    }
...
```

Our P2P network now has basic functionality, brew nodes will connect, request the latest block and replace the chain if neccesary.

我们的P2P网络就有了基本的功能。brew节点能够连接，请求最新的区块，并在需要时替换链。

> 项目github：https://github.com/dbjsdev/BrewChain

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

咪咪 爬虫工程师，区块链技术爱好者，相信区块链技术能够重构社会的信任基础，欢迎加微信号:miao-mimi-miao

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

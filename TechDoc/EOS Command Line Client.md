EOS Command Line Client (eosc)
===
Tool for sending transactions and querying state from eosd. More...

EOS命令行客户端（eosc）,
用于从eosd发送事务和查询状态的工具。 更多...

Introduction to EOSC -- EOSC简介
---
eosc is a command line tool that interfaces with the REST api exposed by eosd. In order to use eosc you will need to have a local copy of eosd running and configured to load the 'eos::chain_api_plugin'.

eosc是用来与eosd 提供的REST api接口进行交互的命令行工具。为了使用eosc，需要在本地运行的 eosd，并且已配置加载 'eos :: chain_api_plugin' 插件。

```
# Plugin(s) to enable, may be specified multiple times
 plugin = eos::producer_plugin
 plugin = eos::chain_api_plugin
```

After starting eosd you should be able to query the current blockchain state like so:

启动eosd后，就可以查询当前的区块状态，如下所示：

```
./eosc info
{
 "head_block_num": 25048,
 "last_irreversible_block_num": 25027,
 "head_block_id": "000061d8ae49d6af614e02779e19261959f22d6d9f37906ed5db2dabd88be142",
 "head_block_time": "2017-07-25T17:44:48",
 "head_block_producer": "initi",
 "recent_slots": "1110000000000000000000000000000000000000000000000000000000000011",
 "participation_rate": "0.07812500000000000"
}
```

Creating an Account -- 创建账户
---
In order to create an account you will need two new keys: owener and active. You can ask eosc to create some keys for you:

为了创建一个帐户，您需要两个新的密钥：owener和active。您可以使用eosc创建密钥：

```
./eosc create key
public: EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq
private: 5JKbLfCXgcafDQVwHMm3shHt6iRWgrr9adcmt6vX3FNjAEtJGaT
```

Note  注意

eosc does not save the generated private key.

eosc不保存生成的私钥。

Next we will create the account tester, but because all accounts need to be created by an existing account we will ask the inita account to create tester. inita was specified in the genesis file.

接下来，我们将创建该帐户tester，但是由于所有帐户都需要由现有帐户创建，我们将要求inita帐户创建tester。inita用户由创世块配置文件设定。

```
./eosc create account inita tester EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq EOS6KdkmwhPyc2wxN9SAFwo2PU2h74nWs7urN1uRduAwkcns2uXsa
{
  "transaction_id": "6acd2ece68c4b86c1fa209c3989235063384020781f2c67bbb80bc8d540ca120",
  "processed": {
    "refBlockNum": "25217",
    "refBlockPrefix": "2095475630",
    "expiration": "2017-07-25T17:54:55",
    "scope": [
      "eos",
      "inita"
    ],
    "signatures": [],
    "messages": [{
        "code": "eos",
        "type": "newaccount",
        "authorization": [{
            "account": "inita",
            "permission": "active"
          }
        ],
        "data": "c9251a0000000000b44c5a2400000000010000000102bcca6347d828d4e1868b7dfa91692a16d5b20d0ee3d16a7ca2ddcc7f6dd03344010000010000000102bcca6347d828d4e1868b7dfa91692a16d5b20d0ee3d16a7ca2ddcc7f6dd03344010000010000000001c9251a000000000061d0640b000000000100010000000000000008454f5300000000"
      }
    ],
    "output": [{
        "notify": [],
        "sync_transactions": [],
        "async_transactions": []
      }
    ]
  }
}

```

After creating the account we can view the current account status like so:

创建帐户后，我们可以查看当前帐户状态：

```
./eosc account tester
{
  "name": "tester",
  "eos_balance": 0,
  "staked_balance": 1,
  "unstaking_balance": 0,
  "last_unstaking_time": "1969-12-31T23:59:59"
}
```

You will note that there is no balance because almost all genesis EOS tokens are currently allocated to the eos account.

你可能会注意到，帐户余额为0，因为几乎所有的EOS代币目前都被分配到eos帐户中。

```
./eosc account eos
{
  "name": "eos",
  "eos_balance": "8999999999998100",
  "staked_balance": 0,
  "unstaking_balance": 0,
  "last_unstaking_time": "1969-12-31T23:59:59",
  "abi": {
    "types": [{
        "newTypeName": "AccountName",
        "type": "Name"
      }
    ],
    "structs": [{
        "name": "transfer",
        "base": "",
        "fields": {
          "from": "AccountName",
          "to": "AccountName",
          "amount": "UInt64"
        }
      }
    ],
    "actions": [{
        "action": "transfer",
        "type": "transfer"
      }
    ],
    "tables": []
  }
}
```

Note  注意

The eos account happens to have an ABI (Application Binary Interface) defined which provides meta-data to tools that want to interface with the eos contract.
We can fund our tester account via eosc with the following command:

该eos帐户刚好配有一个ABI（应用程序二进制接口），它提供元数据给eos智能合约交互工具。
使用 eosc 命令可以给 tester 帐户充值：

```
./eosc transfer eos tester 1000
{
  "transaction_id": "52b488d27ce1f72a2b29f22e5e1638fa5db5d7805565884e795733a15c6c2195",
  "processed": {
    "refBlockNum": "25298",
    "refBlockPrefix": "1151709320",
    "expiration": "2017-07-25T17:58:58",
    "scope": [
      "eos",
      "tester"
    ],
    "signatures": [],
    "messages": [{
        "code": "eos",
        "type": "transfer",
        "authorization": [{
            "account": "eos",
            "permission": "active"
          }
        ],
        "data": {
          "from": "eos",
          "to": "tester",
          "amount": 1000
        },
        "hex_data": "e54d000000000000b44c5a2400000000e803000000000000"
      }
    ],
    "output": [{
        "notify": [{
            "name": "tester",
            "output": {
              "notify": [],
              "sync_transactions": [],
              "async_transactions": []
            }
          }
        ],
        "sync_transactions": [],
        "async_transactions": []
      }
    ]
  }
}
```

Now we can verify that the funds were received.

现在我们可以验证收到的资金。

```
./eosc account tester
{
  "name": "tester",
  "eos_balance": 1000,
  "staked_balance": 1,
  "unstaking_balance": 0,
  "last_unstaking_time": "1969-12-31T23:59:59"
}

```

Creating a Contract -- 创建合约
---

In this section we will use eosc to create and publish a currency contract. You can find the example currency contract in the eos/contracts/currency directory.
The first step is to create an account for currency. We will have the tester account create the currency account.

在本节中，我们将用于eosc创建和发布智能合约。示例在eos/contracts/currency目录中。
第一步是创建合约账号。我们将使用tester帐户创建currency帐户。

```
./eosc create account tester currency EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq EOS6KdkmwhPyc2wxN9SAFwo2PU2h74nWs7urN1uRduAwkcns2uXsa
```

The next step is to publish the contract (.wast) and its abi (.abi)

下一步是发布合约（.wast）及其abi（.abi）

```
./eosc setcode currency ../../contracts/currency/currency.wast ../../contracts/currency/currency.abi
{
  "transaction_id": "738669518a8fc6935394992beec1dc4dc1b60f7d9f232b6ccd6a282619eedca9",
  "processed": {
    "refBlockNum": "25386",
    "refBlockPrefix": "154808726",
    "expiration": "2017-07-25T18:03:22",
    "scope": [
      "eos",
      "currency"
    ],
    "signatures": [],
    "messages": [{
        "code": "eos",
        "type": "setcode",
        "authorization": [{
            "account": "currency",
            "permission": "active"
          }
        ],
        "data": "a34a59dcc80000000000f7090061736d0100000001390a60037e7e7e017f60047e7e7f7f017f60017e0060057e7e7e7f7f017f60027f7f0060027f7f017f60027e7f0060017f0060000060027e7e0002760703656e7606617373657274000403656e76086c6f61645f693634000303656e760b726561644d657373616765000503656e760a72656d6f76655f693634000003656e760b7265717569726541757468000203656e760d726571756972654e6f74696365000203656e760973746f72655f6936340001030504060708090404017000000503010001077e05066d656d6f727902002a5f5a4e3863757272656e6379313273746f72654163636f756e744579524b4e535f374163636f756e74450007355f5a4e3863757272656e637932336170706c795f63757272656e63795f7472616e7366657245524b4e535f385472616e7366657245000804696e69740009056170706c79000a0aaa04043100024020012903084200510d00200042e198deead1002001411010061a0f0b200042e198deead100200129030010031a0bd30202017e017f4100410028020441206b220236020420002903002101200029030810052001100520002903001004200242e198deead10037031020024200370318200029030042a395e5e28d1942e198deead100200241106a411010011a200242e198deead10037030020024200370308200029030842a395e5e28d1942e198deead1002002411010011a200229031820002903105a4110100020022002290318200029031022017d370318200120022903087c20015a41c00010002002200229030820002903107c370308200029030021010240024020022903184200510d00200142e198deead100200241106a411010061a0c010b200142e198deead100200229031010031a0b200041086a290300210102400240200241086a2903004200510d00200142e198deead1002002411010061a0c010b200142e198deead100200229030010031a0b4100200241206a3602040b4901017f4100410028020441106b22003602042000428094ebdc03370308200042e198deead10037030042a395e5e28d1942e198deead1002000411010061a4100200041106a3602040b5701017f4100410028020441206b22023602040240200042a395e5e28d19520d00200142d48cdce99412520d0020024200370318200241086a4118100241174b41f0001000200241086a10080b4100200241206a3602040b0b8b01040041040b04900400000041100b2c696e746567657220756e646572666c6f77207375627472616374696e6720746f6b656e2062616c616e6365000041c0000b26696e7465676572206f766572666c6f7720616464696e6720746f6b656e2062616c616e6365000041f0000b1e6d6573736167652073686f72746572207468616e2065787065637465640000ec01046e616d650b06617373657274020000086c6f61645f6936340500000000000b726561644d6573736167650200000a72656d6f76655f693634030000000b726571756972654175746801000d726571756972654e6f7469636501000973746f72655f69363404000000002a5f5a4e3863757272656e6379313273746f72654163636f756e744579524b4e535f374163636f756e74450201300131355f5a4e3863757272656e637932336170706c795f63757272656e63795f7472616e7366657245524b4e535f385472616e73666572450301300131013204696e6974010130056170706c7903013001310132010b4163636f756e744e616d65044e616d6502087472616e7366657200030466726f6d0b4163636f756e744e616d6502746f0b4163636f756e744e616d6506616d6f756e740655496e743634076163636f756e740002036b65790655496e7436340762616c616e63650655496e743634015406374d91000000087472616e7366657201618c571d05000000076163636f756e74"
      }
    ],
    "output": [{
        "notify": [],
        "sync_transactions": [],
        "async_transactions": []
      }
    ]
  }
}
```

After the contract is published it initially allocates all of the currency to the currency account. So lets transfer some of it to our tester.

合约发布后，它首先将所有代币分配到currency帐户。所以我们先转移一些代币到tester帐户上。

```
./eosc exec currency transfer '{"from":"currency","to":"tester","amount":50}' '["currency","tester"]' '[{"account":"currency","permission":"active"}]'
{
  "transaction_id": "f601f2fdb26e366a19913229e4d2928778b50166811c63c7962401b11d23ef3d",
  "processed": {
    "refBlockNum": "25427",
    "refBlockPrefix": "2231248056",
    "expiration": "2017-07-25T18:05:25",
    "scope": [
      "tester",
      "currency"
    ],
    "signatures": [],
    "messages": [{
        "code": "currency",
        "type": "transfer",
        "authorization": [{
            "account": "currency",
            "permission": "active"
          }
        ],
        "data": {
          "from": "currency",
          "to": "tester",
          "amount": 50
        },
        "hex_data": "a34a59dcc8000000b44c5a24000000003200000000000000"
      }
    ],
    "output": [{
        "notify": [{
            "name": "tester",
            "output": {
              "notify": [],
              "sync_transactions": [],
              "async_transactions": []
            }
          }
        ],
        "sync_transactions": [],
        "async_transactions": []
      }
    ]
  }
}
```

The exec command takes the following arguments:
```
•	code - the account whose contract code should be run
•	action - the type of the message to pass to code
•	data - a JSON blob (or hex string) of the message data as defined by the ABI for the action type.
•	scope - a JSON array of account names which contain data that may be read or modified by code (in this case the sender and receiver)
•	authorization - the account and permission level which authorized the action
```

该exec命令采用以下参数：
```
•	code - 执行代码所属的合约帐户名
•	action - 传递给帐户的消息类型
•	data - 由ABI为消息类型定义的消息数据，使用JSON blob（或十六进制字符串）格式。
•	scope - 一个帐户名称的JSON数组，这个数组是包含一些可以被code(合约账户)读取或修改的数据（在本例中为发送账户和接收账户）
•	authorization - 授权操作的帐户和权限级别
```

Note  注意

at this time the blockchain is not validating signatures so anyone can do anything provided they simply declare the proper authority. In the future this will direct the wallet on which keys to use to sign it. Also future revisions of this API may automatically detect scope and authorization via a trial run of the contract.

目前，区块链没有验证签名，所以所有帐户都可以做任何事情，只要他们声明有相应的权限。以后，将直接使用钱包中的私钥签名。此API的未来版本也可能会通过合约的试运行来自动检测授权和范围。

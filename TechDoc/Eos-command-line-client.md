# EOS Command Line Client (eosc) EOS 命令行客户端（`eosc`）

> 本文翻译自：https://eosio.github.io/eos/group__eosc.html
> 
> 译者：[区块链中文字幕组 胡亮](https://github.com/gumoon)
> 
> 翻译时间：2017-10-15

Tool for sending transactions and querying state from `eosd`. 

向 `eosd` 节点发送交易和从 `eosd` 节点查询状态的工具。

## Table of Contents 目录

* Introduction to EOSC EOSC 简介
* Creating a Wallet 创建钱包
* Importing Key to Wallet 向钱包导入密钥
* Locking and Unlocking Wallet 加锁和解锁钱包
* Opening Wallet 打开钱包
* Creating an Account 创建账号
* Transfer EOS 转移 EOS
* Getting Transaction 获取交易记录
* Creating a Contract 创建合约
* Pushing Message to Contract 向合约发送消息
* Querying Contract 查询合约
* Connecting to Particular Node 连接到特定的节点
* Using Separate Wallet App 使用单独的钱包应用程序
* Skipping Signature 跳过签名
* Additional Documentation 补充文档

## Introduction to EOS Wallet Process EOS 钱包进程简介

`eosc` is a command line tool that interfaces with the REST api exposed by `eosd`. In order to use `eosc` you will need to have a local copy of `eosd` running and configured to load the `'eos::chain_api_plugin'`.

`eosc` 是一个命令行工具，用于跟 `eosd` 节点暴露的 REST 接口进行交互。使用 `eosc` 之前，你需要在本地运行配置了加载 `'eos::chain_api_plugin'` 插件的 `eosd` 服务。

In order to sign transaction and push it to the blockchain, you will need to have the `'eos::wallet_api_plugin'` loaded.

为了签名交易和推送交易到区块链，你需要配置 `eosd` 服务加载 `'eos::wallet_api_plugin'` 插件。

And in order to query account history and transaction, you will need to have the 'eos::account_history_api_plugin' loaded.

为了查询账户历史和账号交易记录，你需要配置 `eosd` 服务加载 `'eos::account_history_api_plugin'` 插件。

```
 # Plugin(s) to enable, may be specified multiple times
 plugin = eos::producer_plugin
 plugin = eos::chain_api_plugin
 plugin = eos::wallet_api_plugin
 plugin = eos::account_history_api_plugin
```
 
After starting `eosd` you should be able to query the current blockchain state like so:

启动了 `eosd` 服务之后，你应该能像这样查询区块链状态：

```
$ ./eosc get info
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

## Creating a Wallet 创建钱包

Any transaction sent to the blockchain will need to be signed by the respective authority's private key. Before you will be able to sign the transaction, you will need a wallet to store and manage the private key.

任何发往区块链的交易都需要被各自的授权人使用私钥签名。在你签名交易之前，你需要一个钱包来存储和管理私钥。

```
$ ./eosc wallet create
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5JD9cw9YY288AXPvnbwUk5JK4Cy6YyZ83wzHcshu8F2akU9rRWE"
```

This will create a wallet called 'default' inside `eos-walletd` and return a password that you can use to unlock your wallet in the future.

这个命令在 `eos-walletd` 服务内创建一个名为 'default' 的钱包并且返回一个密码。未来，你将使用该密码解锁你的钱包。

You can create multiple wallets by specifying unique name.

你可以通过指定唯一的钱包名来创建多个钱包。

```
$ ./eosc wallet create -n second-wallet
Creating wallet: second-wallet
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5Ji6JUrLjhKAVn68nmacLxwhvtqUAV18J7iycZppsPKeoGGgBEw"
```

And you will be see it in the list of your wallets

然后，你将在你的钱包列表中看到它。

```
$ ./eosc wallet list
Wallets:
[
  "default *",
  "second-wallet *"
]
```

>Note 注意
>For any wallet operation, if you don't specify the name of the wallet, it will always resort to default wallet
>对于任意的钱包操作，如果你未指定钱包名，默认操作 default 钱包。

## Importing Key to Wallet 向钱包导入私钥

Import the key that you want to use to sign the transaction to your wallet. The following will import key for genesis accounts (i.e. inita, initb, initc, ..., initu)

导入你想用于加密交易的私钥到你的钱包。下面的命令为创始账号（像：inita, initb, initc, 。。。, initu）导入私钥。

```
$ ./eosc wallet import 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
imported private key for: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```

You will then be able to see the list of imported private keys and their respective public key。

然后，你能看到导入的私钥和它们对应的公钥列表：

```
$ ./eosc wallet keys
[[
    "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
    "5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"
  ]
]
```

## Locking and Unlocking Wallet 加锁和解锁钱包

To keep your private key safe, lock your wallet

为了私钥的安全，对钱包加锁。

```
$ ./eosc wallet lock -n second-wallet
Locked: 'second-wallet'
```

Notice that the locked wallet doesn't have * symbol in the list

注意，被加锁的钱包在查看钱包列表时不显示符号 * ：

```
$ ./eosc wallet list
Wallets:
[
  "default *",
  "second-wallet"
]
```

To unlock it specify the password you get when creating the wallet

解锁钱包需要指定创建钱包时生成的密码：

```
$ ./eosc wallet unlock -n second-wallet --password PW5Ji6JUrLjhKAVn68nmacLxwhvtqUAV18J7iycZppsPKeoGGgBEw
Unlocked: 'second-wallet'
```

## Opening Wallet 打开钱包

All of the wallets data are store inside `data_dir` folder. When you restart your wallet app (in this case `eosd`), you will need to open the wallet so `eosc` can have access to it.

所有钱包数据都存储在 `data_dir` 文件夹内。当你重启钱包程序（现在指：`eosd`），你需要打开钱包来让 `eosc` 能够访问它。

```
$ ./eosc wallet list
Wallets: []
$ ./eosc wallet open
Wallets: [
  "default"
]
$ ./eosc wallet open -n second-wallet
Wallets: [
  "default",
  "second-wallet"
]
```

>Note 注意
>The wallet is locked by default
>钱包默认锁定。

## Creating an Account 创建账号

In order to create an account you will need two new keys: owner and active. You can ask `eosc` to create some keys for you:

创建账号需要两个新的私钥：owner 和 active。你可以让 `eosc` 创建它们。

This will be your owner key,

这是你的 owner 私钥,

```
$ ./eosc create key
public: EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq
private: 5JKbLfCXgcafDQVwHMm3shHt6iRWgrr9adcmt6vX3FNjAEtJGaT
```

And this will be your active key,

这是你的 active 私钥,

```
$ ./eosc create key
public: EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA
private: 5Hv22aPcjnENBv6X9o9nKGdkfrW44En6z4zJUt2PobAvbQXrT9z
```

>Note 注意
>`eosc` does not save the generated private key.
>`eosc` 不保存生成的私钥。


Next we will create the account tester, but because all accounts need to be created by an existing account we will ask the inita account to create tester using the owner and active keys created above. inita was specified in the genesis file.

接下来，我们将创建 tester 账号，但是由于所有的账号都需要由已经存在的账号创建，我们让 inita 使用上面创建的 owner 和 active 私钥来创建账号 tester。inita 存在 genesis 文件中。

In order to push transaction as inita, you first need to import inita's private key to your wallet

为了使用 inita 来发送交易，你需要首先导入 inita 的私钥到你的钱包。*（上面已经讲过怎么往钱包导入私钥）*

Then create an account called tester

然后创建 tester 账号。

```
$ ./eosc create account inita tester EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA
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

You can see that tester is now the controlled_account under inita

你能看到 tester 现在的控制账号是 inita：

```
$ ./eosc get servants inita
{
  "controlled_accounts": [
    "tester"
  ]
}
```

## Transfer EOS 转移 EOS

After creating the account we can view the current account status like so:

创建完账号后，我们可以像这样查看当前账号状态：

```
$ ./eosc get account tester
{
  "name": "tester",
  "eos_balance": 0,
  "staked_balance": 1,
  "unstaking_balance": 0,
  "last_unstaking_time": "1969-12-31T23:59:59",
  "permissions": [{
      "name": "active",
      "parent": "owner",
      "required_auth": {
        "threshold": 1,
        "keys": [{
            "key": "EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA",
            "weight": 1
          }
        ],
        "accounts": []
      }
    },{
      "name": "owner",
      "parent": "owner",
      "required_auth": {
        "threshold": 1,
        "keys": [{
            "key": "EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq",
            "weight": 1
          }
        ],
        "accounts": []
      }
    }
  ]
}
```

You will note that there is no balance because almost all genesis EOS tokens are currently allocated to the eos account and genesis accounts.

你将注意到新创建的账号没有余额。因为几乎所有的初始 EOS 代币当前都被分配给了 eos 账号和创始账号。

```
{
  "name": "eos",
  "eos_balance": "69000000.0000 EOS",
  "staked_balance": "0.0000 EOS",
  "unstaking_balance": "0.0000 EOS",
  "last_unstaking_time": "1969-12-31T23:59:59",
  "permissions": []
}
```

Since we have the private key of the genesis accounts (i.e. inita, initb, initc, etc) in the wallet. We can fund our tester account via eosc through any of the genesis account with the following command:

因为我们钱包里有创始账号的私钥。所以我们能够通过 `eosc` ，使用以下命令，从创始账号给 tester 账号转账。

```
$ ./eosc transfer inita tester 1000
{
  "transaction_id": "eb4b94b72718a369af09eb2e7885b3f494dd1d8a20278a6634611d5edd76b703",
  "processed": {
    "refBlockNum": 2206,
    "refBlockPrefix": 221394282,
    "expiration": "2017-09-05T08:03:58",
    "scope": [
      "inita",
      "tester"
    ],
    "signatures": [
      "1f22e64240e1e479eee6ccbbd79a29f1a6eb6020384b4cca1a958e7c708d3e562009ae6e60afac96f9a3b89d729a50cd5a7b5a7a647540ba1678831bf970e83312"
    ],
    "messages": [{
        "code": "eos",
        "type": "transfer",
        "authorization": [{
            "account": "inita",
            "permission": "active"
          }
        ],
        "data": {
          "from": "inita",
          "to": "tester",
          "amount": 1000,
          "memo": ""
        },
        "hex_data": "000000008040934b00000000c84267a1e80300000000000000"
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
          },{
            "name": "inita",
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

现在，我们验证接收到的资金。

```
$ ./eosc get account tester
{
  "name": "tester",
  "eos_balance": "0.1000 EOS",
  "staked_balance": "0.0001 EOS",
  "unstaking_balance": "0.0000 EOS",
  "last_unstaking_time": "1969-12-31T23:59:59",
  "permissions": [{
      "name": "active",
      "parent": "owner",
      "required_auth": {
        "threshold": 1,
        "keys": [{
            "key": "EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA",
            "weight": 1
          }
        ],
        "accounts": []
      }
    },{
      "name": "owner",
      "parent": "owner",
      "required_auth": {
        "threshold": 1,
        "keys": [{
            "key": "EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq",
            "weight": 1
          }
        ],
        "accounts": []
      }
    }
  ]
}
```

## Getting Transaction 获取交易记录

With `account_history_api_plugin` loaded in `eosd`, we can query for particular transaction

`eosd` 服务加载了 `account_history_api_plugin` 插件，则我们能查询特定的交易。

```
$ ./eosc get transaction eb4b94b72718a369af09eb2e7885b3f494dd1d8a20278a6634611d5edd76b703
{
  "transaction_id": "eb4b94b72718a369af09eb2e7885b3f494dd1d8a20278a6634611d5edd76b703",
  "processed": {
    "refBlockNum": 2206,
    "refBlockPrefix": 221394282,
    "expiration": "2017-09-05T08:03:58",
    "scope": [
      "inita",
      "tester"
    ],
    "signatures": [
      "1f22e64240e1e479eee6ccbbd79a29f1a6eb6020384b4cca1a958e7c708d3e562009ae6e60afac96f9a3b89d729a50cd5a7b5a7a647540ba1678831bf970e83312"
    ],
    "messages": [{
        "code": "eos",
        "type": "transfer",
        "authorization": [{
            "account": "inita",
            "permission": "active"
          }
        ],
        "data": {
          "from": "inita",
          "to": "tester",
          "amount": 1000,
          "memo": ""
        },
        "hex_data": "000000008040934b00000000c84267a1e80300000000000000"
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
          },{
            "name": "inita",
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

Also we can query list of transactions performed by certain account starting from recent one

我们也能查询指定账号最近的交易列表。

```
$ ./eosc get transactions inita
[
  {
    "transaction_id": "eb4b94b72718a369af09eb2e7885b3f494dd1d8a20278a6634611d5edd76b703",
    ...
  },
  {
    "transaction_id": "6acd2ece68c4b86c1fa209c3989235063384020781f2c67bbb80bc8d540ca120",
    ...
  },
  ...
]
```

## Creating a Contract 创建合约

In this section we will use `eosc` to create and publish a currency contract. You can find the example currency contract in the `eos/contracts/currency` directory.

这部分我们使用 `eosc` 来创建和发布一个货币合约。你能在 `eos/contracts/currency` 目录找到这个货币合约示例。

The first step is to create an account for currency. We will have the inita account create the currency account. Ensure you have inita private key imported.

第一步是为这个合约创建一个账号。我们将使用 inita 账号来创建这个 currency 账号。确保你已经导入了 inita 账号的私钥到钱包。

```
$ ./eosc create account inita currency EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA
```

The next step is to publish the contract (.wast) and its abi (.abi).

接着，发布合约（.wast) 和 它的 abi (.abi)。

We will need currency active key in our wallet for this

我们需要导入 currency 账号的 active 私钥。

```
$ ./eosc import 5Hv22aPcjnENBv6X9o9nKGdkfrW44En6z4zJUt2PobAvbQXrT9z
imported private key for: EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA
```

Then proceed with setting the code

然后，执行设置code（合约）。

```
$ ./eosc set contract currency ../../../contracts/currency/currency.wast ../../../contracts/currency/currency.abi
Reading WAST...
Assembling WASM...
Publishing contract...
{
  "transaction_id": "9990306e13f630a9c5436a5a0b6fb8fe2c7f3da2f342b4898a39c4a2c17dcdb3",
  "processed": {
    "refBlockNum": 1208,
    "refBlockPrefix": 3058534156,
    "expiration": "2017-08-24T18:29:52",
    "scope": [
      "currency",
      "eos"
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
        "data": "00000079b822651d0000e8150061736d0100000001390a60017e0060037e7e7f017f60047e7e7f7f017f60017f0060057e7e7e7f7f017f60027f7f0060027f7f017f60027e7f0060000060027e7e00029d010a03656e7606617373657274000503656e76086c6f61645f693634000403656e76067072696e7469000003656e76067072696e746e000003656e76067072696e7473000303656e760b726561644d657373616765000603656e760a72656d6f76655f693634000103656e760b7265717569726541757468000003656e760d726571756972654e6f74696365000003656e760973746f72655f6936340002030706000007030809040401700000050301000107cc0107066d656d6f72790200205f5a4e33656f733133726571756972654e6f74696365454e535f344e616d6545000a1e5f5a4e33656f7331317265717569726541757468454e535f344e616d6545000b345f5a4e3863757272656e6379313273746f72654163636f756e74454e33656f73344e616d6545524b4e535f374163636f756e7445000c355f5a4e3863757272656e637932336170706c795f63757272656e63795f7472616e7366657245524b4e535f385472616e7366657245000d04696e6974000e056170706c79000f0a9d0d060600200010080b0600200010070b3400024020012903084200510d0020004280808080a8d7bee3082001411010091a0f0b20004280808080a8d7bee308200110061a0b8a0604017e027f047e017f4100410028020441206b2208360204200029030821052000290300210720002903102104411010042004100241c000100442808080c887d7c8b21d100341d00010042007100341e000100420051003200029030021052000290308100820051008200029030010072000290300210142002105423b210441f00021034200210603400240024002400240024020054206560d0020032c00002202419f7f6a41ff017141194b0d01200241a0016a21020c020b420021072005420b580d020c030b200241ea016a41002002414f6a41ff01714105491b21020b2002ad42388642388721070b2007421f83200442ffffffff0f838621070b200341016a2103200542017c2105200720068421062004427b7c2204427a520d000b420021052008420037031820082006370310200142808080c887d7c8b21d4280808080a8d7bee308200841106a411010011a200041086a2903002101423b210441f00021034200210603400240024002400240024020054206560d0020032c00002202419f7f6a41ff017141194b0d01200241a0016a21020c020b420021072005420b580d020c030b200241ea016a41002002414f6a41ff01714105491b21020b2002ad42388642388721070b2007421f83200442ffffffff0f838621070b200341016a2103200542017c2105200720068421062004427b7c2204427a520d000b2008200637030020084200370308200142808080c887d7c8b21d4280808080a8d7bee3082008411010011a200841186a2203290300200041106a22022903005a418001100020032003290300200229030022057d370300200520082903087c20055a41b00110002008200829030820022903007c370308200029030021050240024020032903004200510d0020054280808080a8d7bee308200841106a411010091a0c010b20054280808080a8d7bee308200841106a10061a0b200041086a290300210502400240200841086a2903004200510d0020054280808080a8d7bee3082008411010091a0c010b20054280808080a8d7bee308200810061a0b4100200841206a3602040b980303027f057e017f4100410028020441106b220736020442002103423b210241e00121014200210403400240024002400240024020034207560d0020012c00002200419f7f6a41ff017141194b0d01200041a0016a21000c020b420021052003420b580d020c030b200041ea016a41002000414f6a41ff01714105491b21000b2000ad42388642388721050b2005421f83200242ffffffff0f838621050b200141016a2101200342017c2103200520048421042002427b7c2202427a520d000b42002103423b210241f00021014200210603400240024002400240024020034206560d0020012c00002200419f7f6a41ff017141194b0d01200041a0016a21000c020b420021052003420b580d020c030b200041ea016a41002000414f6a41ff01714105491b21000b2000ad42388642388721050b2005421f83200242ffffffff0f838621050b200141016a2101200342017c2103200520068421062002427b7c2202427a520d000b2007428094ebdc033703082007200637030020044280808080a8d7bee3082007411010091a4100200741106a3602040bb10303027f047e017f4100410028020441206b220836020442002105423b210441e00121034200210603400240024002400240024020054207560d0020032c00002202419f7f6a41ff017141194b0d01200241a0016a21020c020b420021072005420b580d020c030b200241ea016a41002002414f6a41ff01714105491b21020b2002ad42388642388721070b2007421f83200442ffffffff0f838621070b200341016a2103200542017c2105200720068421062004427b7c2204427a520d000b024020062000520d0042002105423b210441f00121034200210603400240024002400240024020054207560d0020032c00002202419f7f6a41ff017141194b0d01200241a0016a21020c020b420021072005420b580d020c030b200241ea016a41002002414f6a41ff01714105491b21020b2002ad42388642388721070b2007421f83200442ffffffff0f838621070b200341016a2103200542017c2105200720068421062004427b7c2204427a520d000b20062001520d00200842003703102008420037030820084200370318200841086a4118100541174b4180021000200841086a100d0b4100200841206a3602040b0bff010b0041040b04200500000041100b2254686973206170706561727320746f2062652061207472616e73666572206f6620000041c0000b0220000041d0000b072066726f6d20000041e0000b0520746f20000041f0000b086163636f756e7400004180010b2c696e746567657220756e646572666c6f77207375627472616374696e6720746f6b656e2062616c616e6365000041b0010b26696e7465676572206f766572666c6f7720616464696e6720746f6b656e2062616c616e6365000041e0010b0963757272656e6379000041f0010b097472616e7366657200004180020b1e6d6573736167652073686f72746572207468616e2065787065637465640000fd02046e616d651006617373657274020000086c6f61645f693634050000000000067072696e74690100067072696e746e0100067072696e747301000b726561644d6573736167650200000a72656d6f76655f693634030000000b726571756972654175746801000d726571756972654e6f7469636501000973746f72655f6936340400000000205f5a4e33656f733133726571756972654e6f74696365454e535f344e616d65450101301e5f5a4e33656f7331317265717569726541757468454e535f344e616d6545010130345f5a4e3863757272656e6379313273746f72654163636f756e74454e33656f73344e616d6545524b4e535f374163636f756e74450201300131355f5a4e3863757272656e637932336170706c795f63757272656e63795f7472616e7366657245524b4e535f385472616e73666572450901300131013201330134013501360137013804696e69740801300131013201330134013501360137056170706c7909013001310132013301340135013601370138010b4163636f756e744e616d65044e616d6502087472616e7366657200030466726f6d0b4163636f756e744e616d6502746f0b4163636f756e744e616d65087175616e746974790655496e743634076163636f756e740002036b65790655496e7436340762616c616e63650655496e74363401000000b298e982a4087472616e736665720100000080bafac608076163636f756e74"
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

## Pushing Message to Contract 向合约发送消息

After the contract is published it initially allocates all of the currency to the currency account. So lets transfer some of it to our tester.

合约发布后，初始分配所有的代币给 currency 账号。那么，让我们转账一些给 tester 账号。

We can query the blockchain for the .abi of the contract, on which we can check the list of available actions and their respective message structure

我们可以在区块链上查询合约的 ABI。在合约的 ABI 里，我们可以看到所有可用的 actions 和 它们各自的消息数据结构。

```
$ ./eosc get code --a currency.abi currency
code hash: 9b9db1a7940503a88535517049e64467a6e8f4e9e03af15e9968ec89dd794975
saving abi to currency.abi
$ cat currency.abi
{
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
    },{
      "name": "account",
      "base": "",
      "fields": {
        "account": "Name",
        "balance": "UInt64"
      }
    }
  ],
  "actions": [{
      "action": "transfer",
      "type": "transfer"
    }
  ],
  "tables": [{
      "table": "account",
      "indextype": "i64",
      "keynames": [
        "account"
      ],
      "keytype": [],
      "type": "account"
    }
  ]
}
```

From the above abi, we can see that currency contract accepts an action called transfer that accepts message with fields from, to, and amount.

从以上的 ABI，我们能看到该货币合约接收一个叫 transfer 的 action，它接收带有 from, to, amount 参数的消息。

```
$ ./eosc push message currency transfer '{"from":"currency","to":"tester","amount":50}' -S currency -S tester -p currency@active
1589302ms thread-0   main.cpp:271                  operator()           ] Converting argument to binary...
1589304ms thread-0   main.cpp:290                  operator()           ] Transaction result:
{
  "transaction_id": "1c4911c0b277566dce4217edbbca0f688f7bdef761ed445ff31b31f286720057",
  "processed": {
    "refBlockNum": 1173,
    "refBlockPrefix": 2184027244,
    "expiration": "2017-08-24T18:28:07",
    "scope": [
      "currency",
      "tester"
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
          "quantity": 50
        },
        "hex_data": "00000079b822651d00000000c84267a13200000000000000"
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

Now we can transfer it from tester to inita and require the permission of tester. This should drain the balance of tester to 0.

现在，我们从 tester 转账给 inita 。它要求 tester 的权限, 消耗 tester 的余额为 0 。

```
$ ./eosc push message currency transfer '{"from":"tester","to":"inita","amount":50}' -S inita -S tester -p tester@active
3116153ms thread-0   main.cpp:271                  operator()           ] Converting argument to binary...
3116154ms thread-0   main.cpp:290                  operator()           ] Transaction result:
{
  "transaction_id": "56b9f0f3b9f43254af446c5dca02a6fcb24ebcdb506d7248947fd4d52a27972a",
  "processed": {
    "refBlockNum": 2882,
    "refBlockPrefix": 1880685856,
    "expiration": "2017-08-24T19:53:34",
    "scope": [
      "inita",
      "tester"
    ],
    "signatures": [],
    "messages": [{
        "code": "currency",
        "type": "transfer",
        "authorization": [{
            "account": "tester",
            "permission": "active"
          }
        ],
        "data": {
          "from": "tester",
          "to": "inita",
          "quantity": 50
        },
        "hex_data": "00000000c84267a1000000008040934b3200000000000000"
      }
    ],
    "output": [{
        "notify": [{
            "name": "inita",
            "output": {
              "notify": [],
              "sync_transactions": [],
              "async_transactions": []
            }
          },{
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

Now that tester has a balance of 0, if we attempt this transfer a second time it should fail:

现在，tester 账号余额为 0 了。如果我们再次尝试该转账操作，它应该失败。

```
$ ./eosc push message currency transfer '{"from":"tester","to":"inita","amount":50}' -S inita -S tester -p tester@active
3543610ms thread-0   main.cpp:271                  operator()           ] Converting argument to binary...
3543615ms thread-0   main.cpp:311                  main                 ] Failed with error: 10 assert_exception: Assert Exception
status_code == 200: Error
: 10 assert_exception: Assert Exception
test: assertion failed: integer underflow subtracting token balance
    {"s":"integer underflow subtracting token balance","ptr":176}
    thread-1  wasm_interface.cpp:248 assertnonei32i32
[...snipped...]
```

## Querying Contract 查询合约

After doing the transfer action on currency contract, we can verify the amount of token held by each account by looking at currency's account table.

执行完货币合约的转账行为后，我们可以通过查询 currency 账号的账号表，来验证每个账号的代币持有情况。

This table is stored on the scope of each account instead of on currency scope.

这个表存储在每个账号下，而不是 currency 账号下。

```
$./eosc get table tester currency account
{
  "rows": [],
  "more": false
}
$./eosc get table inita currency account
{
  "rows": [{
      "account": "account",
      "balance": 50
    }
  ],
  "more": true
}
```

## Connecting to Particular Node 连接特定的节点

By default, eosc will connect to eosd running on localhost port 8888. You can connect to another eosd node by specifying its host and port.

默认，`eosc` 将连接本地端口为 8888 的 `eosd` 节点。你可以通过指定主机和端口，连接到其他的 `eosd` 节点。

```
./eosc -H localhost -p 8889
```

## Using Separate Wallet App 使用单独的钱包应用程序

Instead of using the wallet functionality built-in to eosd, you can also use a separate wallet app which can be found inside programs/eos-walletd. By default, port 8888 is used by eosd, so choose another port for the wallet app.

除了使用 `eosd` 内嵌的钱包功能，你也能使用一个单独的钱包应用程序 `programs/eos-walletd` 。 默认，`eosd` 服务使用 8888 端口，故，为钱包应用程序选择另外的端口。

```
./eos-walletd --http-server-endpoint 127.0.0.1:8887
```

Then for any operation that requires signing, use the –wallet-host and –wallet-port option

然后，任何需要使用签名的操作，使用 `--wallet-host` 和 `--wallet-port` 选项。

```
./eosc --wallet-host 127.0.0.1 --wallet-port 8887 <COMMAND> <SUBCOMMAND> <PARAMS>
```

## Skipping Signatures 跳过签名

As an easy way for developers to test functionality without dealing with keys, eosd can be run so that Transaction signatures are not required.

为了方便开发者测试功能，`eosd` 可以以不需要签名的方式运行。

```
./eosd --skip-transaction-signatures
```

And then for any operation that requires signing, use the -s option

然后，需要签名的操作，带上 `-s` 选项即可跳过签名验证。

```
./eosc <COMMAND> <SUBCOMMAND> -s <PARAMS>
```

## Additional Documentation 补充文档

`eosc` contains documentation for all of its commands. For a list of all commands known to `eosc`, simply run it with no arguments:

`eosc` 程序包含所有它的命令的文档。不带参数运行 `eosc`, 会显示所有支持的命令帮助。

```
$ ./eosc
ERROR: RequiredError: Subcommand required
Command Line Interface to Eos Daemon
Usage: ./eosc [OPTIONS] SUBCOMMAND
Options:
  -h,--help                   Print this help message and exit
  -H,--host TEXT=localhost    the host where eosd is running
  -p,--port UINT=8888         the port where eosd is running
  --wallet-host TEXT=localhost
                              the host where eos-walletd is running
  --wallet-port UINT=8888     the port where eos-walletd is running
Subcommands:
  create                      Create various items, on and off the blockchain
  get                         Retrieve various items and information from the blockchain
  set                         Set or update blockchain state
  transfer                    Transfer EOS from account to account
  wallet                      Interact with local wallet
  benchmark                   Configure and execute benchmarks
  push                        Push arbitrary transactions to the blockchain
```

To get help with any particular subcommand, run it with no arguments as well:

不带参数运行子命令，可以获得指定子命令的帮助。


```
$ ./eosc create
ERROR: RequiredError: Subcommand required
Create various items, on and off the blockchain
Usage: ./eosc create SUBCOMMAND
Subcommands:
  key                         Create a new keypair and print the public and private keys
  account                     Create a new account on the blockchain
$ ./eosc create account
ERROR: RequiredError: creator
Create a new account on the blockchain
Usage: ./eosc create account creator name OwnerKey ActiveKey
Positionals:
  creator TEXT                The name of the account creating the new account
  name TEXT                   The name of the new account
  OwnerKey TEXT               The owner public key for the account
  ActiveKey TEXT              The active public key for the account
```

----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

#### 本文译者简介

胡亮 区块链技术爱好者，欢迎加微信号:haobaba-huliang

本文由币乎社区（bihu.com）内容支持计划赞助。

版权所有，转载需完整注明以上内容。

----------------------------------------------------


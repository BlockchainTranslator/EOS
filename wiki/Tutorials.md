- [1. Accounts & Wallets](#1-accounts--wallets--%E8%B4%A6%E6%88%B7%E5%92%8C%E9%92%B1%E5%8C%85)
  * [1.1 Creating and Managing Wallets](#11-creating-and-managing-wallets--%E5%88%9B%E5%BB%BA%E5%92%8C%E7%AE%A1%E7%90%86%E9%92%B1%E5%8C%85)
  * [1.2 Generating and Importing EOS Keys](#12-generating-and-importing-eos-keys--%E7%94%9F%E6%88%90%E5%92%8C%E5%AF%BC%E5%85%A5-eos-%E5%AF%86%E9%92%A5)
  * [1.3 Backing up your Wallet](#13-backing-up-your-wallet--%E5%A4%87%E4%BB%BD%E4%BD%A0%E7%9A%84%E9%92%B1%E5%8C%85)
  * [1.4 Creating an Account](#14-creating-an-account--%E5%88%9B%E5%BB%BA%E8%B4%A6%E6%88%B7)
- [2. Currency Contract Walkthrough](#2-currency-contract-walkthrough--%E8%B4%A7%E5%B8%81%E5%90%88%E7%BA%A6%E6%BC%94%E7%A4%BA)
- [3. Smart Contract "Hello World"](#3-smart-contract-hello-world--%E6%99%BA%E8%83%BD%E5%90%88%E7%BA%A6-hello-world)
- [4. Tic-Tac-Toe](#4-tic-tac-toe--%E4%BA%95%E5%AD%97%E6%B8%B8%E6%88%8F)

## 1. Accounts & Wallets | 账户和钱包

**Notice** This tutorial is geared towards use on a **private testnet**, but will work on public testnet with minor modifications. 

**注意** 本教程适用于**私用测试网络**，但在稍作修改后也可在公共测试网络上使用。

#### What you'll learn | 你将学到的内容

You'll learn how to create and manage wallets, their keys and then use this wallet to interact with the blockchain through `eosc`.

你将学习如何创建和管理钱包及其密钥，然后使用该钱包通过 `eosc` 与区块链进行交互。

#### Who this Tutorial is For | 本教程适用对象

This tutorial is for users who want to learn about wallet and account management. It will attempt to teach you as much about `eosc` and how wallets and accounts on EOS interact with each other. Advanced users may be better suited to check out the **[Command Reference](Command%20Reference)**

本教程适用于想要了解钱包和账户管理的用户。该教程会尽可能多地向你展示 `eosc` 的使用，以及 EOS 上的钱包和账户之间的互相交互。高级用户可能更适合查阅 ** [Command Reference]（Command％20Reference）**

#### Prerequisites | 准备

- Built and running copy of `eosc` and `eos-walletd` on your system.
- Basic understanding of command line interface. 

**Note:** Instructions require slight modification when applied to a docker installation. 

- 在你的系统上构建并运行 `eosc` 和 `eos-walletd` 的副本。
- 基本了解命令行界面的使用。

**注意：** 使用 docker 安装并运行时，该教程需要稍作调整。

### 1.1 Creating and Managing Wallets | 创建和管理钱包

#### Open your terminal and change to the directory where EOS was built | 打开终端并切换至 EOS 所在的目录

This will make it easier for us to interact with `eosc`, which is a command line interface for interacting with `eosd` and `eos-walletd`. 

在这与 `eosc` 交互比较容易，它是一个与 `eosd` 和 `eos-walletd` 交互的命令行界面。

```sh
$ cd /path_to_eos/build/programs/eosc
```

The first thing you'll need to do is create a wallet; use the `wallet create` command of `eosc`

第一步需要创建一个钱包；使用 `eosc` 的 `wallet create` 命令

```sh
$ eosc wallet create
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"A MASTER PASSWORD"
```

A wallet called _default_ is now inside `eos-walletd` and has returned the **master password** for this wallet. Be sure to save this password somewhere safe. This password is used to unlock (decrypt) your wallet file. 

现在，一个名为 _default_ 的钱包位于 `eos-walletd`，并返回了该钱包的**主密码**。请务必将该密码保存至安全的地方。该密码用于解锁（解密）你的钱包文件。

The file for this wallet is named `default.wallet` and is located in the `data-dir` directory of your EOS directory (or the directory you specified with the `--data-dir` argument when launching `eos-walletd`)

钱包文件被命名为 default.wallet，位于 EOS 目录下的 data-dir 目录（或者在启动 `eos-walletd` 时使用 `--data-dir` 参数指定的目录）

#### Managing Multiple Wallets and Wallet Names | 管理多个钱包和钱包名称

`eosc` is capable of managing multiple wallets. Each individual wallet is protected by different wallet master passwords. The example below creates another wallet and demonstrates how to name it by using the `-n` argument.

`eosc` 具有管理多个钱包的功能。每个单独的钱包由不同的钱包主密码来保护。下例中创建了另一个钱包，并展示了如何使用 `-n` 参数来命名它。

```sh
$ eosc wallet create -n periwinkle
Creating wallet: periwinkle
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"A MASTER PASSWORD"
```

Now confirm that the wallet was created with your chosen name.

现在确认钱包是用你指定的名称来创建的。

```sh
$ eosc wallet list
Wallets:
[
  "default *",
  "periwinkle *"
]
```

It's important to notice the asterisk (*) after each listed wallet, which means that the respective wallet is unlocked. When using `create wallet` the resulting wallet is unlocked by default for your convenience.

请特别留意钱包之后的星号（*），很重要，因为这表示该钱包是解锁的。方便起见，使用 `create wallet` 新建的钱包是默认解锁的。

Lock that second wallet using `wallet lock`

使用 `wallet lock` 锁定第二个钱包

```sh
$ eosc wallet lock -n periwinkle
Locked: 'periwinkle'
```

Upon running `wallet list` again, you will see that the asterisk is gone, meaning that the wallet is now locked.

再次运行 `wallet list` ，你会看到星号已消失，这意味着该钱包已锁定。

```sh
$ eosc wallet list
Wallets:
[
  "default *",
  "periwinkle"
]
```

Unlocking a named wallet entails calling `wallet unlock` with an `-n` parameter followed by the name of the wallet and then entering the wallet's master password in the password prompt (yes, you can paste the password). Go ahead and grab the master key for the second wallet you created, execute the command below and when the _password_ prompt appears, paste and press _enter_. You'll be presented with a confirmation.

解锁一个命名钱包需要调用 `wallet unlock` 命令，并在 `-n` 参数后的输入钱包名称，然后在密码提示符中输入钱包主密码（对的，你可以粘贴密码）。继续并准备好第二个钱包的主密码，执行下面的命令，当 _password_ 提示符出现时，粘贴并按 _enter_ 。你会得到一个确认。

```sh
$ eosc wallet unlock -n periwinkle
```

`eosc` will let you know that the wallet was unlocked

`eosc` 会让你知道钱包是否已解锁

```sh
Unlocked: 'periwinkle'
```

_**Note:** You can also use a `--password` argument followed by the master password to skip the prompt, but this results in your master password being visible in the console history_

_**注意：** 你也可以使用在 `--password` 参数后面添加主密码的方式来跳过提示，但是这会导致你的主密码在终端日志中可见_

Now check your progress

现在检查你的进度

```sh
$ eosc wallet list
Wallets:
[
  "default *",
  "periwinkle *"
]
```

Wonderful, the _periwinkle_ wallet is followed by an asterisk, so it is now unlocked. 

_**Note:** Interacting with the 'default' wallet using the wallet command does not require the `-n` parameter_

太棒了，_periwinkle_ 钱包后面跟了个星号，所以它已经解锁了。

_**注意：** 使用钱包命令与 'default' 钱包交互时不需要 `-n` 参数来特指_

Restart `eos-walletd` now, and then go back to where you were calling `eosc` and run the following command

现在重启 `eos-walletd` ，然后回到你调用 `eosc` 的地方运行接下来的命令

```sh
$ eosc wallet list
Wallets:
[]
```

Interesting, where did the wallet go?

Wallets first need to be opened, and because you shut down `eos-walletd`, the wallet wasn't open. Run the following commands.

有意思，钱包去哪了？

这是因为首先需要打开钱包，而你关闭了 `eos-walletd`，所以钱包都没有打开。运行以下命令。

```sh
$ eosc wallet open
$ eosc wallet list
Wallets:
[
  "default"
]
```

That's better. 

这就好多了。

_**Note:** If you wanted to open a named wallet, you would run `$ eosc wallet open -n periwinkle`, see a pattern forming? ;)_

_**注意：** 如果你想打开一个已命名的钱包，你需要运行 `$ eosc wallet open -n periwinkle`，发现一种模式了吗？;)_

You'll notice in the last response that the default wallet is locked by default. Unlock it now, you'll need it in the subsequent steps. 

你会留意到在上一条返回中的默认钱包是默认锁定的。现在请解锁该钱包，你将在后续步骤中使用它。

Run the `wallet unlock` command and paste your _default_ wallet's master password when the password prompt appears.

运行 `wallet unlock` 命令，出现密码提示时，粘贴 _default_ 钱包的主密码。

```sh
$ eosc wallet unlock
Unlocked: 'default'
```

Go ahead and check that the wallet is unlocked

继续检查钱包是否已解锁

```sh
$ eosc wallet list
Wallets:
[
  "default *"
]
```

The wallet is accompanied by an asterisk, so it's unlocked. Excellent. 

钱包上有了个星号，所以它已经解锁了。太棒了。

You've learned how to create multiple wallets, and interact with them in `eosc`. But an empty wallet doesn't do you much good, time to import some keys. 

你已经学会了如何创建多个钱包，并在 `eosc` 中与它们交互。但是一个空钱包对你没什么用处，是时候导入一些密钥了。

### 1.2 Generating and Importing EOS Keys | 生成和导入 EOS 密钥

There are several ways to generate an EOS key pair, but this tutorial will focus on `create key` command in `eosc`

Generate two keypairs

有好几种方法可以生成 EOS 密钥对，但本教程将重点介绍 `eosc` 中的 `create key` 命令

生成两个密钥对

```sh
$ eosc create key
Private key:###
Public key: ###
$ eosc create key
Private key:###
Public key: ###
```

You now have two EOS keypairs. At this point, these are just arbitrary keypairs and by themselves have no authority.

你现在拥有两个 EOS 密钥对。但此时它们还只是些随意的密钥对，本身没有权限。

If you followed all of the previous steps, your _default_ wallet should be open and unlocked.

如果你执行了上述的所有步骤，那你的 _default_ 钱包应该已经打开并解锁。

In this next step, we execute `wallet import` twice, one for each *private key* that were generated earlier. You now need to import these to your `default` wallet.

在下一步中，我们对之前生成的 *私钥* 分别执行一次 `wallet import` 命令，一共两次。 现在将这些私钥导入到你的 `默认` 钱包中。

```sh
$ eosc wallet import ${private_key_1}
```

And then again with the second private key

然后再用第二个私钥执行一次

```sh
$ eosc wallet import ${private_key_2}
```

If successful, each time `wallet import` command responds with the public key corresponding to your private key, your console should look something like..

如果成功，每次 `wallet import` 命令都会返回私钥所对应的公钥，你的控制台应该类似于..

```sh
$ eosc wallet import ${private_key_1}
imported private key for: ${public_key_1}
$ eosc wallet import ${private_key_2}
imported private key for: ${public_key_2}
```

We can check which keys are loaded by calling `wallet keys`

我们可以调用 `wallet keys` 来检查加载了的密钥

```sh
$ eosc wallet keys
[[
    "EOS6....",
    "5KQwr..."
  ],
  [
    "EOS3....",
    "5Ks0e..."
  ]
]
```

The wallet will protect these keys when it's locked. Accessing the keys in a locked wallet requires the master password that was provided to you during wallet creation. Because the wallet file itself is encrypted, it's not _required_ to backup your keypairs, but backing up your wallet file in a safe place is highly recommended. 

钱包是通过锁定来保护这些密钥的。访问锁定钱包中的密钥需要输入在创建钱包时所提供的主密码。由于钱包文件本身是加密的，因此备份密钥对并不是_必需_的，但强烈建议将钱包文件备份在安全的地方。

### 1.3 Backing up your wallet | 备份你的钱包

Now that your wallet contains keys, it's good to get into the habit of a backup, in case some unspeakable event results in the loss of this file. One example may be a flash drive. Without the password, the wallet file is encrypted with high entropy, and the keys inside are incredibly difficult (improbable by all reasonable measures) to access.

现在，你的钱包里包含了密钥，养成备份的习惯是非常好的，可以预防可怕的事件导致这个文件的丢失。比如说使用闪存。如果没有密码，钱包文件是处于高熵加密的状态，密钥是很难被（通过一切合理的措施）获取的。

You can find your wallet files in the `data-dir`. If you did not specify a `--data-dir` parameter when launching eos, you can file this in `/path/to/eos/build/programs/eosd` (the exact path to eos will differ from system to system).

你可以在 `data-dir` 中找到钱包文件。 如果在启动 eos 的时候没有指定 `--data-dir` 参数，你可以在 `/path/to/eos/build/programs/eosd` 中找到该文件（eos的确切路径因系统而异）。

```sh
$ cd /path_to_eos/build/programs/eosd && ls
blockchain   blocks   config.ini   default.wallet   periwinkle.wallet
```

Once in the directory you will the two files, `default.wallet` and `periwinkle.wallet`. Go ahead and save them somewhere (practice makes perfect!)

一旦进入目录，你将看到两个文件，`default.wallet` 和 `periwinkle.wallet`。继续把它们保存在某个地方（熟能生巧！）

### 1.4 Creating an Account | 创建账户

**If you're working with the public testnet, to proceed you will either need to have a genesis allocation or apply for an account from the faucet. And make necessary adjustments below (hint: inita should be replaced with your account)**

**如果你正在使用公测网，那么你需要进行起始分配，或从水龙头申请一个账户。并在接下来进行必要的调整（提示：应该用你的帐户替换 inita ）**

First let's *examine* the `create account` command and its positional arguments.

首先让我们*检查*一下 `create account` 命令及其位置参数。

```sh
$ eosc create account inita ${desired_account_name} ${public_key_1} ${public_key_2}
```

**Breakdown of the positional arguments for `create account` command**

- `inita` is the name of the **account name** that will fund the account creation, and subsequently the new account.
- `desired_account_name` is the name of the account you would like to create
- `public_key_1` and `public_key_2` are public keys, the first one will be permissioned as the owner authority of your account, and the second one will be permissioned for the active authority of your account. 

**`create account` 命令的位置参数分解**

- `inita` 是**帐户名称**的名称，该账户为创建帐户及随后的新帐户提供资金。
- `desired_account_name` 是你想要创建的帐户的名称。
- `public_key_1` 和 `public_key_2` 是公钥，第一个将被授权为账户的所有者权限，第二个将被授权为账户的活跃权限。

You generated two keypairs previously, you can either scroll up in your console, as you executed this command only moments ago, or execute `wallet keys` if you disdain scrolling or have cleared your screen

之前已生成了两个密钥对，因为是刚才执行了命令，所以可以在控制台中向上滚动屏幕找到密钥对。如果你不屑滚动或清除了屏幕，则可以执行 `wallet keys`

```sh
$ eosc wallet keys
[[
    "EOS6....",
    "5KQwr..."
  ],
  [
    "EOS3....",
    "5Ks0e..."
  ]
]
```

As a reminder, your public keys start with `EOS...`. The keys above are arbitrary until you have added them to an authority, which one you decide to user for active and owner are inconsequential until you have created your account.

作为提醒，公钥是由 `EOS ...` 开头的。在你将密钥添加到一个权限之前，它们都是随意不受限的，决定使用哪个作为活跃和所有者权限的授权对象并不重要。

_Reminder,_ your owner key equates to full control of your account, whereas your active key equates to full access over funds in your account. 

_提醒，_你的所有者密钥等同于账户的全部控制权，而活跃密钥等同于帐户资金的全部控制权。

With all you've just learned, replace the placeholders in the following command and press enter. 

使用你刚刚了解到的所有内容，在随后的命令中替换占位符，然后按回车。

```sh
$ eosc create account inita ${desired_account_name} ${public_key_1} ${public_key_2}
```

Did you recieve an error mentioning "authorities" somewhere? Don't fret, I put you through that intentionally. The reason you got an error, is that you do not have the **@inita**  account keys loaded. Sorry about that, couldn't resist. 

你是不是在某些地方遇到了一个提及 "authorities" 的错误？别担心，我是故意带你到那的。遇到错误的原因是没有加载 **@inita** 帐户密钥。 抱歉，无法抗拒啊。

**inita's** keys are included in `config.ini` but for your convenience I've went ahead and grabbed the key and provided it below. Just execute the provided command, maybe that makes up for forcing you through an error?

**inita 的**密钥包含在 `config.ini` 中，但是为了方便，我已经提前获取并下面展示了该密钥。只需执行下面的命令，或许这可以补偿一下迫使你犯错的经历？

```sh
$ eosc wallet import 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

it will respond with 

它会返回

```sh
imported private key for: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```

Now that the **@inita** account's keys are loaded, execute the `create account` command you crafted before I baited you into a trap, and press enter. 

现在已经加载了 **@inita** 账号的密钥，执行在我诱你掉入陷阱之前所键入的 `create account` 命令，然后按回车。

If all goes well, `eosc` will return a json object with a transaction ID, similar to the following

如果一切顺利，`eosc` 将返回一个带有事务 ID 的 json 对象，类似于下面的内容

```text
{
  "transaction_id": "6acd2ece68c4b86c1fa209c3989235063384020781f2c67bbb80bc8d540ca120",
  "processed": {
    "refBlockNum": "25217",
    "refBlockPrefix": "2095475630",
    "expiration": "2017-07-25T17:54:55",
    "scope": [
      "eos"...
```

Great! You now have an account and it is on a blockchain. 

真棒！你现在拥有一个帐户，而且它是在区块链上的。

Go ahead and pat yourself on the back, you've created a wallet, learned a bit about how wallets work, generated keys, imported them into your wallet and created an account. 

继续前行，先自我表扬下，你已经创建了一个钱包，学习了一些钱包的使用方式，生成了密钥，并将它们导入到你的钱包和创建了帐户。

## 2. Currency Contract Walkthrough | 货币合约演示

### Objective | 目标

The following tutorial will guide the user through the sample currency
contract which can be found in the public github repository
[here](https://github.com/EOSIO/eos/tree/master/contracts/currency).

以下教程将引导用户过一遍货币合约的示例，该示例可以在公共 github 代码库中找到[这里](https://github.com/EOSIO/eos/tree/master/contracts/currency)。

### Overview | 概述

The currency contract handles the transfer of a currency from one
account to another, whereas the different account balances are saved for
every user local in their scope.

货币合约处理货币从一个帐户转移到另一个账户，而不同的帐户余额都保存在每个用户的局部范围内。

### Action | 动作

Currently there is only one action exposed by the contract, which is:  
currency_transfer: Transfers an amount of currency from one account to
another.

目前合约只提供了一种动作，即：currency_transfer：从一个账户转一定数量的货币到另个账户上。

### Start! | 开始！

The smart contract is divided in three files:

智能合约共分为三个文件：

| currency.hpp | header file where the declarations and structures of the contract are defined |
|--------------|-------------------------------------------------------------------------------|
| currency.cpp | Contract logic and implementation                                             |
| currency.abi | Interface definition for the user to interact                                 |


| currency.hpp | 头文件定义了合同的声明和结构   |
|--------------|----------------------------|
| currency.cpp | 合约的逻辑和实现             |
| currency.abi | 为用户进行交互所提供的接口定义 |

### Header File: currency.hpp | 头文件：currency.hpp

First import all the necessary libraries and define your own namespace
such as:

首先导入所有必要的库，并定义你的命名空间，比如：

~~~~
// Import necessary libraries

#include <eoslib/eos.hpp>   // Generic eos library, i.e. print, type, math, etc
#include <eoslib/token.hpp> // Token usage
#include <eoslib/db.hpp>    // Database access

namespace currency {
    // Your code here
}
~~~~

Next add a currency token; It’s in fact a uin64_t wrapper which checks
for proper types and under/overflows for standard-compatible token
messages

接着添加一个货币令牌；这实际上是一个 uin64_t 的包装器，用于检测兼容标准的令牌消息的类型是否正确，是否下溢/溢出

~~~~
typedef eosio::token<uint64_t,N(currency)> currency_tokens;
~~~~

A structure for our action, which looks as follows:

一个动作的结构如下：

~~~~
struct transfer {
    account_name from;          //transfer source account
    account_name to;            //transfer destination account
    currency_tokens quantity;   //amount to be transferred
};
~~~~
Additionally, we need to store the balance in a table. The table is
defined as follows:

另外，我们需要将余额存储在一个表格中。该表定义如下：

~~~~
using accounts = eosio::table<N(defaultscope),N(currency),N(account),account,uint64_t>;
~~~~
-   First template parameter defines the default scope of the
    table, i.e. when a data is stored to this table without specifying
    the scope, it will fall back to this account

-   Second template parameter defines the owner of the table (i.e.
    contract's name)

-   Third template parameter defines the name of the table

-   Fourth template parameter defines the structure that it stores (will
    be defined in the next section)

-   Fifth template parameter defines the data type of the table's key

Once the table is defined the structure that needs to be stored (in our
case “account”) needs to be defined as well. This is done in another
struct:

- 第一个模板参数定义了表的默认范围，即当数据存储到这个表中而不指定范围时，它将回退到这个帐户

- 第二个模板参数定义了表的所有者（即合约名称）

- 第三个模板参数定义了表的名称

- 第四个模板参数定义了表的存储结构（将在下一节中定义）

- 第五个模板参数定义了表的键的数据类型

一旦定义了表，同时也需要定义存储结构（在本例中是“帐户”）。这在另一个结构中完成：
~~~~
struct account {
    //Constructor
    account( currency_tokens b = currency_tokens() ):balance(b){}

    //The key is constant because there is only one record per
    //scope/currency/accounts
    const uint64_t key = N(account);

    //Number of tokens in account
    currency_tokens balance;

    // Method to check if account is empty.
    // returns true if the account balance is zero.
    bool is_empty()const { return balance.quantity == 0; }
};
~~~~
The structure contains both a constructor and a standard function for
comparison against an empty account.

It’s important to note, that the key is the first variable who’s type
matches the type defined in the table definition above (as fifth
template parameter).

To round things up, we add an accessor function to access the owners
account information, which returns information stored here:
owner/TOKEN_NAME/account/account. This function goes in the header to
provide 3<sup>rd</sup> party access to a user’s balance:

相比于空账户，该结构包含一个构造器和一个标准函数。

重要的是要留意到其关键是第一个变量，它的类型与之前定义表中类型相匹配（作为第五个模板参数）。

集合起来，我们添加一个访问函数来访问所有者的帐户信息，其返回信息存储在这：owner/TOKEN_NAME/account/account。这个函数在 header 中为用户的余额提供第 3 方的访问权限：
~~~~
inline account get_account( account_name owner ) {
    account owned_account;
    accounts::get( owned_account, owner );
    return owned_account;
}
~~~~
Note: The function accounts:get returns the account owner. In case the
account does not exist, it returns a default constructed account.

注意：函数 accounts:get 返回帐户所有者。如果账户不存在，则返回一个默认构建的账户。

### Source File: currency.cpp | 源文件：currency.cpp
~~~~
#include <currency/currency.hpp>

// The init() and apply() methods must have C calling convention

extern "C" {
    // Only called once
    void init() {
    }

    // The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action_name ) {
        // Put your message handler here
    }
} // extern "C"
~~~~
All contracts have the above skeleton in common. Every contract must
have the above functions:

Init() is being called once at the beginning of the lifetime of a
contract. It can be used to setup the environment in order for the
contract to function properly.

Apply( uint64_t code, uint64_t action_name) is being used a message
sink. Whenever a message is being sent to the contract, this function is
the entry point; The two parameters have the following meaning:

-   code: This is the name of the contract
-   action_name: This is the name of the action

In the case of the currency contract, the init() function looks as
follows:

所有合约都具有上述共同的构架。每份合约都必须含有上述函数：

Init()  在合约生命周期开始时调用一次。它用来设置环境，使合约能正常运行。

Apply( uint64_t code, uint64_t action_name) 用作为消息接收器。每当消息发送到合约时，这个函数就是入口; 其两个参数含义如下：

-   code：这是合约名称
-   action_name：这是动作名称

在货币合约的示例中，init() 函数如下所示：
~~~~
void init() {
    account owned_account;

    //Initialize currency account only if it does not exist
    if ( !accounts::get( owned_account, N(currency) )) {
        store_account( N(currency),
        account( currency_tokens(1000ll\*1000ll\*1000ll) ) );
    }
}
~~~~
The first time this contract runs, it checks, if the currency account
already has a table. In the table the currency balance is recorded. In
case there is no table a new table is being generated and an initial
amount of 1000,000,000, which makes the currency contract the initial
owner of 1000,000,000 currency units.

The message sink looks as follows:

该合约首次运行时会检查货币账户是否已经有一张表。在表中记录着货币余额。如果没有表，则会生成一个新表，其初始数目为 1000,000,000，这使得该货币合约成为 1000,000,000 个货币单位的初始拥有者。

消息接收器如下所示：
~~~~
void apply( uint64_t code, uint64_t action ) {
    if( code == N(currency) ) {
        if( action == N(transfer) )
            account::apply_currency_transfer( current_message<account::transfer >() );
    }
}
~~~~
It is best practice to implement filters as in the above code sample in
order to make sure that only the correct messages are being processed
and then call the atual message handler after filtering.

Notice that current_message<T>() is used before passing it to
specific handler, current_message<T>() is converting the message
that the contract receives to struct T.

最好能像上示代码示例中一样执行过滤，以确保只有正确的消息将被处理，在过滤之后调用真正的消息处理器。

请注意，在将消息传递给指定的处理器之前使用了 current_message<T>()，
current_message<T>() 将合约收到的消息转换成结构 T。

### Actual Message Handler | 真正的消息处理器

The actual transfer of currency is performed in:

实际的货币转移如下所示：
~~~~
void apply_currency_transfer( const account::transfer& transfer_msg )
{
    require_notice( transfer_msg.to, transfer_msg.from );
    require_auth( transfer_msg.from );

    auto from = get_account( transfer_msg.from );
    auto to = get_account( transfer_msg.to );

    from.balance -= transfer_msg.quantity;
    to.balance += transfer_msg.quantity;

    store_account( transfer_msg.from, from );
    store_account( transfer_msg.to, to );
}
~~~~
The code is straight forward, subtracting currency from the source
account and adding it to the destination account.

The require_notice function is an inline action which makes it possible
to forward the received message to another account. In this case the
transfer message is forwarded to the source and destination account.
This is an extremely useful feature as it enables these “notified
accounts” to chain in their own functionality.

The require_auth function makes sure that the message is signed in the
correct way. In this case the holder of the source account needs to sign
the transaction for the transfer to be handled as expected.

Observe that we are using the get_account function that is provided in
the header in order to retrieve the correct account object.

Since we are using tokens, automatic over and underflow assertions are
being backed into the actual subtraction and addition operations.

Finally the amounts are updated via the store_account function.

代码是简明直接的，从源帐户中扣除货币，并将其添加到目标帐户。

require_notice 函数是一个内联动作，可以将收到的消息转发到另一个帐户。在本例中，转账消息被转发到源账户和目标账户。这是一个非常有用的功能，因为它可以使这些“被通知的帐户”在其自己的功能中进行链接。

require_auth 函数确保消息有正确的签名。在本例中，源账户的持有人需要对交易进行签名，以便交易按照预期被处理。

请注意，我们正在使用头部提供的 get_account 函数来获取正确的帐户对象。

由于我们使用的是令牌，因此自动溢出和下溢断言将在实际的减法和加法操作中得到支持。

最后，数量通过 store_account 函数更新。

### Store_account

This function handles the actual storage of the balance:

该函数处理余额的实际存储：
~~~~
void store_account( account_name current_account, const account& value ) {
    if( a.is_empty() ) {
        accounts::remove( value, current_account);
    } else {
        accounts::store( value, current_account);
    }
}
~~~~
The interesting fact about this is, that the account (meaning the table
saved under the scope of current_account gets removed if empty. Since
whenever money is transferred onto a non-existing account the table gets
created.

As such removing unnecessary tables is a resource saving mechanism that
should be applied as best practice when writing any smart contract.

NOTE: When comparing the above code samples with the actual code in the
repository, please be aware of the usage of TOKEN_NAME as a #define in
order to make renaming the account name more easy. In the above code,
TOKEN_NAME has been replaced by account for easier legibility.

有一个有趣的事实是，如果这个帐户（也就是在 current_account 域内保存的表）是空的，那么会被删除。因为每当钱被转移到一个不存在的帐户时表会被创建。

因此，删除不必要的表格是一种节约资源的机制，应作为编写智能合约的最佳实践。

注：将上述代码示例与库中的实际代码进行比较时，请注意将 TOKEN_NAME 作为 #define 的用法，以更容易重命名帐户名称。在上述代码中，为了易于阅读，TOKEN_NAME 已被帐户取代。

### ABI File: currency.abi | ABI 文件： currency.abi

Abi (a.k.a Application Binary Interface) acts as an interface between
the sent message and the binary version of the smart contract. Let's
start with a generic version which includes the following objects:

-   struct: list of data structure used by the action/ table in the
    contract

-   actions: list of actions available in the contract

-   tables: list of tables available in the contract

Abi（也称为应用程序二进制接口）充当发送消息和智能合约的二进制版本之间的接口。我们从一个包含以下对象的通用版本开始：

- 结构：合约中动作/表使用的数据结构列表

- 行动：合约中可用的动作列表

- 表格：合约中可用表的列表

~~~~
{
    "structs": \[{
        "name": "...",
        "base": "...",  
        "fields": { ... }
    }, ...\],
    "actions": \[{
        "action_name": "...",
        "type": "..."
    }, ...\],
    "tables": \[{
        "table_name": "...",
        "type": "...",
        "key_names" : \[...\],
        "key_types" : \[...\]
    }, ...\]
}
~~~~
### struct Objects | struct 对象

From the information in the header file most of the ABI can be created.
As such we start with the structures; There are two structures in the
header file:

从头文件中的信息可以创建大多数的 ABI。 因此，我们从结构开始。 头文件中有两个结构：
~~~~
struct transfer {
    account_name from;
    account_name to;
    currency_tokens quantity;
};

struct account {
    account( currency_tokens b = currency_tokens() ):balance(b){}
    const uint64_t key = N(account);
    currency_tokens balance;
    bool is_empty()const { return balance.quantity == 0; }
};
~~~~
These structures turn into the following ABI information:

这些结构变成以下的 ABI 信息：
~~~~
"structs": \[{
    "name": "transfer",
    "base": "",
    "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
    }
},{
    "name": "account",
    "base": "",
    "fields": {
        "key": "name",
        "balance": "uint64"
    }
}\]
~~~~
### action Object | 动作对象

Action Objects correspond similarly. As such, we have one action named
“transfer” in the currency contract which looks as follows in the ABI
file:

动作对象也有类似的对应。因此，我们在货币合约中有一个名为“转账”的动作，在 ABI 文件中如下：

~~~~
"actions": \[{
    "action_name": "transfer",
    "type": "transfer"
}\]
~~~~
### table Object | 表对象

In the header file a single index called “account” table is being
defined:

在头文件中，一个名为 “account” 表的索引被定义为：
~~~~
eosio::table<N(defaultscope),N(currency),N(account),account,uint64_t>;
~~~~
This table turns into the following ABI object:

该表变成如下的 ABI 对象：
~~~~
"tables": \[{
    "table_name": "account",
    "type": "account",
    "index_type": "i64",
    "key_names" : \["key"\],
    "key_types" : \["name"\]
}\]
~~~~
rounding up the ABI file.

集合 ABI 文件。

### Deploy and run | 部署和运行

Now all the three files (currency.hpp, currency.cpp, currency.abi) can
be deployed from command line:

现在，所有三个文件（currency.hpp，currency.cpp，currency.abi）都可使用命令行部署：
~~~~
$ eosc set contract currency currency.wast currency.abi
~~~~
Make sure that the wallet is unlocked and contains the currency key.
After the deployment the contracts action can be triggered from command
line in the following way:

确保钱包已解锁并包含货币密钥。部署之后，可以通过如下命令行触发合约动作：
~~~~
$ eosc push message currency transfer ‘{“from”:“currency”,“to”:“tester”,“quantity”:50}’ -S currency -S tester -p currency@active
~~~~

## 3. Smart Contract “Hello World” | 智能合约 “Hello World”

To keep things simple we have created a tool called `eoscpp` which can be used to bootstrap a new contract. For this
to work we assume you have installed the eosio/eos code installed and that ${CMAKE_INSTALL_PREFIX}/bin is in your path.

简单起见，我们制作了一个名为 `eoscpp` 的工具，用来引导生成新合约。为了能正常运行，我们假设你已经安装了 eosio/eos 代码，还有 ${CMAKE_INSTALL_PREFIX}/bin 已在你的路径中。

```sh
$ eoscpp -n hello
$ cd hello
$ ls
```

The above will create a new empty project in the './hello' folder with three files:

运行命令后，将会在 './hello' 文件夹中创建一个新的空项目，该文件夹会包含三个文件：

```sh
hello.abi hello.hpp hello.cpp
```

Let's take a look at the simplest possible contract:

让我们来看一下最简单的合约：

```sh
$ cat hello.cpp

#include <hello.hpp>

/**
 *  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
 *  call these methods.
 */
extern "C" {

    /**
     *  This method is called once when the contract is published or updated.
     */
    void init()  {
       eosio::print( "Init World!\n" );
    }

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
    }

} // extern "C"
```

This contract implements the two entry points, `init` and `apply`. All it does is log the messages delivered and makes no other checks. Anyone can deliver any message at any time provided the block producers allow it.  Absent any required signatures, the contract will be billed for the bandwidth consumed.

You can compile this contract into a text version of WASM (.wast) like so:

这个合约实现了两个入口，`init` 和 `apply` 。它所做的只是记录传递的消息，并不做其他检查。只要区块生产者允许，任何人都可以在任何时候传递任何消息。在没有任何所需签名的情况下，合约将因为消耗的带宽而产生费用。

可以将此合约编译为文本版本的 WASM(.wast)，如下所示：

```sh
$ eoscpp -o hello.wast hello.cpp
```

#### Deploying your Contract | 部署合约

Now that you have compiled your application it is time to deploy it. This will require you to do the following first:

1. start eosd with wallet plugin enabled
2. create a wallet & import keys for at least one account
3. keep your wallet unlocked

现在你已经编译了应用程序，是时候进行部署了。这将要求你首先执行以下操作：

1. 启动允许运行钱包插件的 eosd
2. 至少为一个帐户创建一个钱包并导入密钥
3. 保持你的钱包解锁

Assuming your wallet is unlocked and has keys for `${account}`, you can now upload this contract to the blockchain with the following command:

假设你的钱包已解锁，并拥有 `${account}` 的密钥，那就可使用以下命令将此合约上传到区块链上：

```sh
$ eosc set contract ${account} hello.wast hello.abi
Reading WAST...
Assembling WASM...
Publishing contract...
{
  "transaction_id": "1abb46f1b69feb9a88dbff881ea421fd4f39914df769ae09f66bd684436443d5",
  "processed": {
    "ref_block_num": 144,
    "ref_block_prefix": 2192682225,
    "expiration": "2017-09-14T05:39:15",
    "scope": [
      "eos",
      "${account}"
    ],
    "signatures": [
      "2064610856c773423d239a388d22cd30b7ba98f6a9fbabfa621e42cec5dd03c3b87afdcbd68a3a82df020b78126366227674dfbdd33de7d488f2d010ada914b438"
    ],
    "messages": [{
        "code": "eos",
        "type": "setcode",
        "authorization": [{
            "account": "${account}",
            "permission": "active"
          }
        ],
        "data": "0000000080c758410000f1010061736d0100000001110460017f0060017e0060000060027e7e00021b0203656e76067072696e746e000103656e76067072696e7473000003030202030404017000000503010001071903066d656d6f7279020004696e69740002056170706c7900030a20020600411010010b17004120100120001000413010012001100041c00010010b0b3f050041040b04504000000041100b0d496e697420576f726c64210a000041200b0e48656c6c6f20576f726c643a20000041300b032d3e000041c0000b020a000029046e616d6504067072696e746e0100067072696e7473010004696e697400056170706c790201300131010b4163636f756e744e616d65044e616d6502087472616e7366657200030466726f6d0b4163636f756e744e616d6502746f0b4163636f756e744e616d6506616d6f756e740655496e743634076163636f756e740002076163636f756e74044e616d650762616c616e63650655496e74363401000000b298e982a4087472616e736665720100000080bafac6080369363401076163636f756e7400076163636f756e74"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```

If you are monitoring the output of your eosd process you should see:

如果你正在观察 eosd 进程的输出，你会看到：

```sh
...] initt generated block #188249 @ 2017-09-13T22:00:24 with 0 trxs  0 pending
Init World!
Init World!
Init World!
```

You will notice the lines "Init World!" are executed 3 times, this isn't a mistake.  When the blockchain is processing transactions the following happens:

1. eosd receives a new transaction
  * creates a temporary session
  * attempts to apply the transaction
  * **succeeds and prints "Init World!"**
  * or fails undoes the changes (potentially failing after printing "Init World!")
2. eosd starts to produce a block
  * undoes all pending state
  * pushes all transactions as it builds the block
  * **prints "Init World!" a second time**
  * finishes building the block
  * undoes all of the temporary changes while creating block
3. eosd pushes the generated block as if it received it from the network
  * **prints "Init World!" a third time**

At this point your contract is ready to start receiving messages. Since the default message handler accepts all messages we can send it
anything we want. Let's try sending it an empty message:

你会留意到 "Init World!" 这行执行了 3 次，这并非错误。当区块链在处理事务时，情况如下：

1. eosd 收到新的事务
  * 创建一个临时会话
  * 尝试执行事务
  * **成功并打印 "Init World!"**
  * 或者失败则撤销更改（可能在打印 "Init World!" 后失败）
2. eosd 开始产生一个块
  * 撤销所有待处理状态
  * 在构建区块时推送所有事务
  * **第二次打印 "Init World!"**
  * 完成构建区块
  * 撤销创建区块时但所有临时更改
3. eosd 将构建好的块推送出去，如同从网络上接收这个区块一样
  * **第三次打印 "Init World!"**

此时你的合约就已经准备好开始接收消息了。由于默认消息处理器接受所有消息，所以我们可以发送任何想要发送的消息。让我们尝试发送一个空消息：

```sh
$ eosc push message ${account} hello '"abcd"' --scope ${account}
```

This command will send the message "hello" with binary data represented by the hex string "abcd". Note, in a bit we will show how to define the ABI so that you can replace the hex string with a pretty, easy-to-read, JSON object. For now we merely want to demonstrate how the message type "hello" is dispatched to account.

The result is:

该命令将发送使用十六进制字符串 "abcd" 作为其二进制数据表示的消息 "hello"。请注意，稍后我们将演示如何定义 ABI，以便你使用十分易读的 JSON 对象替换十六进制字符串。现在我们仅演示消息类型 "hello" 如何分发到账户。

其结果为：

```sh
{
  "transaction_id": "69d66204ebeeee68c91efef6f8a7f229c22f47bcccd70459e0be833a303956bb",
  "processed": {
    "ref_block_num": 57477,
    "ref_block_prefix": 1051897037,
    "expiration": "2017-09-13T22:17:04",
    "scope": [
      "${account}"
    ],
    "signatures": [],
    "messages": [{
        "code": "${account}",
        "type": "hello",
        "authorization": [],
        "data": "abcd"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```

If you are following along in `eosd` then you should have seen the following scroll by the screen:

如果你在 `eosd` 中进行追踪，那么你应该在屏幕中看到：

```sh
Hello World: ${account}->hello
Hello World: ${account}->hello
Hello World: ${account}->hello
```

Once again your contract was executed and undone twice before being applied the 3rd time as part of a generated block.  

再一次地，你的合约被执行和撤消两次，第三次作为生成区块的一部分。

#### Message name Restrictions | 消息名称限制

Message types (eg. "hello") are actually base32 encoded 64 bit integers. This means they are limited to the charcters a-z, 1-5, and '.' for the first
12 charcters and if there is a 13th character then it is restricted to the first 16 characters ('.' and a-p).

消息类型（例如 "hello"）实际上是 base32 编码的 64 位整数。这意味着前12个字符仅限于字符 a-z，1-5，和 “.”。如果有第13个字符，则只限于前16个字符（'.' 和 a-p）。

#### ABI - Application Binary Interface | ABI - 应用程序二进制接口

The ABI is a JSON-based description on how to convert user actions between their JSON and Binary representations. The ABI also
describes how to convert the database state to/from JSON. Once you have described your contract via an ABI then developers and
users will be able to interact with your contract seemlessly via JSON.

We are working on tools that will automate the generation of the ABI from the C++ source code, but for the time being you may have
to generate it manually.

Here is an example of what the skeleton contract ABI looks like:

ABI 是一个基于 JSON 的描述，关于用户动作的 JSON 和二进制表示之间的转换。 ABI 还介绍了数据库状态和 JSON 之间的转换。一旦通过 ABI 来描述合约，开发人员和用户就可以通过 JSON 无缝地和合约进行交互。

我们正在开发能够自动从 C++ 源代码生成 ABI 的工具，但是目前你需要手动生成 ABI。

下面是架构合约的 ABI 例子：

```json
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
      }
    },{
      "name": "account",
      "base": "",
      "fields": {
        "account": "name",
        "balance": "uint64"
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
      "type": "account",
      "index_type": "i64",
      "key_names" : ["account"],
      "key_types" : ["name"]
    }
  ]
}
```

You will notice that this ABI defines an action `transfer` of type `transfer`.  This tells EOS.IO that when `${account}->transfer` message is seen that the payload is of type `transfer`.  The type `transfer` is defined in the `structs` array in the object with `name` set to `"transfer"`.  

你会留意到，这个 ABI 定义了一个 `transfer` 类型的 `transfer` 动作。这告诉 EOS.IO 当看到 `${account}->transfer` 消息时，其有效载荷是 `transfer` 类型。类型 `transfer` 由 `structs` 数组中的一个 `name` 被设置为 `"transfer"` 的对象所定义。

```json
...
  "structs": [{
      "name": "transfer",
      "base": "",
      "fields": {
        "from": "account_name",
        "to": "account_name",
        "quantity": "uint64"
      }
    },{
...
```

It has several fields, including `from`, `to` and `quantity`.  These fields have the coresponding types `account_name`, `account_name`, and `uint64`.  `account_name` is defined as a typedef in the `types` array to `name`, which is a built in type used to encode a uint64_t as base32 (eg account names).

它有一些字段，包括 `from`, `to` 和 `quantity`。这些字段具有其对应的数据类型 `account_name`, `account_name`, 和 `uint64`。 `account_name` 在 `types` 数组中被定义为一种 `name` 的 typedef，这是一个内置的类型，用于将 uint64_t 编码为 base32（例如账户名称）。

```json
{
  "types": [{
      "new_type_name": "account_name",
      "type": "name"
    }
  ],
...
```

Now that we have reviewed the ABI defined by the skeleton, we can construct a message call for `transfer`:

现在我们已经回顾了由构架定义的 ABI，我们可以构建一个消息来调用 “transfer”：

```sh
eosc push message ${account} transfer '{"from":"currency","to":"inita","quantity":50}' --scope initc
2570494ms thread-0   main.cpp:797                  operator()           ] Converting argument to binary...
{
  "transaction_id": "b191eb8bff3002757839f204ffc310f1bfe5ba1872a64dda3fc42bfc2c8ed688",
  "processed": {
    "ref_block_num": 253,
    "ref_block_prefix": 3297765944,
    "expiration": "2017-09-14T00:44:28",
    "scope": [
      "initc"
    ],
    "signatures": [],
    "messages": [{
        "code": "initc",
        "type": "transfer",
        "authorization": [],
        "data": {
          "from": "currency",
          "to": "inita",
          "quantity": 50
        },
        "hex_data": "00000079b822651d000000008040934b3200000000000000"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```

If you observe the output of `eosd` you should see:

如果你观察 `eosd` 的输出，你会看到：

```text
Hello World: ${account}->transfer
Hello World: ${account}->transfer
Hello World: ${account}->transfer
```

### Processing Arguments of Transfer Message | 处理传输消息的参数

According to the ABI the transfer message has the format: 

根据 ABI，转账消息的格式为：

```json
	 "fields": {
		 "from": "account_name",
		 "to": "account_name",
		 "quantity": "uint64"
	 }
```

We also know that account_name -> name -> uint64 which means that the binary representation of the message is the same as:

我们也知道 account_name -> name -> uint64，这意味着消息的二进制表示等价于：

```c
struct transfer {
    uint64_t from;
    uint64_t to;
    uint64_t quantity;
};
```

The EOS.IO C API provides access to the message payload via the Message API:

EOS.IO 的 C API 使用 Message API 提供了对消息有效载荷的访问：

```text
uint32_t message_size();
uint32_t read_message( void* msg, uint32_t msglen );
```

Let's modify `hello.cpp` to print out the content of the message:

让我们修改 `hello.cpp` 来打印出消息内容：

```c
#include <hello.hpp>

/**
 *  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
 *  call these methods.
 */
extern "C" {

    /**
     *  This method is called once when the contract is published or updated.
     */
    void init()  {
       eosio::print( "Init World!\n" );
    }

    struct transfer {
       uint64_t from;
       uint64_t to;
       uint64_t quantity;
    };

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          transfer message;
          static_assert( sizeof(message) == 3*sizeof(uint64_t), "unexpected padding" );
          auto read = readMessage( &message, sizeof(message) );
          assert( read == sizeof(message), "message too short" );
          eosio::print( "Transfer ", message.quantity, " from ", eosio::name(message.from), " to ", eosio::name(message.to), "\n" );
       }
    }

} // extern "C"
```

Then we can recompile and deploy it with:

接着我们对它进行重新编译和部署：

```sh
eoscpp -o hello.wast hello.cpp 
eosc set contract ${account} hello.wast hello.abi
```

`eosd` will call init() again because of the redeploy

`eosd` 会因为重新部署再次调用 init()

```sh
Init World!
Init World!
Init World!
```

Then we can execute transfer:

接着我们可以执行转账：
```sh
$ eosc push message ${account} transfer '{"from":"currency","to":"inita","quantity":50}' --scope ${account}
{
  "transaction_id": "a777539b7d5f752fb40e6f2d019b65b5401be8bf91c8036440661506875ba1c0",
  "processed": {
    "ref_block_num": 20,
    "ref_block_prefix": 463381070,
    "expiration": "2017-09-14T01:05:49",
    "scope": [
      "${account}"
    ],
    "signatures": [],
    "messages": [{
        "code": "${account}",
        "type": "transfer",
        "authorization": [],
        "data": {
          "from": "currency",
          "to": "inita",
          "quantity": 50
        },
        "hex_data": "00000079b822651d000000008040934b3200000000000000"
      }
    ],
    "output": [{
        "notify": [],
        "deferred_transactions": []
      }
    ]
  }
}
```

And on `eosd` we should see the following output:

在`eosd`上，我们应该看到如下输出：

```sh
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
Hello World: ${account}->transfer
Transfer 50 from currency to inita
```

#### Using C++ API to Read Messages | 使用C ++ API读取消息
So far we used the C API because it is the lowest level API that is directly exposed by EOS.IO to the WASM virtual machine. Fortunately, eoslib provides a higher level API that
removes much of the boiler plate. 

目前为止，我们使用的都是 C API，因为它是 EOS.IO 直接向 WASM 虚拟机暴露的最低级 API。幸运的是，eoslib 提供了一个更高级的 API，可以去除大部分的样板代码。

```c
/// eoslib/message.hpp
namespace eosio {
	 template<typename T>
	 T current_message();
}
```

We can update `hello.cpp` to be more concise as follows:

我们可以把 `hello.cpp` 变得更紧凑，如下所示：

```c
#include <hello.hpp>

/**
 *  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
 *  call these methods.
 */
extern "C" {

    /**
     *  This method is called once when the contract is published or updated.
     */
    void init()  {
       eosio::print( "Init World!\n" );
    }

    struct transfer {
       eosio::name from;
       eosio::name to;
       uint64_t quantity;
    };

    /// The apply method implements the dispatch of events to this contract
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::current_message<transfer>();
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }

} // extern "C"

```

You will notice that we updated the `transfer` struct to use the `eosio::name` type directly, and then condenced the checks around `read_message` to a single call to `current_message`.

After compiling and uploading it you should get the same results as the C version.

你会注意到我们在 `transfer` 结构中直接使用了 `eosio::name` 类型，然后将 `read_message` 周围的检查浓缩为一个 `current_message` 调用。

编译并上传后，你应该得到与 C 版本相同的结果。

### Requiring Sender Authority to Transfer | 发送者对转账的授权要求

One of the most common requirements of any contract is to define who is allowed to perform the action. In the case of a curency transfer, we want require that the account defined by the `from` parameter signs off on the message. 

The EOS.IO software will take care of enforcing and validating the signatures, all you need to do is require the necessary authority.

任何合约最常见的规定之一是定义了允许谁来执行该行动。在资金转账的例子中，我们应该要求由 `from` 参数定义的账户在消息上签名。

EOS.IO 软件将负责强制执行和验证签名，你所需要做的就是要求必要的权限。

```c
    ...
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::current_message<transfer>();
          eosio::require_auth( message.from );
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }
    ...
```

After building and deploying we can attempt to transfer again:

在构建和部署之后，我们可以再次尝试转账：

```sh
 eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account}
 1881603ms thread-0   main.cpp:797                  operator()           ] Converting argument to binary...
 1881630ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
 status_code == 200: Error
 : 3030001 tx_missing_auth: missing required authority
 Transaction is missing required authorization from initb
     {"acct":"initb"}
         thread-0  message_handling_contexts.cpp:19 require_authorization
...
```

If you look on `eosd` you will see this:

如果你查看 `eosd`，会看到：

```text
Hello World: initc->transfer
1881629ms thread-0   chain_api_plugin.cpp:60       operator()           ] Exception encountered while processing chain.push_transaction:
...
```

This shows that it attempted to apply your transaction, printed the initial "Hello World" and then aborted when `eosio::require_auth` failed to find authorization of account `initb`.

We can fix that by telling `eosc` to add the required permission:

这表明它试图执行你的事务，打印出最初的 “Hello World”，然后在执行 `eosio::require_auth` 时找不到帐户 `initb` 的授权而中止。

我们可以通过告诉 `eosc` 添加所需的权限来解决这个问题：

```sh
 eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":50}' --scope ${account} --permission initb@active
```

The `--permission` command defines the account and permission level, in this case we use the `active` authority which is the default.

This time the transfer should have worked like we saw before.

`--permission` 命令定义了帐户和权限级别，在本例中我们使用默认的 `active` 权限。

这下，转账应该像之前我们看到的那样运行了。

### Aborting a Message on Error | 中止错误消息

A large part of contract development is verifying preconditions, such that the quantity transferred is greater than 0. If a user attempts to execute an invalid action, then
the contract must abort and any changes made get automatically reverted.

合约开发的很大一部分工作是验证先决条件，比如转账金额大于零。如果用户试图执行一个无效动作，则合约必须中止，并且所做的任何更改都会自动恢复。

```c
    ...
    void apply( uint64_t code, uint64_t action ) {
       eosio::print( "Hello World: ", eosio::name(code), "->", eosio::name(action), "\n" );
       if( action == N(transfer) ) {
          auto message = eosio::current_message<transfer>();
          assert( message.quantity > 0, "Must transfer a quantity greater than 0" );
          eosio::require_auth( message.from );
          eosio::print( "Transfer ", message.quantity, " from ", message.from, " to ", message.to, "\n" );
       }
    }
    ...
```

We can now compile, deploy, and attempt to execute a transfer of 0:

我们现在可以编译，部署并尝试执行一笔数目为零的转账：

```sh
 $ eoscpp -o hello.wast hello.cpp
 $ eosc set contract ${account} hello.wast hello.abi
 $ eosc push message ${account} transfer '{"from":"initb","to":"inita","quantity":0}' --scope initc --permission initb@active
 3071182ms thread-0   main.cpp:851                  main                 ] Failed with error: 10 assert_exception: Assert Exception
 status_code == 200: Error
 : 10 assert_exception: Assert Exception
 test: assertion failed: Must transfer a quantity greater than 0
```

## 4. Tic-Tac-Toe | 井字游戏

### Objective | 目的

The following tutorial will guide the user to build a sample Player vs Player game contract. We will use tic tac toe game to demonstrate this. Final result of this tutorial can be found [here](https://github.com/EOSIO/eos/tree/master/contracts/tic_tac_toe).

以下教程将指导用户构建一个玩家对玩家的游戏合约示例。我们将使用井字游戏来示范说明。本教程的最终结果可以在[这里](https://github.com/EOSIO/eos/tree/master/contracts/tic_tac_toe)找到。

### Assumption | 假设

For this game, we are using a standard 3x3 tic tac toe board. Players are divided into two roles: **host** and **challenger**. Host always makes the first move. Each pair of players can **ONLY** have up to two games at the same time, one where the first player become the host and the other one where the second player become the host. 

对于这个游戏，我们使用标准的 3x3 井字棋盘。 玩家被分为两个角色：**东道主**和**挑战者**。东道主总是先走第一步。每对玩家最多**只能**同时进行两场比赛，一场是第一位玩家成为东道主，另一场是第二位玩家成为东道主。

#### Board | 棋盘
Instead of using `o` and `x` as in the traditional tic tac toe game. We use `1` to denote movement by host, `2` to denote movement by challenger, and `0` to denote empty cell. Furthermore, we will use one dimensional array to store the board. Hence:

并非像传统井字游戏那样使用 “o” 和 “x”，我们使用 `1` 表示东道主的落子，`2` 表示挑战者的落子，`0` 表示棋盘空格。此外，我们将使用一维数组来存储棋盘。因此：

|           | (0,0) | (1,0) | (2,0) |
| :-------: | :---: | :---: | :---: |
| **(0,0)** | -     | o     | x     |
| **(0,1)** | -     | x     | -     |
| **(0,2)** | x     | o     | o     |

Assuming x is host, the above board is equal to `[0, 2, 1, 0, 1, 0, 1, 2, 2]`

假设 x 是东道主，上面的棋盘等价于 `[0, 2, 1, 0, 1, 0, 1, 2, 2]`

#### Action | 动作
User will have the following actions to interact with this contract:
- create: create a new game
- restart: restart an existing game, host/ challenger is allowed to do this
- close: close an existing game, which frees up the storage used to store the game, only host is allowed to do this 
- move: make a movement

用户将有以下动作与该合约交互：
- 创建：创建一个新的游戏
- 重启：重新启动一个现有的游戏，允许东道主/挑战者执行此操作
- 关闭：关闭现有的游戏，这将释放用于存储游戏的存储空间，只允许东道主执行此操作
- 落子：下一个棋子

#### Contract account | 合约帐户
For the following guide, we are going to push the contract to an account called `tic.tac.toe`. In case `tic.tac.toe` account name is already taken, you can also use another account by replacing any occurence of `tic.tac.toe` in the code with your account name. If you haven't create the account, please create the account first.

对于下面的指南，我们将把合约推送到一个名为 `tic.tac.toe` 的账户。如果 `tic.tac.toe` 帐户名已被占用，你也可以使用其他帐户，将代码中出现的任何 `tic.tac.toe` 替换为你的帐户名称。如果你还没有创建帐户，请先创建帐户。

```sh
$ eosc create account ${creator_name} ${contract_account_name} ${contract_pub_owner_key} ${contract_pub_active_key} --permission ${creator_name}@active
# e.g. $ eosc create account inita tic.tac.toe  EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA --permission inita@active
```

Ensure that you have your wallet unlocked and the creator's private active key in the wallet imported, otherwise the above command will fail.

确保你的钱包已解锁，而且钱包中的创建者的活动私钥已导入，否则上述命令将失败。

### Start! | 开始！
We are going to create three files here:
- tic_tac_toe.hpp => header file where the structure of the contract is defined
- tic_tac_toe.cpp => main logic of the contract
- tic_tac_toe.abi => interface for user to interact with the contract

我们将在这创建三个文件：
- tic_tac_toe.hpp => 定义合约结构的头文件
- tic_tac_toe.cpp => 合约的主要逻辑
- tic_tac_toe.abi => 用户与合约进行交互的接口

### Defining Structure | 定义结构
Let's first start with the header file and define the structure of the contract. Open **tic_tac_toe.hpp** and start with the following boilerplate

我们先从头文件开始，并定义合约的结构。打开 **tic_tac_toe.hpp**，并从下面的样板代码开始

```c
// Import necessary library
#include <eoslib/eos.hpp> // Generic eos library, i.e. print, type, math, etc
#include <eoslib/db.hpp> // Database access

using namespace eosio;
namespace tic_tac_toe {
    // Your code here
}
```

#### Games Table | 游戏表
For this contract, we will need to have a table that store list of games. Let's define it:

对于本合约，我们需要一个存储游戏列表的表。我们定义它为：

```c
...
namespace tic_tac_toe {
    ...
    using Games = eosio::table<N(tic.tac.toe),N(tic.tac.toe),N(games),game,uint64_t>;
}
  
```

NB: In case you upload the contract to other account `tic.tac.toe`, replace `tic.tac.toe` with your account name
- First template parameter  defines the default scope of the table, i.e. when a data is stored to this table without specifying the scope, it will fallback to this account
- Second template parameter defines the account that has write access to this table, in this case it's the contract account name
- Third template parameter defines the name of the table
- Fourth template parameter defines the structure that it stores (will be defined in the next section)
- Fifth template parameter defines the data type of the table's key

注意：如果你将合约上传到有别于 `tic.tac.toe` 的其他账户，请用该账户名称替换 `tic.tac.toe`
- 第一个模板参数定义了表的默认范围，即当数据存储到这个表中而没有指明范围时，它将回退到这个帐户
- 第二个模板参数定义了对该表具有写入权限的帐户，在本例中，它是合约帐户名称
- 第三个模板参数定义表的名称
- 第四个模板参数定义了它的存储结构（将在下一节中定义）
- 第五个模板参数定义了表的键的数据类型

#### Game Structure | 游戏结构
Let's define structure for the game. Ensure that this struct definition appears before the table definition in the code.

我们来定义游戏的结构。在代码中确保此结构的定义出现在表定义之前。

```c
...
namespace tic_tac_toe {
    struct PACKED(game) {
        // Default constructor
        game() {};
        // Constructor
        game(account_name challenger, account_name host):challenger(challenger), host(host), turn(host) {
            // Initialize board
            initialize_board();
        };
        // Account name of the challenger, this also acts as key of the table
        account_name     challenger;
        // Account name of the host
        account_name     host;
        // Whose turn it is, = account name of host/ challenger
        account_name     turn; // = account name of host/ challenger
        // Winner of the game, = none or draw or account name of host/ challenger
        account_name     winner = N(none); 
        // Length of the board array, this need to be placed immediately before the board array. It is needed so the abiserializer can pack/ unpack the array properly from/ to the database
        uint8_t          board_len = 9;
        // Board array
        uint8_t          board[9]; 

        // Initialize board with empty cell
        void initialize_board() {
            for (uint8_t i = 0; i < board_len ; i++) {
            board[i] = 0;
            }
        }

        // Reset game
        void reset_game() {
            initialize_board();
            turn = host;
            winner = N(none);
        }
    };
    ...
}
```

Remember that in the previous table definition, we declare `uint64_t` as the data type of the table's key. Hence, for the above game structure, the first `sizeof(uint64_t)` bytes of the structure will be treated as the table's key. By the way, `account_name` is just an alias for `uint64_t`.

请记住，在之前的表定义中，我们声明 `uint64_t` 作为表的键的数据类型。 因此，对于上述的游戏结构，开头 `sizeof(uint64_t)` 个字节被视为表的键。 顺便一提，`account_name` 只是 `uint64_t` 的别名。

#### Action Structure | 动作结构
##### Create | 新建
To create the game, we need host account name and challenger's account name

要新建游戏，我们需要东道主帐户名称和挑战者帐户名称

```c
...
namespace tic_tac_toe {
    ...
    struct create {
        account_name   challenger;
        account_name   host;
    };
    ...
}
```

##### Restart | 重启
To restart the game, we need host account name and challenger's account name to identify the game. Furthermore, we need to specify who want to restart the game, so we can verify the correct signature is provided.

要重新启动游戏，我们需要东道主帐户名称和挑战者帐户名称来识别游戏。此外，我们需要指定是谁想要重启游戏，由此我们可以验证是否提供了正确的签名。

```c
...
namespace tic_tac_toe {
    ...
    struct restart {
        account_name   challenger;
        account_name   host;
        account_name   by;
    };
    ...
}
```

##### Close | 关闭
To close the game, we need host account name and challenger's account name to identify the game.

要关闭游戏，我们需要东道主帐户名称和挑战者帐户名称来识别游戏。

```c
...
namespace tic_tac_toe {
    ...
    struct close {
        account_name   challenger;
        account_name   host;
    };
    ...
}
```

##### Move | 落子
To make a move, we need host account name and challenger's account name to identify the game. Furthermore, we need to specify who makes this move and the movement he is making.

要落一子，我们需要东道主帐户名称和挑战者帐户名称来识别游戏。 此外，我们需要指定是谁在落子，以及他正在落什么子。

```c
...
namespace tic_tac_toe {
    ...
    struct movement {
        uint32_t    row;
        uint32_t    column;
    };

    struct Move {
        account_name   challenger;
        account_name   host;
        account_name   by; // the account who wants to make the move
        movement       m;
    };
    ...
}
```

You can see the final tic_tac_toe.hpp [here](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe/tic_tac_toe.hpp)

你可以在[这里](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe/tic_tac_toe.hpp)看到最终的 tic_tac_toe.hpp

### Main | 主程序
Let's open tic_tac_toe.cpp and setup the boilerplate

让我们打开 tic_tac_toe.cpp 并设置样板代码

```c
#include <tic_tac_toe.hpp>
using namespace eosio;
/**
*  The init() and apply() methods must have C calling convention so that the blockchain can lookup and
*  call these methods.
*/
extern "C" {

  // Only called once
  void init()  {
  }

  /// The apply method implements the dispatch of events to this contract
  void apply( uint64_t code, uint64_t action_name ) {
      // Put your message handler here
  }

} // extern "C"
```

#### Message handler | 消息处理器
We want tic_tac_toe contract to only react to message send to `tic.tac.toe` account and react differently according to the type of the action. Let's set the message filter inside the apply function:

我们希望 tic_tac_toe 合约只对发送给 `tic.tac.toe` 帐户的消息作出反应，并根据行动的类型作出不同的反应。让我们在 apply 函数中设置消息过滤器：

```c
  ...
  void apply( uint64_t code, uint64_t action_name ) {
        if (code == N(tic.tac.toe)) {
            if (action_name == N(create)) {
                tic_tac_toe::apply_create(current_message<tic_tac_toe::create>());
            } else if (action_name == N(restart)) {
                tic_tac_toe::apply_restart(current_message<tic_tac_toe::restart>());
            } else if (action_name == N(close)) {
                tic_tac_toe::apply_close(current_message<tic_tac_toe::close>());
            } else if (action_name == N(move)) {
                tic_tac_toe::apply_move(current_message<tic_tac_toe::move>());
            }
        }
  }
  ...
```

Notice that we use `current_message<T>()` before passing it to specific handler, `current_message<T>()` is converting the message that the contract receives to `struct T`. 

NB: if you are deploying this contract to an account other than `tic.tac.toe`, replace `tic.tac.toe` with your account name.

To make things tidy, we will encapsulate the message handler inside `namespace tic_tac_toe`:

请注意，我们在将消息传递给指定的处理器之前使用了 `current_message<T>()`，此函数将合约收到的消息转换为 `struct T`。

注意：如果你将此合约部署到 `tic.tac.toe` 之外的帐户，请将 `tic.tac.toe` 替换为你的帐户名称。

为了保持简洁，我们在 `namespace tic_tac_toe` 中封装消息处理器：

```c
namespace tic_tac_toe {
  
  void apply_create(const create& c) {
    // Put code for create action here
  }

  void apply_restart(const restart& r) {
    // Put code for restart action here
  }

 
  void apply_close(const close& c) {
    // Put code for close action here
  }

  void apply_move(const move& m) {
    // Put code for move action here
  }
  ...
}

```

#### Create Message Handler | 新建棋局的消息处理器

For the create message handler, we want to:
1. Ensure that the message has signature from the host
2. Ensure that the game is not played by the same player
3. Ensure that there is no existing game
4. Store the newly created game into the db

对于新建棋局的消息处理器，我们希望：
1. 确保消息具有来自东道主的签名
2. 确保棋局不是由同一个玩家玩的
3. 确保没有已经存在的棋局
4. 将新创建棋局存储到数据库中

```c
namespace tic_tac_toe {
    ...
    void apply_create(const create& c) {
        require_auth(c.host);
        assert(c.challenger != c.host, "challenger shouldn't be the same as host");

        // Check if game already exists
        game existing_game;
        bool game_exists = Games::get(c.challenger, existing_game, c.host);
        assert(game_exists == false, "game already exists");

        game game_to_create(c.challenger, c.host);
        Games::store(game_to_create, c.host);
    }
    ...
}

```

#### Restart Message Handler | 重启棋局的消息处理器

For the create message handler, we want to:
1. Ensure that the message has signature from the host/ challenger
2. Ensure that the game exists
3. Ensure that the restart action is done by host/ challenger
4. Reset the game
5. Store the updated game to the db

对于重启的消息处理器，我们希望：
1. 确保消息具有来自东道主/挑战者的签名
2. 确保棋局存在
3. 确保重启操作由东道主/挑战者发起
4. 重置棋局
5. 将更新后的棋局存储到数据库中

```c
namespace tic_tac_toe {
    ...
    void apply_restart(const restart& r) {
        require_auth(r.by);

        // Check if game exists
        game game_to_restart;
        bool game_exists = Games::get(r.challenger, game_to_restart, r.host);
        assert(game_exists == true, "game doesn't exist!");

        // Check if this game belongs to the message sender
        assert(r.by == game_to_restart.host || r.by == game_to_restart.challenger, "this is not your game!");

        // Reset game
        game_to_restart.reset_game();

        Games::update(game_to_restart, game_to_restart.host);
    }
    ...
}

```

#### Close Message Handler | 结束棋局的消息处理程序

For the create message handler, we want to:
1. Ensure that the message has signature from the host
2. Ensure that the game exists
3. Remove the game from the db

对于结束棋局的消息处理器，我们希望：
1. 确保消息具有来自东道主的签名
2. 确保棋局存在
3. 从数据库中删除棋局

```c
namespace tic_tac_toe {
    ...
    void apply_close(const close& c) {
        require_auth(c.host);

        // Check if game exists
        game game_to_close;
        bool game_exists = Games::get(c.challenger, game_to_close, c.host);
        assert(game_exists == true, "game doesn't exist!");

        Games::remove(game_to_close, game_to_close.host);
    }
    ...
}

```

#### Move Message Handler | 落子消息的处理程序
For the move message handler, we want to:
1. Ensure that the message has signature from the host/ challenger
2. Ensure that the game exists
3. Ensure that the game is not finished yet
4. Ensure that the move action is done by host/ challenger
5. Ensure that this is the right user's turn
6. Verify movement is valid
7. Update board with the new move
8. Change the move_turn to the other player
9. Find the winner
10. Store the updated game to the db

对于落子的消息处理器，我们希望：
1. 确保消息具有来自东道主/挑战者的签名
2. 确保棋局存在
3. 确保棋局尚未完成
4. 确保落子操作由东道主/挑战者完成
5. 确保这是正确的用户在落子
6. 验证落子是否有效
7. 根据新的落子更新棋盘
8. 将 move_turn 更改为另一位玩家
9. 找到胜利者
10. 将更新后的游戏存储到数据库中

```c
namespace tic_tac_toe {
    ...
    bool is_valid_movement(const movement& mvt, const game& game_for_movement) {
    // Put code here
    }

    account_name get_winner(const game& current_game) {
        // Put code here
    }

    void apply_move(const move& m) {
        require_auth(m.by);

        // Check if game exists
        game game_to_move;
        bool game_exists = Games::get(m.challenger, game_to_move, m.host);
        assert(game_exists == true, "game doesn't exist!");

        // Check if this game hasn't ended yet
        assert(game_to_move.winner == N(none), "the game has ended!");
        // Check if this game belongs to the message sender
        assert(m.by == game_to_move.host || m.by == game_to_move.challenger, "this is not your game!");
        // Check if this is the  message sender's turn
        assert(m.by == game_to_move.turn, "it's not your turn yet!");


        // Check if user makes a valid movement
        assert(is_valid_movement(m.mvt, game_to_move), "not a valid movement!");

        // Fill the cell, 1 for host, 2 for challenger
        bool is_movement_by_host = m.by == game_to_move.host;
        if (is_movement_by_host) {
        game_to_move.board[m.mvt.row * 3 + m.mvt.column] = 1;
        game_to_move.turn = game_to_move.challenger;
        } else {
        game_to_move.board[m.mvt.row * 3 + m.mvt.column] = 2;
        game_to_move.turn = game_to_move.host;
        }
        // Update winner
        game_to_move.winner = get_winner(game_to_move);
        Games::update(game_to_move, game_to_move.host);
    }
    ...
}

```

#### Movement Validation | 验证落子的有效性
Valid movement is defined as movement done inside the board on an empty cell:

有效的落子被定义为在棋盘的空格内下子：

```c
namespace tic_tac_toe {
    ...
        bool is_empty_cell(const uint8_t& cell) {
            return cell == 0;
        }
        bool is_valid_movement(const movement& mvt, const game& game_for_movement) {
            uint32_t movement_location = mvt.row * 3 + mvt.column;
            bool is_valid = movement_location < game_for_movement.board_len && is_empty_cell(game_for_movement.board[movement_location]);
            return is_valid;
        }
    ...
}
```

#### Get Winner | 判断获胜者
Winner is defined as the first player who succeeds in placing three of their marks in a horizontal, vertical, or diagonal row.

获胜者被定义为第一个成功地将他们的三个标记放置在水平，垂直或对角线上的玩家。

```c
namespace tic_tac_toe {
    ...
    account_name get_winner(const game& current_game) {
        if((current_game.board[0] == current_game.board[4] && current_game.board[4] == current_game.board[8]) ||
        (current_game.board[1] == current_game.board[4] && current_game.board[4] == current_game.board[7]) ||
        (current_game.board[2] == current_game.board[4] && current_game.board[4] == current_game.board[6]) ||
        (current_game.board[3] == current_game.board[4] && current_game.board[4] == current_game.board[5])) {
            //  - | - | x    x | - | -    - | - | -    - | x | -
            //  - | x | -    - | x | -    x | x | x    - | x | -
            //  x | - | -    - | - | x    - | - | -    - | x | -
            if (current_game.board[4] == 1) {
                return current_game.host;
            } else if (current_game.board[4] == 2) {
                return current_game.challenger;
            }
        } else if ((current_game.board[0] == current_game.board[1] && current_game.board[1] == current_game.board[2]) ||
                (current_game.board[0] == current_game.board[3] && current_game.board[3] == current_game.board[6])) {
            //  x | x | x       x | - | -
            //  - | - | -       x | - | -
            //  - | - | -       x | - | -
            if (current_game.board[0] == 1) {
                return current_game.host;
            } else if (current_game.board[0] == 2) {
                return current_game.challenger;
            }
        } else if ((current_game.board[2] == current_game.board[5] && current_game.board[5] == current_game.board[8]) ||
                (current_game.board[6] == current_game.board[7] && current_game.board[7] == current_game.board[8])) {
            //  - | - | -       - | - | x
            //  - | - | -       - | - | x
            //  x | x | x       - | - | x
            if (current_game.board[8] == 1) {
                return current_game.host;
            } else if (current_game.board[8] == 2) {
                return current_game.challenger;
            }
        } else {
            bool is_board_full = true;
            for (uint8_t i = 0; i < current_game.board_len; i++) {
                if (is_empty_cell(current_game.board[i])) {
                    is_board_full = false;
                    break;
                }
            }
            if (is_board_full) {
                return N(draw);
            }
        }
        return N(none);
    }
    ...
}
```

You can see the final tic_tac_toe.cpp [here](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe/tic_tac_toe.cpp)

你可以在[这里](https://github.com/EOSIO/eos/blob/master/contracts/tic_tac_toe/tic_tac_toe.cpp)看到最终的 tic_tac_toe.cpp

### Creating ABI | 创建ABI
Abi (a.k.a Application Binary Interface) is needed here, so the contract can understand the message that you send as binary.
Let's open tic_tac_toe.abi and defines the boilerplate here:

在这需要 Abi （也就是应用程序二进制接口），由此合约可以理解你以二进制的形式发送的消息。
让我们打开 tic_tac_toe.abi， 并在这定义样板代码：

```json
{
  "structs": [{
      "name": "...",
      "base": "...",
      "fields": { ... }
  }, ...],
  "actions": [{
      "action_name": "...",
      "type": "..."
  }, ...],
  "tables": [{
      "table_name": "...",
      "type": "...",
      "key_names" : [...],
      "key_types" : [...]
  }, ...]
```

- struct: list of data structure used by the action/ table in the contract
- actions: list of actions available in the contract
- tables: list of tables available in the contract

- 结构：合约中动作/表所使用的数据结构列表
- 动作：合约中可用的动作列表
- 表：合约中可用的表的列表

#### Table ABI | 表 ABI
Remember that in tic_tac_toe.hpp, we create an single index i64 table called games. It stores `game` structure and use `challenger` as the key, which data type is `account_name`. Hence, the abi will be:

回想一下，我们在 tic_tac_toe.hpp 中创建了一个名为 games 的 i64 索引表。它存储了 `game` 结构并使用 `challenger` 作为键，其数据类型是 `account_name`。 因此，该 abi 将为：

```json
{
    ...
    "structs": [{
      "name": "game",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name",
        "turn": "account_name",
        "winner": "account_name",
        "board": "uint8[]"
      }
    }],
    "tables": [{
            "table_name": "games",
            "type": "game",
            "index_type": "i64",
            "key_names" : ["challenger"],
            "key_types" : ["account_name"]
        }
    ]
    ...
}
```

#### Actions ABI | 动作 ABI
For the actions, we define the actions inside `actions` and the structure of the actions inside `structs`.

对于这些动作，我们在 `actions` 中定义了动作以及在 `structs` 中定义了动作的结构。

```json
{
    ...
    "structs": [{
      "name": "create",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name"
      }
    },{
      "name": "restart",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name",
        "by": "account_name"
      }
    },{
      "name": "close",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name"
      }
    },{
      "name": "movement",
      "base": "",
      "fields": {
        "row": "uint32",
        "column": "uint32"
      }
    },{
      "name": "move",
      "base": "",
      "fields": {
        "challenger": "account_name",
        "host": "account_name",
        "by": "account_name",
        "movement": "movement"
      }
    }],
  "actions": [{
      "action_name": "create",
      "type": "create"
    },{
      "action_name": "restart",
      "type": "restart"
    },{
      "action_name": "close",
      "type": "close"
    },{
      "action_name": "move",
      "type": "move"
    }
  ]
    ...
}
```

### Deploy! | 部署！
Now all the three files (tic_tac_toe.hpp, tic_tac_toe.cpp, tic_tac_toe.abi) are ready. Time to deploy!

现在所有的三个文件 (tic_tac_toe.hpp, tic_tac_toe.cpp, tic_tac_toe.abi) 都准备好了。是时候部署了！

```sh
$ eosc set contract tic.tac.toe tic_tac_toe.wast tic_tac_toe.abi
```

Ensure that your wallet is unlocked and you have `tic.tac.toe` key imported. If you are going to upload the contract to another account beside `tic.tac.toe`, replace `tic.tac.toe` with your account name and ensure you have the key for that account in your wallet

确保你的钱包已解锁，并且已经导入了 `tic.tac.toe` 的密钥。如果你打算将合约上传到 `tic.tac.toe` 之外的另一个帐户，请将 `tic.tac.toe` 替换为你的帐户名称，并确保你的钱包中有该帐户的密钥

### Play! | 玩！
After the deployment and the transaction is confirmed, the contract is already available in the blockchain. You can play with it now!

部署和交易确认后，合约在区块链中就可以使用了。现在你可以开玩了！

#### Create | 新建

```sh
$ eosc push message tic.tac.toe create '{"challenger":"inita", "host":"initb"}' -S initb -S tic.tac.toe -p initb@active 
```

#### Move | 落子

```sh
$ eosc push message tic.tac.toe move '{"challenger":"inita", "host":"initb", "by":"initb", "movement":{"row":0, "column":0} }' -S initb -S tic.tac.toe -p initb@active 
$ eosc push message tic.tac.toe move '{"challenger":"inita", "host":"initb", "by":"inita", "movement":{"row":1, "column":1} }' -S initb -S tic.tac.toe -p inita@active 
```

#### Restart | 重启

```sh
$ eosc push message tic.tac.toe restart '{"challenger":"inita", "host":"initb", "by":"initb"}' -S initb -S tic.tac.toe -p initb@active 
```

#### Close | 关闭

```sh
$ eosc push message tic.tac.toe close '{"challenger":"inita", "host":"initb"}' -S initb -S tic.tac.toe -p initb@active
```

#### See the game status | 查看棋局

```text
$ eosc get table initb tic.tac.toe games
{
  "rows": [{
      "challenger": "inita",
      "host": "initb",
      "turn": "inita",
      "winner": "none",
      "board": [
        1,
        0,
        0,
        0,
        2,
        0,
        0,
        0,
        0
      ]
    }
  ],
  "more": false
}
```

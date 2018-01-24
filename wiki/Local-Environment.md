# Local Environment
# 本地环境

>原文链接：<https://github.com/EOSIO/eos/wiki/Local-Environment>
>
>翻译：区块链中文字幕组 - [陈伟](https://github.com/weichen000)
>
> 翻译时间：2017-12-29

- [1 Getting the code 获取代码](#1-getting-the-code)
- [2 Building EOS 构建 EOS](#2-building-eos)
	- [2.1 Automated build script 自动构建脚本](#21-automated-build-script)
		- [2.1.1 Ubuntu 16.10](#211-ubuntu-1610)
		- [2.1.2 MacOS Sierra](#212-macos-sierra)
	- [2.2 Manual build script 手动构建脚本](#22-manual-build-script)
		- [2.2.1 Building from source code 从源代码构建](#221-building-from-source-code)
		- [2.2.2 Ubuntu 16.10](#222-clean-install-ubuntu-1610)
		- [2.2.3 MacOS Sierra 10.12.6](#223-macos-sierra-10126)
- [3 Docker](#3-docker)
	- [3.1 Install Dependencies 安装依赖包](#31-install-dependencies)
	- [3.2 Build eos image 构建 eos 映像文件](#32-build-eos-image)
	- [3.3 Start eosd docker container only 只启动 eosd 的 docker 容器](#33-start-eosd-docker-container-only)
	- [3.4 Get chain info 获得链信息](#34-get-chain-info)
	- [3.5 Start both eosd and walletd containers 启动 eosd 和 walletd 容器](#35-start-both-eosd-and-walletd-containers)
		- [3.5.1 Execute eosc commands 执行 eosc 命令集](#351-execute-eosc-commands)
		- [3.5.2 Change default configuration 改变默认设置](#352-change-default-configuration)
		- [3.5.3 Clearn data-dir 清除 data-dir](#353-clear-data-dir)
- [4 Creating and launching a single-node testnet](#4-creating-and-launching-a-single-node-testnet)
- [5 Troubleshooting Guide 故障排查指南](#5-troubleshooting-guide)


## 1. Getting the code
## 1. 获取代码
To download all of the code, download EOS source code and a recursion or two of submodules. The easiest way to get all of this is to do a recursive clone:

为了下载所有的代码，可以递归下载 EOS 或者下载 EOS 和两个子模块。下载所有代码最简单的方法是使用一个递归克隆：
```
$ git clone https://github.com/eosio/eos --recursive
```
If a repo is cloned without the --recursive flag, the submodules can be retrieved after the fact by running this command from within the repo:

如果在克隆版本库的时候并没有使用 --recursive 这个命令行参数，那么在下载完成以后可以通过在版本库中运行这个命令来获取子模块：
```
$ git submodule update --init --recursive
```
## 2. Building EOS
## 2. 构建EOS
### 2.1 Automated build script
### 2.1 自动构建脚本
For Ubuntu 16.10 and MacOS Sierra, there is an automated build script that can install all dependencies and builds EOS.

在`Ubuntu 16.10`版本和`MacOS Sierra`版本上，有一个可以安装所有依赖包并且构建 EOS 的自动构建脚本。

It is called build.sh with following inputs.
* architecture [ubuntu|darwin]
* optional mode [full|build]

这个脚本叫做 build.sh ，它有以下输入。
* 架构 【ubuntu|darwin】
* 可选模式 【full|build】

The first option determines which architecture the build script is run on "darwin" for MacOS and "ubuntu" for Ubuntu.

第一个可选项决定了构建脚本在哪个架构上运行。”darwin“ 代表`MacOS`，”ubuntu“ 代表`Ubuntu`。

The second optional input can be "full" or "build" where "build" only builds EOS while "full" installs all dependencies and builds EOS. When omitted then "full" is implied.

第二个可选输入可以是 ”full“ 或者是 ”build“ ，”build“ 只构建 EOS 而 ”full“ 先安装所有的依赖包然后再构建 EOS 。如果这个可选输入省略掉的话，默认值是 ”full“ 。

```
$ ./build.sh ${architecture} ${optional_mode}
```
Clone EOS repository recursively as below and run build.sh located in root eos folder.

按以下命令递归克隆 EOS 仓库并且运行位于 eos 根目录下的 build.sh 文件。

#### 2.1.1. Ubuntu 16.10
#### Full build
#### 完整构建
```
$ git clone https://github.com/eosio/eos --recursive
$ cd eos
$ ./build.sh ubuntu full
```
#### Incremental build
#### 增量构建
```
$ git clone https://github.com/eosio/eos --recursive

$ cd eos
$ ./build.sh ubuntu
```
Proceed to the next step, [Creating and launching a single-node testnet](#4-creating-and-launching-a-single-node-testnet)

进入下一步，[建立和启动一个单节点的测试网络](#4-creating-and-launching-a-single-node-testnet)
#### 2.1.2. MacOS Sierra
Before running the script make sure you have updated XCode and brew:

在运行脚本之前确保你更新了 XCode 和 brew ：
```
$ xcode-select --install
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
#### Full build
#### 完整构建
```
$ git clone https://github.com/eosio/eos --recursive
$ cd eos
$ build.sh darwin full
```
#### Incremental build
#### 增量构建
```
$ git clone https://github.com/eosio/eos --recursive
$ cd eos
$ build.sh darwin
```
Proceed to the next step, [Creating and launching a single-node testnet](#4-creating-and-launching-a-single-node-testnet)

进入下一步，[建立和启动一个单节点的测试网络](#4-creating-and-launching-a-single-node-testnet)
### 2.2. Manual build script
### 2.2. 手动构建脚本
#### 2.2.1 Building from source code
#### 2.2.1 从源代码构建
It is recommended to build by using build.sh, as explained above. But if you would like to build by your own, please follow the steps below:

如上所述，推荐使用 build.sh 脚本来构建。但是如果你要自己构建的话，请按以下步骤进行：

The *WASM_LLVM_CONFIG* environment variable is used to find our recently built WASM compiler. This is needed to compile the example contracts inside eos/contracts folder and their respective tests.

*WASM_LLVM_CONFIG* 这个环境变量是用来发现我们最近构建的 WASM 编译器的。在编译 eos/contracts 文件夹里的合约用例和他们各自的测试用例时需要用到这个变量。
```
$ cd ~
$ git clone https://github.com/eosio/eos --recursive
$ mkdir -p ~/eos/build && cd ~/eos/build
$ cmake -DBINARYEN_BIN=~/binaryen/bin -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl -DOPENSSL_LIBRARIES=/usr/local/opt/openssl/lib ..
$ make -j4
```
Out-of-source builds are also supported. To override clang's default choice in compiler, add these flags to the CMake command:

EOS 也支持源码外构建。为了覆盖在编译器里的 clang 的默认选择，把这些命令行参数加到 Cmake 的命令中去：
```
-DCMAKE_CXX_COMPILER=/path/to/c++ -DCMAKE_C_COMPILER=/path/to/cc
```
For a debug build, add `-DCMAKE_BUILD_TYPE=Debug`. Other common build types include `Release` and `RelWithDebInfo`.

如果是调试类型构建的话，加入命令行参数 `-DCMAKE_BUILD_TYPE=Debug`。其他常用的构建类型是 `Release` 和 `RelWithDebInfo`。

To run the test suite after building, run the `chain_test` executable in the `tests` folder.

构建之后，运行在`tests`文件夹中的`chain_test`可执行文件来运行测试套例。

EOS comes with a number of programs you can find in `~/eos/build/programs`. They are listed below:
* eosd - server-side blockchain node component
* eosc - command line interface to interact with the blockchain
* eos-walletd - EOS wallet
* launcher - application for nodes network composing and deployment; [more on launcher](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Private#the-launcher-application)

EOS 自带一些程序，这些程序你可以在 `~/eos/build/programs` 文件夹里面找到。它们是以下程序：
* eosd - 服务器端区块链节点组件
* eosc - 命令行接口，可用于和区块链互动
* eos-walletd - EOS 钱包
* launcher - 节点网络编写和部署的应用; [关于 launcher 的更多信息](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Private#the-launcher-application)

Manual installation of the dependencies
手动安装依赖包

If you prefer to manually build dependencies - follow the steps below.

如果你想要手动构建依赖包 - 请按以下步骤进行。

This project is written primarily in C++14 and uses CMake as its build system. An up-to-date Clang and the latest version of CMake is recommended.

这个项目主要是用 C++14 编写的，并且使用了 CMake 作为它的构建系统。推荐使用最新的 Clang 和最新版本的 CMake。

Dependencies:

* Clang 4.0.0
* CMake 3.5.1
* Boost 1.64
* OpenSSL
* LLVM 4.0
* [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)
* [binaryen](https://github.com/WebAssembly/binaryen.git)

#### 2.2.2 Clean install Ubuntu 16.10
#### 2.2.2 全新安装 `Ubuntu 16.10`

Install the development toolkit:

安装开发工具包：

```
$ sudo apt-get update
$ wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
$ sudo apt-get install clang-4.0 lldb-4.0 libclang-4.0-dev cmake make \
                     libbz2-dev libssl-dev libgmp3-dev \
                     autotools-dev build-essential \
                     libbz2-dev libicu-dev python-dev \
                     autoconf libtool git
```

Install Boost 1.64:

安装 `Boost 1.64` ：
```
$ cd ~
$ wget -c 'https://sourceforge.net/projects/boost/files/boost/1.64.0/boost_1_64_0.tar.bz2/download' -O boost_1.64.0.tar.bz2
$ tar xjf boost_1.64.0.tar.bz2
$ cd boost_1_64_0/
$ echo "export BOOST_ROOT=$HOME/opt/boost_1_64_0" >> ~/.bash_profile
$ source ~/.bash_profile
$ ./bootstrap.sh "--prefix=$BOOST_ROOT"
$ ./b2 install
$ source ~/.bash_profile
```

Install [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git):

安装[secp256k1-zkp (Cryptonomex 分支)](https://github.com/cryptonomex/secp256k1-zkp.git):

```
$ cd ~
$ git clone https://github.com/cryptonomex/secp256k1-zkp.git
$ cd secp256k1-zkp
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
```

To use the WASM compiler, EOS has an external dependency on [binaryen](https://github.com/WebAssembly/binaryen.git):

为了用 WASM 编译器，EOS 需要一个外部依赖 [binaryen](https://github.com/WebAssembly/binaryen.git)

```
$ cd ~
$ git clone https://github.com/WebAssembly/binaryen.git
$ cd ~/binaryen
$ git checkout tags/1.37.14
$ cmake . && make
```

Add `BINARYEN_ROOT` to your .bash_profile:

把 `BINARYEN_ROOT` 加到你的 .bash_profile 文件里面：

```
$ echo "export BINARYEN_ROOT=~/binaryen" >> ~/.bash_profile
$ source ~/.bash_profile
```

By default LLVM and clang do not include the WASM build target, so you will have to build it yourself:

LLVM 和 clang 默认是不包括 WASM 的构建目标， 因此你必须自己构建它：

```
$ mkdir  ~/wasm-compiler
$ cd ~/wasm-compiler
$ git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
$ cd llvm/tools
$ git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
$ cd ..
$ mkdir build
$ cd build
$ cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
$ make -j4 install
```

Your environment is set up. Now you can [build EOS and run a node](#4-creating-and-launching-a-single-node-testnet).

你的环境已经设置好了。现在你可以[构建 EOS 并且运行一个节点](#4-creating-and-launching-a-single-node-testnet)

#### 2.2.3 MacOS Sierra 10.12.6

macOS additional Dependencies:

* Brew
* Newest XCode

`macOS` 额外的依赖包：

* Brew
* 最新的 XCode

Upgrade your XCode to the newest version:

升级你的 XCode 到最新版本：

```
$ xcode-select --install
```

Install homebrew:
安装 homebrew:

```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Install the dependencies:

安装依赖包：

```
$ brew update
$ brew install git automake libtool boost openssl llvm@4 gmp ninja gettext
$ brew link gettext --force
```

Install [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git):

安装[secp256k1-zkp (Cryptonomex 分支)](https://github.com/cryptonomex/secp256k1-zkp.git):

```
$ cd ~
$ git clone https://github.com/cryptonomex/secp256k1-zkp.git
$ cd secp256k1-zkp
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
```

Install [binaryen v1.37.14](https://github.com/WebAssembly/binaryen.git)

安装 [binaryen v1.37.14](https://github.com/WebAssembly/binaryen.git)

```
$ cd ~
$ git clone https://github.com/WebAssembly/binaryen.git
$ cd ~/binaryen
$ git checkout tags/1.37.14
$ cmake . && make
```

Add `BINARYEN_ROOT` to your .bash_profile:

把 `BINARYEN_ROOT` 加到你的 .bash_profile 文件中去：

```
$ echo "export BINARYEN_ROOT=~/binaryen" >> ~/.bash_profile
$ source ~/.bash_profile
```

Build LLVM and clang for WASM:

为了 WASM 构建 LLVM 和 clang ：

```
$ mkdir  ~/wasm-compiler
$ cd ~/wasm-compiler
$ git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
$ cd llvm/tools
$ git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
$ cd ..
$ mkdir build
$ cd build
$ cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
$ make -j4 install
```

Add `WASM_LLVM_CONFIG` and `LLVM_DIR` to your `.bash_profile`:

把 `WASM_LLVM_CONFIG` 和 `LLVM_DIR` 加到你的 `.bash_profile` 文件中去：

```
$ echo "export WASM_LLVM_CONFIG=~/wasm-compiler/llvm/bin/llvm-config" >> ~/.bash_profile
$ echo "export LLVM_DIR=/usr/local/Cellar/llvm/4.0.1/lib/cmake/llvm" >> ~/.bash_profile
$ source ~/.bash_profile
```

## 3. Docker

Simple and fast setup of EOS on Docker is also available.

在 Docker 上简单快速的设置 EOS 也可以。

### 3.1. Install Dependencies

* [Docker](https://docs.docker.com/) Docker 17.05 or higher is required

### 3.1. 安装依赖包

* [Docker](https://docs.docker.com/) 需要 Docker 17.05 或以上版本

### 3.2. Build eos image
### 3.2. 构建 eos 映像文件

```
$ git clone https://github.com/EOSIO/eos.git --recursive
$ cd eos/Docker
$ docker build . -t eosio/eos
```

### 3.3. Start eosd docker container only
### 3.3. 只启动 eosd 的 docker 容器

```
$ docker run --name eosd -p 8888:8888 -p 9876:9876 -t eosio/eos start_eosd.sh arg1 arg2
```

By default, all data is persisted in a docker volume. It can be deleted if the data is outdated or corrupted:

默认设置是，所有的数据保存在一个 docker 数据卷上。 如果数据太老了或者损坏了数据卷可以被删除。

```
$ docker inspect --format '{{ range .Mounts }}{{ .Name }} {{ end }}' eosd
fdc265730a4f697346fa8b078c176e315b959e79365fc9cbd11f090ea0cb5cbc
$ docker volume rm fdc265730a4f697346fa8b078c176e315b959e79365fc9cbd11f090ea0cb5cbc
```

Alternately, you can directly mount host directory into the container

另一种方法是，你可以把保存目录直接挂载在容器里

```
$ docker run --name eosd -v /path-to-data-dir:/opt/eos/bin/data-dir -p 8888:8888 -p 9876:9876 -t eosio/eos start_eosd.sh arg1 arg2
```

### 3.4. Get chain info
### 3.4. 获得链信息

```
$ curl http://127.0.0.1:8888/v1/chain/get_info
```

### 3.5. Start both eosd and walletd containers
### 3.5. 启动 eosd 和 walletd 容器

```
$ docker-compose up
```

After `docker-compose up`, two services named eosd and walletd will be started. eosd service will expose ports 8888 and 9876 to the host. walletd service does not expose any port to the host, it is only accessible to eosc when runing eosc is running inside the walletd container as described in "Execute eosc commands" section.

在 `docker-compose up` 命令运行以后，名为 eosd 和 walletd 的两个服务也将被启动。 eosd 服务将会向主机暴露端口8888和9876。walletd 服务对主机不暴露任何端口，只有 eosc 才可以接触到这个服务，而且仅仅是在 eosc 运行在和 walletd 同一个容器中的时候。 这些信息可以在 “执行 eosc 命令集” 章节中找到。

#### 3.5.1. Execute eosc commands
#### 3.5.1. 执行 eosc 命令集

You can run the eosc commands via a bash alias.

你可以通过 bash 别名来运行 eosc 命令集。

```
$ alias eosc='docker-compose exec walletd /opt/eos/bin/eosc -H eosd'
$ eosc get info
$ eosc get account inita
```

Upload sample exchange contract

上传交易所合约示例

```
$ eosc set contract exchange contracts/exchange/exchange.wast contracts/exchange/exchange.abi
```

If you don't need walletd afterwards, you can stop the walletd service using

如果你之后不需要 walletd 了，你可以使用以下命令停止 walletd 服务

```
$ docker-compose stop walletd
```

#### 3.5.2. Change default configuration
#### 3.5.2. 改变默认设置

You can use docker compose override file to change the default configurations. For example, create an alternate config file `config2.ini` and a `docker-compose.override.yml` with the following content.

你可以用 docker compose 覆盖文件来改变默认设置。比如说，创建一个替代的配置文件 `config2.ini` 和 一个 `docker-compose.override.yml` 文件， 这个文件内容如下：

```
version: "2"

services:
  eosd:
    volumes:
      - eosd-data-volume:/opt/eos/bin/data-dir
      - ./config2.ini:/opt/eos/bin/data-dir/config.ini
```

Then restart your docker containers as follows:

然后用以下命令重启你的 docker 容器：

```
$ docker-compose down
$ docker-compose up
```

#### 3.5.3. Clear data-dir
#### 3.5.3. 清除 data-dir

The data volume created by docker-compose can be deleted as follows:

docker-compose 创建的数据卷可以用以下命令删除：

```
$ docker volume rm docker_eosd-data-volume
```

## 4. Creating and launching a single-node testnet
## 4. 创建和启动一个单节点的测试网络

After successfully building the project, the `eosd` binary should be present in the `build/programs/eosd` directory. Go ahead and run `eosd` -- it will probably exit with an error, but if not, close it immediately with `Ctrl-C`. Note that `eosd` created a directory named `data-dir` containing the default configuration (`config.ini`) and some other internals. This default data storage path can be overridden by passing `--data-dir /path/to/data` to `eosd`.

在成功构建项目以后，`eosd` 的二进制文件应该出现在 `build/programs/eosd` 文件夹中。 现在运行 `eosd` -- 可能它会出错并且退出，但是如果没有的话，也马上用 `Ctrl-C` 来把它关掉。注意 `eosd` 创建了一个叫做 `data-dir` 的文件夹，其中有默认配置文件 （`config.ini`）和一些其他的内部文件。默认的数据存储路径可以通过在 `eosd` 上加一个参数 `--data-dir /path/to/data` 来覆盖。

Edit the `config.ini` file, adding the following settings to the defaults already in place:

编辑 `config.ini` 文件， 把以下设置加到已经在这个文件里的设置后面：

```
# Load the testnet genesis state, which creates some initial block producers with the default key
genesis-json = /path/to/eos/source/genesis.json
 # Enable production on a stale chain, since a single-node test chain is pretty much always stale
enable-stale-production = true
# Enable block production with the testnet producers
producer-name = inita
producer-name = initb
producer-name = initc
producer-name = initd
producer-name = inite
producer-name = initf
producer-name = initg
producer-name = inith
producer-name = initi
producer-name = initj
producer-name = initk
producer-name = initl
producer-name = initm
producer-name = initn
producer-name = inito
producer-name = initp
producer-name = initq
producer-name = initr
producer-name = inits
producer-name = initt
producer-name = initu
# Load the block producer plugin, so you can produce blocks
plugin = eosio::producer_plugin
# Wallet plugin
plugin = eosio::wallet_api_plugin
# As well as API and HTTP plugins
plugin = eosio::chain_api_plugin
plugin = eosio::http_plugin
```

Now it should be possible to run `eosd` and see it begin producing blocks.

现在应该可以运行 `eosd` 并且观察到它开始产生区块了。

When running `eosd` you should get log messages similar to below. It means the blocks are successfully produced.

当运行 `eosd` 的时候你应该看到和以下类似的日志消息。 这表明区块成功的产生了。

```
1575001ms thread-0   chain_controller.cpp:235      _push_block          ] initm #1 @2017-09-04T04:26:15  | 0 trx, 0 pending, exectime_ms=0
1575001ms thread-0   producer_plugin.cpp:207       block_production_loo ] initm generated block #1 @ 2017-09-04T04:26:15 with 0 trxs  0 pending
1578001ms thread-0   chain_controller.cpp:235      _push_block          ] initc #2 @2017-09-04T04:26:18  | 0 trx, 0 pending, exectime_ms=0
1578001ms thread-0   producer_plugin.cpp:207       block_production_loo ] initc generated block #2 @ 2017-09-04T04:26:18 with 0 trxs  0 pending
...
```

## 5. Troubleshooting Guide
## 5. 故障排查指南

1) *You get an error such as `St9exception: content of memory does not match data expected by executable` when trying to start `eosd`*

1) *当你试图运行 `eosd` 的时候得到一个错误 `St9exception: content of memory does not match data expected by executable`*

> Try restarting `eosd` with `--resync`

> 尝试重启 `eosd` 并且使用选项 `--resync`

2) How do I find which version of `eosd` I'm running or connecting to?

2) 我如何发现我运行的或者是我连接的 'eosd' 是哪个版本？

> Use `eosc -H ${eosd_host} -p ${eosd_port} get info` and you will see the version number in the field called `server_version`

> 使用 `eosc -H ${eosd_host} -p ${eosd_port} get info` 然后你会在一个叫 `server_version` 的字段里看到版本号

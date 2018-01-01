* [1 Getting the code](#1-getting-the-code)
* [2 Building EOS](#2-building-eos)
  - [2.1 Automated build script](#21-automated-build-script)
    + [2.1.1 Ubuntu 16.10](#211-ubuntu-1610)
    + [2.1.2 MacOS Sierra](#212-macos-sierra)
  - [2.2 Manual build script](#22-manual-build-script)
    + [2.2.1 Building from source code](#221-building-from-source-code)
    + [2.2.2 Ubuntu 16.10](#222-clean-install-ubuntu-1610)
    + [2.2.3 MacOS Sierra 10.12.6](#223-macos-sierra-10126)
* [3 Docker](#3-docker)
  - [3.1 Install Dependencies](#31-install-dependencies)
  - [3.2 Build eos image](#32-build-eos-image)
  - [3.3 Start eosd docker container only](#33-start-eosd-docker-container-only)
  - [3.4 Get chain info](#34-get-chain-info)
  - [3.5 Start both eosd and walletd containers](#35-start-both-eosd-and-walletd-containers)
    + [3.5.1 Execute eosc commands](#351-execute-eosc-commands)
    + [3.5.2 Change default configuration](#352-change-default-configuration)
    + [3.5.3 Clear data-dir](#353-clear-data-dir)
* [4 Creating and launching a single-node testnet](#4-creating-and-launching-a-single-node-testnet)
* [5 Troubleshooting Guide](#5-troubleshooting-guide)
    

## 1. Getting the code 

To download all of the code, download EOS source code and a recursion or two of submodules. The easiest way to get all of this is to do a recursive clone:

```bash
$ git clone https://github.com/eosio/eos --recursive
```

If a repo is cloned without the `--recursive` flag, the submodules can be retrieved after the fact by running this command from within the repo:

```bash
$ git submodule update --init --recursive
```
   
## 2. Building EOS

### 2.1. Automated build script

For Ubuntu 16.10 and MacOS Sierra, there is an automated build script that can install all dependencies and builds EOS.

It is called build.sh with following inputs.
- architecture [ubuntu|darwin]
- optional mode [full|build] 

The first option determines which architecture the build script is run on "darwin" for MacOS and "ubuntu" for Ubuntu.

The second optional input can be "full" or "build" where "build" only builds EOS while "full" installs all dependencies and builds EOS. When omitted then "full" is implied.

```bash
$ ./build.sh ${architecture} ${optional_mode}
```
Clone EOS repository recursively as below and run build.sh located in root `eos` folder.

#### 2.1.1. Ubuntu 16.10 
**Full build**
```bash
$ git clone https://github.com/eosio/eos --recursive
$ cd eos
$ ./build.sh ubuntu full 
```
**Incremental build**
```bash
$ git clone https://github.com/eosio/eos --recursive

$ cd eos
$ ./build.sh ubuntu 
```

Proceed to the next step, [Creating and launching a single-node testnet](#4-creating-and-launching-a-single-node-testnet)

#### 2.1.2. MacOS Sierra
Before running the script make sure you have updated XCode and brew:
```bash
$ xcode-select --install
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**Full build**
```bash
$ git clone https://github.com/eosio/eos --recursive
$ cd eos
$ build.sh darwin full
```

**Incremental build**
```bash
$ git clone https://github.com/eosio/eos --recursive
$ cd eos
$ build.sh darwin
```

Proceed to the next step, [Creating and launching a single-node testnet](#4-creating-and-launching-a-single-node-testnet)



### 2.2. Manual build script

#### 2.2.1 Building from source code 
It is recommended to build by using build.sh, as explained above. But if you would like to build by your own, please follow the steps below:

The *WASM_LLVM_CONFIG* environment variable is used to find our recently built WASM compiler.
This is needed to compile the example contracts inside `eos/contracts` folder and their respective tests.

```bash
$ cd ~
$ git clone https://github.com/eosio/eos --recursive
$ mkdir -p ~/eos/build && cd ~/eos/build
$ cmake -DBINARYEN_BIN=~/binaryen/bin -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl -DOPENSSL_LIBRARIES=/usr/local/opt/openssl/lib ..
$ make -j4
```

Out-of-source builds are also supported. To override clang's default choice in compiler, add these flags to the CMake command:

`-DCMAKE_CXX_COMPILER=/path/to/c++ -DCMAKE_C_COMPILER=/path/to/cc`

For a debug build, add `-DCMAKE_BUILD_TYPE=Debug`. Other common build types include `Release` and `RelWithDebInfo`.

To run the test suite after building, run the `chain_test` executable in the `tests` folder.

EOS comes with a number of programs you can find in `~/eos/build/programs`. They are listed below:

* eosd - server-side blockchain node component
* eosc - command line interface to interact with the blockchain
* eos-walletd - EOS wallet
* launcher - application for nodes network composing and deployment; [more on launcher](Testnet%3A%20Private#the-launcher-application)

Manual installation of the dependencies

If you prefer to manually build dependencies - follow the steps below.

This project is written primarily in C++14 and uses CMake as its build system. An up-to-date Clang and the latest version of CMake is recommended.

Dependencies:

* Clang 4.0.0
* CMake 3.5.1
* Boost 1.64
* OpenSSL
* LLVM 4.0
* [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)
* [binaryen](https://github.com/WebAssembly/binaryen.git)


### 2.2.2 Clean install Ubuntu 16.10 

Install the development toolkit:

```bash
$ sudo apt-get update
$ wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
$ sudo apt-get install clang-4.0 lldb-4.0 libclang-4.0-dev cmake make \
                     libbz2-dev libssl-dev libgmp3-dev \
                     autotools-dev build-essential \
                     libbz2-dev libicu-dev python-dev \
                     autoconf libtool git
```

Install Boost 1.64:

```bash
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
        
```bash
$ cd ~
$ git clone https://github.com/cryptonomex/secp256k1-zkp.git
$ cd secp256k1-zkp
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
```

To use the WASM compiler, EOS has an external dependency on [binaryen](https://github.com/WebAssembly/binaryen.git):

```bash
$ cd ~
$ git clone https://github.com/WebAssembly/binaryen.git
$ cd ~/binaryen
$ git checkout tags/1.37.14
$ cmake . && make
```

Add `BINARYEN_ROOT` to your .bash_profile:

```bash
$ echo "export BINARYEN_ROOT=~/binaryen" >> ~/.bash_profile
$ source ~/.bash_profile
```

By default LLVM and clang do not include the WASM build target, so you will have to build it yourself:

```bash
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
Your environment is set up. Now you can [build EOS and run a node](Local-Environment#4-creating-and-launching-a-single-node-testnet)</a>. 

### 2.2.3 MacOS Sierra 10.12.6 

macOS additional Dependencies:

* Brew
* Newest XCode

Upgrade your XCode to the newest version:

```bash
$ xcode-select --install
```

Install homebrew:

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Install the dependencies:

```bash
$ brew update
$ brew install git automake libtool boost openssl llvm@4 gmp ninja gettext
$ brew link gettext --force
```

Install [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git):
        
```bash
$ cd ~
$ git clone https://github.com/cryptonomex/secp256k1-zkp.git
$ cd secp256k1-zkp
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
```

Install [binaryen v1.37.14](https://github.com/WebAssembly/binaryen.git):

```bash
$ cd ~
$ git clone https://github.com/WebAssembly/binaryen.git
$ cd ~/binaryen
$ git checkout tags/1.37.14
$ cmake . && make
```

Add `BINARYEN_ROOT` to your .bash_profile:

```bash
$ echo "export BINARYEN_ROOT=~/binaryen" >> ~/.bash_profile
$ source ~/.bash_profile
```


Build LLVM and clang for WASM:

```bash
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

```bash
$ echo "export WASM_LLVM_CONFIG=~/wasm-compiler/llvm/bin/llvm-config" >> ~/.bash_profile
$ echo "export LLVM_DIR=/usr/local/Cellar/llvm/4.0.1/lib/cmake/llvm" >> ~/.bash_profile
$ source ~/.bash_profile
```



## 3. Docker

Simple and fast setup of EOS on Docker is also available.

### 3.1. Install Dependencies
 - [Docker](https://docs.docker.com) Docker 17.05 or higher is required

### 3.2. Build eos image

```bash
$ git clone https://github.com/EOSIO/eos.git --recursive
$ cd eos/Docker
$ docker build . -t eosio/eos
```

### 3.3. Start eosd docker container only

```bash
$ docker run --name eosd -p 8888:8888 -p 9876:9876 -t eosio/eos start_eosd.sh arg1 arg2
```

By default, all data is persisted in a docker volume. It can be deleted if the data is outdated or corrupted:
``` bash
$ docker inspect --format '{{ range .Mounts }}{{ .Name }} {{ end }}' eosd
fdc265730a4f697346fa8b078c176e315b959e79365fc9cbd11f090ea0cb5cbc
$ docker volume rm fdc265730a4f697346fa8b078c176e315b959e79365fc9cbd11f090ea0cb5cbc
```

Alternately, you can directly mount host directory into the container
```bash
$ docker run --name eosd -v /path-to-data-dir:/opt/eos/bin/data-dir -p 8888:8888 -p 9876:9876 -t eosio/eos start_eosd.sh arg1 arg2
```

### 3.4. Get chain info

```bash
$ curl http://127.0.0.1:8888/v1/chain/get_info
```

### 3.5. Start both eosd and walletd containers

```bash
$ docker-compose up
```

After `docker-compose up`, two services named eosd and walletd will be started. eosd service will expose ports 8888 and 9876 to the host. walletd service does not expose any port to the host, it is only accessible to eosc when runing eosc is running inside the walletd container as described in "Execute eosc commands" section.


#### 3.5.1. Execute eosc commands

You can run the `eosc` commands via a bash alias.

```bash
$ alias eosc='docker-compose exec walletd /opt/eos/bin/eosc -H eosd'
$ eosc get info
$ eosc get account inita
```

Upload sample exchange contract

```bash
$ eosc set contract exchange contracts/exchange/exchange.wast contracts/exchange/exchange.abi
```

If you don't need walletd afterwards, you can stop the walletd service using

```bash
$ docker-compose stop walletd
```
#### 3.5.2. Change default configuration

You can use docker compose override file to change the default configurations. For example, create an alternate config file `config2.ini` and a `docker-compose.override.yml` with the following content.

```yaml
version: "2"

services:
  eosd:
    volumes:
      - eosd-data-volume:/opt/eos/bin/data-dir
      - ./config2.ini:/opt/eos/bin/data-dir/config.ini
```

Then restart your docker containers as follows:

```bash
$ docker-compose down
$ docker-compose up
```

#### 3.5.3. Clear data-dir
The data volume created by docker-compose can be deleted as follows:

```bash
$ docker volume rm docker_eosd-data-volume
```

## 4. Creating and launching a single-node testnet 

After successfully building the project, the `eosd` binary should be present in the `build/programs/eosd` directory. Go ahead and run `eosd` -- it will probably exit with an error, but if not, close it immediately with <kbd>Ctrl-C</kbd>. Note that `eosd` created a directory named `data-dir` containing the default configuration (`config.ini`) and some other internals. This default data storage path can be overridden by passing `--data-dir /path/to/data` to `eosd`.

Edit the `config.ini` file, adding the following settings to the defaults already in place:

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

When running `eosd` you should get log messages similar to below. It means the blocks are successfully produced.

```
1575001ms thread-0   chain_controller.cpp:235      _push_block          ] initm #1 @2017-09-04T04:26:15  | 0 trx, 0 pending, exectime_ms=0
1575001ms thread-0   producer_plugin.cpp:207       block_production_loo ] initm generated block #1 @ 2017-09-04T04:26:15 with 0 trxs  0 pending
1578001ms thread-0   chain_controller.cpp:235      _push_block          ] initc #2 @2017-09-04T04:26:18  | 0 trx, 0 pending, exectime_ms=0
1578001ms thread-0   producer_plugin.cpp:207       block_production_loo ] initc generated block #2 @ 2017-09-04T04:26:18 with 0 trxs  0 pending
...
```

## 5. Troubleshooting Guide

1. *You get an error such as `St9exception: content of memory does not match data expected by executable` when trying to start `eosd`*
> Try restarting `eosd` with `--resync`
2. How do I find which version of `eosd` I'm running or connecting to?
> Use `eosc -H ${eosd_host} -p ${eosd_port} get info` and you will see the version number in the field called `server_version`

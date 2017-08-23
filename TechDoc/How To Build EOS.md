


How To Build EOS.IO -- 如何构建 EOS.IO
---------------------

Describes how to download, compile, and configure an EOS.IO node.

The following instructions overview the process of getting the software, building it, and running a simple test network that produces blocks.

描述了如何下载，编译，并且配置一个 EOS.IO 的节点。

以下的操作说明概况了如何获得，构建和运行一个能产生区块的简单测试网络的整个过程。

Setting up a build/development environment -- 搭建一个用于构建/开发的环境
---

This project is written primarily in C++14 and uses CMake as its build system. An up-to-date C++ toolchain (such as Clang or GCC) and the latest version of CMake is recommended. At the time of this writing, Nathan uses clang 4.0.0 and CMake 3.8.0.

这个项目主要是用 C++14 编写的，并且使用了 CMake 作为它的构建系统。推荐使用最新的 C++ 工具链（比如说 Clang 或者 GCC）和最新版本的 CMake。在撰写本文档时，Nathan 使用的是 clang 4.0.0和 CMake 3.8.0。

Installing Dependencies -- 安装依赖包
---

Eos has the following external dependencies, which must be installed on your system:

EOS 有如下的外部依赖包必须在你的系统上安装：

 - Boost 1.64
 - OpenSSL
 - LLVM 4.0
 - [secp256k1-zkp (Cryptonomex 分支)](https://github.com/cryptonomex/secp256k1-zkp)
```
git clone https://github.com/cryptonomex/secp256k1-zkp.git
cd secp256k1-zkp
./autogen.sh
./configure
make
sudo make install
```

How to Build LLVM and clang for WASM -- 如何为 WASM 构建 LLVM 和 clang 
---
By default LLVM and clang do not include the WASM build target, so you will have to build it yourself. Note that following these instructions will create a version of LLVM that can only build WASM targets.

LLVM 和 clang 默认是不包括 WASM 的构建目标的，所以你必须要自己构建。注意以下的操作指令将会创建一个只用来构建 WASM 的一个LLVM的版本。

```
mkdir  ~/wasm-compiler
cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd ..
mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
make -j4 install
```

Getting the code -- 获取代码

To download all of the code, download Eos and a recursion or two of submodules. The easiest way to get all of this is to do a recursive clone:

为了下载所有的代码，可以递归下载 EOS 或者下载 EOS 和两个子模块。下载所有代码最简单的方法是使用一个递归克隆：
```
git clone https://github.com/eosio/eos --recursive
```
If a repo is cloned without the --recursive flag, the submodules can be retrieved after the fact by running this command from within the repo:

如果在克隆版本库的时候并没有使用 --recursive 这个命令行参数，那么在下载完成以后可以通过在版本库中运行这个命令来获取子模块：
```
git submodule update --init --recursive
```

Configuring and building -- 配置和构建
---

To do an in-source build, simply run cmake . from the top level directory. Out-of-source builds are also supported. To override clang's default choice in compiler, add these flags to the CMake command:

如果要做源码内构建的话，只需要在顶层文件夹运行 “cmake ." EOS 也支持源码外构建。为了覆盖在编译器里的 clang 的默认选择，把这些命令行参数加到 Cmake 的命令中去：
```
-DCMAKE_CXX_COMPILER=/path/to/c++ -DCMAKE_C_COMPILER=/path/to/cc
```

For a debug build, add -DCMAKE_BUILD_TYPE=Debug. Other common build types include Release and RelWithDebInfo.

如果是调试类型构建的话，加入命令行参数 -DCMAKE_BUILD_TYPE=Debug 。其他常用的构建类型是 Release 和 RelWithDebInfo 。

After successfully running cmake, simply run make to build everything. To run the test suite after building, run the chain_test executable in the tests folder.

cmake成功运行之后，只需要运行 make 来 构建所有的代码。构建以后如果需要运行测试集，就运行 tests 文件夹中的 chain_test 可执行文件。

Using the WASM compiler to perform a full build of the project -- 使用 WASM 编译器来对整个项目进行完全构建
---

The WASM_LLVM_CONFIG environment variable is used to find our recently built WASM compiler. This is needed to compile the example contracts insde eos/contracts folder and their respective tests.

我们用 WASM_LLVM_CONFIG 这个环境变量来发现我们最近构建的 WASM 编译器。在编译 eos/contracts 文件夹里的合约用例和他们各自的测试用例时需要用到这个 WASM 编译器。
```
git clone https://github.com/eosio/eos --recursive
mkdir -p eos/build && cd eos/build
export WASM_LLVM_CONFIG=~/wasm-compiler/llvm/bin/llvm-config 
cmake ..
make -j4
```

If you are doing active development on EOS.IO software you may want to add WASM_LLVM_CONFIG to your .bash_profile

如果你需要经常在 EOS.IO 软件上进行开发的话，你可能会想要把 WASM_LLVM_CONFIG 加到你的 .bash_profile 文件中去。

Creating and launching a single-node testnet -- 创立和启动单节点的测试网络

After successfully building the project, the eosd binary should be present in the programs/eosd directory. Go ahead and run eosd – it will probably exit with an error, but if not, close it immediately with Ctrl-C. Note that eosd will have created a directory named data-dir containing the default configuration (config.ini) and some other internals. This default data storage path can be overridden by passing --data-dir /path/to/data to eosd.

在成功构建项目之后，eosd 的二进制代码就应该出现在 programs/eosd 文件夹中。现在可以运行 eosd - 它可能会由于一个错误而退出，但是如果没有的话，马上用 Ctrl-C来关闭它。注意 eosd 会创建一个叫做 data-dir 的文件夹，里面有默认配置 （ config.ini ) 和一些其他的内部文件。可以通过加一个命令行参数 --data-dir /path/to/data 给 eosd 来覆盖掉这个默认的数据存储文件夹。

Edit the config.ini file, adding the following settings to the defaults already in place:

编辑 config.ini 文件，把以下设置加到已经存在的默认设置中：
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
# Load the block producer plugin, so we can produce blocks
plugin = eos::producer_plugin
```

Now it should be possible to run eosd and see it begin producing blocks. At present, the P2P code is not implemented, so only single-node configurations are possible. When the P2P networking is implemented, these instructions will be updated to show how to create an example multi-node testnet.

现在是应该可以运行 eosd 并且可以看到它开始产生区块。目前 P2P 的代码还未实现，所以只可能有一个单节点的配置。在 P2P 代码实现以后，将会更新这些操作说明来表明如何创建一个多节点测试网络的用例。

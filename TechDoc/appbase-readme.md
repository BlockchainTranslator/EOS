AppBase | AppBase 库
--------------

> 本文翻译自：https://github.com/EOSIO/appbase/blob/754b9d19783e008aa783a12465594f1fe2a49c29/README.md
>
> 译者：[区块链中文字幕组 胡亮](https://github.com/gumoon)
>
> 翻译时间：2017-11-12

The AppBase library provides a basic framework for building applications from
a set of plugins. AppBase manages the plugin life-cycle and ensures that all
plugins are configured, initialized, started, and shutdown in the proper order.

AppBase 库提供一个基础框架，支持以插件方式构建应用程序。AppBase 管理插件生命周期，并且确保所有插件以合适的顺序被配置、初始化、启动和停止。

## Key Features | 主要特点

- Dynamically Specify Plugins to Load | 插件动态加载
- Automaticly Load Dependent Plugins in Order | 自动按顺序加载依赖的插件
- Plugins can specify commandline arguments and configuration file options | 插件可以指定命令行参数和配置文件选项
- Program gracefully exits from SIGINT and SIGTERM | 发送 SIGINT 和 SIGTERM 信号优雅的退出程序
- Minimal Dependencies (Boost 1.60, c++14) | 最小化依赖（Boost 1.60, c++14)


## Defining a Plugin | 定义插件

A simple example of a 2-plugin application can be found in the /examples directory. Each plugin has a simple life cycle:

一个只有两个插件的应用程序的例子可以在代码库的 /examples 目录找到。每个插件有一个简单的生命周期：

1. Initialize - parse configuration file options | 初始化 - 解析配置文件选项
2. Startup - start executing, using configuration file options | 启动 - 使用配置文件选项，开始执行
3. Shutdown - stop everything and free all resources | 退出 - 停止所有工作并且释放所有资源

All plugins complete the Initialize step before any plugin enters the Startup step. Any dependent plugin specified by `APPBASE_PLUGIN_REQUIRES` will be Initialized or Started prior to the plugin being Initialized or Started. 

在任一插件进入启动步骤之前，需要所有的插件都完成了初始化步骤。使用 `APPBASE_PLUGIN_REQUIRES` 参数指定的被依赖插件，将会早于依赖它的插件初始化或者启动。

Shutdown is called in the reverse order of Startup. 

退出的时候，以启动时相反的顺序调用。

```
class net_plugin : public appbase::plugin<net_plugin>
{
   public:
     net_plugin(){};
     ~net_plugin(){};

     APPBASE_PLUGIN_REQUIRES( (chain_plugin) );

     virtual void set_program_options( options_description& cli, options_description& cfg ) override
     {
        cfg.add_options()
              ("listen-endpoint", bpo::value<string>()->default_value( "127.0.0.1:9876" ), "The local IP address and port to listen for incoming connections.")
              ("remote-endpoint", bpo::value< vector<string> >()->composing(), "The IP address and port of a remote peer to sync with.")
              ("public-endpoint", bpo::value<string>()->default_value( "0.0.0.0:9876" ), "The public IP address and port that should be advertized to peers.")
              ;
     }

     void plugin_initialize( const variables_map& options ) { std::cout << "initialize net plugin\n"; }
     void plugin_startup()  { std::cout << "starting net plugin \n"; }
     void plugin_shutdown() { std::cout << "shutdown net plugin \n"; }

};

int main( int argc, char** argv ) {
   try {
      appbase::app().register_plugin<net_plugin>(); // implict registration of chain_plugin dependency
      if( !appbase::app().initialize( argc, argv ) )
         return -1;
      appbase::app().startup();
      appbase::app().exec();
   } catch ( const boost::exception& e ) {
      std::cerr << boost::diagnostic_information(e) << "\n";
   } catch ( const std::exception& e ) {
      std::cerr << e.what() << "\n";
   } catch ( ... ) {
      std::cerr << "unknown exception\n";
   }
   std::cout << "exited cleanly\n";
   return 0;
}
```

This example can be used like follows:

这个例子像下面这样运行：

```
./examples/appbase_example --plugin net_plugin
initialize chain plugin
initialize net plugin
starting chain plugin
starting net plugin
^C
shutdown net plugin
shutdown chain plugin
exited cleanly
```

### Boost ASIO | 启动异步IO

AppBase maintains a singleton `application` instance which can be accessed via `appbase::app()`.  This application owns a `boost::asio::io_service` which starts running when appbase::exec() is called. If a plugin needs to perform IO or other asynchronous operations then it should dispatch it via `app().get_io_service().post( lambda )`.  

AppBase 维护一个 `application` 单例，它可以通过 `appbase::app()` 被访问。在调用了 `appbase::exec()` 之后，应用程序将拥有一个 `boost::asio::io_server` 开始运行。如果一个插件需要执行 IO 或者其他异步操作，该插件应该通过 `app().get_io_service().post( lambda )` 来分发这个操作。

Because the app calls `io_service::run()` from within `application::exec()` all asynchronous operations posted to the io_service should be run in the same thread.  

由于应用程序在 `application::exec()` 中调用 `io_service::run()`, 所以，传递给 io_service 的所有异步操作都应该运行在相同的线程中。

## Graceful Exit | 优雅的退出

To trigger a graceful exit call `appbase::app().quit()` or send SIGTERM or SIGINT to the process.

调用 `appbase::app().quit()` 或者发送 `SIGTERM` 或 `SIGINT` 信号给进程，触发进程优雅的退出。

## Dependencies | 依赖

1. c++14 or newer  (clang or g++) | c++14 或者更新版本
2. Boost 1.60 or newer compiled with C++14 support | Boost 1.60 或者编译了带 c++14 的更新版本

To compile boost with c++14 use:

编译带 c++14 的 boost ：

```
 ./b2 ...  cxxflags="-std=c++0x -stdlib=libc++" linkflags="-stdlib=libc++" ...
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




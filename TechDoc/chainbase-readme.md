# ChainBase - a fast version controlled, transactional database | ChainBase - 一个快速的支持版本控制和交易数据库

> 本文翻译自：https://github.com/EOSIO/chainbase/blob/d48ebabf56b4115753fcabb7648a0ffcf3b0f5e9/README.md
>
> 译者：[区块链中文字幕组 胡亮](https://github.com/gumoon)
>
> 翻译时间：2017-11-23

ChainBase is designed to meet the demanding requirments of blockchain applications, but is suitable for use in any application that requires a robust transactional database with the ability have near-infinate levels of undo history.

ChainBase 为区块链应用程序而设计，但是它适合想要一个健壮的交易数据库的任何应用程序。它支持近乎无限级的撤销历史。

While chainbase was designed for blockchain applications, it is suitable for any program that needs to persist complex application state with the ability to undo.

虽然 chainbase 是为区块链应用程序设计的，但是，通过支持无限级撤销的能力，它适合需要持久化复杂应用状态的任何程序。

## Features | 特点

  - Supports multiple objects (tables) with multiple indicies (based upon boost::multi_index_container) 支持带有多标记的多对象（表）（基于 boost::multi_index_container)
  - State is persistant and sharable among multiple processes 状态可持久化并且多进程可共享
  - Nested Transactional Writes with ability to undo changes 可以撤销的嵌套交易写

## Dependencies | 依赖
  
  - c++11 
  - [Boost](http://www.boost.org/) 
  - CMake Build Process CMake 构建程序
  - Supports Linux, Mac OS X  (no Windows Support) 支持Linux、Mac OS X (不支持 windows）

## Example Usage | 使用实例

``` c++
enum tables {
   book_table
};

/**
 * Defines a "table" for storing books. This table is assigned a 
 * globally unique ID (book_table) and must inherit from chainbase::object<> which
 * decorates the book type by defining "id_type" and "type_id" 
 */
struct book : public chainbase::object<book_table, book> {

   /** defines a default constructor for types that don't have
     * members requiring dynamic memory allocation.
     */
   CHAINBASE_DEFAULT_CONSTRUCTOR( book )
   
   id_type          id; ///< this manditory member is a primary key
   int pages        = 0;
   int publish_date = 0;
};

struct by_id;
struct by_pages;
struct by_date;

/**
 * This is a relatively standard boost multi_index_container definition that has three 
 * requirements to be used withn a chainbase database:
 *   - it must use chainbase::allocator<T> 
 *   - the first index must be on the primary key (id) and must be unique (hashed or ordered)
 */
typedef multi_index_container<
  book,
  indexed_by<
     ordered_unique< tag<by_id>, member<book,book::id_type,&book::id> >, ///< required 
     ordered_non_unique< tag<by_pages>, BOOST_MULTI_INDEX_MEMBER(book,int,pages) >,
     ordered_non_unique< tag<by_date>, BOOST_MULTI_INDEX_MEMBER(book,int,publish_date) >
  >,
  chainbase::allocator<book> ///< required for use with chainbase::database
> book_index;

/**
    This simple program will open database_dir and add two new books every time
    it is run and then print out all of the books in the database.
 */
int main( int argc, char** argv ) {
   chainbase::database db;
   db.open( "database_dir", database::read_write, 1024*1024*8 ); /// open or create a database with 8MB capacity
   db.add_index< book_index >(); /// open or create the book_index 


   const auto& book_idx = db.get_index<book_index>().indicies();

   /**
      Returns a const reference to the book, this pointer will remain
      valid until the book is removed from the database.
    */
   const auto& new_book300 = db.create<book>( [&]( book& b ) {
       b.pages = 300+book_idx.size();
   } );
   const auto& new_book400 = db.create<book>( [&]( book& b ) {
       b.pages = 300+book_idx.size();
   } );

   /**
      You modify a book by passing in a lambda that receives a
      non-const reference to the book you wish to modify. 
   */
   db.modify( new_book300, [&]( book& b ) {
      b.pages++;
   });

   for( const auto& b : book_idx ) {
      std::cout << b.pages << "\n";
   }

   auto itr = book_idx.get<by_pages>().lower_bound( 100 );
   if( itr != book_idx.get<by_pages>().end() ) {
      std::cout << itr->pages;
   }

   db.remove( new_book400 );
   
   return 0;
}

```

## Concurrent Access | 并发访问

By default ChainBase provides no synchronization and has the same concurrency restrictions as any boost::multi_index_container.  This means that two or more threads may read the database at the same time, but all writes must be protected by a mutex.  

默认情况下，ChainBase，像其它 boost::multi_index_container 一样，支持异步，但是有并发约束。这意味着两个或更多线程可以同时读取数据库，但是，写操作是互斥的。

Multiple processes may open the same database if care is taken to use interpocess locking on the database.  

多个进程可以打开相同的数据库，想加锁的话，也可以对数据库加内部进程锁。

## Persistance | 持久化

By default data is only flushed to disk upon request or when the program exits. So long as the program does not crash in the middle of a call to db.modify(), or db.create() the content of the database should remain in a consistant state. This means that you should minimize the complexity of the lambdas used to create and/or modify state.

默认情况下，只在请求结束或者程序退出时，才刷新数据到硬盘。只要在调用 db.modify() 或 db.create() 时，程序没有崩溃，数据库的内容应该保持一致的状态。这意味着你应该最大程度减小 创建或修改状态的 lambdas 函数的复杂度。

If the operating system crashes or the computer loses power, then the database will be left in an undefined state depending upon which memory pages that operating system was able to sync to disk.

如果操作系统崩溃或者电脑掉电，数据库将出现未定义状态，该状态依赖于操作系统的内存页是否能够同步到硬盘。

ChainBase was designed to be used with blockchain applications where an append-only log of blocks is used to secure state in the event of power loss. This block log can be replayed to regenerate the full database
state. Dealing with OS crashes, loss of power, and logs, is beyond the scope of ChainBase.

ChainBase 是为区块链应用程序而设计的，区块链日志的只支持追加的功能，被用于应对掉电时，状态的安全。区块链日志支持重放来重新生成完整的数据库状态。关于操作系统崩溃、掉电、和日志相关的内容，超出了 ChainBase 的范畴。

## Portability | 便捷性

The contents of the database file is dependent upon the memory layout of the computer and process that created the database. Moving the database to a machine that uses a different compiler, operating system, libraries, or build type (release vs debug) will result in undefined behavior.  

数据库文件的内容依赖于计算机的内存布局和创建数据库的程序。移动数据库到一个使用不同编译器、操作系统、类库或者不同构建类型（发行版、调试版）的机器，将导致未定义行为。

If portability is desired, the developer will have to export the database to a suitable format. 

考虑便捷性的话，开发者将不得不导出数据库为一种合适的格式。

## Background  | 背景

Blockchain applications depend upon a high performance database capable of millions of read/write operations per second.  Additionally blockchains operate on the basis of "eventually consistant" which means that any changes made to the database are potentially reversible for an unknown amount of time depending upon the consenus protocol used. 

区块链应用程序依靠每秒能处理百万级读写的高性能数据库。另外，区块链基于“最终一致性”的理念运转，这意味着数据库的任何改变都可能被反转，因为使用不同的的共识协议消耗的时间不同。

Existing database such as [libbitcoin Database](https://github.com/libbitcoin/libbitcoin-database) achieve high peformance using similar techniques (memory mapped files), but they are heavily specialised and do not implement the logic necessary for multiple indicies or undo history. 

既存的数据库，像 [libbitcoin 数据库](https://github.com/libbitcoin/libbitcoin-database) 使用类似的技术（内存映射文件）取得了高性能。但是，它们有较重的业务，并且不支持多标识的必要逻辑和撤销历史。

Databases such as LevelDB provide a simple Key/Value database, but suffer from poor performance relative to memory mapped file implementations.

像 LevelDB 提供一个简单的键值对数据库，但是，相比内存映射文件实现的数据库有较差的性能。

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


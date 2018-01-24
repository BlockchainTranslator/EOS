# Doxygen Guidelines | Doxygen 指南

> 本文翻译自：https://github.com/EOSIO/eos/wiki
>
> 译者：[区块链中文字幕组 龙心小台](https://github.com/BlockchainTranslator/EOS)
>
> 翻译时间：2018-1-1


## Table of Contents | 目录
- [Introduction | 简介](#introduction)
- [How to generate/update the EOS documentation | 如何生成/更新 EOS 文档
](#how-to-generateupdate-the-eos-documentation)
- [How to view the EOS documentation | 如何查看 EOS 文档
](#how-to-view-the-eos-documentation)
- [How to create doxygen style EOS documentation | 如何创建 doxygen 样式的 EOS 文档](#how-to-create-doxygen-style-eos-documentation)
- [Doxygen Command List | Doxygen 命令列表
](#doxygen-command-list)
  * [brief](#@brief)
  * [class](#class)
  * [defgroup](#defgroup)
  * [file](#file)
  * [ingroup](#ingroup)
  * [note](#note)
  * [param](#param)
  * [pre](#pre)
  * [ref](#ref)
  * [return](#return)
  * [section](#section)
  * [see](#see)
  * [subsection](#subsection)
  * [throws](#throws)
  * [tparam](#tparam)


## Introduction | 简介
Doxygen is a documentation generator; A tool for writing software reference documentation. The documentation is written within code, and is thus relatively easy to keep up to date.

Doxygen 是一个文档生成器; 一个用于编写软件参考文档的工具。 文档是用代码编写的，因此相对容易更新。


Doxygen can cross reference documentation and code, so that the reader of a document can easily refer to the actual code. Doxygen extracts documentation from source file comments and has built-in support to generate inheritance diagrams for C++ classes. For more advanced diagrams and graphs, doxygen can use the "dot" tool from Graphviz (http://www.graphviz.org/).

Doxygen 可以交叉引用文档和代码，以便文档的读者可以很容易地参考实际代码。 Doxygen 从源文件注释中提取文档，并具有内置的支持来为 C++ 类生成继承关系图。 对于更高级的图表和图形，doxygen 可以使用 Graphviz 的 “dot” 工具（http://www.graphviz.org/）。

Doxygen supports most Unix-like systems, macOS, and Windows.
It can be downloaded from git, ftp or from the web as source, installer or as zipped version from below location:
http://www.stack.nl/~dimitri/doxygen/download.html

Doxygen 支持大多数类 Unix 系统、macOS 和 Windows。
它可以作为源、安装程序从 git、ftp 或网上下载，也可以从下面网址下载到压缩版本：
http://www.stack.nl/~dimitri/doxygen/download.html

## How to generate/update the EOS documentation | 如何生成/更新 EOS 文档
After downloading and installing doxygen, it needs to be run in order to analyze all source code comments and build the corresponding documentation.

下载并安装 doxygen 之后，需要运行它以分析所有的源代码注释并建立相应的文档。

To be configurable, doxygen uses a configuration file to determine all of its settings. The configuration file is a free-form ASCII text file, which consists of a list of assignment statements and a structure similar to that of a Makefile.

为了可配置，doxygen 使用一个配置文件来确定它的所有设置。 配置文件是一个自由格式的 ASCII 文本文件，它由一个赋值语句列表和一个类似于Makefile 的结构组成。

To generate the documentation you point doxygen to the configuration file as a parameter as follows:

要生成文档，可以将 doxygen 指向配置文件作为参数，如下所示：

```
doxygen <config-file>
```
An alphabetical index of the tags that are supported in the configuration file is situated here:
https://www.stack.nl/~dimitri/doxygen/manual/config.html

配置文件中支持的标签的字母索引位于以下位置：
https://www.stack.nl/~dimitri/doxygen/manual/config.html


For the EOS repository the configuration file is situated in the root directory of the repository (eos.doxygen).

对于 EOS 存储库，配置文件位于存储库的根目录（eos.doxygen）中。

So to generate or update the EOS documentation from command line, navigate to the root folder of the EOS repository and trigger the document generation as follows

因此，要从命令行生成或更新 EOS 文档，请进入 EOS 存储库的根文件夹，并按如下所示触发文档生成


```
doxygen build/eos.doxygen
```
If you don't have build/eos.doxygen, you will need to build EOS first. Check this [guide](Local-Environment#2-building-eos) for the steps.

如果你没有 build/eos.doxygen，你需要先构建 EOS。 有关步骤，请查看本[指南](Local-Environment#2-building-eos)。

After the above command is executed, you will be able to find the updated documents inside `build/docs/html`

执行上述命令后，你将能够在`build / docs / html`中找到更新的文档。

## How to view the EOS documentation | 如何查看 EOS 文档

The EOS doxygen configuration file is set up, so that the documentation will be created as a series of connected HTML files.

EOS doxygen 配置文件已经完成设置，因此文档将被创建为一系列连接的 HTML 文件。

The generated HTML documentation can be viewed via browser, whereas the document root is the index.html file in the docs subfolder of the EOS repository. A direct link can be found here:
https://eosio.github.io/eos/

生成的 HTML 文档可以通过浏览器查看，而文档根目录是 EOS 存储库的文档子文件夹中的 index.html 文件。 链接如下：
https://eosio.github.io/eos/


## How to create doxygen style EOS documentation | 如何创建 doxygen 样式的 EOS 文档

For information to be picked up by doxygen, it needs to be contained in a special comment block.

要想让信息被 doxygen 识取，它需要包含在一个特殊的注释块中。

A special comment block is a C or C++ style comment block with some additional markings, so doxygen knows it is a piece of structured text that needs to end up in the generated documentation.

一个特殊的注释块是带有一些附加标记的 C 或 C++ 样式注释块，因此 doxygen 知道它是一个结构化文本的一部分，需要被包含在生成的文档中。

Doxygen picks up information in all allowed standard comment blocks, such as in the following multiline comment examples:

Doxygen 在所有允许的标准注释块中提取信息，例如下面的多行注释示例：

```
/**
<A short one line description>

<Longer description>
<May span multiple lines or paragraphs as needed>

@param  Description of method's or function's input parameter
@param  ...
@return Description of the return value
*/
```

```
/**
 * <A short one line description>
 *
 * <Longer description>
 * <May span multiple lines or paragraphs as needed>
 *
 * @param  Description of method's or function's input parameter
 * @param  ...
 * @return Description of the return value
 */
```
When using C++ style single line comments, doxygen  parses only comments with additional slashes, such as:

当使用 C++ 样式的单行注释时，doxygen 只解析带有额外斜线的注释，比如：

```
/// <A short one line description>
///
/// <Longer description>
/// <May span multiple lines or paragraphs as needed>
///
/// @param  Description of method's or function's input parameter
/// @param  ...
/// @return Description of the return value
```
Ordinarily comments are being placed **BEFORE** the actual item, however in certain cases such as
documenting the members of a file, struct, union, class or enum as well as the parameters of a function, it is sometimes desired to place the documentation block **AFTER** the member.

一般情况下，注释被放在实际内容**之前**，但在某些情况下，如记录文件、结构、联合、类或枚举的成员以及函数的参数时，有时需要将文档块放在成员**之后**。

For this purpose you have to put an additional < marker in the comment block in order for doxygen to map the information correctly such as demonstrated in below examples:

为了达到这个目的，你必须在注释块中添加一个 < 标记，以便 doxygen 能够正确地映射信息，如下面的例子所示：

```
int var; /**< Detailed description after the member */
```

```
int var; ///< Detailed description after the member
```
Special commands such as param and return in the above examples start either with a backslash (\) or an at-sign (@), so both of the following choices are equivalent:

上述示例中的特殊命令（如 param 和 return）可以以反斜杠（\）或 at 符号（@）开头，因此以下两个选项都是等效的：

```
/**
   @brief  A short description
*/
```
```
/**
   \brief  A short description
*/
```

## Doxygen Command List | Doxygen 命令列表

The list of commands recognised by doxygen is quite exhaustive; (An alphabetically sorted list of all commands can be found here: http://www.stack.nl/~dimitri/doxygen/manual/commands.html).

doxygen 认可的命令清单非常详尽， （可在此找到所有命令的按字母顺序排列的列表：http://www.stack.nl/~dimitri/doxygen/manual/commands.html）。

However in the EOS documentation we are currently using a small subset of the above list. Below is a full list of commands used in the EOS documentation with explanation:

但是在 EOS 文档中，我们使用的是上面列表中的一小部分。 以下是 EOS 文档中使用的命令的完整列表，及其相关说明：

Note:
- \<sharp\> braces are used for single word arguments
- (round) braces are used for arguments that extends until the end of the line
- {curly} braces are used for arguments that extends until the next paragraph
- [square] brackets are used for optinal arguments

注意：
- \<尖\>括号用于单个单词的参数
- （圆）括号用于扩展到行尾的参数
- {卷曲}括号用于扩展到下一段落的参数
- [方]括号用于最优参数

#### @brief
Usage: @brief { brief description }

Starts a paragraph that serves as a brief description. For classes and files the brief description will be used in lists and at the start of the documentation page. For class and file members, the brief description will be placed at the declaration of the member and prepended to the detailed description. A brief description may span several lines (although it is advised to keep it brief!). A brief description ends when a blank line or another sectioning command is encountered. If multiple @brief commands are present they will be joined.

标志一段简要说明的开始。 对于类和文件，简要描述将用于列表和文档页面的开头。 对于类和文件的成员，简要描述将放置在成员的声明中，并被放在详细描述之前。 一个简短的描述可能跨越几行（尽管建议保持简短！）。 简要说明在遇到空白行或其他分段命令时结束。 如果存在多个@brief 命令，它们将被连接。

#### @class
Usage: @class \<name\> [\<header-file\>] [\<header-name\>]

Indicates that a comment block contains documentation for a class with name \<name\>. Optionally a header file and a header name can be specified. If the header-file is specified, a link to a verbatim copy of the header will be included in the HTML documentation. The \<header-name\> argument can be used to overwrite the name of the link that is used in the class documentation to something other than \<header-file\>. With the \<header-name\> argument you can also specify how the include statement should look like, by adding either quotes or sharp brackets around the name. Sharp brackets are used if just the name is given.

表示注释块包含名称为\<name\>的类的文档。 可以选择指定头文件和头名称。 如果指定了头文件，则 HTML 文档中将包含指向头文件逐字副本的链接。 \<header-name\> 参数可用于覆盖类文档中的链接的名称，使其不再是\<header-file\>。 使用\<header-name\>参数，你还可以通过在名称周围添加引号或尖括号来指定 include 语句的外观。 如果仅指定名称，则使用尖括号。

Example:

例子：

```
/* A dummy class */
class Test
{
};
/**
*  @class Test class.h "inc/class.h"
*  @brief This is a test class.
*
*  Some details about the Test class.
*/
```


#### @defgroup
Usage: @defgroup \<name\> (group title)

Indicates that a comment block contains documentation for a group of classes, files or namespaces. This can be used to categorize classes, files or namespaces, and document those categories. You can also use groups as members of other groups, thus building a hierarchy of groups.
The \<name\> argument should be a single-word identifier.

表示注释块包含一组类、文件或命名空间的文档。 这可以用来对类、文件或命名空间进行分类，并记录这些类别。 你也可以使用组作为其他组的成员，从而构建组的层次结构。
\<name\>参数应为一个单字标识符。

#### @file
Usage: @file [\<name\>]

Indicates that a comment block contains documentation for a source or header file with name \<name\>. The file name may include (part of) the path if the file-name alone is not unique. If the file name is omitted (i.e. the line after @file is left blank) then the documentation block that contains the @file command will belong to the file it is located in.
Important:
The documentation of global functions, variables, typedefs, and enums will only be included in the output if the file they are in is documented as well.

表示注释块包含名称为\<name\>的源文件或头文件。 如果单独的文件名不唯一，则文件名可能包括（部分）路径。 如果省略文件名（即 @file 后面的行留空），那么包含 @file 命令的文档块将属于它所在的文件。
重要：
全局函数，变量，typedef 和枚举的文档将只包含在输出中，如果它们所在的文件也记录在文件中。

Example:

例子：

```
/** @file file.h
* A brief file description.
* A more elaborated file description.
*/
/**
* A global integer value.
* More details about this value.
*/
extern int globalValue;
```


#### @ingroup
Usage: @ingroup (\<groupname\> [\<groupname\> \<groupname\>])

If the @ingroup command is placed in a comment block of a class, file or namespace, then it will be added to the group or groups identified by \<groupname\>.

如果 @ingroup 命令被放置在类、文件或命名空间的注释块中，那么它将被添加到 \<groupname\> 标识的组中。

#### @note
Usage: @note { text }

Starts a paragraph where a note can be entered. The paragraph will be indented. The text of the paragraph has no special internal structure. All visual enhancement commands may be used inside the paragraph. Multiple adjacent @note commands will be joined into a single paragraph. Each note description will start on a new line. Alternatively, one @note command may mention several notes. The @note command ends when a blank line or some other sectioning command is encountered.

标志一个可以输入注释的段落的开始。 该段将缩进。 该段文本没有特别的内部结构。 所有视觉增强命令都可以在段落内使用。 多个相邻的 @note 命令将被合并到一个段落中。 每个注释说明将从新行上开始。 或者，一个 @note 命令可能会提到几个注释。 @note 命令在遇到空行或其他分段命令时结束。

#### @param
Usage: @param [(dir)] \<parameter-name\> { parameter description }

Starts a parameter description for a function parameter with name \<parameter-name\>, followed by a description of the parameter. The existence of the parameter is checked and a warning is given if the documentation of this (or any other) parameter is missing or not present in the function declaration or definition.
The @param command has an optional attribute, (dir), specifying the direction of the parameter. Possible values are "[in]", "[in,out]", and "[out]", note the [square] brackets in this description. When a parameter is both input and output, [in,out] is used as attribute. Here is an example for the function memcpy:

为名称为 \<parameter-name\> 的函数参数添加参数描述，对该参数的描述紧随其后。 该参数的存在会被检查，如果函数声明或定义中缺少或不存在此（或其他）参数的文档，则会发出警告。
@param 命令有一个可选的属性（dir），指定参数的方向。 可能的值是 “[in]”、“[in，out]” 和 “[out]”，请注意本说明中的[方]括号。 当参数既是输入又是输出时，[in, out]用作属性。 这里是 memcpy 函数的一个示例：

```
/*!
* Copies bytes from a source memory area to a destination memory area,
* where both areas may not overlap.
* @param[out] dest The memory area to copy to.
* @param[in] src The memory area to copy from.
* @param[in] n The number of bytes to copy
*/
void memcpy(void *dest, const void *src, size_t n);
```

The parameter description is a paragraph with no special internal structure. All visual enhancement commands may be used inside the paragraph.
Multiple adjacent @param commands will be joined into a single paragraph. Each parameter description will start on a new line. The @paramdescription ends when a blank line or some other sectioning command is encountered.
Note that you can also document multiple parameters with a single @param command using a comma separated list. Here is an example:

参数描述是一个没有特殊内部结构的段落。 所有视觉增强命令都可以在段落内使用。
多个相邻的 @param 命令将被合并到一个段落中。 每个参数描述将从新行开始。 遇到空行或其他分段命令时，@paramdescription 结束。
请注意，你也可以使用逗号分隔的列表，使用一个 @param 命令记录多个参数。 下面是一个示例：

```
/** Sets the position.
* @param x,y,z Coordinates of the position in 3D space.
*/
void setPosition(double x,double y,double z,double t)
{
}
```


#### @pre
Usage: @pre { description of the precondition }

Starts a paragraph where the precondition of an entity can be described. The paragraph will be indented. The text of the paragraph has no special internal structure. All visual enhancement commands may be used inside the paragraph. Multiple adjacent @pre commands will be joined into a single paragraph. Each precondition will start on a new line. Alternatively, one @pre command may mention several preconditions. The @pre command ends when a blank line or some other sectioning command is encountered.

开始一段话以描述一个实体的先决条件。 该段将缩进。 该段文本没有特别的内部结构。 所有视觉增强命令都可以在段落内使用。 多个相邻的 @pre 命令将被加入到单个段落中。 每个先决条件将从新的一行开始。 或者，一个 @pre 命令可以提及几个先决条件。 @pre 命令在遇到空行或其他分段命令时结束。

#### @ref
Usage: @ref \<name\> ["(text)"]

Creates a reference to a named section, subsection, page or anchor. For HTML documentation the reference command will generate a link to the section. For a section or subsection the title of the section will be used as the text of the link. For an anchor the optional text between quotes will be used or \<name\> if no text is specified. For documentation the reference command will generate a section number for sections or the text followed by a page number if \<name\> refers to an anchor.

创建对指定节、子节、页面或锚点的引用。 对于 HTML 文档，引用命令将生成一个指向该部分的链接。 对于节或子节，该节的标题将被用作该链接的文本。 对于锚点，将使用引号之间的可选文本，或如果没有指定文本，则使用\<name\>。 对于文档，如果 \<name\> 指向一个锚点，那么引用命令将为节生成节号或生成后面跟着页码的文本。

#### @return
Usage: @return { description of the return value }

Starts a return value description for a function. The text of the paragraph has no special internal structure. All visual enhancement commands may be used inside the paragraph. Multiple adjacent @return commands will be joined into a single paragraph. The @return description ends when a blank line or some other sectioning command is encountered.

标志着函数的返回值描述。 该段文本没有特别的内部结构。 所有视觉增强命令都可以在段落内使用。 多个相邻的 @return 命令将被连接成一个段落。 @return 描述在遇到空行或其他分段命令时结束。

#### @section
Usage: @section \<section-name\> (section title)

Creates a section with name \<section-name\>. The title of the section should be specified as the second argument of the @section command. This command only works inside related page documentation and not in other documentation blocks!

创建名称为\<section-name\>的部分。 该部分的标题应该被指定为 @section 命令的第二个参数。 这个命令仅适用于相关页面文档，不能在其他文档块中使用！

#### @see
Usage: @see { references }

Starts a paragraph where one or more cross-references to classes, functions, methods, variables, files or URL may be specified. Two names joined by either :: or # are understood as referring to a class and one of its members. One of several overloaded methods or constructors may be selected by including a parenthesized list of argument types after the method name.
Equivalent to @sa.

开始一个段落，其中可以指定一个或多个对类、函数、方法、变量、文件或 URL 的交叉引用。 通过::或＃连接的两个名字被理解为是指一个类和它的一个成员。 可以通过在方法名称后面包括一个带括号的参数类型列表，来选择几个重载的方法或构造函数中的一个。
相当于@sa。

#### @subsection
Usage: @subsection \<subsection-name\> (subsection title)

Creates a subsection with name \<subsection-name\>. The title of the subsection should be specified as the second argument of the @subsection command. This command only works inside a section of a related page documentation block and not in other documentation blocks!

创建一个名为\<subsection-name\>的小节。 该小节的标题应该被指定为 @subsection 命令的第二个参数。 此命令只能在相关页面文档块内运行，而不能在其他文档块中运行。

#### @throws
Usage: @throws \<exception-object\> { exception description }

Starts an exception description for an exception object with name \<exception-object\>. Followed by a description of the exception. The existence of the exception object is not checked. The text of the paragraph has no special internal structure. All visual enhancement commands may be used inside the paragraph. Multiple adjacent @throws commands will be joined into a single paragraph. Each exception description will start on a new line. The @throws description ends when a blank line or some other sectioning command is encountered. Equivalent to @throw.

为名称为\<exception-object\>的异常对象进行异常说明。 紧随其后的是对该例外的描述。 不检查是否存在异常对象。 该段文本没有特别的内部结构。 所有视觉增强命令都可以在段落内使用。 多个相邻的 @throws 命令将被加入到一个段落中。 每个异常描述将从新行开始。 @throws 描述在遇到空行或其他分段命令时结束。 相当于@throw。

#### @tparam
Usage: @tparam \<template-parameter-name\> { description }

Starts a template parameter for a class or function template parameter with name \<template-parameter-name\>, followed by a description of the template parameter.
Otherwise similar to @param.

为名称为\<template-parameter-name\>的类或函数模板参数启动模板参数，后跟对模板参数的描述。
除此之外，类似于@param。


----------------------------------------------------

#### 区块链中文字幕组

致力于前沿区块链知识和信息的传播，为中国融入全球区块链世界贡献一份力量。

如果您懂一些技术、懂一些英文，欢迎加入我们，加微信号:w1791520555。

[点击查看项目GITHUB，及更多的译文...](https://github.com/BlockchainTranslator/EOS)

本文由[币乎社区（bihu.com）](http://www.bihu.com)内容支持计划奖励。

版权所有，转载需完整注明以上内容。

----------------------------------------------------

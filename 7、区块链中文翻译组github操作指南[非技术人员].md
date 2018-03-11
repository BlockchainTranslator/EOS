# 区块链中文翻译组github操作指南

为了防止在master分支上对文件进行重复编辑而对master分支的历史记录造成影响，将导致变更难以管理。我们要求每位翻译者在翻译一篇新文章之前需要新建自己的分支，在自己分支进行操作，之后再进行pull request操作回到master分支。

## 步骤如下

### 1、 新建分支

 翻译者在开始工作时应新建以<名字>_<时间>命名的新分支。如下图新建一个ricky_171016的分支。

![WX20171015-223704@2x.png](https://steemitimages.com/DQmYT6akfe1uckSjqisB8s5jnkzBpjv36TzpARYEfG3Xhqz/WX20171015-223704%402x.png)

完成后就可以在这个自己的分支上进行翻译工作了。

![WX20171015-224006@2x.png](https://steemitimages.com/DQmadiZxrxYDUfSVzsjTJ4LAFzVn1hi455Ua5c9hY3PeZUH/WX20171015-224006%402x.png)

### 2、在相应的目录下创建翻译完成的md文件

![WX20171015-224232@2x.png](https://steemitimages.com/DQmXAz1cfq4mxB7CsS5hJvYN8dTjZwpYax4VgXEXXf4aQ1h/WX20171015-224232%402x.png)

文件名为原文标题加.md后缀。

![WX20171016-003518@2x.png](https://steemitimages.com/DQmWVSEaAbdPcibAiaWff1zNfosxodZU4h9PRDs2F6SXoCg/WX20171016-003518%402x.png)


建议使用https://maxiang.io/ 编辑器或者其他markdonw软件进行离线编辑，可以实时看到格式，完成之后再一次性贴入github中。

![WX20171015-225911@2x.png](https://steemitimages.com/DQmZQnJAiJH7zhD34gM8jPXfST5mPKLi1qaPScUZAwHYtFp/WX20171015-225911%402x.png)


保存后就可以在自己的分支上看到这个文件了

![WX20171016-003802@2x.png](https://steemitimages.com/DQmPMZdNhNN2XTqHGgJu8Mey58PU45QPAaDu8xHHF68bDJC/WX20171016-003802%402x.png)

这样先在外部编辑器编辑完成再贴入git中的好处就是你将只有一个commit提交到master分支，这样就便于管理了。

但是难免有时候会有改动，针对技术人员其实可以在本地分支上进行合并commit再推送到远程分支。

那么针对非技术人员的话也很简单, 直接删除这个ricky_171016分支，重新建一个刚才那么名字一样的，重新新建文件，贴入外部编辑器的markdown文本即可。

![WX20171016-003904@2x.png](https://steemitimages.com/DQmYN1EDjjo2UV1GpfNNeAsDRq1LH6LA8ArLg26BU1CRwDH/WX20171016-003904%402x.png)

### 3、merge到master分支

在自己的分支点击 new pull request


![WX20171016-004036@2x.png](https://steemitimages.com/DQmZ64AwUrykFquB6PPuhjAm8zQ2X3cJvevNbLN4Rs91bev/WX20171016-004036%402x.png)

PR的标题标准如下，如果需要他人帮忙Review，可以在这里选择你希望帮你审稿的人，并需要通知对方。

![WX20171016-002756@2x.png](https://steemitimages.com/DQmRvmyDYjFbLTxm4baZeecfJofx4KKt4aPMUfJ2R6i9Aeg/WX20171016-002756%402x.png)

只需点击下方绿色按钮，你的改动就到master分支上了。merge后，你也可以直接删除这个分支。下次翻译新的文章时再重新新建分支, 按照上述步骤重新操作即可。

技术人员
----------------

如果你是技术人员，请在本地环境建立本地分支，推送远程分支之前请合并多个commit为一个，再与master分支做rebase操作，然后再进行pull request

markdown文本语法
----------------

github文本使用markdown语法，不是所见即所得的WORD文档。如果WORD文档直接拷贝过来，将很难阅读。
所以你需要：

1、译文提交时，文件名称结尾需要为：.md；

2、关于markdown的语法说明，请见：

新手如何入门：markdown-https://www.zhihu.com/question/20409634；

markdown语法说明：https://www.appinn.com/markdown/


技术支持
---------------
任何关于git的问题都可以咨询我。

胖哥 wechat: 37858036 

20180311-更新何德林 wechat: w1791520555.

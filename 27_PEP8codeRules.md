
# 【Python 学习分享文章】_PEP8codeRules（PEP8编码规范）

## 综述

语言里面，表达出意思，到底怎么使用什么语句、方式去达到，都是可以的，但是我们不会说一些病句（比如：我今天可能一定去做公交车）、也不会说一些不简洁的表达（比如：明天的明天我过生日，而是会说“后天我过生日”），Python 里面也有这样的规则，这就是 PEP8编码规范。

【作用】：最有用的作用就是在程序出错的时候，可以更快地寻找地问题的地方。

## 介绍

### - The Zen of Python

这是 Python 作者确定的 Python 这门语言的编写的核心基础，所以可以看到【优雅性】在Python 的重要地位了。简单理解，【优雅性】就是【可读性】。


在终端上进入 Python，输入 ```import this```，就可以看到 Python 作者的一首诗，算是一个 geek 的小幽默、小文艺。

摘录如下：

> The Zen of Python, by Tim Peters  
>
Beautiful is better than ugly.  
Explicit is better than implicit.  
Simple is better than complex.  
Complex is better than complicated.  
Flat is better than nested.  
Sparse is better than dense.  
Readability counts.  
Special cases aren't special enough to break the rules.  
Although practicality beats purity.  
Errors should never pass silently.  
Unless explicitly silenced.  
In the face of ambiguity, refuse the temptation to guess.  
There should be one-- and preferably only one --obvious way to do it.  
Although that way may not be obvious at first unless you're Dutch.  
Now is better than never.  
Although never is often better than *right* now.  
If the implementation is hard to explain, it's a bad idea.  
If the implementation is easy to explain, it may be a good idea.  
Namespaces are one honking great idea -- let's do more of those!  

### - 编码规范内容

可以在一下地址看到详细内容：

https://www.python.org/dev/peps/pep-0008/

页面里面详细介绍了所有的语法规则，比如命名的方法、语句太长的换行处理等等。

虽然说建议详细看一遍，但是，作为初学者，相信大部分人是没有耐心去看一遍的，（我学习变成语言是为了创造东西的，不是为了学习枷锁的，如果磕绊到了，我才会再来看这个。）并且，还有一个更加方便的处理，见下面。

### - 插件自动修正

如果使用的是 PyCharm 这个软件，是可以通过一款名叫 autopep8 的插件自动修正自己 code 里面的不合规范的书写的。

#### -- 下载安装

在终端（不需要进入 Python）输入 ```pip install autopep8```（如果是 mac 系统，好像如果有两个版本的 pip，需要输入 pip2 或者 pip3）

#### -- 和 PyCharm 整合

整合后，可以直接 右键 - 扩展External Tools - autopep8，就可以进行自动修改书写了。

那么如何整合呢？如下：

1. 左上角的 PyCharm - Preferences - Tools External Tools - 左下角 + - 进入 Edit Tool，
2. 除了 Name 按自己喜欢的来命名，其他的都是规范属性值，固定的。  
Tools setting:
    Programs:'autopep8'  
    Parameters:'--in-place --aggressive --aggressive \$FilePath$'  
    Working directory:'\$ProjectFileDir$'  
点击 Output Fileters - 添加，在对话框中：  
    Regular expression to match output 中入：‘\$FILE_PATH\$\:\$LINE\$\:\$COLUMNS\$\:.*’

#### -- 完成

然后就可以想开头写的那样的操作进行自动修正了。

## 总结

主要是统一格式，方便所有人员阅读。相当于遵守交通规则，整个交通才能顺畅、安全，大家一致准守这个 code rule，那么阅读 Python 就会轻松很多。

不过前期学习需要多多克服，不要嫌麻烦，对以后的正规性具有良好的作用。

---
注：  
个人微信公众号：codeAndWrite

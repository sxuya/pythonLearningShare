
# 34.【Python学习分享文章】\_standardLibrary_标准库

## 综述

Python 的库十分丰富。

其中最重要的是标准库，内容是核心、基础，之前的文章介绍的内容基本就是 standard library 的部分内容。

网址是：  
https://docs.python.org/3/library/index.html

## 核心内容

- 内建函数 Built-in Functions
- 内建类型 Built-in Tpyes
- 6.Text Processing Services 文本处理
- 8.Data Types 日期、时间的处理
- 16.Generic Operationg System Services 通用操作系统处理
- 19.Internet Data Handing 网络数据处理
- 26.Development Tools 开发工具
- 27.Debugging and Profiling 调试工具

## re（正则表达式）

### - 综述

6.Text Processing Services 里面的一个子库、子方法。  
链接如下：  
https://docs.python.org/3/library/re.html  
详细内容**还是**要看官方的文档。

re，regular expression 的缩写。不用官方的名字“正则表达式”，实在是让人不明所以，这是谁想出来的定义名字呢？（我认为知识最大的功能是有效地传递知识，哦，不，是传递思想，因此，表达要简要，更重要的是明了，没有很多人知道的“知识”，最后都会消失。这点就是尤其讨厌中国以前的独家秘笈、传男不传女而导致有效技能、工艺的丧失，金钱是生不带来、死不带去，脑袋里面知识也是一样的道理呀，你留着、埋葬着，有什么用呢？起码死前要留下点什么吧？）

按照英文直译，应该说是**“有规律的表达方法”**、**“有规则的表达形式”**等等，主要的目的是把现在网络上**“冗余、复杂、繁杂的文本信息”**，按照**一定的规则、规律进行匹配**，比如“\*”代表是重复的规则，那么“A\*”就是代表“无论多少个A重复的一段文本（string）”的一个表达、书写规则，可以代替“A”、“AA”、“AAA”、“AAAA”或者“AAAAA”等等。其他还有很多很多其他的规则，就是详细介绍的内容了。

主要的**目的**或者**作用**，是为了进行文本的匹配，最直接的例子就是**搜索引擎**的搜索信息的匹配需要使用这个技术。

### - demo_1

纯介绍简单功能，没有实际价值，了解即可，看过即可忽略。


```python
import re

p = re.compile('a')  # 要匹配的 string、要寻找的 string
p.match('a')  # .match() 就是被匹配的 string、匹配的范围
# 只能 match 一次，……不知如何多次输出，那就傻傻地用其他方法吧
```




    <_sre.SRE_Match object; span=(0, 1), match='a'>




```python
p_2 = re.compile('a')
print(p_2.match('abc'))  # 下面的展示稍稍有些区别
```

    <_sre.SRE_Match object; span=(0, 1), match='a'>
    


```python
p_3 = re.compile('a')
print(p_3.match('baaa'))
```

    None
    

### - demo\_2\_匹配相同、重复字符

【目标】：  
匹配“google”、“gogle”、“gooogle”、“goooogle”等等这样可能输入错误导致的字符，但是意思我们可以明白：都是要找“google”这个正确的 string。

【解释】：  
1. 那么，使用“固定字符”（确定的字符）是无法解决这个问题，因为我们也不知道用户到底输入错误成什么样子，到底输入了多少个“o”。
2. 这种重复的字符，比如本 demo 里面所涉及的“o”叫做“**元字符**”（元，就是起始的意思嘛，都是从第一个字符起始重复的嘛）。

【demo_2-1】：单纯可匹配


```python
import re

p = re.compile('google')
p.match('google')
```




    <_sre.SRE_Match object; span=(0, 6), match='google'>



【demo_2-2】：单纯不可匹配


```python
print(p.match('goooogle'))
```

    None
    

【demo_2-3】：正则表达式法可匹配


```python
p = re.compile('go*gle')
p.match('gooooooooogle')
```




    <_sre.SRE_Match object; span=(0, 13), match='gooooooooogle'>



【解释】：  
“o”后面加上“*”这个特殊字符，代表的是正则表达式“重复”的规则，无论重复多少次，只要是重复，就可以一直判定正确下去。

## 总结

上面是是为了引入、介绍“正则表达”的概念、作用、方法，具体的、详细的内容、方法在下面一篇文章里面介绍

---
注：  
个人微信公众号：codeAndWrite

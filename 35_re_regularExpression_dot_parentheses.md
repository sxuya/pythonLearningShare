
# 【Python学习分享文章】_re_详细介绍

## 综述

re 的具体内容有很多，我们主要是把握几个常见、常用的规则方法，即可满足大部分 code 工作。

这些，用来表达规则、方法的特殊字符叫做“**元字符**”。

常见元字符有：
- ```.``` （代表任意单个字符）
- ```^``` （从头开始匹配）
- ```$``` （从结尾开始匹配）
- ```*``` （前面的字符重复多次，包括0次）
- ```+``` （前面的字符重复多次，**不**包括0次）
- ```?``` （前面的字符重复0次或者1次）
- ```{重复出现的次数}``` （指定具体重复的次数）
- ```{min,max}``` （可以重复的次数，从min次到max次）
- ```[]``` （list，将.的任意匹配字符的功能限制为有限的字符）
- ```|``` （需要和“（）”括号一起使用）
- ```\d``` （匹配的是数字的 string，等价于```[0-9]+```
- ```\D``` （匹配不包含数字的 string）
- ```\s``` （只匹配 a-z 的 string）
- ```()``` （进行分组）
- ```^$``` （什么都不包括，代表空行）
- ```.\*?``` （不适用贪婪模式，就匹配到第一个就停止）（```*``` 这个方法就是贪婪模式）

## 点 ```.```（匹配任意单个字符）

### - 理解

一个点```.```代表一个字符，**任意的**，可以代表“a”、“b”、“3”等等。  
比如：“goog.e”可以匹配到“google”、“googpe”、“googje”、“googke”、“goog1e”（对应位置是数字1）等等所有可能。

【demo】：


```python
import re

p = re.compile("goog.e")
print(p.match("googee"))  # 这里的 match 是确认是否相同的意思，如果非要准确翻译的话就是“吻合”，
print(p.match("googke"))  # 意译上我觉得“验证是否完全一致”更好一些。
print(p.match("googlle")) # 因为只有一个任意字符，这里是两个了，不符合规则了
```

    <_sre.SRE_Match object; span=(0, 6), match='googee'>
    <_sre.SRE_Match object; span=(0, 6), match='googke'>
    None
    

### - 扩展使用

使用多个 ```.``` 来匹配多个任意字符，达到扩大陪陪范围的目的。  
比如：“g..gle”可以匹配到“gaagle”、“guugle”、“gxogle”、“geogle”等等中间对应**两个位置**为任意字符的 string。

【demo】：


```python
g = re.compile("g..gle")
print(g.match('gaogle'))
print(g.match('go8gle'))
print(g.match('g8o0gle')) # 规则是三个，这里是两个，不适用建立的规则
```

    <_sre.SRE_Match object; span=(0, 6), match='gaogle'>
    <_sre.SRE_Match object; span=(0, 6), match='go8gle'>
    None
    

### - 组合使用

如果个数太多，自己也会看晕掉，所有可以和 ```{n}``` 组合使用，形成重复 n 次的点，然后 n 个点就可以匹配 n 个任意字符了。

【demo】：确认输入的 string 是否为5个


```python
f = re.compile(".{5}")
print(f.match("adklkjb"))
print(f.match("ud8u3"))
print(f.match("ayuxsey"))
```

    <_sre.SRE_Match object; span=(0, 5), match='adklk'>
    <_sre.SRE_Match object; span=(0, 5), match='ud8u3'>
    <_sre.SRE_Match object; span=(0, 5), match='ayuxs'>
    

【理解】：  
其实只匹配对应```.```所在的位置的内容，后面的内容会**被忽略**，不会报错。  
那么，“goo”是可以匹配“google”的？确认一下，demo 如下：


```python
h = re.compile('goo')
print(h.match('google'))
```

    <_sre.SRE_Match object; span=(0, 3), match='goo'>
    

【确认】：  
nice，就是这样的理解，只会判断 ```.compile()``` 里面的内容，多余的 string **不会影响**这部分的判断。

## 分组```()```字符应用

以一个 demo 进行说明如何使用**分组功能**的 ```()``` 这个括号字符。

【目的】of demo：  
将用户输出的“日期”信息进行“年、月、日”的单独输出，这里直接用一个 string 替代当作输入的内容，不输出“用户输入”的 code。

【基调】of demo：  
使用```.```进行粗略搭建。


```python
birth = re.compile('....-..-..')
print(birth.match('2018-11-05'))
```

    <_sre.SRE_Match object; span=(0, 10), match='2018-11-05'>
    

【问题】of 原始 demo：  
如果用户的日期有个位数，像上面的“05”，并且用户输出成了“5”，那么两个点```..```的方法就会报错——就是会得到```None```，如下：


```python
print(birth.match('2018-11-5'))
```

    None
    

【调整】1_数字 of demo：  
对于数字，一个比较好的解决方法是使用 ```\d``` 这个专门匹配数学字符的方法来进行数字的匹配。如下：


```python
birth_2 = re.compile('\d-\d-\d')
print(birth_2.match('2018-11-05'))
```

    None
    

【问题】：  
没有内容输出！为什么？因为一个 ```\d``` 就是判别一个数字字符，而这里都不是一个。为了避免个数问题导致错误，可以使用 ```*``` 或者 ```+``` 让程序对数字个数进行动态调整。如下：  
（那其实，上面的 ```.``` 的方法也可以进行这样的设计！）


```python
birth_3 = re.compile('\d+-\d+-\d+')
print(birth_3.match('2018-11-05'))
```

    <_sre.SRE_Match object; span=(0, 10), match='2018-11-05'>
    

### - 进行分组设计

#### -- 进行匹配时的分组

使用 ```()``` 对年、月、日举行分组。如下：


```python
birth_4 = re.compile('(\d+)-(\d+)-(\d+)')  # 对于需要分入一组的内容，前后加上（括号）即可
print(birth_4.match('2018-11-05'))
```

    <_sre.SRE_Match object; span=(0, 10), match='2018-11-05'>
    

【分析】：  
好像并没有什么区别……等等下面的操作就可以看出区别了。

#### -- 进行分组后的输出

如下：


```python
birth_5 = re.compile('(\d+)-(\d+)-(\d+)')
print(birth_5.match('2018-11-05').group())  # .group() 什么参数都不添加，就是输出所有组的数据
```

    2018-11-05
    

#### -- 分组后的单个组的输出

如下：


```python
birth_6 = re.compile('(\d+)-(\d+)-(\d+)')
print(birth_6.match('2018-11-05').group(1))  # 输出第一组
```

    2018
    

【强烈疑问】：  
程序里面的第一个不都是用数字0进行指定的嘛！为什么这个方法的语法是使用数字1？中国程序员开发的库？……

#### -- 所有组内容分开全部输出

方法：```.groups()```。如下：


```python
birth_7 = re.compile('(\d+)-(\d+)-(\d+)')
print(birth_7.match('2018-11-5').groups())
```

    ('2018', '11', '5')
    

#### -- 将年月日三个数据分开进行赋值

因为最后产生的数据是 tuple 类型，所以直接用 tuple 对应的方法进行单个赋值。如下：


```python
birth_8 = re.compile('(\d+)-(\d+)-(\d+)')
year, month, day = birth_8.match('2018-11-5').groups()
print(year)
print(month)
print(day)
```

    2018
    11
    5
    

## 补充：不进行转义标记```r```

对于转义符，可以是按照转义的结构进行输出，也可以保留原始字符。如果保留，则要使用 ```r``` 进行标记。

比如，**文本内容** ```\n``` 如果按照转义的形式表现，就是换行，如果**前面**加入```r``` 的标记，就不会进行转义的表达，只会当作普通字符进行看待。

【demo】：进行转义表达输出：


```python
print('\nx\nxx')  # 就会先输出一个换行，再输出一个 x，紧跟着换行，在下一行输出一个 xx。
```

    
    x
    xx
    

【demo】：**不**进行转义表达输出：


```python
theInputStrings = r'\nx\nxx'
print(theInputStrings)  # 只会把这些所有的符号，当作纯字符看待，
```

    \nx\nxx
    

【完善】of demo：

避免输入的信息有什么转义符的使用，比如```\s```（匹配空白）、```\S```（匹配非空白），空白包括：```\n```（换行）、```\t```（制表符）。

如下：


```python
birth_9 = re.compile(r'(\d+)-(\d+)-(\d+)')  # 这里加入一个 r。最后结果并没有改变，
print(birth_9.match('2018-11-5').groups())  # 因为这里的内容没有特殊转义符嘛
```

    ('2018', '11', '5')
    

---
注：  
个人微信公众号：codeAndWrite

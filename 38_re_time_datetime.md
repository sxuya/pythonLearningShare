
# 38.【Python学习分享文章】_time\_datetime\_时间相关操作

## 综述

比较常用的两个方法就是：
- 8.Date Types 里面的 ```.datetime()```
- 16.Generic Operating Services 里面的 ```.time()```

【常用作用】

- ```.time()```：时间的查看
- ```.datetime()```：时间的修改

## ```.time()```

是系统操作里面的模块（功能），和操作系统的时间有关。主要用于“查看”，举例几个常见时间调用。

### - 时间的秒数

code 如下：


```python
import time
print(time.time())
```

    1542596249.5257728
    

【解释】：  
这个数字代表的是“从1970年1月1日到当前时间点的总秒数”。

### - 年月日形式封装

上面的时间不是人类所使用的，因此使用一些 .time 封装好的、处理过的时间表达，如 ```.localtime()```。

如下：


```python
print(time.localtime())
```

    time.struct_time(tm_year=2018, tm_mon=11, tm_mday=19, tm_hour=11, tm_min=16, tm_sec=28, tm_wday=0, tm_yday=323, tm_isdst=0)
    

### - 再优化的封装

上述的表述还是不是太适合阅读，所以使用另外一个方法，进行**格式化地**表达，如 ```.strftime()```（string 的缩写，f 是 format格式 的缩写）。  
这个方法是需要给定输出格式的表达方式的，不能直接使用。

一种格式的 argument 给定方式，如下：


```python
print(time.strftime('%Y-%m-%d %H:%M:%S'))
```

    2018-11-19 11:24:46
    

【解释】：
- “%一个字母”。是一种参数的引用，是有大小写区分的，有些是只有大写的参数 or 小写的参数，另外一些大小写的参数形式都有，但是代表的是不同的内容，具体的内容参见https://docs.python.org/3/library/time.html#time.strftime
- 连接格式。中间的“-”和“：”可以自己根据需要换成其他的连接字符，形成自己想要的**时间格式**。

【变形使用】：  
如果进行文件的命名使用，时间的格式希望就是纯数字，那么就“不使用连接符号”即可，如下：


```python
print(time.strftime('%Y%m%d'))
```

    20181119
    

## ```.datetime()```

主要用于时间的处理，比如修改、指定特定时间等等。

### - 获取当前时间数据


```python
import datetime

print(datetime.datetime.now())
```

    2018-11-19 11:38:24.090691
    

【疑惑】：  
那这个模块获取的时间不是更符合人类阅读么？那么两个模块有区别作用呢？——再说了，在这里保留先。2018年11月19日 11:39:33

### - 获取现在时间的一段时间后的时间数据

【目的】：  
取得当前时间10min后的时间数据。如下：


```python
timeDelta = datetime.timedelta(minutes=10)  # 理科里，差值默认使用 △（delta） 作为表达符号，
newTime = datetime.datetime.now() + timeDelta  # 比如 △t 表示时间差
print(datetime.datetime.now())
print(newTime)
```

    2018-11-19 11:43:58.470262
    2018-11-19 11:53:58.470262
    

### - 获取指定时间的一段时间后的时间数据

步骤：  
1. 先指定一个时间
1. 再指定一个时间差
1. 指定时间上叠加时间差


```python
oneDay = datetime.datetime(2018, 5, 11)  # 指定了一个时间，直接用参数输入
timeDelta = datetime.timedelta(days=25)
updatedDay = oneDay + timeDelta
print('指定的时间：%s' %oneDay)
print('时间差是：%s' %timeDelta)
print('新的时间是：%s' %updatedDay)
```

    指定的时间：2018-05-11 00:00:00
    时间差是：25 days, 0:00:00
    新的时间是：2018-06-05 00:00:00
    

## 总结

还是常规的，就是参数的格式要注意：
- datetime 里面很多是要有“s”的；
- 方法的名字是没有“驼峰形式的”；
- “5”是不能输入成“05”的；

具体的使用的时候再用文档进行验证、核对了。

---
注：  
个人微信公众号：codeAndWrite

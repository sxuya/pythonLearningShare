
# 22.【Python学习分享文章】_build-in function（内建函数）

## 综述

### - 主体

主要介绍四个 build-in functions，分别是：
1. filter()
2. map()
3. reduce()
4. zip()

#### - 主要作用

对下面的数据处理：
1. 合并
2. 累加工作
3. 等等

会使用到这几个函数。

## filter()

### - 个人理解

filter 的意思是“过滤”、“筛选”，主要就是“根据自己建立的规则，去筛选数据”。

一个朴素的类比：
1. “原始数据”就是“原料沙石”；
2. “处理规则”就是“筛眼大小”；
3. “处理后数据”就是“细分的沙石”。

### - demo

#### -- filter() list


```python
aList = [1, 5, 7, 2, 4, 6, 9, -2]
filteredList = list(filter(lambda x:x<4, aList))  # 需要使用list将结果序列化，要不然无法进行输出、处理。
print(filteredList)  # 进行输出。
```

    [1, 2, -2]
    

## map()

### - 理解

将过个参数、数据，依次进行处理。相当于构造一个“数学上的函数”，建立函数的映射关系，“原始输入”相当于“自变量x”，“输出结果”相当于“函数值y”

### - demo

#### -- 单个list


```python
bList = [1, 14, 5]
bListMaped = list(map(lambda x:2*(x-1), bList)) # 中间的乘号 * 不能像平时数学书写省略掉
print(bListMaped)
```

    [0, 26, 8]
    

#### -- 两个list（长度一致）


```python
cList = [3, 2, 1]
bcListMaped = list(map(lambda x,y:x-y,bList, cList)) # 相同个数，相同位置的数据进行 lambda 规则运算
print(bcListMaped)
```

    [-2, 12, 4]
    

#### -- 两个list（长度不同）


```python
dList = [2, 5, 3, 7]
bdListMaped = list(map(lambda x,y:x-y,bList, dList))
print(bdListMaped)
```

    [-1, 9, 2]
    

分析：

也就是以最短的、可算的位置为准，其他位置的数据被遗弃。

## reduce()

### - 注意

1. 不能直接使用，需要进行导入：```from functools import reduce```；
2. 也是只能处理一个序列。
3. 所有的数据和相同的 initial（初始值）做函数定义的运算

### - demo

#### -- 


```python
from functools import reduce
eList = [1, 2, 3, 4]
print(reduce(lambda x,y:x-y, [2,5,11],1) )
print(reduce(lambda x,y:x-y, [11,5,2],1) )
print(reduce(lambda x,y:y-x, [11,5,2,3],1) )
print(reduce(lambda x,y:y-x, [3,2,5,11],1) )
# 这是一个单个数字的结果，计算的是最终的函数值，因此不需要 list 呈现结果

```

    -17
    -17
    -4
    6
    

解释：

后面的“1”就是 initial，代表的是x的初始值，每次计算的结果是赋值给x的。

1. ((1-2)-5)-11 = -17
2. ((1-11)-5)-2 = -17
3. 3-(2-((5-(11-1))) = 7
4. 11-(5-(2-(3-1))) = 6

## zip()

### - 整体感觉

电脑上的用法叫压缩，也就是把多个数据合成一个感觉。code 里面的 zip 是将两个（多个可以？）数据一次运算成一个。

### - demo

#### -- 合并两个元组


```python
aTuple = (1, 2, 4)
bTuple = (33, 6, 5)
cTuple = (-11, -4, 7)
abTupleZiped = zip(aTuple, bTuple)
print(abTupleZiped)
abcTupleZiped =  zip(aTuple, bTuple, cTuple)
print(abcTupleZiped)
for i in abTupleZiped:
    print(i)
for i in abcTupleZiped:
    print(i)
```

    <zip object at 0x0000023F3692DCC8>
    <zip object at 0x0000023F3692DD08>
    (1, 33)
    (2, 6)
    (4, 5)
    (1, 33, -11)
    (2, 6, -4)
    (4, 5, 7)
    

解释：

纵向变换后进行整合。就是线性代数里面的“矩阵转换”。

因为使用了 ```for … i …```的语句，说明最后的数据是可迭代的数据类型iter。

#### -- 对调字典的key和value


```python
aDict = {'a':'aaa', 'b':999, 'c':577}
aDictZiped = dict(zip(aDict.values(), aDict.keys()))
print(aDictZiped)
```

    {'aaa': 'a', 999: 'b', 577: 'c'}
    

---
注：  
个人微信公众号：codeAndWrite

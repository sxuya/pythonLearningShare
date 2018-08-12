
# 14.【Python学习分享文章】_列表推导式&字典推导式

## 综述

新建一个带有初始化数值的 list 和 dict，C 语言、Java 等语言采用的普通的方法是，即“不优雅”的方法是：

1. 先定义数据类型；
2. 再输入初始化值。

Python 里面的“推导式”，就是将这两部合并为一步的操作。

**独有的**语法呦~

## list 推导式的 demo 介绍

### - 例子1

【目标：】得到一个1~20范围内的偶数的平方值的 list：

#### “不优雅”方式：


```python
# 获得1~20的偶数的平方值的 list

list = []
for i in range(1, 21):
    if i % 2 == 0:
        list.append(i*i)
        
print(list)
```

    [4, 16, 36, 64, 100, 144, 196, 256, 324, 400]
    

#### “优雅”方式：

主要思路：将 ```for```、```if``` 语句整合到“[ ]”里面，从而变得简洁。


```python
# step 1:[]
# step 2:[for i in range(1, 21) if i%2==0]
# step 3:[i*i for i in range(1, 21) if i%2==0]
betterList = [i*i for i in range(1, 21) if i%2==0]

print(betterList)
```

    [4, 16, 36, 64, 100, 144, 196, 256, 324, 400]
    

【结果：】获得了同样的结果，但是可读性增加了很多。（这里的“可读性”只是相对来说，看多了“不优雅”的写法，也能马上明白 code 表达的内容。）

## dict 推导式的 demo 介绍

### - 例子1

之前的 dict 文章里面已经出现了，这里再摘录过来。

【目标：】记录统计到的生肖人数，建立初始化 dict。

#### “不优雅”方式：


```python
chinese_zodiac = "猴鸡狗猪鼠牛虎兔龙蛇马羊"

c_list = {}
for animal in chinese_zodiac:
    c_list[animal] = 0
    
print(c_list)
```

    {'鼠': 0, '虎': 0, '龙': 0, '狗': 0, '马': 0, '猪': 0, '蛇': 0, '猴': 0, '兔': 0, '羊': 0, '牛': 0, '鸡': 0}
    

#### “优雅”方式：


```python
# step 1:d_list = {for animal in chinese_zodiac} # 这里的 animal 会历遍所有生肖进行指代。
# step 2:
d_list = {animal:0 for animal in chinese_zodiac}

print(d_list)
```

    {'鼠': 0, '虎': 0, '龙': 0, '狗': 0, '马': 0, '猪': 0, '蛇': 0, '猴': 0, '兔': 0, '羊': 0, '牛': 0, '鸡': 0}
    

---
注：  
个人微信公众号：codeAndWrite

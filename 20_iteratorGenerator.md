
# 20.【Python学习分享文章】_iterator（迭代器）&generator（生成器）

## 综述

还不太清楚有什么用。

整体的表现就是可以一个一个排列地一次取出数据。取出一个数据，如果没有进行连续操作，下一个数据的提取会暂停，等待操作。

**【个人理解】**  
iterator（迭代器）：  
无循环、单向、可暂停取出数据的一个东西。

generator（生成器）：  
通过一个特定方法 code 的iterator。

## iterator（迭代器）

定义？：能够实现依次处理数据的**函数**就是叫做迭代器。

### - 基本方法 method

method 也是函数，相当于函数的子函数，所以可能因为这个原因，就换做一个叫法（可能我的理解是不对的）。

iterator（迭代器）两个基本 method：
1. ```iter()```
2. ```next()```

#### -- 例子：


```python
aList = ["smartian", "geek", 10000, "love"]
# print(aList)
it = iter(aList)
print(it) # 理解：也就是生成器默认不带数据，只有调用 next 才会产生数据？
print(next(it)) # 之前都没有进行数据调用，所以 next 获取的是第0个数据
```

    <list_iterator object at 0x0000020F3783F668>
    smartian
    


```python
print(next(it)) # 接下来一个数据
print(next(it)) # 再接下来一个数据
print(next(it)) # 再接下来一个数据进行打印输出
```

    geek
    10000
    love
    


```python
print(next(it)) # 因为 iterator 里面只有4个数据，再没有数据可以取出了，
# StopIteration 就是“超出了迭代器的个数”，需要停止了
```


    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    <ipython-input-11-3504ed077bb3> in <module>()
    ----> 1 print(next(it)) # 因为 iterator 里面只有4个数据，再没有数据可以取出了，
          2 # StopIteration 就是“超出了迭代器的个数”，需要停止了
    

    StopIteration: 


### - 自带的简单 iterator

也就是```range(start， stop， step)```

#### -- 例子1：  
默认 step（步长）=1的增加。


```python
for i in range(10, 15):
    print(i)
```

    10
    11
    12
    13
    14
    

#### -- 例子2：  
修改 step 为其他数值。


```python
for i in range(10, 18, 2):
    print(i)
```

    10
    12
    14
    16
    

#### -- 反例3：  
修改为 float（小数）的 step，```range()```是不支持的。


```python
for i in range(10, 18, 0.5):
    print(i)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-14-78c49d4392e6> in <module>()
    ----> 1 for i in range(10, 18, 0.5):
          2     print(i)
    

    TypeError: 'float' object cannot be interpreted as an integer


## generator（生成器）

个人理解：  
感觉像自己制作自己需要的 iterator，用一个特定的 method。

### - 关键 method：
```yield()```

### - demo 说明
#### -- 例子1：step 可为 float 的 range


```python
def frange(start, stop, step):
    tempX = start
    while tempX < stop:
        yield tempX
        tempX += step

it2 = frange(10, 14, 0.5)
# print(list(it2)) # 写了这句可以得到list，
# 但是生成器好像用完了，后面再 next 就会报 StopIterator 错误
# 也就是说，迭代器&生成器是一次性的
# print(it2)
# it3 = iter(it2)
# print(it3)
print(next(it2))
print(next(it2))
print(next(it2))

for i in frange(20, 22, 0.5):
    print(i)
```

    10
    10.5
    11.0
    20
    20.5
    21.0
    21.5
    

#### -- 例子2：不使用 yield 的后果


```python
def frange2(start, stop, step):
    tempX = start
    while tempX < stop:
        print(tempX)
        tempX += step
        
it4 = frange2(3, 5, 0.5)
for i in frange2(41, 43, 0.5):
    i # 这个时候就没有可以用了。
    # for 语句应该是需要 iterator or generator的
    # 现在记住就好，以后碰到深入理解再说吧。
```

    3
    3.5
    4.0
    4.5
    41
    41.5
    42.0
    42.5
    


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-46-9188e9da5bf6> in <module>()
          6 
          7 it4 = frange2(3, 5, 0.5)
    ----> 8 for i in frange2(41, 43, 0.5):
          9     i # 这个时候就没有可以用了。
         10     # for 语句应该是需要 iterator or generator的
    

    TypeError: 'NoneType' object is not iterable


---
注：  
个人微信公众号：codeAndWrite

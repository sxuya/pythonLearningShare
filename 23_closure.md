
# 23.【Python学习分享文章】_closure（闭包）

## 综述理解

1. 闭包也是函数，只不过是一个名字的变化。“函数里面引用函数的函数”就叫做“闭包closure”。
2. 来源：if 和 while 是可以嵌套的，所以想法就是“函数能不能也嵌套”呢？

### - demo说明结构

非有用结构，只是将“闭包closure”的思想说明。*对于简单的实现使用高级的方法，肯定会“看起来更加复杂”。*

#### -- 【目的】：计算了个数字的和

#### -- 函数实现：


```python
def sumTwoNum():
    a = 2
    b = 4
    return a+b
```

#### -- closure 实现：


```python
def sum(a):    # 两个函数是嵌套。将这一层的函数叫做“外部函数”
    def add(b):    # 将这一层的函数叫做“内部函数”
        return a+b    # 内部函数引用了外部函数的参数a
    return add    # 返回的是函数的名字，【不能】带括号
```

#### -- 【解释】

想这种“内部函数引用外部函数的参数”，从而形成嵌套、关联的情形的函数结构，就叫做“closure闭包”。

```add```：函数的引用 or 函数名称，相当于复制结构。  
```add()```：函数的调用，也就是使用的意思。

#### -- 类型区别辨析


```python
sumFunc = sumTwoNum()
print(type(sumFunc))
sumClos = sum(2)
print((type(sumClos)))
```

    <class 'int'>
    <class 'function'>
    

【解释】

```sumTwoNum```这个函数很直接，返回的是计算完成的结果，计算的结果就是 int 数据类型

```sum(2)```说明整体函数中，“外部函数” ```sum(a)``` 的参数 “a” 是2，这个“参数值”传入到了“内部函数”，“外部函数”定义的返回是函数 “add”，所以相当于现在 ```sumClos``` 是一个“以2为基础的计算和另一个数字和的函数”，所以类型是 ```function```。

因此，```sumClos``` 就是函数名字，需要传入数值就可以直接“调用”了：


```python
print(sumClos(4))
```

    6
    

### - 整体框架

#### -- 统一形式


```python
def 外部函数名字(外部函数参数):
    def 内部函数名字(内部函数参数名字):
        需要进行的参数处理的 code；【一定】需要使用外部函数参数，否则就不需要 closure 结构了。
    return 不带括号的内部函数的名字，进行引用
```

#### -- demo展示


```python
def sum():
    def add():
        return 
    return add
```

## 实现“计数器”功能

### - 实现功能：

每次调用函数，就进行数值增1处理。

### - 第一步：套路

```
def counter():
    一个用来计数用的变量
    def add_one():
        +1功能实现的 code
    return add_one
```

### - 第二步：变量确定
如果是整型数据，离开了函数里面，也就是之前笔记里面的“作用域是局部的”，离开函数之后就失效了。失效了？对于内部函数来说的。

一个解决方法：list 数据。

### - 第三步：填写变量、功能 code


```python
def counter():
    cnt = [0]    # 定义一个只有一个数据的 list，初始值是0
    def add_one():
        cnt[0] += 1
        return cnt[0]
    return add_one

zeroCounter = counter()
print(zeroCounter())
print(zeroCounter())
print(zeroCounter())
print(zeroCounter())
```

#### -- 使用整数变量实现

只要将前面函数的“作用域”理解到位，就可以使用整型来实现相同的功能，不过变量书写不那么优雅。

code 如下：


```python
aCounter = 0
def counter():  
    def add_one():
        global aCounter
        aCounter += 1
        return aCounter
    return add_one

zeroCounter = counter()
print(zeroCounter())
print(zeroCounter())
print(zeroCounter())
print(zeroCounter())
```

    1
    2
    3
    4
    

### - 建立两个计数器


```python
def counterB(first=0):    # first 默认是0，如果有传入数据，则按照传入的数据进行。
    cnt = [first]    # 定义一个只有一个数据的 list，初始值是0
    def add_one():
        cnt[0] += 1
        return cnt[0]
    return add_one

tenCounter = counterB(9)
print(tenCounter())
print(tenCounter())
print(tenCounter())
fiveCounter = counterB(4)
print(fiveCounter())
print(fiveCounter())
print(fiveCounter())
zeroCounter = counterB()
print(zeroCounter())
print(zeroCounter())
print(zeroCounter())


```

    10
    11
    12
    5
    6
    7
    1
    2
    3
    

## 再次理解

闭包，相当于数学里面建立一组相同结构的函数，比如一次函数 y = kx + b，二次函数 y = ax^2 + bx + c......将相同的字母进行分离，相当于把“参数”（比如k、a、b、c）和“自变量”（x）分离开来。

如果参数比较多，可以再把参数分成多组，进行分离设定。

## 更有价值的功能：一次函数的实现

### - 功能背景

进行一次函数计算的时候，我们在一些高级的计算机会这么操作：
1. 先确定、给定结构，定下 斜率k、截距b
2. 计算大量不同 x 对应的函数值 y

### - 普通函数实现

```
def 函数名字(k, b, x):
    实现功能的 code
```
【问题】：  
1. 每一次输入x的时候，即使函数没有变动，也需要再一次输入 k、b 的数值。
2. 如果定义了 k、b 的情况，那么这两个参数就不能在变动了。
3. 如果使用变量去赋值 k、b，那么也基本可以，但是会把这个功能分裂开来，可读性不高。

### - 闭包实现

code 如下：


```python
def line(k, b):
    def calculateY(x):
        return k*x + b
    return calculateY
aLine = line(3, 5)    # 定下结构为 3*x+5
print(aLine(4))    # 计算 3*4+5
print(aLine(8))    # 计算 3*8+5
bLine = line(-4, 2)
print(bLine(7))    #计算-4*7+2
print(bLine(-1))    #计算-4*（-1）+2
```

    17
    29
    -26
    6
    

## 好处总结

0. 将“传递变量”升级为“传递函数”。
1. 减少很多参数的传输、定义、调用。
2. code 会优雅，即可读性快

---
注：  
个人微信公众号：codeAndWrite

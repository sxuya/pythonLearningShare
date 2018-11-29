
# 24.【Python学习分享文章】_decorator（装饰器）

## 综述

装饰器，是“闭包”的更加接近自然语意的表达，也是函数。

这种使代码获得相同效果，但是代码更加简洁，有更高的可读性的处理，就叫做“**加糖**”（甜蜜到飞起），这样的结构就叫做“**Syntactic sugar语法糖**”

### - demo 说明作用

#### -- 目的：

计算显示“程序运行时间”。

#### -- 常规code：


```python
import time

print(time.time())   
# 返回从1970年01月01号到运行这句code时的总时间秒数
# 从1970.01.01的“绝对时间”

def sleepSomeTime():
    time.sleep(3)    # 让程序休息（停止）3秒钟，单位是【秒】
    
startTime = time.time()    # 获得程序开始运行到这里的绝对时间
sleepSomeTime()    # 调用停止3秒的函数
stopTime = time.time()    # 获得程序运行到这里（结束的地方）的绝对时间
print('函数运行了 %s 秒' %(stopTime-startTime))    # 计算中间程序运行的时间
```

    1538103425.260957
    函数运行了 3.0007355213165283 秒
    

#### -- 问题

如果 ```sleepSomeTime``` 所代表的函数（可以是很复杂，因为只是讲解思路，所以会感觉很奇怪，一句的 code 函数后变成了两句）需要多次运行，那么就需要多次建立 ```startTime```、```stopTime```，很很冗杂。

能不能把这些重复的内容使用函数处理呢？

#### -- 目的

decorator 的作用是吧函数中还需要构建功能的部分也构造函数，但是不在原函数（即“被装饰函数”）进行处理，进行单独编写，使代码层次更加明确、易读。

#### -- decorator 写法:


```python
import time

def timer(func):    # 外部函数
    def wrapper():    # 内部函数
        startTime = time.time()
        func()    # 需要的功能，在外部进行函数构造，这里进行调用。这里用sleep代替进行演示
        # 外部函数传入了“函数 func” 到内部函数，相当少“闭包”的逻辑，不过闭包是传入参数
        stopTime = time.time()
        print('函数运行了 %s 秒' %(stopTime-startTime))
    return wrapper

@timer    # 这个函数叫做“装饰函数”，这里面（也就是上面）的code对下面的函数进行装饰、补充
def sleepSomeTime():    # 这个函数叫做“被装饰函数”，这个是【主体】
    time.sleep(3)
    
sleepSomeTime()    # 被被装饰函数才是主体，所以使用功能是用调用这个函数名字的
# 建立 decorator 后，调用 timer 和 sleepSomeTime 的嵌套的函数
# 只要写一句 sleepSomeTime 就可以了，不用再写 startTime 和 stopTime 了。
```

    函数运行了 3.0049169063568115 秒
    

#### -- 解释(**important**）

当运行 ```sleepSomeTime``` 时，Python 会寻找到定义的 ```def sleepSomeTime```,然后上面有一个装饰器语句，不会直接运行 ```sleepSomeTime```，而是会再向上寻找 @ 后面的 ```timer``` 函数，然后会把 ```sleepSomeTime``` 传输到 ```timer``` 中，也就是相当于：

```
timer(sleepSomeTime())
```

如果要完成得到结果，就是如下code：
```
getSleepTime = timer(sleepSomeTime())    # getSleepTime 成为定义的函数里面的 wrapper 的结构的函数
getSleepTime()    # 运行这个函数
```

因为不够【优雅】，然后就演化成了 decorator 的写法。

## 复杂demo_1

被装饰函数（主体函数）带的【参数】传递到装饰函数 的 装饰器的构建。

### - 框架


```python
def waiFunc(chuanFunc):
    def neiFunc():
        start
        chuanFunc
        stop
    return neiFunc
```

### - 填充功能

【功能】：实现“计算两个数据的累加结果”


```python
def waiFunc(chuanFunc):
    def neiFunc(a, b):    # 下面 add 函数的参数a、b需要写在内函数这里
        start
        chuanFunc(a, b)
        stop
    return neiFunc

@waiFunc
def add(a, b):
    print(a+b)
```

### - 外函数建立功能

只是简单建立一个功能呢：进行提示程序运行到哪里。


```python
def tip(chuanFunc):
    def neiFunc(a, b):
        print('开始要调用外函数传递过来的函数了')
        chuanFunc(a, b)
        print('调用结束了')
    return neiFunc

@tip
def add(a, b):
    print(a+b)
    
add(4, 5)
```

    开始要调用外函数传递过来的函数了
    9
    调用结束了
    

### - 延伸展示用法

可以把 ```tip``` 这个装饰函数，去装饰其他主体函数，进行相同的提示。

（可以有什么变形呢？遇到的code 不够多，不明白到底有什么作用）

#### -- 装饰减法


```python
@tip
def sub(a, b):
    print(a-b)
    
sub(3, 99)
```

    开始要调用外函数传递过来的函数了
    -96
    调用结束了
    

#### -- 装饰乘法


```python
@tip
def multi(a,b):
    print(a * b)
    
multi(2, -5)
```

    开始要调用外函数传递过来的函数了
    -10
    调用结束了
    

## demo_2_装饰器参数

将装饰器的参数传入进行处理、调用。

### - 增加装饰器的参数


```python
def tip(chuanFunc):
    def neiFunc(a, b):
        print('开始要调用外函数传递过来的函数了')
        chuanFunc(a, b)
        print('调用结束了')
    return neiFunc

@tip('add')    # 给装饰器一个特定标记，因为下面的被装饰函数是add，所以增加“add”的标记参数
def add(a, b):
    print(a+b)
```

### - 结构调整

【问题】：tip 的函数定义的时候，已经说明使用的参数是```chuanFunc```，所以这个 @ 后面增加的参数没有位置传入了。

【解决】：再嵌套一层外函数，将装饰器的参数通过最外面一层传入，让里面的 ```tip```和```neiFunc```可以进行调用。

code 如下：


```python
def tipWithParam(opName):
    def tip(chuanFunc):
        def neiFunc(a, b):
            print('开始要调用外函数传递过来的函数了，')
            print('且运行的机制是装饰器参数定义的"%s"计算方式' %opName)
            chuanFunc(a, b)
            print('调用结束了')
        return neiFunc
    return tip

@tipWithParam('addOperation')
def add(a, b):
    print(a+b)
# 上面这个语句结构，说明 Python 机制是：
# 如果装饰器没有参数，那么就是把装饰器下面跟着的主体函数进行装饰，也就是传入到装饰函数
# 如果装饰器函数有参数，那么先会把参数传输装饰器函数，得到一个新的装饰器函数
# 这时候，再把主体函数传入到生成的具有参数特征的装饰器函数，再进行之前的逻辑的运行顺序

add(3, 5)

@tipWithParam('subOperation')
def sub(a, b):
    print(a-b)

sub(3, 8)
```

    开始要调用外函数传递过来的函数了，
    且运行的机制是装饰器参数定义的"addOperation"计算方式
    8
    调用结束了
    开始要调用外函数传递过来的函数了，
    且运行的机制是装饰器参数定义的"subOperation"计算方式
    -5
    调用结束了
    

### - 作用&好处

可以把装饰器变得通用化，可以根据被装饰的主体函数的特点，设定不一样的装饰情况。

## demo_3_获取其他数据

【目的】：下面的 code 是为了获取“主体函数”（被装饰函数）的函数名。

code 如下：


```python
def tipWithParam(opName):
    def tip(chuanFunc):
        def neiFunc(a, b):
            print('开始要调用外函数传递过来的函数了，')
            print('且运行的机制是装饰器参数定义的"%s"计算方式' %opName)
            print('但是，注意，真正的运算是按照函数名字进行的（如果你主体函数没有错的话），')
            print('主体函数的名字是什么呢？是"%s"'%chuanFunc.__name__)
            chuanFunc(a, b)
            print('调用结束了')
        return neiFunc
    return tip

@tipWithParam('addOperation')
def add(a, b):
    print(a+b)

add(3, 5)

@tipWithParam('subOperation')
def sub(a, b):
    print(a-b)

sub(3, 8)
```

    开始要调用外函数传递过来的函数了，
    且运行的机制是装饰器参数定义的"addOperation"计算方式
    但是，注意，真正的运算是按照函数名字进行的（如果你主体函数没有错的话），
    主体函数的名字是什么呢？是"add"
    8
    调用结束了
    开始要调用外函数传递过来的函数了，
    且运行的机制是装饰器参数定义的"subOperation"计算方式
    但是，注意，真正的运算是按照函数名字进行的（如果你主体函数没有错的话），
    主体函数的名字是什么呢？是"sub"
    -5
    调用结束了
    

## 总结

1. 调用函数的时候，不用重复在主体前后添加修饰代码
2. 构建函数的时候，只需在主体函数前面增加“@引用的装饰函数名字”，如果有参数，就使用“调用”的语句
3. 让 code 更加简洁。

---
注：  
个人微信公众号：codeAndWrite


# 21.【Python学习分享文章】_lambda函数

## 综述

主要的目的是：使得代码优美。

主要的用途是：简化简单的函数，复杂的函数就不在处理的范围里面了。

## demo 解释

主要的方式是：通过化简前后的对比进行说明。

### - 例子1：返回型

【原始函数】：


```python
def true():
    return True

true()
```




    True



个人感受：看到的这个教程的例子，感觉这个没有什么能够理解的，到底为什么这么出教程呢？大家看看过一遍就好了。

这需要 lambda 的函数的特点：建立函数比直接引用还要复杂。（可能有些地方必须需要函数，但是又是简单的，如果没有 lambda 会不优美。）

【lambda 型】

【化简思路】

步骤1.两行变成：


```python
def true(): return True
```

步骤2.精简函数名（其实就是不要了，因为这类函数简单，且一般只是一次性使用）


```python
lambda : return True
```

步骤3.省略 return 这个关键字。（也就是说，lambda 默认是 return 数据结果的，而不是 print）


```python
lambda : True
```

### - 例子2：简单计算

目的：计算、返回两个数的和。

【函数型】


```python
def add(x, y):
    return x+y

print(add(4, 5))
```

    9
    

【lambda 型】


```python
lambda x, y: x+y
# 例子1 的函数没有参数，这个例子有
# 省略的只是函数名字，参数的名字是要使用，所以不能省略。
# 因为这个 lambda 应该是不能建立变量，所以这里只是展示他的结构。
```




    <function __main__.<lambda>(x, y)>



### - 例子3：还原 lambda 函数1

【lambda 型】

之前星座程序用过的一个（第7篇文章例子）：


```python
lambda x: x <= (month, day)
```

【函数型】


```python
def compare(x):
    return x <= (month, day)
```

### - 例子4：还原 lambda 函数2

【lambda 型】


```python
lambda item:item[1]
```

【函数型】


```python
def getFirst(item):
    return item[1]
```

## 总结

1. lambda 函数主要用于函数、方法里面的简单处理的函数的代替；

2. 不会作为单独使用；

3. 具有临时性、一次性的特点。

---
注：  
个人微信公众号：codeAndWrite


#  31.【Python学习分享文章】_with 自定义类的情况

## 综述

自定义信息，什么信息呢？使用某个 class类 的时候的，对使用和停止使用两个状态进行信息输出。

## 想法来源

对文件进行打开等操作的时候，会对“异常”进行处理，相应的完整语句是：


```python
f = open('fileName.txt', 'r')

try:
    r = f.read()
except:  # 出现异常会进行的操作
    pass  # 这里不进行操作，只是 pass 掉，让程序继续往下运行
finally: # 无论正确还是错误，都进行的操作
    f.close()  # 这里是进行文件的关闭，释放内存
```

因为 Python 所追求的简洁语法的特点，就创造了如下的方法：


```python
with open('fileName', 'r') as f:
    f.read()
```

使用 ```with``` 语句，就默认自带文件的最终关闭操作。

以此为准，出现了下面的类似的操作。

## 使用 with 方法调用 class类

### - 基本结构


```python
class NewCreatedClassName():
    def __enter__(self):  # class 初始化的时候会自动调用的特殊语句
        pass  # 一个操作，这里用无害的 pass 代替、
    def __exit__(self, exc_type, exc_val, exc_tb):  # class 结束的时候会自动调用的特殊语句
        pass
    
with NewCreatedClassName():
    pass  # 执行的操作、代码，需要的目的
```

自动调用的两个语句：```__enter__```、```__exit__``` 和原先使用的初始化的特数语句 ```__init__``` 是一个意思。

### - with 语句简单 demo（无异常）

展示 ```__enter__```、```__exit__``` 的执行效果。如下：


```python
class AClassWhatever():
    def __init__(self):
        pass
    def __enter__(self):
        print("1.现在进入了，所以马上到这里，执行 __enter__ 这里的代码")
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("2.结束使用这个 class 时，会执行这里面的代码，用打印内容代替")
        
with AClassWhatever():
    print("3.这里的内容是class之外的操作，是在开始确认使用类AClassWithWith、执行 __enter__ 后才执行的，")
    print("4.执行完之后，就自动执行结束的 __exit__ 里面的内容，什么呢？如下：")
```

    1.现在进入了，所以马上到这里，执行 __enter__ 这里的代码
    3.这里的内容是class之外的操作，是在开始确认使用类AClassWithWith、执行 __enter__ 后才执行的，
    4.执行完之后，就自动执行结束的 __exit__ 里面的内容，什么呢？如下：
    2.结束使用这个 class 时，会执行这里面的代码，用打印内容代替
    

【牢骚】：  
我自己编写的解释demo，可能更好理解吧，新手就是不知道代码里面到底是什么，总是简称代指，真的着急费解。

一直无法理解demo就是demo为什么非要那么简单呢？太简单了理解就多了，只有**信息冗余、互相关联**，才能表达明确的意思。

学习课程介绍的代码：

```
class Testwith():
    def __enter__(self):
        print('run')
    def __exit__(self, exc_type, exc_val, exc_ty):
        print('exit')
        
with TestWith():
    print('Test is running')
```

关键词有 exit，打印内容也出现 exit，不明白的人很容易被带乱了吧。

### - with 语句有异常的处理方法

如果 class类 发生了异常，那么 ```__exit__``` 里面的 ```exc_tb``` 这个属性值就会捕获错误的提示，获得 参数值，如果没有异常，就会是 ```None``` 这个参数值，判断关系使用 ```is``` 关键字。代码如下：


```python
class AClassWhatever():
    def __init__(self):
        pass
    def __enter__(self):
        print("运行这个class内容之前，会先执行这个内容")
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("运行完前面的功能、离开这个class之前，用这里的代码作为结束")
        if exc_tb is None:
            print("everything is OK~")
        else:
            print("there is error,it's %s" %exc_tb)
        
with AClassWhatever():
    print("开始类之外、这里的正文的内容，")
    raise NameError('随意写入的提示信息')  # 这里只是认为制造一个错误，程序会停止，具体情况看实际创建的代码了
```

    运行这个class内容之前，会先执行这个内容
    开始类之外、这里的正文的内容，
    运行完前面的功能、离开这个class之前，用这里的代码作为结束
    there is error,it's <traceback object at 0x0000023EE169E508>
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-16-728b29d29f03> in <module>()
         13 with AClassWhatever():
         14     print("开始类之外、这里的正文的内容，")
    ---> 15     raise NameError('随意写入的提示信息')  # 这里只是认为制造一个错误，程序会停止，具体情况看实际创建的代码了
    

    NameError: 随意写入的提示信息


## 总结

并不清楚到底有什么使用的场景。。。这种教程完全看不懂这么隐晦的功能到底什么逻辑、使用作用。

---
注：  
个人微信公众号：codeAndWrite


# 32.【Python学习分享文章】\_multithreadedPrograming多线程编程_并发编程

## 综述

目的是为了提高计算机的硬件性能，从而减少程序的执行时间。

相当于物理里面线路的连接问题：将串联的程序改变成并联的，一次进行的任务量会增加。

“线程”的“线’相当于“排队”的“队”，排队买票当然是队伍越多速度越快。简单理解就是将多个任务的执行情况，从单线变成多线。但是火车站的售票窗口无能无限多，即队伍数量不会无限多，有场地的限制，计算机因为有硬件的限制，所以也不会无限多线程。

总的思路就是：  
1. 尽可能多开售票窗口，增加卖票速度；
1. 尽可能充分利用硬件可以达到的最大线程，缩短程序运行时间。

## 单线程 demo

### - 创建一个基础线程作为讲解基础

其实之前编写的程序都是单线程的执行过程，也就是串联的关系，一个程序语句执行完之后再执行下一个程序。


```python
def basedThread(temp_a, temp_b):
    print("第一个参数是：%s，第二个参数是：%s" %(temp_a, temp_b))
    
for i in range(1, 6, 1):  # 包括前面不包括后面，第三个数字“1”是“递增量”
    basedThread(i, i**2)
```

    第一个参数是：1，第二个参数是：1
    第一个参数是：2，第二个参数是：4
    第一个参数是：3，第二个参数是：9
    第一个参数是：4，第二个参数是：16
    第一个参数是：5，第二个参数是：25
    

【解释】：  
for 语句执行过程的逻辑是“依次执行里面的内容，执行玩第i个情况之后，再执行第i+1个情况”，也就是单线程的方式。

### - 显示单线程执行过程

现在的计算机硬件太强了，对于这样的单线程程序，不到一眨眼的功夫就执行完了，和多线程的区别看不出来，所以为了放慢程序的执行过程，我们加入之前使用过的暂停（休眠）功能 ```sleep()```。


```python
import time

def basedThread(temp_a, temp_b):
    print("第一个参数是：%s，第二个参数是：%s" %(temp_a, temp_b))
    time.sleep(1)  # 这里执行完之后，暂停1s
    print("暂停了1s")
    
for i in range(1, 6, 1):
    basedThread(i, i**2)
```

    第一个参数是：1，第二个参数是：1
    暂停了1s
    第一个参数是：2，第二个参数是：4
    暂停了1s
    第一个参数是：3，第二个参数是：9
    暂停了1s
    第一个参数是：4，第二个参数是：16
    暂停了1s
    第一个参数是：5，第二个参数是：25
    暂停了1s
    

【解释】：  
这个就需要自己在电脑上执行看看效果了。我们会看到，上面每一个操作（打印代替）是依次进行的，相当于一个人买完票，再下一个，是串联的关系。

## 改编成多线程 multithread

使用的是 Python3 里面的 ```threading``` 库，有些老旧的，比如```_thread``` 被取代了。

### - 简单改编

使用 ```threading``` 里面的 ```Thread()``` 功能。

Thread(target, args):  
1. target。使用的函数，输入函数名字
2. args。传入函数的参数值，根据第1点传入的函数而输入。

如下：


```python
import time, threading

def basedThread(temp_a, temp_b):
    print("第一个参数是：%s，第二个参数是：%s" %(temp_a, temp_b))
    time.sleep(1)  # 这里执行完之后，暂停1s
    print("暂停了1s")
    
for i in range(1, 6, 1):
    t1 = threading.Thread(target=basedThread, args=(i, i**2))  ## 只是创建一个多线程程序
    t1.start()  # 运行 t1 这个多线程程序
```

    第一个参数是：1，第二个参数是：1
    第一个参数是：2，第二个参数是：4
    第一个参数是：3，第二个参数是：9第一个参数是：4，第二个参数是：16
    
    第一个参数是：5，第二个参数是：25
    暂停了1s
    暂停了1s
    暂停了1s暂停了1s
    
    暂停了1s
    

【解释】：  
因为是多线程是同步运行的，所以大家一起执行，所以是一起输出打印的第一个内容，然后休息1s，再一起输出打印的第二个内容。

### - 线程运行的时候增加线程名字标志

#### -- 单线程的：


```python
from threading import current_thread

def basedThread(temp_a, temp_b):
    print(current_thread().getName(),'这个线程开始啦~')  # 获取进程的名字，自己添加的注释（英文的话就是start）
    print("第一个参数是：%s，第二个参数是：%s" %(temp_a, temp_b))
    time.sleep(2)
    print(current_thread().getName(),'这个线程结束了')
    
for i in range(1, 6, 1):
    basedThread(i, i**2)
```

    MainThread 这个线程开始啦~
    第一个参数是：1，第二个参数是：1
    MainThread 这个线程结束了
    MainThread 这个线程开始啦~
    第一个参数是：2，第二个参数是：4
    MainThread 这个线程结束了
    MainThread 这个线程开始啦~
    第一个参数是：3，第二个参数是：9
    MainThread 这个线程结束了
    MainThread 这个线程开始啦~
    第一个参数是：4，第二个参数是：16
    MainThread 这个线程结束了
    MainThread 这个线程开始啦~
    第一个参数是：5，第二个参数是：25
    MainThread 这个线程结束了
    

【解释】：  
没有多线程，所以就一个线程，相当于电路里面的“干路”，这个线程就叫做主线程 MainThread。

#### -- 多线程的：


```python
def basedThread(temp_a, temp_b):
    print(current_thread().getName(),'这个线程开始啦~')  # 获取进程的名字，自己添加的注释（英文的话就是start）
    print("第一个参数是：%s，第二个参数是：%s" %(temp_a, temp_b))
    time.sleep(2)
    print(current_thread().getName(),'这个线程结束了')
    
for i in range(1, 6, 1):
    t1 = threading.Thread(target=basedThread, args=(i, i**2))
    t1.start()
    
print(current_thread().getName(), '都结束了')
```

    Thread-11Thread-12 这个线程开始啦~
    第一个参数是：1，第二个参数是：1
    Thread-13 这个线程开始啦~
    第一个参数是：3，第二个参数是：9
     这个线程开始啦~
    第一个参数是：2，第二个参数是：4
    Thread-14 Thread-15MainThread 这个线程开始啦~
    第一个参数是：5，第二个参数是：25
    这个线程开始啦~ 都结束了
    
    第一个参数是：4，第二个参数是：16
    Thread-13Thread-11 这个线程结束了
     这个线程结束了
    Thread-12 这个线程结束了
    Thread-15Thread-14 这个线程结束了 这个线程结束了
    
    

【解释】：  
因为是jupyter一直在运行，所以进程应该是没有关闭的，所以进程的数字标志就在一直增加。

## 多线程顺序整理

【问题】：  
上述的多线程的程序运行的结果中，我们可以看到，主线程MainThread 是先结束的，然后是（带数字的）子线程结束，顺序上不太符合我们的想法。

【目的】：  
建立依赖关系，使得线程的运行是和其他现成有“先后关系”的，也就是希望得到**“线程的同步”**，比如：一个线程的运行需要等待另外一个线程的结束。

【控制方法】：  
1. 使用“面向对象”的形式去编写；
2. 使用 ```join()``` 的方法

【背景/原理】：  
1. ```Thread()``` start() 后，函数这个参数的条用，是进行了 ```run()``` 这个方法；
2. 使用面向对象的方法，建立自己的类，这个类作为 Thread 的子类，继承所有的内容；
3. 单独修改其中 ```run()``` 的方法，即 run 成为一个多态的方法。

### - 1. 建立进程的类


```python
import threading

class MyNewThread(threading.Thread()):  # 建立一个自己的类，从 Thread 继承，作为其中一个子类
    def run(self):
        pass  # 搭建框架而已，内容应该是自己修改的内容。
```

### - 2.修改自己需要的功能


```python
from threading import current_thread  # 如果名字太长，建议使用 from...import... 的语句

class MyNewThread(threading.Thread):  # 这里没有括号（）
    def run(self):
        print(current_thread().getName(),"这个线程开始了~")
        print('run')
        print(current_thread().getName(),"这个线程结束了！")

for i in range(1, 4, 1):
    t2 = MyNewThread()
    t2.start()
    t2.join()  # 没有太明白这个方法具体到底有什么用。
    # 不写这句，MainThread 会乱跑，也就是并发处理看随机先打印谁，
    # 写了这句，子线程会先全部处理，最后再去处理干路的 MainThread
    
print(current_thread().getName(),"主进程结束了！")
```

    Thread-16 这个线程开始了~
    run
    Thread-16 这个线程结束了！
    Thread-17 这个线程开始了~
    run
    Thread-17 这个线程结束了！
    Thread-18 这个线程开始了~
    run
    Thread-18 这个线程结束了！
    MainThread 主进程结束了！
    

## 总结

多线程处理，就是 ```threading``` 这个库，遇到是后再寻找具体的方法了。

---
注：  
个人微信公众号：codeAndWrite

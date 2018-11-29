
# 33.【Python学习分享文章】_multithreadProducerConsumerProblem生产者消费者问题

## 综述

现实生活中的一个例子：  
> 一个游泳池，有进水口和出水口，泳池的总水量既会增加、也会减少，并且是同步进行的。

对应到编程里面就是：  
> “泳池”就是“分配的硬盘空间”，“水”就是“数据”，“进水口”就是“产生数据的方法”，“出水口”就是“消耗数据的方法”，最后总是要看数据发生了什么变化，对数据进行控制。

数据的产生和消耗，就是经典的**“生产者和消费者”问题**了。

### - 使用的方法：

#### -- 工具1：

多线程编程，对应出水口和进水口可以同时工作的状态，所以需要多个线程同时进行了。

#### -- 工具2：

```queue```，即“队列的库”，对应泳池，需要以固定的容量作为基准，算是控制数据多少的数据容器尺寸。

### - 背景例子：

比如马上就要进行的双十一活动（反正我是尽量做到需要的东西随时购买，尽量远离这个“活动”），购买的时候多多少少就要和客服进行沟通确认，所有的“顾客”（生产者）发送消息，就生产的了一个“请求”数据，“客服”（消费者）就要回答消息，就消耗了一个请求。

【泳池】：客服的数量不是无穷多，所以要控制消息的容量。（如果超出了容量，解决方法可以是额外开一个“泳池”先放着存储请求，等前一个泳池消耗完了再处理下面一个泳池）

## queue 队列 概念

### - 理解

相当于一个 list，不过更对应的理解是“排队的队伍”，依次排序，从前开始处理、消耗数据（对应“结账”），处理完的数据就从 queue 里面消失（对应“结完账的顾客回家了，不用再进行结账了”）。

### - demo

如下：

- 首先先创建一个 queue队列


```python
import queue  # 导入 queue 这个库进行使用

myNewQueue = queue.Queue()  # 创建一个 Queue 类型的变量
myNewQueue.put("banana")  # put 就是增加一个数据
myNewQueue.put(10086)  # 再 put 一个数据，就是想排队一样，排在了后面
myNewQueue.put("love1024")  # 同理，排在第3位
```

- 在取出数据（可以跟着进行数据处理，这里不展开）


```python
myNewQueue.get()  # 取出排在第一个的数据，在 原queue 里面就消失了
```




    'banana'




```python
myNewQueue.get()  # 取出 queue 剩下的数据的第一个
```




    10086




```python
myNewQueue.get()  #  同理
```




    'love1024'



如果再取数据呢？现在 myNewQueue 这个 queue 已经没有数据了，看看输出结果是什么。


```python
myNewQueue.get()  # 运行这个会一直处于等待的状态，不要运行呦~
```

【结果】：  
没有响应，一直处于处理的状态，怎么办。。。使用 ```get_nowait()``` 方法。  
如果使用上面这个方法，会报错，这时候就需要使用之前的“捕获错误”（try...except...finally...）的方法进行处理了。


```python
myNewQueue.get_nowait()
```


    ---------------------------------------------------------------------------

    Empty                                     Traceback (most recent call last)

    <ipython-input-5-82c6db71c36a> in <module>()
    ----> 1 myNewQueue.get_nowait()
    

    ~\Anaconda2\envs\tensorflow\lib\queue.py in get_nowait(self)
        190         raise the Empty exception.
        191         '''
    --> 192         return self.get(block=False)
        193 
        194     # Override these methods to implement other queue organizations
    

    ~\Anaconda2\envs\tensorflow\lib\queue.py in get(self, block, timeout)
        159             if not block:
        160                 if not self._qsize():
    --> 161                     raise Empty
        162             elif timeout is None:
        163                 while not self._qsize():
    

    Empty: 


## demo说明

### - demo 如下：


```python
from threading import Thread, current_thread
import time, random
from queue import Queue

queueDemo = Queue(5)  # 定义一个队列，长度是5

class ProducerThread(Thread):
    def run(self):
        name = current_thread().getName()  # 获取线程的名字
        nums = range(100)  # 产生0~99的数字
        global queueDemo
        for i in range(5):
            num = random.choice(nums)  # 随机选取一个数字作为生产者生产的数字
            queueDemo.put(num)  # 将上面生产的数字放入到队列 queueDemo 中
            print('生产者 %s 生产了数据： %s' %(name, num))  # 打印信息
            t = random.randint(1, 3)  # 随机选择一个休眠/暂停的时间
            time.sleep(t)  # 按照选取的长度进行休眠
            print('生产者 %s 睡眠了 %s 秒' %(name, t))  # 打印休眠信息

class ConsumerThread(Thread):
    def run(self):
        name = current_thread().getName()
        global queueDemo
        for i in range(5):
            num = queueDemo.get()  # 消费队列 queueDemo 里面第一个数字
            queueDemo.task_done()  # 封装好了线程的 等待、同步 的问题，直接拿过来常用
            print('消费者 %s 消耗了数据：%s' %(name, num))
            t = random.randint(1, 5)
            time.sleep(t)
            print('消费者 %s 休眠了 %s 秒' %(name, t))
```

### - 情况1：生产少，消费多


```python
p1 = ProducerThread(name = 'p1')
p1.start()
c1 = ConsumerThread(name = 'c1')
c1.start()
c2 = ConsumerThread(name = 'c2')
c2.start()
```

    生产者 p1 生产了数据： 47
    消费者 c2 消耗了数据：47
    生产者 p1 睡眠了 3 秒
    生产者 p1 生产了数据： 25消费者 c1 消耗了数据：25
    
    消费者 c2 休眠了 4 秒
    生产者 p1 睡眠了 2 秒
    生产者 p1 生产了数据： 75
    消费者 c1 消耗了数据：75
    消费者 c1 休眠了 3 秒
    生产者 p1 睡眠了 1 秒
    生产者 p1 生产了数据： 5消费者 c2 消耗了数据：5
    
    消费者 c1 休眠了 3 秒
    生产者 p1 睡眠了 2 秒
    生产者 p1 生产了数据： 88消费者 c2 消耗了数据：88
    
    消费者 c2 休眠了 1 秒
    消费者 c2 休眠了 4 秒
    生产者 p1 睡眠了 2 秒
    

【解释】：  
数据生产得慢，消耗得快，c1 和 c2 轮流消耗 p1 生产出来的数据。

### - 情况2：生产多， 消费少

【注意】：  
在 jupyterNotebook 里面运行下面这个代码是，要点击上方的“Kernel”-“Restart”，将程序注销重新运行。  
【原因】：  
无法像其他编辑器一样有“停止”按钮，所以上面运行的 p1、c2、c3 还在，会影响下面的代码。为什么还会在呢？我现在的水平是无法回答的。  
【补充】：  
或者，既然原先的 p1、c1、c2不消失，那么就直接只增加 p2、p3就好了嘛。


```python
p2 = ProducerThread(name='p2')
p2.start()
p3 = ProducerThread(name='p3')
p3.start()
c3 = ConsumerThread(name='c3')
c3.start()
```

    生产者 p2 生产了数据： 20
    生产者 p3 生产了数据： 87消费者 c3 消耗了数据：20
    
    消费者 c3 休眠了 1 秒
    消费者 c3 消耗了数据：87
    生产者 p2 睡眠了 2 秒
    生产者 p2 生产了数据： 15
    生产者 p3 睡眠了 3 秒
    生产者 p3 生产了数据： 29
    生产者 p2 睡眠了 2 秒
    生产者 p2 生产了数据： 73
    生产者 p3 睡眠了 1 秒
    生产者 p3 生产了数据： 61
    生产者 p2 睡眠了 1 秒
    生产者 p2 生产了数据： 7
    消费者 c3 休眠了 5 秒
    消费者 c3 消耗了数据：15
    生产者 p3 睡眠了 2 秒
    生产者 p3 生产了数据： 68
    生产者 p2 睡眠了 2 秒
    消费者 c3 休眠了 2 秒
    消费者 c3 消耗了数据：29
    生产者 p2 生产了数据： 95
    生产者 p3 睡眠了 3 秒
    生产者 p2 睡眠了 2 秒消费者 c3 休眠了 2 秒
    
    消费者 c3 消耗了数据：73生产者 p3 生产了数据： 51
    
    消费者 c3 休眠了 2 秒
    生产者 p3 睡眠了 3 秒
    

【解释】：  
生产者 p2 和 p3 依次产生了数据：20、87、15、29、73、61、7、68、95、51  
消费者 c3 依次消耗了：20、87、15、29、73

【验证】：  
如果推到正确，那么接下来如果取出数据的话，应该是 61，如下：

【注】：因为是随机的，所以上面所说的数字数据，只是我现在运行的结果，每个人、每次运行的结果都是不一样的。


```python
print(queueDemo.get())
```

    61
    

【结果】：  
NICE！对的。

---
注：  
个人微信公众号：codeAndWrite

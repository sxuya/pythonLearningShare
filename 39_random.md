
# 39.【Python学习分享文章】\_random\_随机选取方法

## 综述

两个数学相关的库（9. Numeric and Mathematical Modules）：
- math。主要用于机器学习、深度学习中。比如计算正弦值、余弦值，不用在自己编写 code。
- random。产生随机数字、字母等，主要用于软件测试、密码学中。

这里主要演示 ```random``` 这个库。

## ```random```

### - 生成随机整数

按照格式来 code 就好，如下：


```python
import random  # 导入库

randomIntMine_1 = random.randint(1, 37)  # 在包括1、包括37的范围里面“随机产生”一个整数
randomIntMine_2 = random.randint(1, 37)
randomIntMine_3 = random.randint(1, 37)

print(randomIntMine_1)
print(randomIntMine_2)
print(randomIntMine_3)
```

    25
    36
    1
    

【解释】：  
每次运行的结果都会不一样。

### - “随机”抽取字符（即非数字，/D）

方式是使用：```choice()````，如下：


```python
rangeList = ['abcd', 'sxu', 'yang', 10086]
randomStringMine_1 = random.choice(rangeList)
randomStringMine_2 = random.choice(rangeList)
randomStringMine_3 = random.choice(rangeList)

print(randomStringMine_1)
print(randomStringMine_2)
print(randomStringMine_3)
```

    10086
    abcd
    yang
    

## 总结

主要是在我们给定的数据范围里面，进行随机产生（其实是伪随机产生，毕竟计算机只能公式产生，只不过我们看着有点像随机数字。那这就有一个问题了：世界上真的有随机数这个概念么？人类想的随机数，也是根据一定的情景想出来的，也算是一种算法吧）。

具体希望产生什么样的随机方案、目标，到用的时候再在 ```random``` 这个库/模块里面来寻找对应的方法即可。

---
注：  
个人微信公众号：codeAndWrite

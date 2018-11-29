
# 40.【Python学习分享文章】_osPathOperation_Python文件操作库os

## 综述



## ```os.path``` 库

### - 获取当前位置的绝对路径


```python
import os

pathTemp = os.path.abspath('.')
print(pathTemp)
```

    C:\Users\yeray\Documents\GitHub\pythonLearningShare
    

### - 获取当前位置上级目录的绝对路径


```python
print(os.path.abspath('..'))
```

    C:\Users\yeray\Documents\GitHub
    

### - 验证一个路径是否存在


```python
print(os.path.exists('/Users'))
```

    True
    

### - 判断一个路径是否为“文件”类型。


```python
print(os.path.isfile('/Users'))
```

    False
    

### - 判断是否为目录

其实差不多就是我们口头上说的“文件夹”的意思。


```python
print(os.path.isdir('/Users'))
print(os.path.isdir('/Users/yeray'))
```

    True
    True
    

### - 连接多个路径组成长路径

或者说：拆分一个很长的目录路径为多个部分。 


```python
os.path.join('the name of path NO.1', 'the name of path NO.2')
```

【注释】：

暂时不运行上面的 code，没有什么应用。

## ```pathlib``` 库

很多实现的功能和 ```os.path``` 相同，**但是**书写的方式不一样，需要注意。


```python
from pathlib import Path
```

### - 相对路径的 ```.``` 的绝对路径

需要用变量先封装成 Path 类型才可以使用.

**这个库的基本原理是使用 class 进行功能实现**。


```python
p = Path('.')
print(p.resolve())
```

    C:\Users\yeray\Documents\GitHub\pythonLearningShare
    

### - 判断是否为目录


```python
print(p.is_dir())
```

    True
    

### - 新建一个目录

**最大的**不同功能。


```python
q = Path('/Users/yeray/Documents/GitHub/pythonLearningShare/temp/a/b/cc')  # 这里是绝对路径的内容
Path.mkdir(q, parents=True)
```

【解释】：

参数 parents=True 的作用：创建的目标目录 cc 的上面两级是不存在的，即 父目录 不存在，如果参数值设置为 False，那么就是说一定要有对应的父目录才可以创建，而我是没有的，就会报错，所以要把参数改为 True。

最后下创建结果如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/41_1.png?raw=true)

---
注：  
个人微信公众号：codeAndWrite

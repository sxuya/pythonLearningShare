
# 43.【Python学习分享文章】\_hierachicalIndexing_层次化索引


### 综述

相当于数据的标签也成为多维，一个维度无法定位唯一数据，可以再使用其他的维度，再进行精细定位。

两层 index 的 Series 数据，就相当于二维的 DataFrame 数据。

## 建立两层 index 的 Series 数据

一层的标签是“a、b、c”，另外一层的 index 是“1、2、3”。如下：


```python
import numpy as np
from pandas import Series, DataFrame
```


```python
seriesData = Series(np.random.randn(10),
                   index=[['a', 'a', 'a', 'b', 'b', 'b', 'c', 'c', 'd', 'd'],
                          ['one', 'two', 'three', 'one', 'two', 'three','one', 'two', 'one', 'two']])

print(seriesData)
```

    a  one      0.335351
       two      0.099215
       three   -0.127803
    b  one     -0.572319
       two      1.091742
       three    0.918033
    c  one     -0.238926
       two      0.321934
    d  one      0.299117
       two     -0.461843
    dtype: float64
    

## 提取数据

### - 按照一层 index 进行提取

比如提取 index 是“b”的数据，如下：


```python
print(seriesData['b'])
```

    one     -0.572319
    two      1.091742
    three    0.918033
    dtype: float64
    

如果 index 输入数字，只能提取到第几个的数据，如下：


```python
print(seriesData[0])
print(seriesData[8])
```

    0.3353505835470968
    0.29911683532303146
    

### - 无法跨层进行提取

否则会报错，如下：


```python
print(seriesData['one'])
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\Anaconda2\envs\tensorflow\lib\site-packages\pandas\core\indexes\multi.py in get_value(self, series, key)
        867             try:
    --> 868                 return libindex.get_value_at(s, k)
        869             except IndexError:
    

    pandas/_libs/index.pyx in pandas._libs.index.get_value_at()
    

    pandas/_libs/src/util.pxd in util.get_value_at()
    

    TypeError: 'str' object cannot be interpreted as an integer

    
    During handling of the above exception, another exception occurred:
    

    KeyError                                  Traceback (most recent call last)

    <ipython-input-48-388f0e8e0020> in <module>()
    ----> 1 print(seriesData['one'])
    

    ~\Anaconda2\envs\tensorflow\lib\site-packages\pandas\core\series.py in __getitem__(self, key)
        621         key = com._apply_if_callable(key, self)
        622         try:
    --> 623             result = self.index.get_value(self, key)
        624 
        625             if not is_scalar(result):
    

    ~\Anaconda2\envs\tensorflow\lib\site-packages\pandas\core\indexes\multi.py in get_value(self, series, key)
        874                     raise InvalidIndexError(key)
        875                 else:
    --> 876                     raise e1
        877             except Exception:  # pragma: no cover
        878                 raise e1
    

    ~\Anaconda2\envs\tensorflow\lib\site-packages\pandas\core\indexes\multi.py in get_value(self, series, key)
        858 
        859         try:
    --> 860             return self._engine.get_value(s, k)
        861         except KeyError as e1:
        862             try:
    

    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_value()
    

    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_value()
    

    pandas/_libs/index.pyx in pandas._libs.index.MultiIndexObjectEngine.get_loc()
    

    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()
    

    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()
    

    pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()
    

    pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()
    

    KeyError: 'one'


### - 两层次提取

我猜就是一个 index 嵌套的写法，如下：


```python
print(seriesData['b']['two'])
```

    1.0917416154754636
    

### - 输出多个一级 index

和 list 的操作很像了，如下：


```python
print(seriesData['b':'d'])
```

    b  one     -0.572319
       two      1.091742
       three    0.918033
    c  one     -0.238926
       two      0.321934
    d  one      0.299117
       two     -0.461843
    dtype: float64
    

## 与 DataFrame 数据互相转化

方法是：```unstack()``` 和 ```stack()```，如下：


```python
dataFrameData = seriesData.unstack()

print(dataFrameData)
```

            one     three       two
    a  0.335351 -0.127803  0.099215
    b -0.572319  0.918033  1.091742
    c -0.238926       NaN  0.321934
    d  0.299117       NaN -0.461843
    


```python
print(dataFrameData.stack())
```

    a  one      0.335351
       three   -0.127803
       two      0.099215
    b  one     -0.572319
       three    0.918033
       two      1.091742
    c  one     -0.238926
       two      0.321934
    d  one      0.299117
       two     -0.461843
    dtype: float64
    

## 总结

主要就是是一个 index 的定义的理解，或者说是结构的理解。

---
注：  
个人微信公众号：codeAndWrite


# 【Python学习分享文章】_list(列表)介绍及基本操作

## 综述

列表相比 tuple（元组），数据集里面的数据可以修改（增加、删除等）。

## - 创建一个列表


```python
a_list = ['abc', 'xyz', '123', '10086'] # 字符串的 list，还可以是数字类型的 list
print(a_list)
# 结果如下：
```

    ['abc', 'xyz', '123', '10086']
    

## - 增加数据  
方法 ```.append()``` ,数据增加至尾部。例子：


```python
a_list.append('opq')
print(a_list)
# 结果如下：
```

    ['abc', 'xyz', '123', '10086', 'opq']
    

## - 移除数据
方法 ```.remove()```。

### 1. 按照数据本身
使用 ```.remove()``` ,括号内容为“列表存在数据”。


```python
a_list.remove('123')
print(a_list)
# the result is:
```

    ['abc', 'xyz', '10086', 'opq']
    

### 2. 按照位置
使用 ```.pop()``` ，括号内容为“数据的下标数字”,被 ```.pop()``` 位置的数据如果没有“被承接”，就消失了。


```python
temp = a_list.pop(1) # 此处被 pop 的下标为 1 位置的 ‘xyz’ 被 temp 承接
print(temp)
print(a_list)
# the result is:
```

    xyz
    ['abc', '10086', 'opq']
    

## - 基本操作

### 1. 关系判断。
```in``` ， ```not in```。用法同 tuple（元组）一样。
### 2. 连接操作
```+``` 。用法同 tuple（元组）一样。
### 3. 重复处理
```*``` 。用法同 tuple（元组）一样。
### 4. 提取（摘取）数据（切片操作）
```[:]``` ，用法同 tuple（元组）一样。

---
注：  
个人微信公众号：codeAndWrite

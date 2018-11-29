
# 25.【Python学习分享文章】_customSetting（自定义上下文管理器）

## 综述

就是之前打开文件使用过的 ```with```。

这个的内容完全不知道在讲解什么，好像没有什么用。

就是文件的“打开”、“命名”、“关闭”的一系列操作。

## demo说明

### -【目的】：

打开文件；如果打开失败，则关闭文件。

### - 普通 code


```python
fileA = open('name.txt')
try:
    for line in fileA:
        print(line)
finally:
    fileA.close()
```

这个也不太优雅。

### - 使用上下文管理器 with 语句


```python
with open('name.txt') as f:
    for line in f:
        print(line)
```

#### -- 解释：

使用了 with，如果打开失败，Python 会默认调用 finally，然后关闭文件。

详细的内容在后面讲解完“类”等的知识的时候在详细讲解。

---
注：  
个人微信公众号：codeAndWrite

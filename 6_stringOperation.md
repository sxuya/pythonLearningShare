【Python学习分享文章】_字符串的基础操作功能

## 综述

1. 关系判断  
```in``` 、 ```not in```
2. 连接操作  
```+```
3. 重复处理  
```*```
4. 切片操作（就是提取子集的意思）  
```[:]```

## 关系判断（in、not in）

目的：判断一个数据是否在一个序列（数据集）中。

### 例子

```
chinese_zodiac = "鼠牛虎兔龙蛇马羊猴鸡狗猪"
print('牛' in chinese_zodiac)
print('鸡' not in chinese_zodiac)
print('其他的数据都可以' in chinese_zodiac)
```
结果是：
```
True
False
False
```
这是我见过最人性化的一个语句了T_T，第一次看到的时候感动得一塌糊涂。

## 连接操作（+）

### 例子
```
print(chinese_zodiac + chinese_zodiac)
print(chinese_zodiac + '我是可爱的其他字符数据')
```
结果是：
```
鼠牛虎兔龙蛇马羊猴鸡狗猪鼠牛虎兔龙蛇马羊猴鸡狗猪
鼠牛虎兔龙蛇马羊猴鸡狗猪我是可爱的其他字符数据
```

### 报错例子
```
print(chinese_zodiac + 123)
```
错误原因：  
“+”不能够连接非“字符串”数据

## 重复处理（\*）

### 例子
```
print(chinese_zodiac * 3)
print('头尾四次' * 4)
```
结果是：
```
鼠牛虎兔龙蛇马羊猴鸡狗猪鼠牛虎兔龙蛇马羊猴鸡狗猪鼠牛虎兔龙蛇马羊猴鸡狗猪
头尾四次头尾四次头尾四次头尾四次
```

## 切片操作

上一篇有介绍。

---

注：
个人微信公众号：codeAndWrite
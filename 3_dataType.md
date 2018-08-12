【Python学习分享文章】_数据类型整理

## 综述

1. 整数（int）。  
比如1、2、3...顾名思义，只能是整数，不能存储小数。  
【特点：】存储空间占用少。  
数据引用使用 ```%d```。
2. 浮点数（float）。  
比如1.1、42.8...平时说的小数，也可以存储整数，比如8.0。  
【特点：】存储空间比 int 类型大。记得应该是2倍的关系。
3. 字符串（str）。  
string 的简称。需要用单引号（‘’）或者双引号（“”）进行输入。比如“abcd”、‘我们这里面的东西是字符串数据，来编辑我吧’、‘10086’...  
【注释：】数字加上引号，就成为字符串数据了，不再是 int 或者 float 数据类型了。  
数据引用使用 ```%s```
4. 布尔值（bool）。  
boolean 的简称。只有两种```True```（真）、```False```（假）两种，当数据非0、非None时，就是 ```True``` ，反之为 ```False``` 。  

## 操作code

### 确认数据类型

1. 终端简便编程，可直接输出结果
```
type(要查看类型的数据输入到这里即可)
```
2. IDE 里面的代码：
```
print(type(要查看类型的数据输入到这里即可))
```
比如：
```
a = "随便一个字符串输入到这里即可"
print(type(8))
print(type('8'))
print(type(a))
print(type(True))
```
输出的结果就是：
```
<class 'int'>
<class 'str'>
<class 'str'>
<class 'bool'>
```
说明第一个是整数类型的数据，第二和第三个是字符串类型的数据，第四个是布尔值类型的数据。

### 数据转换

1. 将int 和 float（数字类型数据）--> str（字符串）：
```
a = str(8)
print(a)
```
输出的结果：
```
8
```
但是是字符串类型的“8”

2. 将str（字符类型）数据 --> int 或者 float（数字类型）：
```
 b = int('10')
 print(b)
```
输出的结果：
```
10
```
如果字符串内容不是数字，则会报错，比如：
```
c = int('abc')
print(c)
```

3. 将 int、float、str --> bool（布尔类型）：
```
d = bool('8')
e = bool(8)
f = bool("this's string data")
g = bool(0)
h = bool('0')
i = bool('None')
j = bool(None)
print(d)
print(e)
print(f)
print(g)
print(h)
print(i)
print(j)
```
结果是：
```
True
True
True
False
True
True
False
```

---

注：
个人微信公众号：codeAndWrite
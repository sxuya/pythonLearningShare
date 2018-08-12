
#  16.【Python学习分享文章】_“异常”处理

## 综述

异常不是错误，只是一些小瑕疵，程序不正常运行。

主要分为两类：

1. 开发人员编写程序产生的；
2. 用户的输入导致的。

一般的处理流程：
1. 检测到错误；
2. 程序发生异常；
3. 对检测到的异常进行的判断操作。

## 开发人员产生的

### - NameError

解释：变量未被定义。

#### 例子：


```python
i = j
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-028937b60c65> in <module>()
    ----> 1 i = j
    

    NameError: name 'j' is not defined


### - SyntaxError

解释：语法错误。可以根据提示找到错误位置。

#### 例子：


```python
print(5))
```


      File "<ipython-input-2-4bec4eb058a8>", line 1
        print(5))
                ^
    SyntaxError: invalid syntax
    


### - IndexError

解释：超出 sequence 范围，需要调整数字下标（索引）的情况。

#### 例子：


```python
a_string = 'abcdefg'
print(a_string[12])
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-4-2d3881729ec6> in <module>()
          1 a_string = 'abcdefg'
    ----> 2 print(a_string[12])
    

    IndexError: string index out of range


```a_string```  只有7个字母，下标是 0 到 6，设定的“12”大大超出了范围。

### - KeyError

解释：字典的 key 值（键值）超出了给定的内容。

#### 例子：


```python
a_dict = {'a':1, 'b':22}
print(a_dict['z'])
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-5-43ad1916fa42> in <module>()
          1 a_dict = {'a':1, 'b':22}
    ----> 2 print(a_dict['z'])
    

    KeyError: 'z'


 ```a_dict``` 没有 “z” 的数值，所以会提示“KeyError”

### - AttributeError

解释：属性错误，采取的变量内容没有对应的属性、方法等。

#### 例子：


```python
a =  1234
a.append('a')
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-8-29b444b31a8e> in <module>()
          1 a =  1234
    ----> 2 a.append('a')
    

    AttributeError: 'int' object has no attribute 'append'


解读：int 类型的数据没有 ```append()``` 的操作方法，这个是 ```list()``` 数据类型才有的方法，用来在 list 后面增加数据。

## 用户产生的

### - ValueError

解释：输入的数据类型不吻合，导致程序运行不正常。

#### 例子：


```python
year = int(input('please input the number of yaer.For error, not input number:'))
```

    please input the number of yaer.For error, not input number:abcd
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-6-0651ad0dc129> in <module>()
    ----> 1 year = int(input('please input the number of yaer.For error, not input number:'))
    

    ValueError: invalid literal for int() with base 10: 'abcd'


## 异常捕获、处理

### - 整体框架：

```
try:
    运行代码
except 系统会提示的错误代码:
    如果遇到对应的错误代码执行的操作
finally:
    无论如何都会执行的操作
```

### - 捕获单个异常

#### 例子：处理用户输入不符合的数据类型


```python
try:
    year = int(input("please input the year.But not a number:"))
except ValueError:
    print('now, please input the number:')
```

    please input the year.But not a number:ad
    now, please input the number:
    

#### 例子：将“错误提示的内容”进行输出


```python
try:
    print(1/0)
except ZeroDivisionError as e:
    print("0 不能作为除数，系统提示的错误代码是：%s"%e)
```

    0 不能作为除数，系统提示的错误代码是：division by zero
    

### -  捕获多个异常

#### 例子：

```
except (ValueError, AtrributeError, KeyError)
```
因为 except 后面只能接一个参数，因此需要写成 tuple 类型。

### - 捕获【所有】错误

#### 例子：


```python
try:
    print(1/'a')
except Exception as e:
    print("系统提示的错误信息是：%s"%e)
```

    系统提示的错误信息是：unsupported operand type(s) for /: 'int' and 'str'
    

解读：无法对‘int’和‘str’进行‘/’（除法）操作。

**用处**：用来对未知的错误信息进行侦测，用于 debug。

### - 重新定义异常的提示信息

使用的语法是：```raise```

#### 例子：

*没有搞懂这个到底是什么意思，简直是\*\*程序员教程。


```python
try:
    raise NameError("what's fuck meaning here")
except  NameError:
    print("why print what that is here")
```

    why print what that is here
    

### - 增加 finally 内容

无论获得什么异常、还是正常运行，都进行的操作的部分内容。

#### 例子：
##### 错误的情况：



```python
try:
    a = open('name.txt')
except Exception as e:
    print('系统的错误信息是：%s'%e)
finally:
    a.close()
```

    系统的错误信息是：[Errno 2] No such file or directory: 'name.txt'
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-6-d30ddd7bcc29> in <module>()
          4     print('系统的错误信息是：%s'%e)
          5 finally:
    ----> 6     a.close()
    

    NameError: name 'a' is not defined


解读：之前已经建立了“enNames.txt”文件，但是```open()```里面的文件名字错误，所以错误。

##### 正确的情况：


```python
try:
    a = open('enNames.txt')
except Exception as e:
    print('系统的错误信息是：%s'%e)
finally:
    a.close()
```

解读：正确处理了，也就是正常打开了已经存在的“enNames.txt”文件，然后就直接关闭了文件，什么也不会报错，也就什么信息也没有。

---
注：  
个人微信公众号：codeAndWrite

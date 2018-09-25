
#  15.【Python学习分享文章】_file（文件）及其操作

## 综述

### - file（文件）的含义

Python 中的 file 不止使用 PC 时所说的单个文件，比如 .txt、.exe 等这类文件，也包括“打开一个网址”、程序间的通信数据等，都抽象成 file 的概念。

### - 好处

所有的这些数据处理，可以通过一套相同的操作函数进行，简化文件操作逻辑，降低了学习难度。

## 具体内容

### - 基本读写操作

以下是 Python 自带的文件操作函数（即“**内建函数**”）：

1. open()  
打开文件。如果没有文件，就会新建这个文件。
2. read()  
读取，官方：输入。输入到编写的程序里面
3. readline()  
输入一行
4. seek()  
文件内移动（光标操作位置）
5. write()  
写入，官方；输出。输出到其他文件中。
6. close()  
关闭文件。**一定要进行的操作**，否则文件是“**非保存**”状态，关机操作会丢失数据。

### - 【写入文件】的 demo 说明

#### 整体逻辑：

open() --> write() --> close()  
打开 --> 写入内容 --> 保存关闭文件

#### 目标：

记录常见的“英文名字”。

【说明：】不采用中文，是因为中文的字符不是统一的，一个汉字是两个字符位，而标点是一个字符位，不容易理解。

#### 打开（新建）文件：

使用 ```open()``` 函数。


```python
# 记录常见的英文名字到 txt 文件中

file_names = open('enNames.txt','w') # 需要添加‘’，说明为 操作标记，否则被认为是 变量

print("file_names 的文件 type 是：")
print(type(file_names))
```

    file_names 的文件 type 是：
    <class '_io.TextIOWrapper'>
    

- 过程解释：


1. 最完整（冗杂）版本：  
```open('enName.txt', mode = 'w')```  
2. 简略（省略的）版本：  
file 为第一个参数，mode 为第二个参数，不写参数名字，就默认按照参数顺序排列  
```open('enName.txt', 'w')```  
3. file 赋值给一个变量，使用变量操作文件:  
```file_names = open('enName.txt','w')```  


- “完整”的参数说明：

    ```open(file, mode, buffering, encoding, errors, newline, ...)```

- 参数名字解释：

    ```open(file 是处理的文件名字，需要为 str 数据类型，只有这个是必填项（不然干嘛还用这个函数呢）；mode 是处理文件的模式，有 'r'（read 只读模式，不能修改里面的数据）、'w'（write 写入模式，清空内容写入）、'a'（不清楚原有内容的写入），不输入就用默认的 r 模式；buffering 后面这些暂时不需要用到，放过)```

#### 向 file 内写入内容：

使用 ```write``` 函数。


```python
# 向 file_names 文件内写入 “John” 这个名字，string 类型的。
file_names.write('John')
```




    4



#### 关闭、保存文件：

使用 ```close()``` 函数。


```python
file_names.close()
```

### - 【读取文件】的 demo 说明

#### 整体逻辑：

open() --> read() --> close()  
打开 --> 读取内容 --> 保存关闭文件

#### 目标：

读取到文件内容，并进行打印输出。

#### code：


```python
# 打开需要操作的文件，赋值给一个变量以便操作
file_2 = open('enNames.txt') # 默认是 r 模式，所以不用书写
# 读取 file_2 内容，也就是 file_names.txt 的内容
# file_2.read()
# 对读取的内容进行输出打印：
print('file_names.txt 的内容是：')
print(file_2.read())
# 关闭保存文件
file_2.close()
```

    file_names.txt 的内容是：
    John
    

### - 【增加内容】的 demo 说明

#### 目标1：

在文件原有的内容上增加内容。

#### code：


```python
# 增加写入 ‘Bob’ 名字
file_3 = open('enNames.txt','a')
file_3.write('Bob')
file_3.close()

# 需要重新定义变量进行查看，原来的模式为 write，是 unreadable 状态
file_4 = open('enNames.txt')

print("新增内容后的全部内容是：")
print(file_4.read())
file_4.close()
```

    新增内容后的全部内容是：
    JohnBob
    

#### 目标2：

增加的内容在新的一行上。

#### code：


```python
file_5 = open('enNames.txt', 'w')
file_5.write('John\n')
file_5.write('Bob\n')
file_5.write('Jack\n')
file_5.write('Rose\n')
file_5.close()

file_6 = open('enNames.txt')

print("具有多行 string 的内容是：")
print(file_6.read())
file_6.close()
```

    具有多行 string 的内容是：
    John
    Bob
    Jack
    Rose
    
    

### - 【逐行读取】的 demo 说明

#### 目标1：

逐行读取内容，以 string 类型的数据为例子。

#### code：


```python
file_7 = open('enNames.txt')

print('一行的内容是：')
print(file_7.readline())
print('下一行的内容是：')
print(file_7.readline())

file_7.close()
```

    一行的内容是：
    John
    
    下一行的内容是：
    Bob
    
    

#### 目标2：

批量逐行读取内容，用到 ```for``` 函数。

#### code：


```python
file_8 = open('enNames.txt')
for line in file_8.readlines():
    print('这行的内容是：'+line)
    print('=*=*=*=')
    
file_8.close()
```

    这行的内容是：John
    
    =*=*=*=
    这行的内容是：Bob
    
    =*=*=*=
    这行的内容是：Jack
    
    =*=*=*=
    这行的内容是：Rose
    
    =*=*=*=
    

### - 定位指针指定位置

【指针】：可以简单理解为我们进行 word 编辑的时候的那个“光标”，位置和 sequence 的下标一样，用数字表示。对应的“函数”是 ```tell()``` 。

#### 目标1：

获得指针位置信息。

#### code：


```python
file_9 = open('enNames.txt', 'rb') # 需要增加 b 字符，才能在后面进行相对偏移的操作，否则没有权限。
print('初始指针位置（应该是 0）：')
print(file_9.tell())
print("读取3个字符，内容是：")
print(file_9.read(3)) # read()默认是读取全部内容，增加的数字是指定读取的字符数量。
print("现在的指针位置是：")
print(file_9.tell())
print('再读取4个字符，内容是（我不知道换行符是不是算一个字符）：')
print(file_9.read(4))
print("处理两次后，当前的指针位置：")
print(file_9.tell())
```

    初始指针位置（应该是 0）：
    0
    读取3个字符，内容是：
    b'Joh'
    现在的指针位置是：
    3
    再读取4个字符，内容是（我不知道换行符是不是算一个字符）：
    b'n\r\nB'
    处理两次后，当前的指针位置：
    7
    

```mode = 'r'```的情况  
【分析：】为什么最后是8，不应该是3+4=7的么？【猜想：】应该是换行符有点特别吧。

```mode = 'rb```的情况  
【分析：】打印的内容为什么出现```b''```字样？【基本猜测：】b 的意思是 binary mode，即 二级制，需要进行提醒。

#### 目标2：

将指针返回到文件开头。使用的是 ```seek()``` 函数。

#### code:


```python
print("我们进行了 seek() 的操作，seek（0）")
file_9.seek(0) # 输入的数字是定位的位置的数字标记。
print("当前的指针位置是：")
print(file_9.tell())
print("重新定位指针后，读取的两个字符内容是：")
print(file_9.read(2))
print("读取完成后，当前的指针位置是：")
print(file_9.tell())
```

    我们进行了 seek() 的操作，seek（0）
    当前的指针位置是：
    0
    重新定位指针后，读取的两个字符内容是：
    b'Jo'
    读取完成后，当前的指针位置是：
    2
    

#### 目标3：

在当前位置相对移动指针。

#### code：

接着上面，指针已经在 2 位置处。


```python
print("当前位置偏移4个字符的 seek() 操作")
file_9.seek(4, 1)
print("当前的指针位置是：%s"%file_9.tell())
print("读取2个字符，内容是：%s"%file_9.read(2))

print("从文件开头位置偏移3个字符的 seek() 操作")
file_9.seek(3, 0)
print("当前的指针位置是：%s"%file_9.tell())
print("读取2个字符，内容是：%s"%file_9.read(2))
print("从文件结尾位置偏移3个字符的 seek() 操作")
file_9.seek(-3, 2)
print("当前的指针位置是：%s"%file_9.tell())
print("读取2个字符，内容是：%s"%file_9.read(2))

file_9.close()
```

    当前位置偏移4个字符的 seek() 操作
    当前的指针位置是：6
    读取2个字符，内容是：b'Bo'
    从文件开头位置偏移3个字符的 seek() 操作
    当前的指针位置是：3
    读取2个字符，内容是：b'n\r'
    从文件结尾位置偏移3个字符的 seek() 操作
    当前的指针位置是：20
    读取2个字符，内容是：b'e\r'
    

【参数说明：】

seek


---
注：  
个人微信公众号：codeAndWrite

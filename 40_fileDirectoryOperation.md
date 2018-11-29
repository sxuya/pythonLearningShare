
# 40.【Python学习分享文章】_fileDirectoryOperation_文件目录操作介绍

## 综述

我们在处理数据的时候，总会进行输入或者输出，而输入或者输出的文件总要放置在一个特定的位置，不然所有数据都放在一个原始文件夹中，实在是太凌乱了。

而在进行编程的时候，目录的显示就没有图形化界面了，只有路径的名字，比如 ```C:\Users\yeray\Documents\AndroidFiles```，其实就代表我们平时看到的图形界面的：


![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_1.png?raw=true)

（看地址栏就好了，不过我们平时使用的操作系统将数据图形化展示了。）

主要使用的两个文件夹操作的库是：

- path
- path....

【注意！】：  
这里的内容不是在 Python 里面进行操作的，而是在 Mac 的终端、win 的 powershell 终端 进行的。  
我使用的是 Windows10，所以图片展示的是 PC 的操作情况，Mac 的情况基本差不多。

【进入方式】：  
直接按 win 键进行搜索即可。

终端展示如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_2.png?raw=true)

## 查看文件夹目录地址

使用的命令是 ```pwd```，为 “print working directory”的缩写。

查看当前停留在的文件夹的路径/位置。（这里是绝对路径，相关介绍看最后的补充）

情况如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_4.png?raw=true)

## 查看当前文件夹内部文件情况

使用的命令是 ```ls```，展示内容如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_3.png?raw=true)

【解释】：  
说明我们现在进行操作的位置是 ```C:\Users\yeray``` 这一个层级中。

【解释】：

第一个字符，

- 如果是“-”，表示这个名字的内容是“文件”

- 如果是“d”，表示这个名字的内容是“文件夹”，directory 的缩写。

## 进入到下一级目录

命令如下：```cd ./当前位置子目录名字```。

可以省略 ```./```，变成 ```cd 当前位置子目录名字```，例子如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_7.png?raw=true)

## 回到/进入“上一级目录”

命令如下： ```cd ..```，例子如下即上一张图片的中间一行（文字的第6行）。

## 进入/访问特定路径/目录

方法 ```cd 路径```，change directory 的缩写。

### - 绝对路径：

从 ```C:\``` 开始，个人感觉使用的情况是：

1. 进入了很“深”的目录，但是又要回到比较浅的目录才会使用的方法；
2. 从一个路径，直接跳转到另外一个不同的路径；

例子如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_8.png?raw=true)

### - 相对路径：

和 **进入到下一级目录** 的方法类似，直接书写当前位置之后的路径即可，demo 如下，下面两行内容：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_9.png?raw=true)

## 创建目录

命令是 ```mkdir```（make directory，创建目录）的缩写。

整体结构如下：

- 当前目录、相对路径创建：

```mkdir 层级目录名字```

例子：

1. 创建前：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_10.png?raw=true)

1. 创建命令：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_11.png?raw=true)

1. 创建后：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_12.png?raw=true)

- 绝对路径创建：

```mkdir 绝对路径```

暂时还想不到使用的途径，暂时不写出来了。先来用到的更多的是相对路径。

完全可以是用“使用绝对路径进入目录”+“使用相对路径创建目录”的组合进行规避这个问题。

## 删除文件夹

```rmdir```，感觉是 remove directory 的缩写。

**注意：慎用，是全部删除，没有保存、备份的数据也会一并毫不留情地删除！！**

**数据才是无价的**。

按照提示输入对应的确认操作命令。

Mac 貌似是要用特殊的命令符，```rm -rf 路径格式的string```

Windows 10 的删除的界面如下：

![Image of fileDirectory](https://github.com/sxuya/pythonLearningShare/blob/master/picOfDemo/40_13.png?raw=true)


## 绝对路径vs相对路径

### - 绝对路径

即写出毫无歧义的路径表达，全部从根目录（不懂需自行搜索）开始书写。

我现在使用的是 Windows 10 系统，绝对路径都是以 ```C:\Users\balabala``` 开始是的。比如我现在的位置是 ```C:\Users\yeray\documents```，那么在 documents 的文件夹里面增加一个文件夹，表达的路径还是要带上前面的位置，如下：```C:\Users\yeray\documents\我想要的文件夹名字\也可以顺便有子文件夹的名字```。

主要的问题是，我已经在 ```C:\Users\yeray\documents```，为什么还要书写这部分呢？于是，就有了下面的“相对路径”这一个概念。

### - 相对路径

就是基于当前所在的目录位置开始进行操作，有点想我们点击浏览器的“前进”或者“后退”按钮一样，都是在当前位置基础上，如何进入、退出文件夹位置。比如我现在的位置是 ```C:\Users\yeray\documents```，那么增加一个文件夹，直接写 ```想要的文件夹名字\也可以用斜杠一起增加子文件夹```，

---
注：  
个人微信公众号：codeAndWrite

## 介绍  	

### 个人的一些感受

自己接触下来，python的语法更接近英语语言的使用，对于一些编程语言是严格使用符号作为结尾，比如分号“；”（java语言要求）等等，减少了前期学习不必要的精力分散，可以将更多的注意力集中在功能的实现上，而不是一直需要分散精力集中在书写格式上。对于初期学习的人员很友好。

第二点，python有大量的第三方库（就是可以使用的做好功能的工具，好比桌子，拿过来用就可以放置东西，而不用自己重新砍树、切割尺寸、钉起来，库就是不用再自己从0开始码代码的、具有一定高级功能的代码，可以直接拿来使用），对于用代码使用功能十分有利。

名人推荐：

> Facebook CEO 扎克伯格：  
把 python 当作一个工具就好了。

### （官方一点的说法）特点、有点

1. 语法简洁。
2. 类库丰富。  
类库，其他大牛编写的功能，可以直接拿来使用。
3. 跨平台。
4. 可扩展性。把其他语言编写的库作为扩展工具进行使用。
5. 开源。（这一点可以看一下《黑客与画家》这本书里面说的（自行购买，强烈推荐），开源的软件具有更加丰富的生态，作者格雷厄姆对开源软件十分推崇）

## 历史

- 1990。诞生。
- 2000。Python 2.0 发布。
- 2008。Python 3.0 发布，为了满足现代开发的需求。但是和 2.0 版本（包括 Python 语言最具特点的库）兼容。
- 2013、2014。3.0 版本的库丰富起来，目前成为 Python 版本的主力。
- 2010。Python 2.7 版本发布，也是 2.X 版本的最后一个版本。
- 类库逐渐对2.X版本**放弃**支持。

**【总结】** 新学 Python 使用 3.X 版本。

> Python 作者  
Python 2.X 已经是遗产，Python 3.X 是现在和未来的语言。

## 工具软件介绍

1. 官方版。
2. 发行版。

### 区别介绍
1. 官方本只有基础“解释器”、标准库。对于编程的帮助有限。
2. 发行版。比如最流行的 Anaconda。除了官方版的内容，还会附带很多常用的软件工具（软件包），最重用的是“科学计算”使用的工具（包）。
3. 发行版解决另一个重要问题。包和包之间具有以来关系，比如使用A，需要B，自己从头安装很可能会遗漏，导致编写的程序（对于新手来说，很头疼）很难顺利运行。

### 下载地址
1. Python 官方网址。  
https://www.python.org/  
选择电脑操作系统对应的系统即可。**官方文档**也在这里。
2. Anaconda 官方网址。  
https://www.anaconda.com/download/  
同上。可能打开慢，我没有什么问题。如果实在不行，使用下面的镜像源网站下载。
3. Anaconda 镜像源。  
https://mirror.tuna.tsinghua.edu.cn/help/anaconda/  
应该是安全的。

### 其他软件、工具
1. iPython。  
https://www.ipython.org/  
交互式编译器。可以提示、补全代码，帮助新手集中精力进行编程。
2. jupyter notebook。  
http://jupyter-notebook.readthedocs.io/en/latest/  
在网页上进行编程。**强烈推荐**学习，可以进行远程编写程序，比如进行“机器学习”，自己电脑硬件不行，可以使用 AWS 的强大的云电脑进行处理，这时候使用这个软件可以将代码通过浏览器运行在云电脑上面。
3. sublime text。  
https://www.sublimetext.com  
文本编辑器。用于编写大型程序。多平台，轻量级，打开快速。
4. PyCharm。  
https://www.jetbrains.com/pycharm/
集成开发环境。胜任编写更加大型的软件。
5. Pip。  
https://pip.pypa.io/en/stable/installing/
可以自动解决包与包依赖关系的安装问题。但是使用发行版 Anaconda 就不用考虑，应该是再带的。
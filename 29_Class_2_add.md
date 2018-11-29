
# 29.【Python学习分享文章】_class类的增加与丰富

## 综述

为了体现一个项目的情况，去增加一些功能，然后距离讲解一些修改数值的（update data）的操作，和一些注意事项。

## 增加多个class

方法同之前建立 ```Player()``` 这个类是一样的道理，如下：


```python
class Player():
    def __init__(self, inputName, inputHp):
        self.name = inputName
        self.hp = inputHp
    def printHelp(self):
        print("Mayday.it's %s,****" %(self.name))

class Monster():
    # 里面就是需要输入的属性和方法了
    
playerB2 = Player('beita',120)
playerA2.printHelp()
```

### - 搁置处理

1. 在开发的时候，如果考虑要增加某一个 class，比如 怪物monster；
2. 但是还没有具体想好里面的内容到底要怎么设定；
3. 但是又不想程序在这里报错。

那么，就是下面的处理方法：


```python
class Monster():
    '{这里的内容是说明性文字，比如：}定义一个怪物的 class'
    pass
```

【解释】：

1. ```''``` 单引号里面的内容是为了防止以后忘记当初思考的想法进行的说明、**解释文字**
2. ```pass``` 的意思相当于对程序说：“到我这了是吧，没事，这里面没有内容，跳过我先，你先运行后面的程序，别在我这里就停住报错了，生活需要继续，你也要继续向下运行”

## 增加 class 的属性

解释：class 里面的“变量”就叫做 **class 的属性**。

目的：给 beita 增加 驾驶员driver 的职业身份，给 shuke 增加 飞行员pilot 的职业身份。

代码如下：


```python
class Player():
    def __init__(self, inputName, inputHp, inputCareer):  # added
        self.name = inputName
        self.hp = inputHp
        self.career = inputCareer  # added
    def printHelp(self):
        print("Mayday.it's %s,****" %(self.name))

class Monster():
    # 里面就是需要输入的属性和方法了
    pass

playerA2 = Player('shuke', 100, 'pilot')  # added
playerB2 = Player('beita',120, 'driver')  # added

```

## 增加改名的“方法”

解释：class 里面的定义的“函数”就叫做 **class 方法**。


### - “正确的”构建方法

目的：增加一个方法，来实现修改名字的效果。

代码如下：


```python
class Player():
    def __init__(self, inputName, inputHp, inputCareer):
        self.name = inputName
        self.hp = inputHp
        self.career = inputCareer
    def printInfo(self):  # 调整的
        print("Hi, my name is %s, and my hp is %s, my career is %s, and I do love my job!"
              %(self.name, self.hp, self.career))
    def updateName(self, newName):  # 增加的
        self.name = newName

class Monster():
    # 里面就是需要输入的属性和方法了
    pass

playerA2 = Player('shuke', 100, 'pilot')
# playerB2 = Player('beita',120, 'driver')
playerA2.printInfo()
playerA2.updateName('sxuya')  # 增加的，为了修改名字
playerA2.printInfo()  # 看看改名字的效果
```

    Hi, my name is shuke, and my hp is 100, my career is pilot, and I do love my job!
    Hi, my name is sxuya, and my hp is 100, my career is pilot, and I do love my job!
    

### - 改名字的取巧方法

通过 class 里面属性值的再次赋值进行改名字。

代码如下：


```python
playerA2 = Player('shuke', 100, 'pilot')
# playerB2 = Player('beita',120, 'driver')
playerA2.printInfo()
playerA2.name = 'sxuyaNotSuggest'  # 变量赋值的不推荐方法
playerA2.printInfo()
```

    Hi, my name is shuke, and my hp is 100, my career is pilot, and I do love my job!
    Hi, my name is sxuyaNotSuggest, and my hp is 100, my career is pilot, and I do love my job!
    

### - 属性值不可访问

class 的属性值可以设置成不可访问，也就是相当于“隐藏了”，上述的改名字的方法就不可实现了。

【**不可访问**】：让 class 里面的属性设定成“不可访问”的形式，在属性值前面增加两个下划线 ```__```，如下：


```python
self.__name = inputName
```

如此情况，就无法使用上述方法实现改名字的效果了。

表现如下：


```python
class Player():
    def __init__(self, inputName, inputHp, inputCareer):
        self.__name = inputName
        self.hp = inputHp
        self.career = inputCareer
    def printInfo(self):
        print("Hi, my name is %s, and my hp is %s, my career is %s, and I do love my job!"
              %(self.__name, self.hp, self.career))

# monster 没有用，就先删除了。

playerA2 = Player('shuke', 100, 'pilot')
# playerB2 = Player('beita',120, 'driver')
playerA2.printInfo()
playerA2.name = "sxuyaNotOK"  # 进行了上述改名的操作
playerA2.printInfo()  # 但是信息会发现并没有改变
```

    Hi, my name is shuke, and my hp is 100, my career is pilot, and I do love my job!
    Hi, my name is shuke, and my hp is 100, my career is pilot, and I do love my job!
    

【分析】我们可以看到，即使进行了 ```playerA2.name = "sxuyaNotOK"``` 的改名操作，最后名字也是没有变化的。

### - 属性值不可访问——修改

需要通过“method方法”去修改，也就是说的“正确的”修改属性值方法。

代码如下：


```python
class Player():
    def __init__(self, inputName, inputHp, inputCareer):
        self.__name = inputName
        self.hp = inputHp
        self.career = inputCareer
    def printInfo(self):
        print("Hi, my name is %s, and my hp is %s, my career is %s, and I do love my job!"
              %(self.__name, self.hp, self.career))
    def updataName(self, newName):
        self.__name = newName  # 这里面也要改成两个下划线的结构

playerA2 = Player('shuke', 100, 'pilot')
playerA2.printInfo()
playerA2.updataName('sxuyaIsOK')
playerA2.printInfo()
```

    Hi, my name is shuke, and my hp is 100, my career is pilot, and I do love my job!
    Hi, my name is sxuyaIsOK, and my hp is 100, my career is pilot, and I do love my job!
    

## class 的封装

上述将 ```name``` 改成 ```__name``` 后，变成“不可访问”的状态，这种“特性”就叫做“class 的封装”，即封装后，属性值不可以通过赋值的方法改变.

封装了嘛，就像快递封装了，你就不能在加东西进去了，但是可以通过拆开、重新包装的方法去加东西。

---
注：  
个人微信公众号：codeAndWrite

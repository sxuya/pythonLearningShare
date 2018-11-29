
# 30.【Python学习分享文章】_class 的继承

## 综述

类的继承，即 class 的继承，这里的“继承”是从生物学上的概念拿来延伸的。

生物上的继承，是有相同、有不同，比如你继承了父亲（母亲，不考虑，单对单的关系进行说明）的基因，你有很多地方是和父母是一样的，比如眼睛的颜色、血型，但是也有不同的，比如近视度数、发型，有很多是后天自己进行修改的的。

这同 class 的继承 是一样的情况。“子类”（son）集成“父类”（parent）的情况，包括属性值、方法，这是相同的方面；但是也可以覆盖修改，比如把100改成200，这就是不同的方面。

再来一个更像“class类”的情况。生物学上有“界门纲目科属种”的分类，比如“猫科动物”下面就包含“雪豹”、“家猫”两个（其他的不说明），两者都具有相同的特点，而这些特点就是“父类”（上层分类）的特点，但是两个也有不同，比如体型大小方面。

【作用】：  
建立 class 的时候，不用重复设定同样的属性、方法，减少 code 数量。

## 搭建类的继承框架

后面以之前定义的 ```monster()``` 这一 class 为搭建对象进行说明。

【基础】：  
比如搭建游戏，我们想：“怪物“”要分很多类别，有厉害的，比如 “boss”，有弱鸡的，比如我们说的“小怪”，但是无论如何，他们都是“怪物”，应该具有怪物相同的属性，比如“血量”、“普通攻击”等，但是“boss”可能有厉害的“大招”，小怪没有。

【结构】：  
“怪物”下分“boss”和“小怪”，“怪物”是“boss”和“小怪”的父类，“boss”和“小怪”是“怪物”的子类。  
如下：  

```
        /---->子类1（boss）
父类（怪物）-->子类2（小怪）
        |\--- > ……
        |---->子类n（其他各种小怪）
```

【方法】：  
在 class 的括号里面写入“父类”的名字，即可。

【代码如下】：


```python
class Monster():
    '定义怪物类的内容'
    pass

class Boss(Monster):  # 括号里面Monster，即继承的父类  # 忘记首字母大写了
    '定义boss的内容，Monster的子类'
    pass

class XiaoGuai(Monster):  # 同样继承父类 Monster
    '定义小怪的内容，Monster的子类'
    pass
```

【解释】  
对于大型一些的代码，class 比较多的情况下，这先使用 ```pass``` 的方法，先把逻辑关系编写出来；然后在慢慢编写每一个 class 里面的“属性”和“方法”。

## 增添父类parent 的初始属性和方法

属性，比如生命值等；方法，比如行为动作等，如移动、攻击、说话等。

【代码如下】：


```python
class Monster():
    def __init__(self, input_hp=100):  # 100是作为默认值的，可以被传入的参数覆盖掉
        self.hp = input_hp
    def move(self):  # 忘记打 self 了
        return('我移动到了一个地方，因为现在学习的功能很少，动作就以打印出内容作为替代表达')
```

【设定怪物】：  
设定一个通用的怪物，属于这个一会会作为 parent 的 class。  
代码如下：


```python
mons_1 = Monster(200)  # 将默认值100覆盖成200
print(mons_1.hp)
print(mons_1.move())  # 注意，有括号
```

    200
    我移动到了一个地方，因为现在学习的功能很少，动作就以打印出内容作为替代表达
    

## 完成第一个子类boss

【目的】：  
在```Monster```的基础上增加一个 boss 等级的属性；不增加其他方法，直接继承父类的 ```move()``` 的方法


```python
class Boss(Monster):
    '定义boss的内容，Monster的子类'
    def __init__(self, input_hp, input_level):
        self.hp = input_hp
        self.level = input_level
        
boss_99 = Boss(999, '99级')
print(boss_99.hp)
print(boss_99.level)
print(boss_99.move())
```

    999
    99级
    我移动到了一个地方，因为现在学习的功能很少，动作就以打印出内容作为替代表达
    

### - 改善原始设定

因为 ```hp``` 这个属性已经在父类 ```Monster()``` 已经进行了，如果使用子类 ```boss()```，默认会自动进行 ```Monster()``` 初始化进程，然后子类自己又进行了一次初始化，所以一共进行了两次，会大大**浪费计算资源**。

【改进方法】：  
使用 ```super()``` 方法进行优化，代码如下：


```python
class Boss(Monster):
    '定义boss的内容，Monster的子类'
    def __init__(self, input_level, input_hp=20):  # 错误提示竟然是直译的意思，需要把有默认值的属性值放在后面，
                                            # 没有默认值的放在前面才可以正常运行，这个规则明仔之后正常，
                                            # 但是不明白真的想不到呀
        self.level = input_level
        super().__init__(input_hp) # 子类的hp初始化就跳过，节省了计算资源。
                            #（假设玩吃鸡游戏，几百个人，那资源是很大的）
            # 【解释】super()的意思是：把括号里的输入参数作为输出到父类Monster作为“有顺序”的输入进行赋值
            # 只是减少了重新初始化，但是赋值的逻辑要自己【注意】

boss_99 = Boss('99级', 900) # 设定级别是99级,把血量默认值20改为900
print(boss_99.hp)
print(boss_99.level)
print(boss_99.move())
# Boss() 里面是没有定义 move() 这个方法的，是从父类Monster() 继承过来的。
```

    900
    99级
    我移动到了一个地方，因为现在学习的功能很少，动作就以打印出内容作为替代表达
    

### - 方法覆盖

属性值是可以被覆盖的，同样的，子类定义的相同的“方法”也可以把“父类”的同名方法覆盖掉。

这个情况就是一个概念：【**多态**】，例子后面解释。

【父类增加一个方法】  
代码如下：


```python
class Monster():
    def __init__(self, input_name, input_hp):
        self.name = input_name
        self.hp = input_hp
    def move(self):
        return('我移动到了……（简写）')
    def ask(self):
        print('%s ask:"who am I?"(父类的话)'%(self.name))
```

【子类增加同名方法】  
代码如下：


```python
class Boss(Monster):
    '定义boss的内容，Monster的子类'
    def __init__(self, input_name, input_level, input_hp=7):
        super().__init__(input_name, input_hp)  # 要与父类Monster的属性名字顺序对应，不然就属性值就错位了。
        self.level = input_level

    def ask(self):
        print('%s ask:"which one to be ated first among you?"(子类的话)'%self.name)
```

【运行结果】：


```python
boss_99 = Boss(input_name='boss_99', input_level='99级', input_hp=900)
# 按照顺序，可以把属性名字省略，如下：
# boss_99 = Boss('boss_99', '99级', 900)
print(boss_99.hp)
print(boss_99.level)
print(boss_99.move())
boss_99.ask()
```

    900
    99级
    我移动到了……（简写）
    boss_99 ask:"which one to be ated first among you?"(子类的话)
    

【分析】：  
我们可以看到，父类Monster 和 子类Boss 都有 ```ask()``` 的方法，但是最后子类自己的方法才是最后的代码内容（从print的内容可以看出，最后打印的是子类的话），父类的内容被覆盖了。

也就是说，方法可以继承，同名冲突就按照子类的定义进行运算。

【**多态**定义】：如上述情况，同名方法```aks()```有多种情况，也就是多种状态——父类实例化就按照父类的状态、内容去定义，子类实例化就按照子类的状态、内容去定义，就是**多态**（这是在类的面向对象里面的一个概念，主体是方法；另一个重要特征就是**继承**）。

## 判断 class 的关系

### - 方法

```type()``` 和 ```isinstance```

### - 判断类别

输出实例是那个 class，使用 ```type()``` 进行输出。

【作用】  
在大型项目中，有时候忘记了定义的实例到底是那个类型了，快速的方法是直接电脑输出，而不是在成堆的代码里面去寻找。

代码如下：

- 先增加一个子类2——XiaoGuai（小怪）：


```python
class XiaoGuai(Monster):
    '定义小怪的内容，Monster的子类'
    def __init__(self, input_animalName, input_hp=3):
        super().__init__(input_animalName, input_hp)

    def ask(self):  # ask() 的多肽的另一个
        print('%s ask:"please do not attack me~"(子类小怪的话)'%self.name)

xiao_cat = XiaoGuai('cat_01', 11)
```

- 对 ```mons_1```、```boss_99```、```xiao_cat```进行类别判断、输出结果，代码如下：


```python
print('mons_1 的类是：%s' %type(mons_1))
print('boss_99的类是：%s' %type(boss_99))
print('xiao_cat的类是：%s' %type(xiao_cat))
```

    mons_1 的类是：<class '__main__.Monster'>
    boss_99的类是：<class '__main__.Boss'>
    xiao_cat的类是：<class '__main__.XiaoGuai'>
    

### - 判断父子关系

代码如下：


```python
print(isinstance(mons_1,Monster)) # 不是子类，是同级的
print(isinstance(boss_99,Monster)) # 是子类
print(isinstance(xiao_cat,Monster)) # 是子类
print(isinstance(xiao_cat,Boss)) # 不是子类，两个都是父类Monster的子类，是同级关系
```

    False
    True
    True
    False
    

### - class 关系判断拓展

所有的数据类型都是隶属于一个 class 的，例子如下：


```python
print(type(list))
print(type(123))
print(isinstance(123, object))
print(isinstance(type, object))
print(isinstance(list, object))
```

    <class 'type'>
    <class 'int'>
    True
    True
    True
    

【说明】  
说明 list 是 type 这个 class、123这样的数字是 int 这个 class、所有的 class 总的 parent 是 object，也就是：所有的数据类型是类的树状结构，倒立的，object 是总起点，向下伸出不同的分支，代表不同的 class。

## 总结

class 是具有相同“属性”、“方法”的数据的**集合**，具有相同的特点，但是具体表现、数值是不一样的。

特征：  
1. 属性可以被封装（外界无法访问）；
2. 继承（不用重复定义属性、方法）；
3. 多肽（相当于if，“method方法”根据情况做出不同的动作）；
4. class 无法直接使用，需要实例化，处理的对象也是实例。

---
注：  
个人微信公众号：codeAndWrite

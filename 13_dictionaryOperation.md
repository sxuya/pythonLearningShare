
# 【Python学习分享文章】_dictionary（字典）

## 综述

### 数据类型特点

dictionary（字典）类型的数据特最大**特点**，就是可以记录信息、统计信息。

不同类型数据的特点对比：

- string（字符串）：类别和数量的对应关系不明显。
- list（列表）：强调的是“顺序”这一个数据特点。
- dictionary（字典）：名字和对应的数值的数据类型。好比我们平时用的字典，一个“名词”，后面跟着这个名词的“数据”，即解释的内容，计算机的这一数据类型就是“数之内容”。

## 详细介绍

数据的逻辑基础：高中数学学习的一个概念：映射。

### 数据结构：

使用“{ }”，里面每一个数据包括一个“哈希值”和对应的“对象”（即数据内容），两者用“:”连接；不同的字典内容，用“,”隔开.

“哈希值”在程序里面的名字是“key”，“哈希值”一般都叫做“键值”（key 不翻译成“钥匙”，而是“keyboard”（键盘）的 key 的意思）

如下结构：


```python
a_dict = {'哈希值':"对象"}

### 比如个人信息的例子

aPersonInformation = {"name":"sxuya", "height":183, "age": 18}
```

查看数据类型的名字，显示的“dict”字样即是。


```python
print(type(aPersonInformation))
```

    <class 'dict'>
    

### 基本操作

#### 增加内容

使用中括号“[ ]”输入“哈希值”，使用“=”赋予其数据（即“对象”），如下：


```python
aPersonInformation['phone'] = 10086
print(aPersonInformation)
```

    {'height': 183, 'phone': 10086, 'name': 'sxuya', 'age': 18}
    

**【注意：】**输出的信息是没有顺序的，每次输出顺序很可能不一样。

比如不改变内容、不进行操作，再输出一次信息,,,竟然是一样的，是只要进行输出，那么就固定下来顺序了么？：


```python
print(aPersonInformation)
```

    {'height': 183, 'phone': 10086, 'name': 'sxuya', 'age': 18}
    

### demo 说明

之前的生肖、星座 demo 的扩展，增加**“记录、统计输入的信息的数据”**。


```python
zodiac_name = (u'摩羯座', u'水瓶座', u'双鱼座', u'白羊座', u'金牛座', u'双子座',
               u'巨蟹座', u'狮子座', u'处女座', u'天秤座', u'天蝎座', u'射手座')
zodiac_days = ((1, 20), (2,19), (3, 21), (4, 21), (5, 21), (6, 22),
               (7, 23), (8, 23), (9, 23), (10, 23), (11, 23), (12, 23))
chinese_zodiac = "猴鸡狗猪鼠牛虎兔龙蛇马羊"

# 增加用于统计信息用的字典
## 不够“优雅”的写法：
# cz_num_dict = {}
# for animal in chinese_zodiac:
#     ca_num_dict[animal] = 0

# zodiac_num_dict = {}
# for name in zodiac_name:
#     zodiac_num_dict[name] = 0
## “优雅”的写法：
cz_num_dict = {animal:0 for animal in chinese_zodiac}
zodiac_num_dict = {name:0 for name in zodiac_name}

print(cz_num_dict)
print(zodiac_num_dict)
```

    {'鼠': 0, '羊': 0, '蛇': 0, '马': 0, '虎': 0, '龙': 0, '鸡': 0, '猪': 0, '牛': 0, '狗': 0, '兔': 0, '猴': 0}
    {'狮子座': 0, '金牛座': 0, '天秤座': 0, '巨蟹座': 0, '天蝎座': 0, '摩羯座': 0, '白羊座': 0, '射手座': 0, '处女座': 0, '双子座': 0, '双鱼座': 0, '水瓶座': 0}
    


```python
# 由用户输入年、月、日信息
## 放入 while 语句，使得可以持续输入
while True: # 这里是一个死循环，只是为了演示方便而已
    year = int(input("please input the year of your birthday:"))
    month = int(input("please input the month of your birthday:"))
    day = int(input("please input the day of your birthday:"))
    
    # 判断星座的下标，用 n 来表明
    n = 0
    while zodiac_days[n] < (month, day):
        if month == 12 and day > 23:
            break
        n += 1
    
    # 对输入的信息，判定生肖、星座，对相应的 key 值进行数据更新
    zodiac_num_dict[zodiac_name[n]] += 1
    cz_num_dict[chinese_zodiac[year % 12]] += 1
    
    # 输出两个字典信息
    print(zodiac_num_dict)
    print(cz_num_dict)
    
    # 用“key”键值、对象代替文本信息，来进行信息输出，获得统计信息。
    for key_xingzuo in zodiac_num_dict.keys():
        print("星座 %s 有 %d 个"%(key_xingzuo, zodiac_num_dict[key_xingzuo]))
    for key_animal in cz_num_dict.keys():
        print("生肖 %s 有 %d 个"%(key_animal, cz_num_dict[key_animal]))
```

    please input the year of your birthday:2018
    please input the month of your birthday:12
    please input the day of your birthday:01
    {'双鱼座': 0, '射手座': 1, '巨蟹座': 0, '天蝎座': 0, '水瓶座': 0, '天秤座': 0, '摩羯座': 0, '双子座': 0, '白羊座': 0, '金牛座': 0, '狮子座': 0, '处女座': 0}
    {'虎': 0, '兔': 0, '鼠': 0, '羊': 0, '牛': 0, '蛇': 0, '猴': 0, '猪': 0, '狗': 1, '鸡': 0, '马': 0, '龙': 0}
    星座 双鱼座 有 0 个
    星座 射手座 有 1 个
    星座 巨蟹座 有 0 个
    星座 天蝎座 有 0 个
    星座 水瓶座 有 0 个
    星座 天秤座 有 0 个
    星座 摩羯座 有 0 个
    星座 双子座 有 0 个
    星座 白羊座 有 0 个
    星座 金牛座 有 0 个
    星座 狮子座 有 0 个
    星座 处女座 有 0 个
    生肖 虎 有 0 个
    生肖 兔 有 0 个
    生肖 鼠 有 0 个
    生肖 羊 有 0 个
    生肖 牛 有 0 个
    生肖 蛇 有 0 个
    生肖 猴 有 0 个
    生肖 猪 有 0 个
    生肖 狗 有 1 个
    生肖 鸡 有 0 个
    生肖 马 有 0 个
    生肖 龙 有 0 个
    please input the year of your birthday:2018
    please input the month of your birthday:12
    please input the day of your birthday:01
    {'双鱼座': 0, '射手座': 2, '巨蟹座': 0, '天蝎座': 0, '水瓶座': 0, '天秤座': 0, '摩羯座': 0, '双子座': 0, '白羊座': 0, '金牛座': 0, '狮子座': 0, '处女座': 0}
    {'虎': 0, '兔': 0, '鼠': 0, '羊': 0, '牛': 0, '蛇': 0, '猴': 0, '猪': 0, '狗': 2, '鸡': 0, '马': 0, '龙': 0}
    星座 双鱼座 有 0 个
    星座 射手座 有 2 个
    星座 巨蟹座 有 0 个
    星座 天蝎座 有 0 个
    星座 水瓶座 有 0 个
    星座 天秤座 有 0 个
    星座 摩羯座 有 0 个
    星座 双子座 有 0 个
    星座 白羊座 有 0 个
    星座 金牛座 有 0 个
    星座 狮子座 有 0 个
    星座 处女座 有 0 个
    生肖 虎 有 0 个
    生肖 兔 有 0 个
    生肖 鼠 有 0 个
    生肖 羊 有 0 个
    生肖 牛 有 0 个
    生肖 蛇 有 0 个
    生肖 猴 有 0 个
    生肖 猪 有 0 个
    生肖 狗 有 2 个
    生肖 鸡 有 0 个
    生肖 马 有 0 个
    生肖 龙 有 0 个
    

---
注：  
个人微信公众号：codeAndWrite

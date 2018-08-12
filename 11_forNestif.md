
# 【Python学习分享文章】_for 嵌套 if

### 原始数据


```python
zodiac_name = (u'摩羯座', u'水瓶座', u'双鱼座', u'白羊座', u'金牛座', u'双子座',
               u'巨蟹座', u'狮子座', u'处女座', u'天秤座', u'天蝎座', u'射手座')
zodiac_days = ((1, 20), (2,19), (3, 21), (4, 21), (5, 21), (6, 22),
               (7, 23), (8, 23), (9, 23), (10, 23), (11, 23), (12, 23))
```

### 数据改为由用户输入


```python
# month = input('请输入月份：') # 这样的语句，得到的数据默认是 string（字符串）
month = int(input("请输入月份："))
# print(type(month))
day = int(input("请输入日期："))
```

    请输入月份：5
    请输入日期：21
    


```python
for zd_num in range(len(zodiac_days)):
    if zodiac_days[zd_num] >= (month, day):
        print(zodiac_name[zd_num])
        break # 如果没有这个“终止”操作，金牛座后面的数据也会进行比较，并且也是 True 的判定，所以都会输出，但不是我们想要的
```

    金牛座
    

### 补充结尾判断，形成闭环


```python
month2 = int(input("请输入月份（请等于12）："))
day2 = int(input("请输入日期（请在24-31之间选择一个数）："))
for zd_num in range(len(zodiac_days)):
    if zodiac_days[zd_num] >= (month2, day2):
        print(zodiac_name[zd_num])
        break
    elif month2 == 12 and day2 >23:
        print(zodiac_name[0])
        break # 获得结果后，就是一个，就终止语句
```

    请输入月份（请等于12）：12
    请输入日期（请在24-31之间选择一个数）：25
    摩羯座
    

**注释：** 参考之前的 tuple.md 文件，里面的 lambda 和 filter 结合也是实现同样的功能。

---
注：  
个人微信公众号：codeAndWrite

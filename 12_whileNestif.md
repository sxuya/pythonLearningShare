
# 【Python学习分享文章】_while 嵌套 if

### 数据基础


```python
zodiac_name = (u'摩羯座', u'水瓶座', u'双鱼座', u'白羊座', u'金牛座', u'双子座',
               u'巨蟹座', u'狮子座', u'处女座', u'天秤座', u'天蝎座', u'射手座')
zodiac_days = ((1, 20), (2,19), (3, 21), (4, 21), (5, 21), (6, 22),
               (7, 23), (8, 23), (9, 23), (10, 23), (11, 23), (12, 23))
```

### 嵌套实现


```python
month = int(input("请输入月份："))
day = int(input("请输入日期："))
```

    请输入月份：8
    请输入日期：15
    


```python
n = 0
while zodiac_days[n] < (month, day):
    n += 1 # 一直向上取，直到无法超越，就找到最接近输入日期的之前的日期、及其对应的下标
print(zodiac_name[n])
```

    狮子座
    

【问题：】

但是上述代码，不能执行 12月23 之后日期的判断，因为那时候 n 就会变成 12，当作下标，就会指向第 13 个数据，但是数据就只有 12 个。所以会报错，提示 ```out of range``` 字样。


```python
(month2, day2) = (12, 25)
while zodiac_days[n] < (month2, day2):
    n += 1
print(zodiac_name[n])
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-4-fe27edd72949> in <module>()
          1 (month2, day2) = (12, 25)
    ----> 2 while zodiac_days[n] < (month2, day2):
          3     n += 1
          4 print(zodiac_name[n])
    

    IndexError: tuple index out of range


【解决方法：】加入 ```if``` 语句，排除掉这种可能的错误。


```python
n = 0
(month2, day2) = (12, 25)
while zodiac_days[n] < (month2, day2):
    if month2 == 12 and day2 > 23: # 提前判断进行终止，保持 n=0 的状态。个人认为把 while 写在 if 里面，会更有效率吧。
        break # 此处的 break 终止的是所在的上级循环语句，即 while 语句
    n += 1
print(zodiac_name[n])
```

    摩羯座
    

---
注：  
个人微信公众号：codeAndWrite

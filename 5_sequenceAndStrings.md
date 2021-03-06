【Python学习分享文章】_序列概念+字符串详细内容

## 综述 

### 官方说法：

> 是指他的成员都是有序排列，并且可以通过下标偏移量访问到他的一个或者几个成员。

严格是严格，但是不接地气。

### 我的理解：

数据是有规律排列的一组数据，比如字符类型的数据生肖，是“子丑寅卯辰巳午未申酉戌亥”。默认是带有位置数字标签的，以“0”开头，即前面的“子”是序列的第0个，数组的第0个就是“子”，第11个就是“亥”。  
因为是有数字（第几个）标签，所以可以进行计算处理，让计算机进行运算“思考”。

## 类别
1. 字符串。  
一个字符对应一个数字标签。比如：  
```
“abcdefg”
```
2. 列表。  
以中括号“[]”形式表示，一个逗号一个数字标签。比如：  
```
[1992, 1883, 2030],['abd', 'xyz'],[123, 'abc']
```
3. 元组。  
以括号“()”形式表示，通常是2个数据作为一个元祖。比如：
```
('abd', 'def')
```

## 提取（第几个）数据

方法：  
使用中括号“[]”，中括号内的数字就是第几个标签的意思。

1. 得到其中某一个数据
例子：  
```
# 记录生肖，根据年份来判断生肖
chinese_zodiac = "鼠牛虎兔龙蛇马羊猴鸡狗猪"
a = chinese_zodiac[0]
print(a)
print(chinese_zodiac[11])
```
输出结果：
```
鼠
猪
```
2. 取出连续几个数据  
【方法：】采用“：”表达方式：
```
print(chinese_zodiac[0:4])
print(chinese_zodiac[2:4])
```
结果是：
```
鼠牛虎兔
虎兔
```
【理解1：】[0:4]相当于高中数学的[0,4)，前面的包含，后面的不包含。  
【理解2：】第一个表示起点数字标签，第二个表示结尾到开头一共几个。  
个人更偏向第一种理解，方便。
3. 从后面取出数据  
【方法：】“[]”内的数字用负数表示。  
例子：
```
print(chinese_zodiac[-1])
print(chinese_zodiac[-1:-4])
print(chinese_zodiac[-4:-1])
print(chinese_zodiac[-4:])
```
结果是：
```
猪
（这行是空的，没有东西，为了markdown格式排版，这里补出内容）
猴鸡狗
猴鸡狗猪
```
【注意：】区间选定多个数据，也是要保证向前到后的顺序，不然会得到空的数据。

---

注：
个人微信公众号：codeAndWrite
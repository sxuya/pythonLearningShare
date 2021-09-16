
# 7. 【Python学习分享文章】\_webData_requests

## 综述

requests 是第三方库，所以是需要自己安装的，在命令窗口输入 ```pip install requests``` 安装即可。

## 代码演示

### - get 形式上传数据

代码如下：


```python
import requests

url = 'http://httpbin.org/get'
data = {'key':'value', 'username':'sxuya'}
# 方便的地方是：data 数据不用自己加工处理，库的.get方法自动进行处理。
response = requests.get(url, data)
print(response.text)  # 不是 .read()，而是库里面的 .text 方法，显示成“文本格式”
```

    {
      "args": {
        "key": "value", 
        "username": "sxuya"
      }, 
      "headers": {
        "Accept": "*/*", 
        "Accept-Encoding": "gzip, deflate", 
        "Host": "httpbin.org", 
        "User-Agent": "python-requests/2.18.4"
      }, 
      "origin": "121.8.227.29, 121.8.227.29", 
      "url": "https://httpbin.org/get?key=value&username=sxuya"
    }
    
    

【结果说明】  
和之前用 urllib 得到的结果是一样的。

### - post 形式上传数据

代码如下：


```python
url_post = 'http://httpbin.org/post'
response_post = requests.post(url_post, data)
print(response_post.json())
# 另外一种格式，我现在也不找到这种格式有什么用，
# 反正就是说，这个库，可以方便转化成很多不同形式的数据。
```

    {'data': '', 'args': {}, 'headers': {'Host': 'httpbin.org', 'Content-Type': 'application/x-www-form-urlencoded', 'Accept': '*/*', 'User-Agent': 'python-requests/2.18.4', 'Content-Length': '24', 'Accept-Encoding': 'gzip, deflate'}, 'origin': '121.8.227.29, 121.8.227.29', 'form': {'key': 'value', 'username': 'sxuya'}, 'files': {}, 'json': None, 'url': 'https://httpbin.org/post'}
    

【结果说明】  
同样的，使用 requests 库后，打码的可读性得到很大的提升，不用将精力放在很多对于初学者来说很晦涩的底层代码的转化、编写。

---
注：  
个人微信公众号：codeAndWrite

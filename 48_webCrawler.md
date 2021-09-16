
# 48. 【Python学习分享文章】\_webCrawler

## 综述  
一个网站的相同类型的内容（比如一个模块里面所有的图片），使用 HTML 语言编写的形式是有相同的格式，只要找到其中的格式模式，使用正则表达式将格式匹配出来，然后将其中单个元素的内容切出来，就好了。

## demo 演示

### - 目的

抓取网址（ http://www.cnu.cc/discoveryPage/hot-人像 ）单个页面里面所有的图片的标题&链接地址。

### - 寻找格式模式

获取网页的 HTML 语言文本（如下：），从其中找到图片的格式模式。

更方便的方法，直接在 Chrome 浏览器里面，在对应的位置“右键”-“检查”，在“Elements”下面寻找到对应的代码模块即可。
如下：


```python
import requests, re

content = requests.get('http://www.cnu.cc/discoveryPage/hot-人像')
print(content.text)
```

    <!doctype html>
    <html class="no-js" >
    
      <head>
        <meta charset="utf-8">
        <title>
            原创 - CNU视觉联盟 
    
    </title>
        <meta name="keywords" content=" CNU,视觉,摄影,视觉联盟,照片,摄影师,摄影作品集,在线摄影作品集,照片精选,网络摄影作品集,在线照片展廊,分享图片,专业摄影,社会摄影,上传照片,分享照片,出色的摄影作品集,摄影社区,最新摄影作品,快速创建作品集,模特和摄影师,商业摄影,建筑摄影,专业作品集管理,视觉中国图库,视觉中国,视觉联盟,摄影作品,摄影作品欣赏,时尚摄影,时尚摄影作品,艺术,艺术作品,艺术摄影作品,人体艺术,时尚杂志,品牌广告,视觉,视觉艺术,视觉作品,视觉作品欣赏,时尚,设计,当代艺术 " />
        <meta name="description" content=" 中国视觉联盟cnu.cc-是一家致力于传播优秀视觉文化,研究视觉艺术、交流视觉理念、开拓大众审美视野的专业性视觉网站。 ">
    
        <meta name="viewport" content="width=device-width">
          <link rel="icon" href="http://img.cnu.cc/assets/images/favicon.ico" type="image/x-icon" />
          <link rel="shortcut icon" href="http://img.cnu.cc/assets/images/favicon.ico" type="image/x-icon" />
        <link rel="stylesheet" href="http://www.cnu.cc/assets/font-awesome-4.4.0/css/font-awesome.css">
    
    
          <link rel="stylesheet" href="http://img.cnu.cc/assets/bootstrap/css/bootstrap.min.css">
          <link rel="stylesheet" href="http://img.cnu.cc/assets/styles/main.css">
          <!--[if lt IE 9]>
          <!--
          <script src="http://cdnjs.cloudflare.com/ajax/libs/respond.js/1.4.2/respond.min.js"></script>
          <script src="http://cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.2/html5shiv.min.js"></script>
          -->
          <script src="http://img.cnu.cc/assets/scripts/lib/respond.min.js"></script>
          <script src="http://img.cnu.cc/assets/scripts/lib/html5shiv.min.js"></script>
          <![endif]-->
        <script>
            
            Config = {
                'cdnDomain': 'http://img.cnu.cc',
                'user_id': 0,
                'routes': {
                },
                'token': 'L6bHyAnmqI7fMlEZOwf4iq8i0Sc5ncfpzuZKsASE'
            };
        </script>
          <script>
              var _hmt = _hmt || [];
              (function() {
                  var hm = document.createElement("script");
                  hm.src = "//hm.baidu.com/hm.js?debc91213222aae0abfdb6176ec8d28a";
                  var s = document.getElementsByTagName("script")[0];
                  s.parentNode.insertBefore(hm, s);
              })();
          </script>
        
        <link rel="stylesheet" href="http://img.cnu.cc/assets/styles/discovery.css">
        <link rel="stylesheet" href="http://img.cnu.cc/assets/styles/public.css">
    
    
      </head>
    
      <body>
            <nav class="navbar navbar-inverse navbar-fixed-top">
    
        <div class="navbar-header">
            <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" style="padding: 0px 20px;" href="http://www.cnu.cc"><div id="logo" ></div></a>
        </div>
        <div class="collapse navbar-collapse">
            <ul id="navbar" class="nav navbar-nav">
                <li>
                    <a href="http://www.cnu.cc/selectedPage"><i class="myicon icon-home"></i> <span>首页</span></a>
                </li>
                <li>
                    <a href="http://www.cnu.cc/inspirationPage/recent-0"><i class="myicon icon-inspiration"></i> <span>灵感</span></a>
                </li>
    
                <li>
                    <a href="http://www.cnu.cc/discoveryPage/hot-0"><i class="myicon icon-discovery"></i> <span>原创</span></a>
                </li>
                
            </ul>
    
    
            <ul class="nav navbar-nav navbar-right" style="margin-right: 10px;">
    <li><form method="GET" action="http://www.cnu.cc/search" accept-charset="UTF-8" id="searchForm" autocomplete="off" role="search" class="navbar-form navbar-left">
    
        <div class="search-group">
            <input type="text" id="keyword" value="" class="search-control" placeholder="登录后搜索">
        </div>
        </form>
    </li>
    
    
                    <li class="dropdown active publishBtn">
                        <a class="dropdown-toggle " id="dropdownMenu1" data-toggle="dropdown" href="#">
                             投稿
                            <span class="caret"></span>
                        </a>
                        <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
    
    
    
                            <li><a href="http://www.cnu.cc/works/create"> 原创图集</a></li>
                            <li><a href="http://www.cnu.cc/work/createTutorial"> 原创教程</a></li>
                           
                                                </ul>
                    </li>
                                <li ><a href="http://www.cnu.cc/signup">注册</a></li>
                    <li ><a href="http://www.cnu.cc/login">登录</a></li>
                
    
            </ul>
        </div>
    
    </nav>
    
    
            
    
    
          <div style ="display:none">
             
             </div>
    
        <div class="page-header second-nav" >
    
            <ul class="container nav nav-pills">
                <li class="select"><a href="http://www.cnu.cc/discoveryPage/hot-0">发现</a></li>
                <li ><a href="http://www.cnu.cc/activities">动态</a></li>
                <li ><a href="http://www.cnu.cc/following">我的关注</a></li>
            </ul>
        </div>
    
        <div class="container pc" >
            <form method="POST" action="http://www.cnu.cc/works/recommend" accept-charset="UTF-8" id="recommendForm" class="recommendForm"><input name="_token" type="hidden" value="L6bHyAnmqI7fMlEZOwf4iq8i0Sc5ncfpzuZKsASE">
    
    
        <div class="grid">
            <div class="grid-item">
                <div class="menu">
                    <a href="http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E5%83%8F" class='orderType selected'><h3>热门</h3></a>
                    <a href="http://www.cnu.cc/discoveryPage/recommend-%E4%BA%BA%E5%83%8F" class='orderType '><h3>推荐</h3></a>
                    <a href="http://www.cnu.cc/discoveryPage/recent-%E4%BA%BA%E5%83%8F" class='orderType '><h3>最新</h3></a>
    
                        <hr>
                        <div class="all">
                            <a  class="category" category_id="0" href="http://www.cnu.cc/discoveryPage/hot-0"><h4><span class="">全部</span></h4></a>
                        </div>
                        <div class="group row">
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E5%83%8F"><span class="">人像</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E8%83%B6%E7%89%87"><span class="">胶片</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E8%87%AA%E7%84%B6"><span class="">自然</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E8%89%BA%E6%9C%AF"><span class="">艺术</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E8%A1%97%E9%81%93"><span class="">街道</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E8%A1%A8%E6%BC%94"><span class="">表演</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E9%9D%99%E7%89%A9"><span class="">静物</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E9%A3%8E%E5%85%89"><span class="">风光</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E9%BB%91%E7%99%BD"><span class="">黑白</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E6%97%B6%E5%B0%9A"><span class="">时尚</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E6%97%85%E8%A1%8C"><span class="">旅行</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E6%96%B0%E9%97%BB"><span class="">新闻</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E5%8A%A8%E7%89%A9"><span class="">动物</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E5%BB%BA%E7%AD%91"><span class="">建筑</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E5%A9%9A%E7%A4%BC"><span class="">婚礼</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E5%AE%B6%E5%BA%AD"><span class="">家庭</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E5%B9%BF%E5%91%8A"><span class="">广告</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E5%BE%AE%E8%B7%9D"><span class="">微距</span></a>
                            <a class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E6%8A%BD%E8%B1%A1"><span class="">抽象</span></a>
                            <a  class="category col-xs-6" category_id="220" href="http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E6%96%87"><span class="">人文</span></a>
                        </div>
                                    </div>
    
                </div>
                                                    <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/336905" class="thumbnail" target="_blank">
                            <div class="title">
                                女孩与花
                                </div>
                            <div class="author">
                                Serendipity_zx
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1903/12/78a5a446f12e38bcbc347cd0956650c7.jpg?width=920&amp;height=1466" alt="女孩与花">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/335746" class="thumbnail" target="_blank">
                            <div class="title">
                                "摄影里的民谣爱情故事”
                                </div>
                            <div class="author">
                                安正圆
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1903/05/45a69eb60a3e3e93beddbf900178210e.jpg?width=2400&amp;height=1350" alt=""摄影里的民谣爱情故事”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/335224" class="thumbnail" target="_blank">
                            <div class="title">
                                不渝
                                </div>
                            <div class="author">
                                拍照的古德卡特
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1903/05/f26d24119f283f5cbc5d8a3ae11b2ed2.jpg?width=2872&amp;height=3869" alt="不渝">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/334692" class="thumbnail" target="_blank">
                            <div class="title">
                                妖怪也喜欢小朋友啊
                                </div>
                            <div class="author">
                                食物的小剧场
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/27/36091f982de63833bd39a0bf26d477d7.jpg?width=4896&amp;height=3264" alt="妖怪也喜欢小朋友啊">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/333806" class="thumbnail" target="_blank">
                            <div class="title">
                                一颗草莓。
                                </div>
                            <div class="author">
                                蔬茉
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/21/85087fc9bfee3cd4b3ffb8cad1af398a.jpg?width=1000&amp;height=1620" alt="一颗草莓。">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/333607" class="thumbnail" target="_blank">
                            <div class="title">
                                住在村里的人
                                </div>
                            <div class="author">
                                食物的小剧场
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/20/a3473448e65437ecbfa4151b1437dd78.jpg?width=4896&amp;height=3264" alt="住在村里的人">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/332291" class="thumbnail" target="_blank">
                            <div class="title">
                                #On the STREET of daylight. 
                                </div>
                            <div class="author">
                                摄影师Gin
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/12/aa5c7cb485813dd3bebe9c0204364f58.jpg?width=893&amp;height=1339" alt="#On the STREET of daylight. ">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/332289" class="thumbnail" target="_blank">
                            <div class="title">
                                《流浪又自由》
                                </div>
                            <div class="author">
                                寒photo
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/12/7134e5470a6038f39260c9e0874ae6fc.jpg?width=1417&amp;height=944" alt="《流浪又自由》">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/332090" class="thumbnail" target="_blank">
                            <div class="title">
                                黑白肖像
                                </div>
                            <div class="author">
                                两脚兽
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/10/d085e51540ea3fd6a7bf29f8f33612d4.jpg?width=5165&amp;height=7747" alt="黑白肖像">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/331443" class="thumbnail" target="_blank">
                            <div class="title">
                                FRONT风尚周刊 X 吴莫愁
                                </div>
                            <div class="author">
                                MeirJin
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1902/03/f3542eac8b9c3d59b8cf430ced080584.jpg?width=4480&amp;height=6720" alt="FRONT风尚周刊 X 吴莫愁">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/330503" class="thumbnail" target="_blank">
                            <div class="title">
                                安安
                                </div>
                            <div class="author">
                                鹿千千_
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1901/27/40aed5a738603c72bcd70c6bfd40b228.jpg?width=3358&amp;height=1889" alt="安安">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/329928" class="thumbnail" target="_blank">
                            <div class="title">
                                四十七
                                </div>
                            <div class="author">
                                拍照的古德卡特
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1901/23/5288829e4751352bb4e43082a992e5fd.jpg?width=6671&amp;height=4530" alt="四十七">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/329472" class="thumbnail" target="_blank">
                            <div class="title">
                                心裡 
                                </div>
                            <div class="author">
                                林小仙仙仙仙仙
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1901/19/fcf2298c8e0f3d83b64554a9b523c76f.jpg?width=3000&amp;height=4485" alt="心裡 ">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/329030" class="thumbnail" target="_blank">
                            <div class="title">
                                阿筱与花童
                                </div>
                            <div class="author">
                                韋韋韋維斯
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1901/15/d28845666e28337fa1716dd97b06b9ae.jpg?width=3649&amp;height=5444" alt="阿筱与花童">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/323707" class="thumbnail" target="_blank">
                            <div class="title">
                                章若楠
                                </div>
                            <div class="author">
                                嘉朔JiaShuo
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/29/0593177efc503db89ff2183c38627655.jpg?width=3472&amp;height=5208" alt="章若楠">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/323792" class="thumbnail" target="_blank">
                            <div class="title">
                                遇见了冬天
                                </div>
                            <div class="author">
                                六六一_
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/29/694ccd450edd38028bb2c509bd8b462a.jpg?width=920&amp;height=367" alt="遇见了冬天">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/323484" class="thumbnail" target="_blank">
                            <div class="title">
                                『陌生如你』
                                </div>
                            <div class="author">
                                三更过客
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/27/4c983541443e3e5fbe3aac087ddc147e.jpg?width=920&amp;height=1380" alt="『陌生如你』">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/323474" class="thumbnail" target="_blank">
                            <div class="title">
                                绛
                                </div>
                            <div class="author">
                                拍照的古德卡特
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/27/ca3025168302345ba2cb54149407a680.jpg?width=920&amp;height=607" alt="绛">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/323371" class="thumbnail" target="_blank">
                            <div class="title">
                                "她 在山林里 在心房里“
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/26/1f9e4275b4313460bc434512718124f2.jpg?width=2093&amp;height=2928" alt=""她 在山林里 在心房里“">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/323301" class="thumbnail" target="_blank">
                            <div class="title">
                                “爱恋是道无解的题”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/26/25d6b1d4a0ca3f1f9722bea8349cb923.jpg?width=3637&amp;height=2045" alt="“爱恋是道无解的题”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/322732" class="thumbnail" target="_blank">
                            <div class="title">
                                预售等待
                                </div>
                            <div class="author">
                                曰樂
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/23/11af2b2857c735fca303e319cdf7041b.jpg?width=4480&amp;height=6720" alt="预售等待">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/319565" class="thumbnail" target="_blank">
                            <div class="title">
                                Diving in Love
                                </div>
                            <div class="author">
                                CNH
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/17/fb2ba2860d00388d9ef8e5a435cbbcc4.jpg?width=1228&amp;height=1818" alt="Diving in Love">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/318906" class="thumbnail" target="_blank">
                            <div class="title">
                                ”心内的一场雨”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/13/aac58ec87d473f13b0a864625970d413.jpg?width=3264&amp;height=4352" alt="”心内的一场雨”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/318419" class="thumbnail" target="_blank">
                            <div class="title">
                                Xion
                                </div>
                            <div class="author">
                                橙AAA
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/15/c1d6a430b2673f3ebef099310e4b0a58.jpg?width=2433&amp;height=3637" alt="Xion">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/317994" class="thumbnail" target="_blank">
                            <div class="title">
                                阴天
                                </div>
                            <div class="author">
                                快门怪咖
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/10/d757a332864433068e5cc5c4409df548.jpg?width=1920&amp;height=1080" alt="阴天">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/318250" class="thumbnail" target="_blank">
                            <div class="title">
                                我说我想等一个命中注定之人出现，然后刻骨铭心爱一场，不计得失，不计结果
                                </div>
                            <div class="author">
                                麻雀大人
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/11/252b1b41b5203300b3025fae2e1ce805.jpg?width=2436&amp;height=1588" alt="我说我想等一个命中注定之人出现，然后刻骨铭心爱一场，不计得失，不计结果">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/316962" class="thumbnail" target="_blank">
                            <div class="title">
                                "那些女孩的样子”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/04/46d7893d26a933f69ee10a113cbb29f9.jpg?width=2070&amp;height=1164" alt=""那些女孩的样子”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/316966" class="thumbnail" target="_blank">
                            <div class="title">
                                The Enchanted
                                </div>
                            <div class="author">
                                Shyphoniths
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1903/13/88f997210ef93e79812b3964f9ece80b.jpg?width=2072&amp;height=3000" alt="The Enchanted">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/315937" class="thumbnail" target="_blank">
                            <div class="title">
                                "又是一年入冬时！”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/02/d0692695ae9c37128860ddd01ed83d9e.jpg?width=2080&amp;height=3105" alt=""又是一年入冬时！”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/315850" class="thumbnail" target="_blank">
                            <div class="title">
                                往朗目山顶开
                                </div>
                            <div class="author">
                                雷克雅未克的冰川和海
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1812/01/033170ea00dd3e45a0de18d5c68f58a4.jpg?width=3389&amp;height=2311" alt="往朗目山顶开">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/314018" class="thumbnail" target="_blank">
                            <div class="title">
                                "是的，你又初恋了！”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/21/9f6856a5f7563a35a393b2ef81db8bbb.jpg?width=3264&amp;height=1836" alt=""是的，你又初恋了！”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/313821" class="thumbnail" target="_blank">
                            <div class="title">
                                ”我想我会努力忘了你的模样， 但依然忘不了你的眼睛，那曾经最最深爱着的爱笑的眼睛  ！”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/21/298ada8846ba36d2ba7412585e584a64.jpg?width=2447&amp;height=1376" alt="”我想我会努力忘了你的模样， 但依然忘不了你的眼睛，那曾经最最深爱着的爱笑的眼睛  ！”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/313619" class="thumbnail" target="_blank">
                            <div class="title">
                                髪をほどいて
                                </div>
                            <div class="author">
                                鹿野良
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/19/9b63059b6789347588ef07835b918e83.jpg?width=3047&amp;height=2098" alt="髪をほどいて">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/313677" class="thumbnail" target="_blank">
                            <div class="title">
                                ”如果你愿意 一层一层 一层的剥开我的心”
                                </div>
                            <div class="author">
                                darling安老师
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/19/83203935219c3337ae8a5d135cbb7840.jpg?width=4352&amp;height=2448" alt="”如果你愿意 一层一层 一层的剥开我的心”">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/312745" class="thumbnail" target="_blank">
                            <div class="title">
                                夜
                                </div>
                            <div class="author">
                                拍照的古德卡特
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/14/7e3b90518530316e9fa18ca29eaad272.jpg?width=5000&amp;height=3739" alt="夜">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/312375" class="thumbnail" target="_blank">
                            <div class="title">
                                Beneath the silver moon
                                </div>
                            <div class="author">
                                梦境记录册
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/12/4b7bfc19904d3edbbcf51f14955ebbf1.jpg?width=2500&amp;height=3500" alt="Beneath the silver moon">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/310060" class="thumbnail" target="_blank">
                            <div class="title">
                                GALS
                                </div>
                            <div class="author">
                                鲁子烨
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1810/30/cb4d6bd7dc943bddb99cf789c5f52415.jpg?width=1346&amp;height=1683" alt="GALS">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/309064" class="thumbnail" target="_blank">
                            <div class="title">
                                葵
                                </div>
                            <div class="author">
                                Lara_禗蕴
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1811/18/af48d6413b2330bf8facffbddf82212c.jpg?width=3000&amp;height=2003" alt="葵">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/306635" class="thumbnail" target="_blank">
                            <div class="title">
                                 余
                                </div>
                            <div class="author">
                                拍照的古德卡特
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1810/10/f7235a3d74553808a8e91cfacd15f436.jpg?width=6122&amp;height=3808" alt=" 余">
                        </a>
                    </div>
    
                                <div class="grid-item work-thumbnail">
                        <a href="http://www.cnu.cc/works/306354" class="thumbnail" target="_blank">
                            <div class="title">
                                等待時光
                                </div>
                            <div class="author">
                                天天樂事
    
                            </div>
                                                                            <img src="http://img.cnu.cc/uploads/images/flow/1810/09/990aad36822d31529d54f9e4f0662bb3.jpg?width=920&amp;height=613" alt="等待時光">
                        </a>
                    </div>
    
                        
            </div>
    
                </form>
    
            <div class="pager_box">
                
                    <ul class="pagination">
    			<li class="disabled"><span>&laquo;</span></li><li class="active"><span>1</span></li><li><a href="http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E5%83%8F?page=2">2</a></li><li><a href="http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E5%83%8F?page=2" rel="next">&raquo;</a></li>	</ul>
    
                        </div>
    
    
        </div>
        <!--
            <div class="view-mask"></div>
            <div class="view">
                <div class="view-header">
                    <span class="title">图片标题1</span>
    
                    <div class="right">
                        <span class="icon-a share"></span>
                        <span class="vote"><span class="icon-a"></span><span>投一票</span></span>
                        <span class="icon-a tip-l"></span>
                        <span class="icon-a tip-r"></span>
                        <div class="float-l">
                            <span class="icon-b close"></span>
                            <span class="icon-b big"></span>
                        </div>
                    </div>
                </div>
                <div class="view-box">
    
                    <div class="multi" ></div>
    
                </div>
    
                <div  class="view-list">
                    <ul></ul>
                </div>
            </div>-->
        
    
    
    
    
    
      
        <div class="pageFooter">
            <span>@ CNU视觉联盟（www.cnu.cc）</span><span><a target="_blank" href="http://www.miitbeian.gov.cn/" style="color:#666666">粤ICP备10023979号-3</a></span>
    
      </div>
      </body>
      <!--
        <script src="http://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.3/jquery.js"></script>
        <script src="http://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.5/js/bootstrap.js"></script>
        <script src="http://cdnjs.cloudflare.com/ajax/libs/moment.js/2.8.3/moment.js"></script>
    -->
      <script src="http://img.cnu.cc/assets/scripts/lib/jquery.js"></script>
      <script src="http://img.cnu.cc/assets/scripts/lib/bootstrap.js"></script>
      <script src="http://img.cnu.cc/assets/scripts/lib/moment.js"></script>
        <script src="http://img.cnu.cc/assets/scripts/jquery.pjax.js"></script>
        <script src="http://img.cnu.cc/assets/scripts/jquery.scrollUp.js"></script>
        <script src="http://img.cnu.cc/assets/scripts/nprogress.js"></script>
        <script src="http://img.cnu.cc/assets/scripts/main.js"></script>
    
                <script>
                var category = "人像";
                if(category=="0"){
                    $(".menu .all span").addClass("badge");
                }else{
                    $(".menu .group span").each(function(){
                        if($(this).text()==category){
                            $(this).addClass("badge");
                            return;
                        }
                    });
                }
            </script>
            <script type="text/javascript" src="http://img.cnu.cc/assets/scripts/user_index.js"></script>
            <script type="text/javascript" src="http://img.cnu.cc/assets/scripts/lib/unslider.min.js"></script>
            <script type="text/javascript" src="http://img.cnu.cc/assets/masonry/masonry.pkgd.min.js"></script>
            <script type="text/javascript" src="http://img.cnu.cc/assets/scripts/imagesLoaded.min.js"></script>
            <script >
                $("#navbar li")[2].className = "active";
    
                var cdn = "http://img.cnu.cc/uploads/images/";
                var works=new Array();
                var workIDs=new Array();
    
    
                $('.banner').unslider({
                    speed: 500,               //  The speed to animate each slide (in milliseconds)
                    delay: 5000,              //  The delay between slide animations (in milliseconds)
                    complete: function() {},  //  A function that gets called after every slide animation
                    keys: true,               //  Enable keyboard (left, right) arrow shortcuts
                    dots: true,               //  Display dot navigation
                    fluid: false,              //  Support responsive design. May break non-responsive designs
                    arrows:true
                }).hover(function(){
                    $(this).find(".arrow").show();
                },function(){
                    $(this).find(".arrow").hide();
                });
    
    
    
                $(document).ready(function() {
    
    
                    var $grid = $('.grid').imagesLoaded(function () {
    
                        // init Masonry after all images have loaded
                        $grid.masonry({
                            itemSelector: '.grid-item'
                        });
    
                    });
    
                });
    
    
                Array.prototype.contains = function(item){
                    return RegExp("\\b"+item+"\\b").test(this);
                };
    
    
    
    
            </script>
    
            <script type="text/javascript" src="http://img.cnu.cc/assets/scripts/public.js"></script>
    
          
    <script>
    
        $("#searchForm").submit(function(){
            var input = $(this).find("#keyword");
            var keyword =input.val();
            if($.trim(keyword)==""){
                return false;
            }
            $(this).attr("action",$(this).attr("action")+"/"+keyword);
    
        });
        </script>
    
    
    
    
    </html>
    
    

上面这个网址，找到的其中主体部分的一个图片的 HTML 格式如下，其他图片的格式都是一样的：

```
<div class="grid-item work-thumbnail">
                    <a href="http://www.cnu.cc/works/336905" class="thumbnail" target="_blank">
                        <div class="title">
                            女孩与花
                            </div>
                        <div class="author">
                            Serendipity_zx

                        </div>
```

### - 方法

获取所有的图片的方法是 requests 库里面的 ```findall```

### - 建立正则表达式

#### 1. 首先找到对应部分

上述的 HTML 里面，a href 后面的 ```http://www.cnu.cc/works/336905``` 是图片的网址部分；<div class="title"> 后面的 ```女孩与花``` 是图片的名字部分。

这两个部分是要提取的部分。

#### 2. 使用元字符替换

替换后的内容为：

```
<div class="grid-item work-thumbnail">
                    <a href=".*?" class="thumbnail" target="_blank">
                        <div class="title">
                            .*?
                            </div>
                        <div class="author">
                            Serendipity_zx

                        </div>
```

#### 3. 避免一些问题

两个主要部分中间的内容可能会有所不同，为了避免其中的影响，把中间的内容也进行正则表达，替换后如下：

```
<div class="grid-item work-thumbnail">
                    <a href=".*?" .*?class="title">
                            .*?
                            </div>
                        <div class="author">
                            Serendipity_zx

                        </div>
```

### - requests 结合正则

代码如下：


```python
pattern = re.compile(r'<a href="(.*?)".*?class="title">(.*?)</div>', re.S)
# 第二个 .*? 前面不能有 空格，如果有空格，就出现很多奇奇怪怪的内容，数据很乱。
results = re.findall(pattern, content.text)
print(results)
```

    [('http://www.cnu.cc/selectedPage', '\n                            女孩与花\n                            '), ('http://www.cnu.cc/works/335746', '\n                            "摄影里的民谣爱情故事”\n                            '), ('http://www.cnu.cc/works/335224', '\n                            不渝\n                            '), ('http://www.cnu.cc/works/334692', '\n                            妖怪也喜欢小朋友啊\n                            '), ('http://www.cnu.cc/works/333806', '\n                            一颗草莓。\n                            '), ('http://www.cnu.cc/works/333607', '\n                            住在村里的人\n                            '), ('http://www.cnu.cc/works/332291', '\n                            #On the STREET of daylight. \n                            '), ('http://www.cnu.cc/works/332289', '\n                            《流浪又自由》\n                            '), ('http://www.cnu.cc/works/332090', '\n                            黑白肖像\n                            '), ('http://www.cnu.cc/works/331443', '\n                            FRONT风尚周刊 X 吴莫愁\n                            '), ('http://www.cnu.cc/works/330503', '\n                            安安\n                            '), ('http://www.cnu.cc/works/329928', '\n                            四十七\n                            '), ('http://www.cnu.cc/works/329472', '\n                            心裡 \n                            '), ('http://www.cnu.cc/works/329030', '\n                            阿筱与花童\n                            '), ('http://www.cnu.cc/works/323707', '\n                            章若楠\n                            '), ('http://www.cnu.cc/works/323792', '\n                            遇见了冬天\n                            '), ('http://www.cnu.cc/works/323484', '\n                            『陌生如你』\n                            '), ('http://www.cnu.cc/works/323474', '\n                            绛\n                            '), ('http://www.cnu.cc/works/323371', '\n                            "她 在山林里 在心房里“\n                            '), ('http://www.cnu.cc/works/323301', '\n                            “爱恋是道无解的题”\n                            '), ('http://www.cnu.cc/works/322732', '\n                            预售等待\n                            '), ('http://www.cnu.cc/works/319565', '\n                            Diving in Love\n                            '), ('http://www.cnu.cc/works/318906', '\n                            ”心内的一场雨”\n                            '), ('http://www.cnu.cc/works/318419', '\n                            Xion\n                            '), ('http://www.cnu.cc/works/317994', '\n                            阴天\n                            '), ('http://www.cnu.cc/works/318250', '\n                            我说我想等一个命中注定之人出现，然后刻骨铭心爱一场，不计得失，不计结果\n                            '), ('http://www.cnu.cc/works/316962', '\n                            "那些女孩的样子”\n                            '), ('http://www.cnu.cc/works/316966', '\n                            The Enchanted\n                            '), ('http://www.cnu.cc/works/315937', '\n                            "又是一年入冬时！”\n                            '), ('http://www.cnu.cc/works/315850', '\n                            往朗目山顶开\n                            '), ('http://www.cnu.cc/works/314018', '\n                            "是的，你又初恋了！”\n                            '), ('http://www.cnu.cc/works/313821', '\n                            ”我想我会努力忘了你的模样， 但依然忘不了你的眼睛，那曾经最最深爱着的爱笑的眼睛  ！”\n                            '), ('http://www.cnu.cc/works/313619', '\n                            髪をほどいて\n                            '), ('http://www.cnu.cc/works/313677', '\n                            ”如果你愿意 一层一层 一层的剥开我的心”\n                            '), ('http://www.cnu.cc/works/312745', '\n                            夜\n                            '), ('http://www.cnu.cc/works/312375', '\n                            Beneath the silver moon\n                            '), ('http://www.cnu.cc/works/310060', '\n                            GALS\n                            '), ('http://www.cnu.cc/works/309064', '\n                            葵\n                            '), ('http://www.cnu.cc/works/306635', '\n                             余\n                            '), ('http://www.cnu.cc/works/306354', '\n                            等待時光\n                            '), ('http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E5%83%8F?page=2', '图片标题1</span>\n\n                <div class="right">\n                    <span class="icon-a share"></span>\n                    <span class="vote"><span class="icon-a"></span><span>投一票</span></span>\n                    <span class="icon-a tip-l"></span>\n                    <span class="icon-a tip-r"></span>\n                    <div class="float-l">\n                        <span class="icon-b close"></span>\n                        <span class="icon-b big"></span>\n                    ')]
    

### - 数据格式整理

【目的】：去掉中间的空格、换行符“\n”  
【分析】：最后的数据是列表里面的元组
【方法】：列表推导式整理

如下：


```python
for result in results:
    url, name = result
    print(url, re.sub('\s', '', name))
    # 解释：由于 name 里面有换行符、空格，这些是无意义的字符，可以使用 \s 的方法全部替换，
    # 这里替换的内容是 空，所以就去掉了。
#     print(url, name)
```

    http://www.cnu.cc/selectedPage 女孩与花
    http://www.cnu.cc/works/335746 "摄影里的民谣爱情故事”
    http://www.cnu.cc/works/335224 不渝
    http://www.cnu.cc/works/334692 妖怪也喜欢小朋友啊
    http://www.cnu.cc/works/333806 一颗草莓。
    http://www.cnu.cc/works/333607 住在村里的人
    http://www.cnu.cc/works/332291 #OntheSTREETofdaylight.
    http://www.cnu.cc/works/332289 《流浪又自由》
    http://www.cnu.cc/works/332090 黑白肖像
    http://www.cnu.cc/works/331443 FRONT风尚周刊X吴莫愁
    http://www.cnu.cc/works/330503 安安
    http://www.cnu.cc/works/329928 四十七
    http://www.cnu.cc/works/329472 心裡
    http://www.cnu.cc/works/329030 阿筱与花童
    http://www.cnu.cc/works/323707 章若楠
    http://www.cnu.cc/works/323792 遇见了冬天
    http://www.cnu.cc/works/323484 『陌生如你』
    http://www.cnu.cc/works/323474 绛
    http://www.cnu.cc/works/323371 "她在山林里在心房里“
    http://www.cnu.cc/works/323301 “爱恋是道无解的题”
    http://www.cnu.cc/works/322732 预售等待
    http://www.cnu.cc/works/319565 DivinginLove
    http://www.cnu.cc/works/318906 ”心内的一场雨”
    http://www.cnu.cc/works/318419 Xion
    http://www.cnu.cc/works/317994 阴天
    http://www.cnu.cc/works/318250 我说我想等一个命中注定之人出现，然后刻骨铭心爱一场，不计得失，不计结果
    http://www.cnu.cc/works/316962 "那些女孩的样子”
    http://www.cnu.cc/works/316966 TheEnchanted
    http://www.cnu.cc/works/315937 "又是一年入冬时！”
    http://www.cnu.cc/works/315850 往朗目山顶开
    http://www.cnu.cc/works/314018 "是的，你又初恋了！”
    http://www.cnu.cc/works/313821 ”我想我会努力忘了你的模样，但依然忘不了你的眼睛，那曾经最最深爱着的爱笑的眼睛！”
    http://www.cnu.cc/works/313619 髪をほどいて
    http://www.cnu.cc/works/313677 ”如果你愿意一层一层一层的剥开我的心”
    http://www.cnu.cc/works/312745 夜
    http://www.cnu.cc/works/312375 Beneaththesilvermoon
    http://www.cnu.cc/works/310060 GALS
    http://www.cnu.cc/works/309064 葵
    http://www.cnu.cc/works/306635 余
    http://www.cnu.cc/works/306354 等待時光
    http://www.cnu.cc/discoveryPage/hot-%E4%BA%BA%E5%83%8F?page=2 图片标题1</span><divclass="right"><spanclass="icon-ashare"></span><spanclass="vote"><spanclass="icon-a"></span><span>投一票</span></span><spanclass="icon-atip-l"></span><spanclass="icon-atip-r"></span><divclass="float-l"><spanclass="icon-bclose"></span><spanclass="icon-bbig"></span>
    

【分析】  
最后一个是不想要的数据，应该是由于正则的语句没有匹配好，导致出现了这个内容，如何规避可能是一件效率上不好的事情（调整所有的内容，只是为了去掉一个内容，有些吃力不讨好。但是用人工的方式手动剔除，又显得很土。）

## 总结

实现了目的，但是编写正则加比较麻烦了。

难道有比较简单的方法？看看下一章到底是什么了。下一章的内容是 beautifulSoup，难道是一个更加整合的库？

---
注：  
个人微信公众号：codeAndWrite

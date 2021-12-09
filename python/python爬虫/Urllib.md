# 一、Urllib

## 1、什么是互联网爬虫？  

* 解释1：通过一个程序，根据Url(http://www.taobao.com)进行爬取网页，获取有用信息
* 解释2：使用程序模拟浏览器，去向服务器发送请求，获取响应信息  

## 2、爬虫核心

1. 爬取网页：爬取整个网页 包含了网页中所有得内容
2. 解析数据：将网页中你得到的数据 进行解析
3. 难点：爬虫和反爬虫之间的博弈  

## 3、爬虫的用途？  

* 数据分析/人工数据集

* 社交软件冷启动
* 舆情监控
* 竞争对手监控  

## 4、爬虫分类

1. 通用爬虫：
   实例
   	百度、360、google、sougou等搜索引擎‐‐‐伯乐在线
   功能
   	访问网页‐>抓取数据‐>数据存储‐>数据处理‐>提供检索服务
   robots协议
   	一个约定俗成的协议，添加robots.txt文件，来说明本网站哪些内容不可以被抓取，起不到限制作用
   	自己写的爬虫无需遵守
   网站排名(SEO)

   	1. 根据pagerank算法值进行排名（参考个网站流量、点击率等指标）
   	2. 百度竞价排名

   缺点

   1. 抓取的数据大多是无用的
   2. 不能根据用户的需求来精准获取数据  

2. 聚焦爬虫

   功能

   ​	根据需求，实现爬虫程序，抓取需要的数据

   设计思路

   ​	1.确定要爬取的url

   ​		如何获取Url

   ​	2.模拟浏览器通过http协议访问url，获取服务器返回的html代码

   ​		如何访问

   ​	3.解析html字符串（根据一定规则提取需要的数据）

   ​		如何解析  

## 5、反爬手段

1.User‐Agent：  

​	User Agent中文名为用户代理，简称 UA，它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版
本、CPU 类型、浏览器及版本、浏览器渲染引擎、浏览器语言、浏览器插件等。
2.代理IP
​	西次代理
​	快代理
​	什么是高匿名、匿名和透明代理？它们有什么区别？
​		1.使用透明代理，对方服务器可以知道你使用了代理，并且也知道你的真实IP。
​		2.使用匿名代理，对方服务器可以知道你使用了代理，但不知道你的真实IP。
​		3.使用高匿名代理，对方服务器不知道你使用了代理，更不知道你的真实IP。
3.验证码访问
​	打码平台
​		云打码平台
​		超级🦅
4.动态加载网页 网站返回的是js数据 并不是网页的真实数据
​	selenium驱动真实的浏览器发送请求
5.数据加密
​	分析js代码  

## 6、请求对象的定制

```
urllib.request.urlopen() 模拟浏览器向服务器发送请求
response 服务器返回的数据
	response的数据类型是HttpResponse
		字节‐‐>字符串
			解码decode
    	字符串‐‐>字节
			编码encode
		read() 字节形式读取二进制 扩展：rede(5)返回前几个字节
		readline() 读取一行
		readlines() 一行一行读取 直至结束
		getcode() 获取状态码
		geturl() 获取url
		getheaders() 获取headers
	urllib.request.urlretrieve(url,格式) 下载文件
		请求网页
		请求图片
		请求视频
```

## 7、请求对象的定制

UA介绍：User Agent中文名为用户代理，简称 UA，它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版本、CPU 类型、浏览器及版本。浏览器内核、浏览器渲染引擎、浏览器语言、浏览器插件等
语法：request = urllib.request.Request()  

## 8、编解码  

1. get请求方式：urllib.parse.quote（）

```python
eg：
import urllib.request
import urllib.parse
url = 'https://www.baidu.com/s?wd='
headers = {
'User‐Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like
Gecko) Chrome/74.0.3729.169 Safari/537.36'
} u
rl = url + urllib.parse.quote('小野')
request = urllib.request.Request(url=url,headers=headers)
response = urllib.request.urlopen(request)
print(response.read().decode('utf‐8'))
```

2. get请求方式：urllib.parse.urlencode（）  

```python
eg:
import urllib.request
import urllib.parse
url = 'http://www.baidu.com/s?'
data = {
'name':'小刚',
'sex':'男',
} d
ata = urllib.parse.urlencode(data)
url = url + data
print(url)
headers = {
'User‐Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like
Gecko) Chrome/74.0.3729.169 Safari/537.36'
} r
equest = urllib.request.Request(url=url,headers=headers)
response = urllib.request.urlopen(request)
print(response.read().decode('utf‐8'))
```

3. post请求方式  

```python
eg:百度翻译
    import urllib.request
    import urllib.parse
    url = 'https://fanyi.baidu.com/sug'
    headers = {
        'user‐agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like
        Gecko) Chrome/74.0.3729.169 Safari/537.36'
    } 
    keyword = input('请输入您要查询的单词')
    data = {
        'kw':keyword
    } 
    data = urllib.parse.urlencode(data).encode('utf‐8')
    request = urllib.request.Request(url=url,headers=headers,data=data)
    response = urllib.request.urlopen(request)
    print(response.read().decode('utf‐8'))
```


总结：post和get区别？

```python
1：get请求方式的参数必须编码，参数是拼接到url后面，编码之后不需要调用encode方法
2：post请求方式的参数必须编码，参数是放在请求对象定制的方法中，编码之后需要调用encode方法
```


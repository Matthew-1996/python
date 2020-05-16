# beautifulsoup
## beautifulsoup：基础
beautifulsoup可以帮助我们匹配更加方便（替代正则表达式）  
中文官网：https://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/ ，具体用法可查询官网 
简易版本：https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#  
### 安装beautifulsoup4  
官网下载包或者终端指令，mac的终端指令可以是pip3 install beautfulsoup4(安装pip3情况下用其安装)，或者用conda install  
### 导入beautifulsoup库并使用
BeautifulSoup 第一个参数应该是要被解析的字符串、html、xml等,第二个参数用来标识怎样解析文档.如果第二个参数为空,那么Beautiful Soup根据当前系统安装的库自动选择解析器,解析器的优先数序: lxml, html5lib  
**不同解析器的区别介绍**
![加载失败](https://github.com/Matthew-1996/python/blob/master/%E7%88%AC%E8%99%AB/%E4%B8%8D%E5%90%8C%E8%A7%A3%E6%9E%90%E5%99%A8%E5%AF%B9%E6%AF%94.png)
beautifulsoup的用法和直接用正则表达式大致类似，这边html就采用beautifulsoup官网提供的例子
```html
html_doc = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""
```
我们先了解一些简单的操作
```python
#为了模拟一个完整的过程，假设我们上面的html来自一个url
from bs4 import BeautifulSoup
from urllib import urlopen

#上面的html没有中文，所以不recode('utf-8')
html = urlopen('链接').read()
#首先我们要把html放入这个soup中
soup = BeautifulSoup(html，‘lxml’)
#一般会使用lxml解析器，但注意要安装了对应的c语言库
#这样beautifulsoup已经完成了解析，我们可以用以下的方式检索对应对tag部分

soup.title
# <title>The Dormouse's story</title>
#并且可以继续检索title结构下的tag

soup.title.name
# u'title'

soup.title.string
# u'The Dormouse's story'

soup.title.parent.name
# u'head'

soup.p
# <p class="title"><b>The Dormouse's story</b></p>

soup.p['class']
# u'title'

soup.a
# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
#假设我们想要其中的链接<a>，因为链接有多个。soup.a只会返回第一个，我们可以用find_all()。 仍以上面的html为例

soup.find_all('a')
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

#find()还可以用来实现字符串匹配的操作
soup.find(id="link3")
# <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>

#但是以上返回的结果都是包含tag的<title>内容</title>这样一种形式，如果我们只需要其中的链接，我们可以把<a></a>中的href当作<a>的一个属性，用['href']去索引  
all_href = soup.find_all('a')
all_href = [l['href'] for l in all_href]

#[http://example.com/elsie,
# http://example.com/lacie,
# http://example.com/tillie]
```
## beautfulsoup：CSS
## beautfulsoup：正则表达式
## 小练习

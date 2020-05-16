# beautifulsoup
## beautifulsoup：基础
beautifulsoup可以帮助我们匹配更加方便（替代正则表达式）  
中文官网：https://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/ ，具体用法可查询官网 
简易版本：https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/#  
### 安装beautifulsoup4  
官网下载包或者终端指令，mac的终端指令可以是pip3 install beautfulsoup4(安装pip3情况下用其安装)，或者用conda install  
### 导入beautifulsoup库并使用
BeautifulSoup 第一个参数应该是要被解析的html或xml等,第二个参数用来标识怎样解析文档.如果第二个参数为空,那么Beautiful Soup根据当前系统安装的库自动选择解析器,解析器的优先数序: lxml, html5lib  

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
soup = BeautifulSoup(html)
```
## beautfulsoup：CSS
## beautfulsoup：正则表达式
## 小练习

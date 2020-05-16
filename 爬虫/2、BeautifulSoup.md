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
### css简介
css是html的好搭档，没有css的html就是一份文档形式的内容，用css就可以装饰html。  
css的详细规则：https://www.w3schools.com/css/  
在用beautifulsoup的时候，由于css和html是相关的，我们也可以用css的class来选择内容。  
### css的class
在用css装饰html的时候，他会给每一个网页部件取名。而同一种类型的部件，名字*都可以*一样。我们就可以利用这个特性来寻找。  
举一个通俗一些的例子，在一个网页里面，我们可能会把所有段落的小标题/或是所有日期/等等，用一样的字体、颜色、背景颜色等等去装饰。这就成为了这些内容的一个共性。那么在css里面，他们的class可能取名就是一样的（为同一种样式取同一个名字）。所以beautifulsoup也可以利用css的class来检索到这些内容。  
css代码*可能*会放在html的<head>中，用<style>样式信息</style>表示。  
  
```html
<head>
	  ...
	  <style>
	  .jan {
		  background-color: yellow;
	  }
	  ...
	  .month {
		  color: red;
	  }
	  </style>
</head>

<body>
...
<ul>
	  <li class="month">一月</li>
	  <ul class="jan">
		  <li>一月一号</li>
		  <li>一月二号</li>
		  <li>一月三号</li>
	  </ul>
	  ...
</ul>
</body>
```

比如上面一段html代码，它的<head>里面就有class的格式信息（jan格式是黄色背景，month格式是红色字体）
下面的内容就可以看到一月这种月份用了month格式，一月几号这些所有的都用了jan格式。那我们就可以用class='jan'去找到下面所有的一月几号了。 
下面示例以下找到所有一月几号（jan）
	
```python
#就跳过前面打开url，导入beautifulsoup等操作了
jan = soup.find('ul', {'class': 'jan'})
#上面的html没有写全，但是我们可以看到上面的ul（列表）是很多的。有月列表，每个月下面还有列表。那假设我们只需要一月的那个列表，它刚好也有一个单独的class。那在soup.find('ul')的基础上，我们可以在后面加一个字典的形式{'class': 'jan'}，表示class也是要jan的。
#另外可能会奇怪，为什么不直接find('ul class="jan"')呢？那是因为现实中class（或者我们要以别的为依据）未必跟在ul后面。
#刚才会返回的结果是所有<ul class="jan">里面的内容，那事实上我们只要其中<li>的内容，所以继续使用
jan_li = jan.find_all('li')
for l in jan_li:
    print(l.get_text())
    
#"""
#一月一号
#一月二号
#一月三号
#"""
```
## beautifulsoup：正则表达式
beautifulsoup加正则表达式就可以做到更多  
比如找图片的时候，假如我们要的是jpg，正则表达式应该是这样 r‘.\*?\\.jpg’  
然后图片一般都位于这样的tag中 \<img src="https://morvanzhou.github.io/static/img/course_cover/tf.jpg"> 
我们可以这样来实现  
```python
from bs4 import BeautifulSoup
from urllib import urlopen
import re

html = urlopen('wangzhi').read().recode('utf-8')
soup = BeautifulSoup(html,'lxml')
img = soup.find_all('img', {'src': re.compile('.*?\.jpg')})
#这里要注意的是，虽然正则表达式是r‘.*?\.jpg’，但是这是用在re.search等一系列re下面的，不能直接用在beautifulsoup里面。所以我们用了re.compile把这个正则表达式合成

print(l['src'] for l in img)
```
又或者，我们要找的链接可能有一些共有的特征，例如是 https://morvan.* 

## 小练习

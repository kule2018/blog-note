[toc]

# scrapy 自学入门demo分享

> 本文基于python 3.7.0，win10平台； 2018-08

> 完整项目代码：[https://github.com/NameHewei/python-scrapy](https://github.com/NameHewei/python-scrapy)

# 安装
## 安装python 
1. 官网下载 https://www.python.org/
2. 注意环境变量是否配置成功

## 安装scrapy
> 为了安装顺利，请备好梯子

- pip install Scrapy

**安装过程中注意以下报错信息：**

**Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools"** 

解决办法：
1. https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted 下载对应版本twisted的whl文件
2. cp：表示python版本
3. amd64：表示64位
4. 下载后在文件目录下执行： pip install Twisted-18.7.0-cp37-cp37m-win_amd64.whl(文件名)

# 创建项目

- 创建scrapy：scrapy startproject youName
- 创建spider：scrapy genspider <name> <domain> // 在项目跟目录执行

## 配置settings.py文件
1. 如果抓取的内容包含中文可配置：FEED_EXPORT_ENCODING = 'utf-8'
2. 报错误信息403：把USER_AGENT加上（可在网站请求头信息中查看）

## 编写items.py文件
```python
import scrapy

class NovelItem(scrapy.Item):
    title = scrapy.Field()
    content = scrapy.Field()
```
这些即你需要保存的字段名

## 编写spider
```python
import scrapy

# 引入自定义的items
from myTest.items import NovelItem

# # 继承scrapy.Spider
class NovelSpider(scrapy.Spider):
    # 爬虫名
    name = 'novel_spider'
    # 允许的域名
    allowed_domains = ['http://www.danmeila.com']
    # 入口url 扔到调度器里面去
    start_urls = ['http://www.danmeila.com/chapter/20180406/29649.html']


    def parse(self, response):
        movieList = response.xpath('//*[@id="container"]/div[3]/div[2]/div[2]/div/div/ul/li')
        novelContent = NovelItem()
        for item in movieList:
            u = 'http://www.danmeila.com' + item.xpath('.//a/@href').extract_first()
            
            yield scrapy.Request(u, callback= self.content_a, meta= { 'nc': novelContent }, dont_filter = True)
            # 放到管道里否则 pipeline获取不到
            # 如果你发现拿到的内容一直为空，注意是否被过滤了，即dont_filter没有设置


    def content_a(self, response):
        novelContent = response.meta['nc']
        novelContent['title'] = response.xpath('//*[@id="J_article"]/div[1]/h1/text()').extract_first()

        yield novelContent
```

注意以下几点：
  - 采用xpath编写，在浏览器中可以直接查看元素，找到要爬取内容的标签，右键选copy xpath
  - extract_first()的使用；text() 获取文本；@属性名  获取属性值
  - 在父节点下使用xpath路径前要加./
  - 去除换行空格用 xpath('normalize-space('.//div/text()')')

## 执行
导出为json： scrapy crawl your-spider-name -o test.json

如果出现报错信息：
- async语法错误，把用到该名称作为参数的文件全部作修改 把这个参数名改为其它即可
- 报错 No module named 'win32api'： 到https://pypi.org/project/pypiwin32/#files（下载文件pypiwin32-223-py3-none-any.whl 执行 pip install pypiwin32-223-py3-none-any.whl ）

> 若有疑问或错误，请留言，谢谢！[Github blog issues](https://github.com/NameHewei/blog/issues)
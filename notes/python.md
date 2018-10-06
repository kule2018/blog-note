[toc]
# scrapy
## python 安装scrapy
```
pip install Scrapy
```
- 安装scrapy报错：Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools"
  1. https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted 下载对应版本twisted的whl文件
  2. cp:python版本
  3. amd64：64位
  4. 下载后在文件目录下执行： pip install Twisted-18.7.0-cp37-cp37m-win_amd64.whl(文件名)

 - scrapy startproject youName  创建项目
 - scrapy genspider <name> <domain> 创建spider(在项目跟目录执行)
 - scrapy crawl spider名称
    - 第一次执行会报错async语法错误 把用到改名称作为参数的文件全部作修改 把这个参数名改为其它即可
    - 报错 No module named 'win32api'： https://pypi.org/project/pypiwin32/#files（下载文件pypiwin32-223-py3-none-any.whl 执行 pip install pypiwin32-223-py3-none-any.whl ）

- [scrapy.spidermiddlewares.offsite] DEBUG: Filtered offsite request to: 表示request的地址和allow_domain地址冲突，被过滤。
  - 设置 yield Request(url, callback=self.parse_item, ***dont_filter=True***)


导出为json
scrapy crawl spider名称 -o test.json

注意配置FEED_EXPORT_ENCODING = 'utf-8' 否则中文会被转码

报403时注意把USER_AGENT加上

text() 获取文本
@属性名  获取属性值

在父节点下又使用xpath路径前要加./

去除换行空格用 xpath('normalize-space('.//div/text()')')
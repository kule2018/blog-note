[toc]


- Ctrl+Z，再按回车 退出命令行
- python -m pip install --upgrade pip  升级pip
- 添加新文件，将不会触发自动重新加载，这时你得自己手动重启服务器
- 监听所有服务器的公开IP（这你运行 Vagrant 或想要向网络上的其它电脑展示你的成果时很有用） python manage.py runserver 0:8000; 0 是 0.0.0.0 的简写

# Django

## 安装
> 参考官网
- 注意与python版本对应
- 使用pip安装(时间慢) 

## 项目(包含应用与配置)
- 创建 django-admin startproject mysite(名称)
- 创建应用 python manage.py startapp appname


# scrapy
- 报错 Spider must return Request, BaseItem, dict or None, 表示没有返回正确yield 后面的值
## 安装
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
 - scrapy crawl(爬) spider名称
    - 第一次执行会报错async语法错误 把用到该名称作为参数的文件全部作修改 把这个参数名改为其它即可
    - 报错 No module named 'win32api'： https://pypi.org/project/pypiwin32/#files（下载文件pypiwin32-223-py3-none-any.whl 执行 pip install pypiwin32-223-py3-none-any.whl ）

- [scrapy.spidermiddlewares.offsite] DEBUG: Filtered offsite request to: 表示request的地址和allow_domain地址冲突，被过滤。

- 设置 yield Request(url, callback=self.parse_item, ***dont_filter=True***)


导出为json
scrapy crawl spider名称 -o test.json

注意配置FEED_EXPORT_ENCODING = 'utf-8' 否则中文会被转码

报403时注意把USER_AGENT加上

text() 获取文本
@属性名  获取属性值

在父节点下使用xpath路径前要加./

去除换行空格用 xpath('normalize-space('.//div/text()')')

css:
- 获取内容
css('::text')

- 返回属性值
response.css('.logo a::attr(href)').extract() 返回的值数组

- 去掉空格
python字符串对象的 strip() 方法

- 去掉换行
python字符串对象的 .replace('\n', '')
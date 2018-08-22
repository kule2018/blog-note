[toc]
# python 安装scrapy
 Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools"

 - scrapy startproject youName  创建项目
 - scrapy genspider [options] <name> <domain> 创建spider
 - scrapy crawl spider名称  执行爬虫

 导出为json
 scrapy crawl spider名称 -o test.json

注意配置FEED_EXPORT_ENCODING = 'utf-8' 否则中文会被转码

报403时注意把USER_AGENT加上

text() 获取文本
@属性名  获取属性值

在父节点下又使用xpath路径前要加./

去除换行空格用 xpath('normalize-space('.//div/text()')')
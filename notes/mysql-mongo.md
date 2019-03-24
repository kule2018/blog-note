比特位Bit(b), 字节Byte(B), 千字节Kilobytes(KB), 兆字节 Megabytes(MB), 吉字节Gigabyte(GB), 太字节terabyte(TB)

1字节 = 8位

2进制表示： 1kb = 1024B

utf-8(utf-8就是Unicode最重要的实现方式之一)中

一个英文字母占一个字节

一个中文字母占三个字节

# Mongo
## 报错信息
- 发生系统错误 5。 ：请使用管理员权限

## 安装mongoDB
> 如下方法写于（版本v3.4.6）

https://docs.mongodb.com/manual/tutorial/install-mongodb-enterprise-on-windows/

1. 官网下载安装[https://www.mongodb.com/](https://www.mongodb.com/)

2. 将安装的bin目录（默认一般在C:\Program Files\MongoDB\Server\3.4）添加到环境变量即可在任意目录打开命令行执行mongo命令

3. 安装为Windows服务，使用命令：mongod --config F:\mongodb\mongo.config --install --serviceName "any name" 当前版本已经自带了MongoDB服务

4. 启动服务  net start/stop name（管理员权限）    删除用  sc delete name 


启动mongod服务：  
bin目录下执行'mongod'即可（当已经创建了将MongoDB服务器作为Windows服务运行时就可用上面的命令:net...）

- 进入目录bin中然后执行mongo.exe||mongo (在powershell中用 **.\mongo.exe**)
- 然后进入mongodb shell（是mongodb自带的交互式JavaScript shell）用来是对mongodb 的后台进行操作和管理。  
- 当你进入mongodb后台后，默认链接到test文档（数据库）


## 操作
---
创建数据库：  
use databaseName(如果数据库不存在就创建，存在就切换到指定数据库)。  
删除数据库  
	db.dropDatabase();//先进入数据库
	
---
show dbs  查看所有数据库

---
db 显示当前数据库名

---
删除数据库：（先进入数据库）    
db.dropDatabase()

---
查看数据库中有哪些表：（先进数据库）  
show collections（集合，收集）

---
创建表  
db.createCollection(表名)||或者直接添加数据时会自动创建表  
删除表  
db.表名.drop()//先进入数据库

---
添加数据：  
db(固定).任意名称.insert({键值对})||用数组[{}，{}]批量插入  

---
查看数据：  
db.表名.find()//查看所有数据
findOne(query, options, callback)  
options:fields(fields to include{a:1} or exclude{a:0} ) 

--- 
更改字段值//只修改搜到的第一个  
db.表名.update({"条件字段名":"字段值"},{$set:{"要修改的字段名":"修改后的字段值"}});

---
删除数据  
db.表名.remove({键值对})//当不加参数时就直接删除表中所有数据(name:’hew’||’name’:’hew’)

## node调用

有两种驱动 MongoDB Driver 和 Mongoose

- mongodb driver 参考 node-koa/graphql
- mongoose 参考 node-egg/

# MySQL

查看安装路径：在mysql command line client 中输入 show variables like "%char%"

执行mysql命令后面注意加分号

在powershell 下执行命令注意是否要加 ./ 当前目录



## 用installer msi 安装

下载 installer 带web的版本表示安装时需要联网

https://dev.mysql.com/downloads/installer/

MySQL Community Server 社区版本，开源免费，但不提供官方技术支持

MySQL Workbench（GUI TOOL）一款专为MySQL设计的ER/数据库建模工具

一直默认 只安装server

注意账号密码 mysql123456 port 3310

- 没有my.init文件，可以在C:\ProgramData\MySQL\MySQL Server 8.0中拷贝一份

- 报错
1. Client does not support authentication protocol requested by server; consider upgrading MySQL client
```
处理方式为 执行如下命令
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '对应用户的密码';
```


## zip 安装
- 将解压后的文件放到任意目录，可改名

- 将\bin 添加到环境变量中（this PC > properties > advanced system settings）

- bin的同级目录 创建my.ini文件 

```
[mysqld]

 # 设置mysql客户端默认字符集
default-character-set=utf8 
[mysqld]
#设置3306端口
port = 6767 
# 设置mysql的安装目录
basedir=C:\Program Files\mysql

# 设置mysql数据库的数据的存放目录

datadir=C:\Program Files\mysql\data

# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```
注意用 mysqld --console 查看错误

1. mysqld --romve  //删除mysql服务
2. mysqld --install //安装mysql服务 
3. mysqld --initialize //一定要初始化 
4. net start mysql




# navicat

下载 https://www.navicat.com.cn/products 
Navicat Premium

https://www.lanzous.com/b607627/ Navicat Premium 12注册机，提取密码：RCNJTECH

激活教程 https://www.jianshu.com/p/5f693b4c9468

## 使用

创建或修改表的时候，注意表中是否有数据

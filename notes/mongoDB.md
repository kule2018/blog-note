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

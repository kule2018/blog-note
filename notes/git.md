
[TOC]  

# github  
直接访问版本号前7位也是可以访问的。  

---
# git

> 状态

A：在本地新增的文件（服务器上没有）  
C：文件的一个新拷贝  
D：本地删除的文件（服务器上还在）  
M：文件的内容或mode被修改  
R：文件名被修改  
T：文件类型被修改  
U：文件没有被合并（你需要完成合并才能提交）  
X：未知状态  
搜索：man git diff-files。

---
>Linux或Mac系统使用LF作为行结束符

---
git config - -system   

git config - -global - -list 
//用户级别  

git config - -local  
//当前仓库  

由上往下，底层配置会覆盖顶层配置  
git config - -list  
//查看所有  

修改  
git config - -global user.name ‘其它’  

---
git clone 会默认将本地与远程分支进行追踪

---
当在merge时产生了冲突（branchname|Marging）  
执行git add filename|. ,git commit –m ‘message’,再次将工作区的更改提交到本地仓库-区，告诉Git 冲突已解决。

---
>分支

新建分支时会基于当前所在分支commit的内容新建。所以新建的分支会包含所有所基于的分支内容。

---
- git branch                    
  //显示所有分支（*表示当前所在分支）  
- git branch branchName         
  //创建新分支  
- git checkout –b branchName     
  //创建新分支并切换到该分支  
- git branch –d branchName       
  //删除分支  

>远程

- git remote add anyname url  定义了一个本地的anyname远程端，这个anyname远程端指向url所代表的远程端。当用git clone时默认的anyname为origin。 

- git push origin [localbranch | HEAD(就是当前活跃分支的游标)] : remotebranch (当远程和本地分支相同时可以简写：git push origin branchname)  

- 当远程没有branchname时就新建分支，确保本地已有branchname分支
- git push origin  :remotebranch  删除远程分支 ||   
- git push origin --delete remotebranch

- git pull origin remotebranch:localbranch  表示获取远程分支的更新与本地分支合并.
- git pull origin remotebranch  表示与当前本地分支合并;

  相当于 git fetch origin 和git merge origin/remotebranch

---

- 取消最近一次的commit： **git reset --soft HEAD^**
---

- 更新远程跟踪分支：**git fetch origin**,获取远程的所有分支，不然branch -a 查看不到新的远程分支

- git fetch origin master：只取回特定分支的更新

---
- git branch命令的 **-r** 选项，可以用来查看远程分支，**-a**选项查看所有分支

---
- 打tag 前请先commit； git tag -a v1.1.1 -m 'describe'； git push --tags；然后git push 否者当前分支对应的远程分支没有接收到本地最新代码

---
- 拉取远程分支并创建本地分支
  - git checkout -b localBranch origin/originBranch
  - git fetch origin originBranch:localBranch  //区别是不会切换到本地新分支

[toc]
# 使用windows powershell ISE管理命令窗口，并集成git命令
> 写于2018-09-03（基于win10）
## 开启 
1. win + s
2. 输入 ise

## 操作
> 主要使用新建的power shell选项卡

### 将git集成到power shell中

#### 安装准备
1. 确定你的power shell版本是5.X或者power Shell Core 6.0（使用$PSVersionTable.PSVersion查看版本）

2. 检查脚本执行规则是否设置为RemoteSigned或Unrestricted（使用Get-ExecutionPolicy查看，使用Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Confirm）

3. git 命令要添加到环境变量中

#### 开始安装
1. 打开powershell ise

2. 执行命令 PowerShellGet\Install-Module posh-git -Scope CurrentUser -AllowPrerelease -Force 或是 PowerShellGet\Update-Module posh-git（更新）

3. 引入并且支持所有用户所有主机，在管理员权限下打开powershell，执行命令 Add-PoshGitToProfile -AllUsers -AllHosts

4. 完毕，重启powershell即可

### 补充
1. 在powershell ise中，直接ctrl + c可能会在右下角一直提示正在停止，实际并未停止，所以这里采用杀死进程的方式将其关闭
    - 方式一： stop-process -Name 'node' （将所有node进程全部关闭）
    - 方式二： get-process node 查看与node相关的所有进程(主要看id)，再执行stop-process -id id号 关闭对应的node进程

## 参考
- [posh-git](https://github.com/dahlbyk/posh-git)
- [powershell](https://docs.microsoft.com/en-us/powershell/scripting/powershell-scripting?view=powershell-6)

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)
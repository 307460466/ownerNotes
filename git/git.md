# Git

<a name="jSSPD"></a>
## 参考文档
[Git（git-scm）](https://git-scm.com/book/zh/v2) <br />

<a name="cft8r"></a>
## 快速使用

- Git安装：[Win下载](https://git-scm.com/download/win) | [Linux安装](https://git-scm.com/download/linux)
   - centeOs：
```bash
$yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
```

- Git版本查看：git --version
<a name="Zgf23"></a>
### Git设置
```bash
# 设置全局用户名和邮箱
$git config --global user.name "测试名"
$git config --global user.email "ceshi.a@test.com"
```

<br />

<a name="b0LVP"></a>
## 相关命令
<a name="v3xT5"></a>
### git remote
```bash
# 查看远程仓库简写名及对应URL
$ git remote -v
# 添加远程仓库 简写名和url
$ git remote add [name] [url]
# 移除远程仓库简写名及映射关系
$ git rmeote rm [name]
# 远程仓库简写名重命名
$ git remote rename [oldName] [newName]
```
<a name="DyfGv"></a>
### git branch
```bash
# 查看本地所有分支及当前所在分支
$ git branch
# 查看远程仓库所有的分支
$ git branch -r
# 查看本地分支与远程关系关联关系（无[origin/Xxx]标识未绑定远程分支）
$ git branch -vv
```


<a name="M8cF2"></a>
## 常用命令
<a name="U3BLJ"></a>
### 提交相关
```bash
# 查看当前add后的修改状态
$ git status
# 添加指定目录或文件的修改内容 [directory] or [directory/filename]
$ git add a.md test/b.md
# 添加该仓库下所有修改的文件
$ git add .
# 将本轮所有'git add'暂存的文件，提交到本地仓库，并增加提交注释
$ git commit -m '提交注释'
```
<a name="MN7DX"></a>
### 本地与远程的拉取及推送
```bash
# 拉取指定远程的指定分支（默认为origin,分支默认同当前名如无则为master）
$ git fetch [origin name] [branch name]
# 拉取指定远程的指定分支，并合并到当前分支中 git pull = git fetch + git merge
$ git pull [origin name] [branch name] 
# 将本地分支推送到指定远程的指定分支上
$ git push [origin name] [branch name]
```
<a name="BDN10"></a>
### 本地与远程的关联
```bash
# 查看远程分支
$ git branch -r
# 查看本地分支与远程分支关联（无[origin/Xxx]标识未绑定远程分支）
$ git branch -vv
master 139edea[origin/master:behind 3] f
v1.0 139edeb a
# 当前分支关联远程分支
$ git branch --set-upstream-to=origin/branch
```
<a name="69aVM"></a>
### 克隆时更改文件夹名称
```bash
$ git clone https://github.com/527515025/springBoot.git spring-boot
```
<a name="Wp4LK"></a>
### 克隆指定分支
```bash
$ git clone -b dev https://github.com/527515025/springBoot.git
```
<a name="5EwkC"></a>
### 配置免密登录（SSH）

- 查看本机ssh publicKey：`ls -al ~/.ssh`,如无`id_ras/id_ras.pub`这一类的文件就表示无
- 指定email生成shh公钥：`ssh-keygen -t rsa -C 'youremail@email.com`
   - 要求输入公钥文件生成地址和文件名,默认为`${system}/Users/${user}/.ssh/id_rsa`,输入相对路径则为当前目录下
   - 输入使用公钥时要输入的密码，可为空
   - 确认密码
   - 控制台输出相关生成信息
- 项目绑定远程仓库ssh地址
   - 移除原有origin地址:`git remote rm origin`
   - 添加新origin地址:`git remote add origin [git@github.com]():sshurl
- github添加ssh公钥,在生成的目录下查看`id_rsa.pub`
- 使用ssh-agent管理ssh密钥
   - 确认ssh-agent是否启用：`eval "$(ssh-agent -s)"`
   - 添加密钥管理:`ssh-add ${system}/Users/${user}/.ssh/id_rsa`
- 输入`ssh -T git@github.com`，确认是否为`successfully`
<a name="b4fa9512"></a>
### 查看文件变动记录
```bash
# 查看git status中文件的详细变动
$ git diff
# 查看某个文件变动,commit形式展现
$ git log filename
# 查看某个文件的历史变动记录（commit记录及变动详情）
$ git log -p filename
# 查看两个分支之间差异文件
$ git diff branchA branchB --stat
```


<a name="6AAXU"></a>
## 其他
<a name="V0s3a"></a>
### 常用插件

- GitLens：快速定位每行代码的提交记录；快速查看文件的提交历史

# Git 使用方法
## 参考
- [Git 教程|菜鸟教程](https://www.runoob.com/git/git-tutorial.html "")
## 目录
- [Git 基本操作](#git-基本操作)
    - [创建仓库命令](#1创建仓库命令)
    - [提交与修改](#2提交与修改)
    - [提交日志](#3提交日志)
    - [远程操作](#4远程操作)
- [GitHub代理设置](#github代理设置)
    - [git设置](#11全局设置不推荐)
    - [config文件配置](#2配置一个config就可以了)
- [使用git在两台机器间同步代码](#git在两台机器间同步代码)   
    - [在github上提交](#21在github提交)
    - [局域网内](#22在局域网内提交)

## Git 基本操作

### 1.创建仓库命令

命令|说明
-|-
git init    |初始化仓库
git clone	|拷贝一份远程仓库，也就是下载一个项目。

### 2.提交与修改

命令|	说明
-|-
git add	|添加文件到暂存区
git status	|查看仓库当前的状态，显示有变更的文件。
git diff	|比较文件的不同，即暂存区和工作区的差异。
git commit	|提交暂存区到本地仓库。
git reset	|回退版本。```git reset HEAD #回退到当前版本git reset HEAD^ # 回退到上一个版本```
git checkout file-name  |恢复修改，没有任何 git 操作
git rm	|将文件从暂存区和工作区中删除。
git mv [file] [newfile]	|移动或重命名工作区文件。


### 3.提交日志
命令|	说明
-|-
git log	|查看历史提交记录
git blame <file>	|以列表形式查看指定文件的历史修改记录

### 4.远程操作
命令|	说明
-|-
git remote	|远程仓库操作
git fetch	|从远程获取代码库
git pull	|下载远程代码并合并
git push	|上传远程代码并合并


## git设置
### git pull/push时免密码

    git config --global credential.helper store

之后会在.gitconfig文件中多加红色字体项"[credential] helper = store",再次提交输入密码后会在根目录生成一个.git-credentials文件

## github代理设置

### 1.1全局设置（不推荐）

    #使用http代理 
    git config --global http.proxy http://127.0.0.1:1080
    git config --global https.proxy https://127.0.0.1:1080
    #使用socks5代理
    git config --global http.proxy socks5://127.0.0.1:51837
    git config --global https.proxy socks5://127.0.0.1:51837

### 1.2只对Github代理（推荐）

    #使用socks5代理（推荐）
    git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
    #使用http代理（不推荐）
    git config --global http.https://github.com.proxy http://127.0.0.1:1080

### 1.3取消代理

当你不需要使用代理时，可以取消之前设置的代理。

    git config --global --unset http.proxy git config --global --unset https.proxy

### 2.配置一个config就可以了。

Linux、MacOS

    nano ~/.ssh/config

Windows 

到C:\Users\your_user_name\.ssh目录下，新建一个config文件（无后缀名）

将下面内容加到config文件中即可

对于windows用户，代理会用到connect.exe，你如果安装了Git都会自带connect.exe，如我的路径为C:\APP\Git\mingw64\bin\connect

#Windows用户，注意替换你的端口号和connect.exe的路径

    ProxyCommand "C:\APP\Git\mingw64\bin\connect" -S 127.0.0.1:1080 -a none %h %p

#MacOS用户用下方这条命令，注意替换你的端口号

    #ProxyCommand nc -v -x 127.0.0.1:1080 %h %p

```
Host github.com
  User git
  Port 22
  Hostname github.com
  # 注意修改路径为你的路径
  IdentityFile "C:\Users\Your_User_Name\.ssh\id_rsa"
  TCPKeepAlive yes

Host ssh.github.com
  User git
  Port 443
  Hostname ssh.github.com
  # 注意修改路径为你的路径
  IdentityFile "C:\Users\Your_User_Name\.ssh\id_rsa"
  TCPKeepAlive yes
```

保存后文件后测试方法如下，返回successful之类的就成功了。

### 2.1测试是否设置成功

    ssh -T git@github.com

## git在两台机器间同步代码
步骤
### 1.设置提交代码用的用户名和邮箱

全局:
```
git config --global user.name "xxx"
git config --global user.email "xxx"
```
特定的项目：
```
git config user.name "xxx"
git config user.email "xxx"
```

### 2.1在GitHub提交

先克隆项目 git clone ***

    git clone https://github.com/***.git

我们先在本地建立 a 分支，在项目文件夹下执行：

    // 建立并切换到a分支
    git checkout -b a
这条命令相当于执行下面这两条命令：

    git branch a
    git checkout a
然后，我们在a分支上进行a模块代码的编写。比如我们在README.md文件里添加一句话：a分支第一次编写

编写完以后，我们提交代码到远程的 a 分支。我们按顺序执行下面代码：

    // 将项目的代码变化提交到缓存区（包括修改、添加和删除）
    git add -A

    // 将缓存区的所有内容提交到当前本地分支，并附上提交说明：'xxx'
    git commit -m 'xxx'

    // 确认分支是从最新的 master 分支,在GitHub上发起 Pull requests 请求
    git pull

    // 将代码提交到远程a分支
    git push origin a

后面就是等待项目管理员同意你的合并请求。

如果从你克隆项目到本地到你准备合并 a 分支的这个过程中有人提交过代码到 master 分支。那么，我们需要先将本地项目切回 master 分支：

    git checkout master
将最新的远程 master 分支代码拉到本地的 master 分支：

    git pull origin master
切换到本地 a 分支：

    git checkout a
将本地 master 分支合并到当前分支：

    git merge master
如果合并的过程中有冲突，那么我们可以借助 vscode 去查看冲突的代码并选择我们需要保留的代码。

合并好了以后，我们需要将本地的 a 分支代码更新到远程 a 分支：

    git add -A

    git commit -m "xxx"

    git push origin a
这样远程的 a 分支代码就不会比远程的 master 代码落后了，这样我们就可以提合并请求了。

### 2.2在局域网内提交
建一个空文件夹来做仓库，例如建为 cangku
    
    //cd 到 cangku目录下 创建远程仓库容器
    cd cangku
    mkdir mycangku.git
    //创建初始化git仓库
    cd mycangku.git
    git init —bare
    //pwd查看仓库路径，假设为 /abcd.git
    pwd

重复步骤2.1提交过程[在github上提交](#21在github提交)

    ps:remote地址(Linux)
    ssh://仓库本机名字(打开git 顶部@符号前面就是本机名字)@本机ip地址/abcd.git
    //192.168.***.***/***.git
操作过程

    git clone ***
    git add .
    git commit -m "first"
    git push origin master

    //如果别人修改过仓库里面的项目，那么先拉下来和自己的合并再上传
    //a.拉下来 
    git fetch
    //b.合并 
    git merge origin/master
    //这两小步，可以用
    git pull
    //c.合并后上传到仓库 
    git push origin master 

其他：ip地址改变之后，需要删除remote 重新和仓库建立连接
    
    //查看是否存在remote
    git remote
    //删除本地添加指定的远程地址
    git remote remove origin
    git remote add origin  ***
    //修改远程地址
    git remote set-url origin ***
    //查看远程服务器地址和仓库名称
    git remote -v  
    1. 远程仓别名的重命名
    git remote  -v // 查看远程仓
    git remote rename trunk(现有远程仓别名)  private(自定义的远程仓别名) 
    //修改远程仓别名
    git remote  // 将会显示 master(默认远程主仓别名) 和 private (自定义的个人仓别名)
    //删除远程仓
    git remote private // 删除远程仓
    git remote // 只会显示master(默认远程主仓别名)

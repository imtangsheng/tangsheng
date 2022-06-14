# Git 使用方法
## 目录
- [Git与SVN的区别](#git与svn的区别)
- [git在两台机器间同步代码](#git在两台机器间同步代码)

### Git与SVN的区别:
    1)Git是分布式的,SVN不是:这是Git和其他非分布式的版本控制系统,例如SVN,CSV等,最核心的区别.
    2)Git把内容按元数据方式存储,而SVN是按文件:所有的资源控制系统都是把文件的元信息隐藏载一个类似.svn,.cvs等的文件夹里.
    3)Git分支和SVN的分支不同:分支在SVN中一点都不特别,其实它就是版本库中的另外一个目录.
    4)Git没有一个全局的版本号,而SVN有:目前为止这是跟SVN相比Git缺少的最大的一个特征.
    5)Git的内容完整性要优于SVN:Git的内容存储使用的是SHA-1哈希算法.这能确保代码内容的完整性,确保在遇到磁盘故障和网络问题时降低对版本库的破坏.


### git在两台机器间同步代码
步骤
#### 1.在存放原始代码的机器上，比如A，假设代码目录为：/codes/project,
```
cd /codes/project

# 创建git代码仓库
git init
git add .
git commit -m "create project"

# 切换到project父目录，创建一个project-bare目录
cd ..
mkdir project-bare
cd project-bare

# 从原始代码仓库创建bare仓库，作为“中央”仓库，其他机器(包括本机的原始仓库)往这里push，从这里pull
git clone --bare ../project ./project-bare.git

# 回到project仓库目录
cd ../project

# 把project-bare添加为remote，
git remote add origin ../project-bare.git
git branch --set-upstream-to=origin/master master
```
#### 2.在其它机器上，比如B:
假设通过ssh来连接机器A
```
git clone ssh://<username>@<ip>:<port>:/codes/project-bare/project-bare.git ./project
```

clone下来之后，在机器B上做修改，然后commit，push之后，在机器A上就可以pull到了。反之在机器A的project目录做修改，commit，push之后，在机器B上也能pull下来了。

若要再添加一台开发机，重复第2步，clone操作即可。

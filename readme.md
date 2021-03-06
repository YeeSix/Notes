# Git

## 什么是Git？

- Git是目前世界上最先进的分布式版本控制系统
- Git是一款代码管理工具(版本控制工具)
- 源代码管理有必要 因为人工去处理不同的版本 做响应的备份会很麻烦
- svn,vss,vcs,...git

## [SVN与Git的最主要的区别？](https://blog.csdn.net/qq_36150631/article/details/81038485?utm_source=app)

- SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了。

- Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

## [工作原理/流程](https://blog.csdn.net/qq_36150631/article/details/81038485?utm_source=app)

Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库

## [Git安装](https://git-scm.com/)

## Git操作

### 初始化Git仓库

- 仓库存放git对我们项目代码进行备份的文件
- 在项目目录右键打开 git bash
- 命令: ` git init`

### 配置用户名和邮箱 用以区分备份者信息

- 配置用户名 `git config --global user.name '用户名'`
- 配置邮箱 `git config --global user.email '邮箱'`

### 把代码储存进.git仓库中

- 1. 把代码放在仓库门口(暂存区)
    + `git add ./readme.md`
    + `git add ./`  (简写 将所有修改的文件添加到仓库门口--暂存区)
- 2. 把仓库门口(暂存区)代码放入里面房间中(仓库区)
    + `git commit -m "此次提交代码说明信息"`
- 可以一次性把修改的代码放入房间中(仓库区)
    + `git commit --all -m "说明信息"`

### 查看当前提交状态

- 可以看当前代码处于1修改未提交状态2提交到暂存区未存到仓库区3已存储到仓库区
    + `git status`

### git中的忽略文件

- .gitignore,这个文件中可以设置被忽略的文件或者目录,被忽略的文件不会提交到仓库中
- 在.gitignore文件中书写以/开头,一行写一个路径,这些路径对应的文件就会被忽略
    + 写法
        * `/.idea `  会忽略.idea文件
        * `/js `     会忽略js目录下的所有文件
        * `/js/*.js` 会忽略js目录下的所有js文件

### 查看日志

- `git log` 可以查看历史提交日志
- `git log --oneline` 可以查看简洁版日志

### 回退到指定版本

- `git reset --hard Head~0` 表示回退到上次一代码提交时的状态
- `git reset --hard Head~1` 表示回退到上上次一代码提交时的状态
- `git reset --hard [版本号]` 可以通过版本号精确退回某一次提交的状态

- `git reflog` 可以看到每一次切换版本的记录 可以看到所有提交的版本号

### 分支

- 默认分支是master

- 创建分支
    + `git branch dev` 创建了一个dev的分支 新创建的dev分支的内容和master是一样的

- 切换分支
    + `git checkout dev` 切换到指定的分支(这里切换到dev的分支)
    + `git branch` 可以查看有哪些分支 当前所在的分支前面有*号

- 合并分支
    + `git merge dev` 合并分支内容,把当前分支(master)与指定分支(dev)进行合并
    + 合并时如果出现冲突,需要手动去处理,处理后再提交一次

## Github

- 不是git,只是一个网站; 只是这个网站提供了允许通过git上传代码的能力

### 把代码提交到github中(即把github当做git的服务器)

- `git push [地址] master` 会把当前分支上的内容上传到远程的master分支上

- `git pull [地址] master` 会得到远程分支上的数据(*注意本地要初始化一个仓库*)

- `git clone [地址]` 会得到远程仓库的相同数据,多次执行会覆盖本地内容

- push和pull简写方法
    + `git remote add origin [地址]` 即添加一个远程仓库的地址变量origin,方便后期使用
        - `git remote` 查看当前的远程仓库变量
        - `git remote remove origin` 可以删除之前保存的远程仓库
        - `git origin -v` 可以查看具体绑定的地址
    + `git pull origin -u master` 即加上-u参数,git会把当前分支和远程的对应分支进行关联
    + `git push` `git pull`


- 注意:
    + 修改文件之后要现在本地提交,然后push到服务器
    + 在本地提交之前,要先pull把最新数据拿回来,再push自己修改的代码
    + (因为先pull就可以手动去解决服务器和本地之间冲突的代码,再去把最新的版本上传)

### ssh方式上传代码

- 公钥,私钥 两者室友关联的(私钥不能告诉别人)
    + 1 `ssh-keygen -t rsa -C "邮箱"`
    + 2 生成的公钥私钥在管理员文件夹中的.ssh文件中 `C:\Users\yeesix\.ssh`
    + 3 在github中settings中设置添加公钥(直接复制剪贴公钥)

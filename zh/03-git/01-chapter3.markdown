# 分布式版本控制 Git #
如果你还停留在svn阶段，或者从没有玩过Git，那太落伍了。Git是版本控制的一个飞跃，它极大的提高了软件开发的效率。

## 工作环境 ##
 * 服务器端推荐用 Gerrit <http://code.google.com/p/gerrit/>
 * 客户端用Windows版的Git：<http://code.google.com/p/msysgit/>
 
## 什么是Git ##
Git最早是Linus用于Linux内核开发的版本控制工具。与常用的版本控制工具 CVS, Subversion 等不同， 它采用了分布式版本库的方式，不必服务器端软件支持，使源代码的发布和交流极其方便。 

Git的速度很快，这对于诸如Linux kernel这样的大项目来说自然很重要。 

Git最为出色的是它的合并跟踪（merge tracing）能力和强大的社区支持。

### 集中式和分布式 ###



## 基本 Git ##
### 安装 ###
先装好Windows版的Git，["Git for windows"](http://code.google.com/p/msysgit/downloads/list?can=3&q=official+Git)，很多人老是说装msysgit，实际上msysgit是一个含有整套源码环境的系统（如C编译器），除非你是个Git极客，否者别自讨麻烦。

缺省安装就可以了，除非你是专家，否者别选Putty的ssh。初学者80%的Git的问题出在ssh连接上。

### 配置 Git ###
先要告诉Git你是谁，怎么联系你，要看彩色还是黑白的。

    $ git config --global user.name "Your name"  
	$ git config --global user.email "Your email address"
	$ git config --global color.ui auto

`--global`就是把配置放在你的HOME下 `~/.gitconfig`，下面两条命令都可看到全局定义。

    $ less ~/.gitconfig	
	$ git config -l
	
### 建立本地 Git 库 ###
既然是分布式，就可以直接干活了。创一个干净目录`helloworld`

    $ cd ~
	$ mkdir helloworld
	$ git init
	
养成习惯经常看看有什么变化了。

    $ find .
	...
	
你会发现建了`.git`目录，下面有很多东西，自己瞅瞅，琢磨琢磨。

### 第一个提交 ###
继续吧

    $ cat "Hello Git World" > README # 建一个空文件
	$ git status 
	$ git add README # 加入索引区
	$ git status & find .
	$ git commit -am "add first empty file” # 养成好习惯写好提交的注释。
	$ git status & find .
	$ git log
	$ git blame # 查看谁改的
	
体会每次的变化。就这么简单。

### 分支(Branch)和合并(Merge) ###
分支和合并在其他大多数的版本控制系统中（如svn，clearcase）都是高级课程，而在Git中，一会儿就学到了。这是一种很常用的工作方式。

    $ git branch bug123
	$ git branch ...
	
	
## 和Git服务器远程连接 ##
 
### 几种协议 ###
 * git@
 * https://
 * larrycai@
 
### 配置 ssh ###

### 克隆 ###

### 与远程服务器相连的Git命令 ###

## 常用的几种工作模式 ##
### 本地特性分支 ###
## Git的缺点 ##
相比svn，mercurial，Git的学习曲线有点高，但是掌握基本的命令就可以畅通无阻了。

如果你喜欢上了她，你可能会喜欢她的一切，对Git也如此。作为技术人员，看到一些小命令、小技巧，会越来越有兴趣。

所以绕过缺点或喜欢上缺点，就是我的建议。

## 课后练习 ##
 * 习惯使用Windows版的Git Bash环境
 * 继续练习常用的例子，如本地分支，服务器同步
 
## 总结 ##
Git是一个分布式版本控制系统，不应该用以前集中式的版本控制系统的思路去考虑。而且它的学习曲线相对较高，要反复练习来熟悉一些基本的用法，慢慢提高使用水平。

随着Git的日益普及，网上的资料已经很多，多问多玩。

## 参考 ##
 1. Git权威指南：<http://www.worldhello.net/gotgit/>
 2. Pro Git: <http://progit.org>
 3. Git Community Book 中文版 <http://gitbook.liuhui998.com/>
 4. Gerrit <http://code.google.com/p/gerrit/>
 5. Windows版的Git：<http://code.google.com/p/msysgit/>


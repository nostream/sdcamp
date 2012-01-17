# 版本控制Git和代码审阅Gerrit #
如果你还停留在svn阶段，或者从没有玩过Git，那太落伍了。Git是版本控制的一个飞跃，它极大的提高了软件开发的效率。

代码审阅有好几种方式，走读式效果不佳（有点事后诸葛亮的味道），结对编程（Pair Programming）一直是蛮多人推荐的方式，但真正在企业中实施成功的不是很多，不过还是值得推荐的。

基于Gerrit方式的代码审阅有很多的优点，能很好得满足企业的需要。

## 工作环境 ##
 * 服务器端推荐用 Gerrit <http://code.google.com/p/gerrit/>
 * 客户端用Windows版的Git：<http://code.google.com/p/msysgit/>
 
## 什么是Git ##
Git最早是Linus用于Linux内核开发的版本控制工具。与常用的版本控制工具 CVS、Subversion 等不同， 它采用了分布式版本库的方式，不需服务器端软件支持，使源代码的发布和交流极其方便。 

Git的速度很快，这对于诸如Linux kernel这样的大项目来说自然很重要。 

Git最为出色的是它的合并跟踪（merge tracing）能力和强大的社区支持。

### 集中式和分布式 ###

Insert 18333fig0301.png
图 3-1. 集中式和分布式版本控制

## 基本 Git ##
Git的学习曲线相对来说还是有点陡的，但只要掌握了基本的一些命令，日常的工作就没有问题了。

### 安装 ###
先装好Windows版的Git，["Git for windows"](http://code.google.com/p/msysgit/downloads/list?can=3&q=official+Git)，很多人老是说装msysgit，实际上msysgit是一个含有整套源码环境的系统（如C编译器），除非你是个Git极客，否者别自寻麻烦。

缺省安装就可以了，除非你是专家，否者别选Putty的ssh。初学者80%的Git的问题出在ssh连接上。

### 配置 Git ###
先要告诉Git你是谁，怎么联系你，这样在代码库中才能找到提交者。界面也可设置成彩色。

~~~~~~~~~~~~~ {.bash}
$ git config --global user.name "Your name"  
$ git config --global user.email "Your email address"
$ git config --global color.ui auto
~~~~~~~~~~~~~~

`--global`就是把配置放在你的HOME下 `~/.gitconfig`，下面两条命令都可看到全局定义。

~~~~~~~~~~~~~ {.bash}
$ less ~/.gitconfig	
$ git config -l --global
~~~~~~~~~~~~~ 
	
### 建立本地 Git 仓库 ###
既然是分布式，就可以直接干活了。创一个干净目录`helloworld`

~~~~~~~~~~~~~ {.bash}
$ cd ~
$ mkdir helloworld
$ cd helloworld
$ git init   # 初始化本地仓库
Initialized empty Git repository in c:/Users/larrycai/helloworld/.git/
~~~~~~~~~~~~~~~~~~
	
养成习惯经常看看有什么变化了。

~~~~~~~~~~~~~ {.bash}
$ find .
.
./.git
./.git/config
./.git/hooks
...
./.git/hooks/update.sample
./.git/info
./.git/objects
./.git/refs
./.git/refs/heads
./.git/refs/tags
~~~~~~~~~~~~~~~~~~~
	
你会发现建了`.git`目录，下面有很多东西，自己瞅瞅，琢磨琢磨，这也是平时自我提高的一个办法。不管怎样，这就是你的本地Git仓库了。

### 第一个提交 ###
继续吧

~~~~~~~~~~~~~ {.bash}
$ cat "Hello Git World" > README # 建一个空文件
$ git status # 会发现报告红色的未跟踪的文件
$ git add README # 加入暂存（stage)区
$ git status & find . # 变绿色，跟踪了。产生一个索引
$ git commit -am "add first empty file” # 签入代码到本地，要养成好习惯写好提交的注释。
$ git status & find . # 干净了，索引变化了。
$ git log
$ git blame # 查看谁改的
~~~~~~~~~~~~~
	
体会每次的变化，就这么简单。

### 分支(Branch)和合并(Merge) ###
分支和合并在其他大多数的版本控制系统中（如svn，clearcase）都是高级课程，而在Git中，一会儿就学到了。记住，这是一种很常用的工作方式。

一个Git仓库可以维护很多开发分支并快速切换。

~~~~~~~~~~~~~ {.bash}
$ git branch bug123 #创建关于 bug 123的分支
$ git branch  # 看看有哪些分支，master是主分支。
  bug123
* master
$ git checkout bug123 # 切换到bug123分支。
Switched to branch 'bug123'
$ git checkout -b bug234 # 创建并直接切换到bug234分支
~~~~~~~~~~~~~ 
	
### Git使用的良好习惯 ###	
	
## 和Git服务器远程连接 ##
在本地练习的比较久了，该把代码上传到Git服务器了。Git服务器有好几种，企业建议用Gerrit。

先来熟悉各种传输的协议

... 持续码字中，休息一会儿，休息一会儿 ...
 
### 几种协议 ###

 1. git clone git@gitserver/repo.git
 2. git clone ssh://git@gitserver/repo.git
 3. git clone larrycai@gitserver/repo.git
 4. git clone ssh://larrycai@gitserver:29418/repo.git
 5. git clone git://gitserver/repo.git
 6. git clone https://larrycai@gitserver/repo.git
 
  
### 配置 ssh ###


### 克隆 ###

~~~~~~~~~~~~~ {.bash}
$ git clone 
~~~~~~~~~~~~~ 
	
### 与远程服务器相连的Git命令 ###

## 常用的几种工作模式 ##
### 本地特性分支 ###
## Git的缺点 ##
相比SVN、Mercurial，Git的学习还是需要花更多的时间，但是掌握基本的命令就可以畅通无阻了。

如果你喜欢上了她，你可能会喜欢她的一切，对Git也如此。作为技术人员，看到一些小命令、小技巧，会越来越有兴趣。

所以绕过缺点或喜欢上缺点，就是我的建议。

## 代码审阅和Gerrit ##

代码审阅是一个不错的敏捷开发实践，让人非常头疼的是实施。大企业中通常是制定出一大堆相关的规范和流程来指导代码审阅。谷歌的 Android 系统是现在非常热门的开源项目，它的代码审阅（包括贡献者的代码）使用的是Gerrit，非常棒的东西，在自己的企业中架设起来也非常方便。

Insert 18333fig0302.png
图 3-2. Gerrit代码审阅系统

Gerrit是一个基于 Web 的代码评审和项目管理的工具，面向基于 Git 版本控制系统的项目（git是一个分布式版本控制系统），所以如果你没用git，就没法用gerrit了，接下来看看在gerrit中怎么实施代码评审的。

 * 首先开发者（贡献者）的代码变更通过 git 命令被推送（push）到 gerrit 管理下的 Git 版本库，推送的提交转化为一个一个的代码审核任务
 * 代码审核者可以通过 Web 界面查看审核任务、代码变更，通过 Web 界面做出通过代码审核（Review）或者拒绝（Reject）等决定。
 * 测试者（一般可以设定为CI服务器执行）可以通过访问来获取代码变更进行相应测试，如果测试通过，就可以把这个评审任务设置为校验通过（Verified）。
 * 最后经过了审核（Review）和校验(Verified) 的代码变更可以通过 gerrit 界面中提交动作合并到版本库的对应分支。

相比代码走读，它的好处在于，审阅动作发生在向主干提交代码前，可以只看变更的部分显得很贴心，网上随时随地审阅起来也很方便，这也是有别于结对编程的一个好处。

任何人都可以审阅提交的代码，整个团队的代码都一目了然，审阅起来更方便，非常符合开放、透明的敏捷精神。使用之后能够显著提高代码质量，甚至于等到习惯了以后，代码不被审阅一下，都觉得实在是不好意思提交代码到主干上去。

Gerrit中通过特定分支，任何审核任务的代码变更都能访问，所以如果需要细看或是合并到本地都异常的方便。

## 课后练习 ##
 * 习惯使用Windows版的Git Bash环境
 * 继续练习常用的例子，如熟练应用本地分支来开发任务、服务器同步。
 * 尝试给你所在产品代码进行审阅
 
## 总结 ##
Git是一个分布式版本控制系统，不应该用以前集中式的版本控制系统的思路去考虑。要反复练习来熟悉一些基本的用法，慢慢提高使用水平。

随着Git的日益普及，网上的资料已经很多，多问多玩。

## 参考 ##
 1. Git权威指南：<http://www.worldhello.net/gotgit/>
 2. Pro Git: <http://progit.org>
 3. Git Community Book 中文版 <http://gitbook.liuhui998.com/>
 4. Gerrit <http://code.google.com/p/gerrit/>
 5. Windows版的Git：<http://code.google.com/p/msysgit/>


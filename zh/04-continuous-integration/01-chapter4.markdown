# 持续集成 #

持续集成是一种软件开发实践，它是Martin Fowler先生提出的[1]。一个在企业开发中必须的软件实践，谁也不会容忍企业的软件发布是在一个私人机器上完成的。

在持续集成中，团队成员频繁集成他们的工作成果，一般每人每天至少集成一次，在保证质量的同事也可以多次。每次集成会经过自动构建（包括自动测试）的验证，以尽快发现集成错误。许多团队发现这种方法可以显著减少集成引起的问题，并可以加快团队合作软件开发的速度[2]。

## 环境准备 ##
服务器端准备好 Game of life项目的git仓库，客户端需要:

 * Maven 2.x 包 <http://maven.apache.org/download.html>
 * JDK 6 <http://www.oracle.com/technetwork/java/javase/downloads/index.html>
 * Jenkins <http://jenkins-ci.org/>

## 持续集成流程 ##
持续集成的一个简单流程

 1. 将已集成的源代码复制一份到本地计算机。（git clone/pull)
 2. 修改产品代码和添加修改自动化测试。
 3. 把修改提交到源码仓库。(git commit/git push)
 4. 在持续集成服务器上基于主干（master）的代码再做一次构建（编译，单元测试，构建，打包）。
 5. 在持续集成服务器进行测试（验收）
 
如果上述所有操作没有任何错误，没有人工干预，并通过了所有测试，我们认为这才是一次成功的构建。

Insert 18333fig0401.png 
图 4-1. 持续集成流程

## Maven ##
Maven是一个Java项目管理工具，就像Make对于c/c++项目。和它“类似”的是Ant。Maven比Ant的好处是：

 * 依赖包的管理只要写配置文件就可以了，Ant需要把依赖的3pp的二进制包放在项目里。
 * 定义了标准集合，简单了项目的管理。

Maven还包括：

 * 一个项目对象模型 (Project Object Model)
 * 一组标准集合
 * 一个项目生命周期(Project Lifecycle)
 * 一个依赖管理系统(Dependency Management System)，和用来运行定义在生命周期阶段(phase)中插件(plugin)目标(goal)的逻辑。

### 安装Maven ###
装好JDK6，熟悉Unix环境，用Git bash安装Maven

	$ cd /c  # Windows C:/
	$ tar -zxvf ~/Desktop/apache-maven-2.2.1-bin.tar.gz
	$ mv apache-maven-2.2.1 maven
	
在系统中配好环境变量`M2`、`M2_HOME`、`MAVEN_OPTS`、`PATH`，如下图

Insert 18333fig0402.png 
图 4-2. 系统中配好maven

需要重新打开bash后配置才会起作用。

	$ mvn --version
	Apache Maven 2.2.1 (r801777; 2009-08-07 03:16:01+0800)

### Maven仓库管理器：Nexus ###
不管怎么样，java的包在编译时还是要下载下来的，在企业中，最方便的是架设一个管理java的包的服务器，这就是Nexus。它会缓存远程仓库的Jar包。如下图 (源: http://today.java.net/article/2010/01/04/maven-repository-managers-enterprise)

Insert 18333fig0403.png 
图 4-3. Maven仓库管理器

对于个人来说，你不需要安装，只要在`~/.m2/settings.xml`配置指向Nexus服务器就好了，如

	# ~/.m2/settings.xml
	<mirrors>
	  <mirror>
	    <id>nexus</id>
		<mirrorOf>*</mirrorOf>
		<url>http://localhost:8081/nexus/content/groups/public</url>
      </mirror>
	</mirrors>
	
### 第一个maven命令 ###
在你的Game of life项目中，输入命令`mvn package`，查看 `~/.m2`目录的变化。

### 体会两层缓存 ###
实际上很容易理解，在个人机器上会有一个缓存，它在 `~/.m2/repository`。在Nexus服务器上是整个项目的缓存。

## 持续集成服务器：Jenkins ##
Jenkins是现在最流行也最有效的持续集成服务器，它的前身是著名的Hudson。

### 安装 ###
不需要安装，直接启动后就可以在你的浏览器中打开。<http://localhost:7080>

	$ java -jar ~/Deskop/jenkins.war --httpPort=7080
	
### 安装Git插件 ###
你可以从Jenkins系统中下载Git插件，也可以直接把它拷到`~/.jenkins/plugins`下，重启后就能起作用了。

### 系统配置Maven ###
在系统中配置好maven目录，别忘了把自动安装选项去掉。

Insert 18333fig0404.png 
图 4-4. Jenkins 系统配置Maven

### 设置构建任务 ###
新建一个任务`game-of-life`，选择自由风格（freestyle）。

  1. 源码管理：配置好Git的远端仓库。
  2. 构建触发器：设置轮询（Poll）策略：`*/1 * * * *` （每分钟一次）
  3. 构建：用`Invoke top-level maven targets`构建，填上`clean package`
  4. 构建后操作: `Archive the artifacts`选中后填上`**/target/*.jar,**/target/*.war`
  
Insert 18333fig0405.png 
图 4-5. Jenkins game-of-life配置。  

### 在Sonar中观察结果 ###

## 课后练习 ##
 1. 装一些插件（Raditor，cobertura）体会一下。
 2. 把JUnit的单元测试结果显示出来。
 3. 查找构建输出在哪里。
 
## 总结 ##
持续集成是敏捷软件开发的重中之重，一定要养成好的习惯。
 
## 参考 ##
 * Jenkins: The Definitive Guide：<http://www.wakaleo.com/books/jenkins-the-definitive-guide>
 * Maven实战：<http://www.juvenxu.com/mvn-in-action/>
 * 持续集成软件质量改进和风险降低之道: <http://product.dangdang.com/product.aspx?product_id=20098017>
 * 持续集成理论和实践的新进展: <http://www.infoq.com/cn/articles/ci-theory-practice>
 * Repository Management with Nexus : <http://www.sonatype.com/books/nexus-book/reference/index.html>
 
 [1]: <http://martinfowler.com/articles/continuousIntegration.html>
 [2]: <http://www.infoq.com/cn/articles/ci-theory-practice>

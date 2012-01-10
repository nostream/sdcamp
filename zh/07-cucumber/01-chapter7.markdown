# 需求管理和Cucumber #

在本章，我们会通过学习相关联的Cucumber软件来切身体会怎么将需求贯穿下去。

## Cucumber ##
Cucumber（英文：黄瓜）是一个实例化需求的极佳实现伴侣。它是基于Ruby的开源测试工具，得益于Ruby便于创建和使用DSL的特性，它可以通过自然语言（文本文字）来描述需求（业务层），并通过关键字驱动和正则表达式匹配告诉去做哪些事情（驱动层），在运行自动化测试结束以后，还会给出详细的报告。

Insert 18333fig0701.png
图 7-1. Cucumber的架构

下面就是一个加法的例子，无需解释也能明白。Cucumber文件已`.feature`结尾。

	# 加法 adding.feature
	Feature: Adding
	  In order to avoid silly mistakes
	  As a math idiot
	  I want to be told the sum of two numbers
	  
	  Scenario: Add two numbers
		Given the input "2+2"
		When the calculator is run
		Then the output should be "4"

	  Scenario Outline: Add two numbers
		Given the input "<input>"
		When the calculator is run
		Then the output should be "<output>"
		Examples:
		  | input | output |
		  | 2+2 | 4 |
		  | 98+1 | 99 |

Cucumber的官方网站是http://cukes.info/ 
		
### 安装 ###
在Windows上，RubyInstaller提供了ruby的环境，下载安装包（如`rubyinstaller-1.9.3-p0.exe`)，运行即可，别忘了把“Ruby放入PATH中”的选项选上。

Insert 18333fig0702.png 
图 7-2. Windows平台安装Cucumber

	$ gem install cucumber # 如果需要配代理，-p http://<proxyserver>:<port>
	$ gem install rspec # cucumber 需要
	
### 运行Cucumber ###

一旦Cucumber装好了，我们就可以使用 cucumber 命令来运行feature文件。

feature文件放在`features`目录下，如果cucumber命令后不跟任何东西的话，那么它会执行所有的.feature文件。如果我们只想运行某一个.feature文件，我们可以使用命令 `cucumber features\feature_name`

	$ cucumber features/adding.feature
	Feature: Adding
	  In order to avoid silly mistakes
	  As a math idiot
	  I want to be told the sum of two numbers

	  Scenario: Add two numbers       # features\adding.feature:3
		Given the input "2+2"         # features\adding.feature:4
		When the calculator is run    # features\adding.feature:5
		Then the output should be "4" # features\adding.feature:6

	  Scenario Outline: Add two numbers      # features\adding.feature:8
		Given the input "<input>"            # features\adding.feature:9
		When the calculator is run           # features\adding.feature:10
		Then the output should be "<output>" # features\adding.feature:11

		Examples:
		  | input | output |
		  | 2+2   | 4      |
		  | 98+1  | 99     |

	3 scenarios (3 undefined)
	9 steps (9 undefined)
	0m0.046s

	You can implement step definitions for undefined steps with these snippets:

	Given /^the input "([^"]*)"$/ do |arg1|
	  pending # express the regexp above with the code you wish you had
	end
	...

你就可以看到它被正常执行了，后面几行是驱动层的模板，稍后解释。

### 驱动层 ###
Cucumber的驱动层可以用ruby，java和其他语言来支持，很多时候主要依赖团队的兴趣。

建一个`step_definitions`目录，把上面运行的代码模板片段写入`calculator_steps.rb`文件中，并且把`pending`注释掉，再次运行`cucumber`，就很顺利通过了。

在ruby程序中，`Given`后面的就是一个正则表达式来匹配关键字，如`"2+2"`，然后把这个关键字处理后，传递到被测的系统。

驱动层可以把结果返回，并和设定的期望值匹配来确定测试结果。

### Gherkin语言 ###
Cucumber是一个解释程序，Cucumber用来执行解释 .feature文件里的Gehrkin代码（有翻译叫格莱克林），它的关键字就是“Given”、“And”等等这样的字眼。

一个常见的Cucumber文件描述分为 **Feature（特性）**、**scenarios（场景）**、和**steps（步骤）**。让我们来看看上面的例子:

 1. `Feature: Adding`: 每一个feature文件以关键字**Feature**开始，且紧跟着一个冒号和一个简单描述。
 2. 接下来的几行描述不会被解析，一般写成(In order to... As an... I want to...)格式。这些行只提供背景的人读你的功能，并描述列入在软件功能衍生的商业价值。
 3. `Scenario: Add two numbers`：关键字_Scenario_后面紧跟一个冒号和一个对应该场景的描述，也是简短的一句话。
 4. 接下来的几行也不会被解析，也是为了了解背景而用。
 5. 后面的以 _Given_/_When_/_Then_/_And_/_But_ 开头的都是步骤（步骤后面不需要跟冒号），用来阐述到底要的是什么样的需求。
 6. `Scenario Outline: Add two numbers`: 关键字Scenario Outline，和Scenario不同的是它是支持表格的形式。
 7. **Scenario** 和 **Scenario Outline**提供了特性的多个场景，可以出现多次。

### 常用的目录结构 ###
常用的目录结构是

	$ find calculator
	calculator/
	calculator/feature.html
	calculator/features
	calculator/features/adding.feature
	calculator/features/division.feature
	calculator/step_definitions
	calculator/step_definitions/calculator_steps.rb

 1. `features`下面按功能放置各个业务。
 2. `step_definitions`存放驱动层的脚本。
 3. TODO：`config` (profile), `support`
 
### 课后练习 ###
 1. 把网上书店的例子，尝试用实例化需求说明的方式来描述清楚，并写成Cucumber的格式。
 2. 了解Gherkin语言的详细内容，如**tag**，并结合Cucumber去执行。
 3. 看看如何能够实施Cucumber，使它能够整合到持续集成中去。

## 总结 ##

Cucumber也只是一种工具，如果不理解实例化需求说明的真正意义，它会被用得很累，好自为之。

## 参考 ##
 1. Book: Specification by example. <http://manning.com/adzic>
 2. Specification by example <http://specificationbyexample.com>
 3. Cucumber <http://cukes.info>
 4. Gherkin语言：<https://github.com/cucumber/cucumber/wiki/Gherkin>
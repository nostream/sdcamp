# 需求管理和Cucumber #

在一个项目中，需求是推动整个软件开发的源泉。它确定了方向，方向（需求）错了，后面开发测试的再辛苦，再正确都是白搭。

在本章，我们一起来学习需求管理中现在最有效果的一种实践-实例化需求（Specification by example)。同时会通过学习相关联的Cucumber软件来切身体会怎么将需求贯穿下去。

## 需求的困惑 ##

如果你做过开发，就知道软件开发的最大问题之一就是需求，而且它也很容易的被作为替罪羊。在公司项目延迟和出大问题的最大借口（也是事实），就是“需求不清楚”。

那把需求找点弄清楚不就行了嘛？听着挺容易，需求不清楚，不能开始项目，需求文档必须高级人员一起审核，实际上这就是瀑布模型中的思路，大家已经知道它不大行得通，因为早期把所有的需求都弄清楚不太容易。

敏捷迭代起来以后是否就好点呢。理论上会好点，因为需求在一个迭代中东西会少点，有机会理清楚一点。但就是因为一个迭代的周期短，在开完计划会议后（Planning meeting），团队会很快愿意投入到代码开发中去，他们认为需求已经清楚了。

实际上，往往到迭代的后面几天开始测试的时候发现，测试人员、开发人员、产品负责人想的都不是很一样，但时间不够了，这就是技术债务（Technical Debt)的最大根源。

那是否有好的办法把需求质量有效得提高？

### 实例化需求 ###

#### 例子 1 ####

## Cucumber ##
Cucumber（英文：黄瓜）是一个实例化需求的极佳实现伴侣。它是基于Ruby的开源测试工具，得益于Ruby便于创建和使用DSL的特性，它可以通过自然语言（文本文字）来描述需求（业务层），并通过关键字驱动和正则表达式匹配告诉去做哪些事情（驱动层），在运行自动化测试结束以后，还会给出详细的报告。

<add 2 layers picture, could refer to concordior>

下面就是一个加法的例子，无需解释也能明白。

~~~~~~~~~~~~~~~~~~~~~~~ {.cucumber .numberLines}
# 加法 adding.feature
Feature: Adding
  This is basic function to make sure the calculator works
  
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
~~~~~~~~~~~~~~~~~~~~~~~~~~~		

Cucumber的官方网站是http://cukes.info/ 
		
### 安装 ###
在Windows上，RubyInstaller提供了ruby的环境，下载安装包（如`rubyinstaller-1.9.3-p0.exe`)，运行即可，别忘了把“Ruby放入PATH中”的选项选上。

Insert 18333fig0701.png 
图 7-1. 本地版本控制系统

	$ gem install cucumber # 如果需要配代理，-p http://<proxyserver>:<port>
	$ gem install rspec # cucumber 需要

### Gherkin语言 ####
编写Cucumber文件的语言是Gherkin（有翻译叫格莱克林），它的关键字就是“Given”、“And”等等这样的字眼。

一个常见的Cucumber文件描述分为"Feature" (加粗）（特性）、scenarios（场景）、和steps（步骤）。让我们来看看上面的例子:

 1. `Feature: Adding`: 关键字Feature，加上简单的描述要做什么，想想看怎么搜索，就用这个搜索关键字就可以了。
 2. 接下来的几行不会被解析，一般写成(In order to... As an... I want to...)格式。这些行只提供背景的人读你的功能，并描述列入在软件功能衍生的商业价值。
 3. `Scenario: Add two numbers`：关键字Scenario情景：描述这个特性的一个场景，也是简短的一句话。
 4. 接下来的几行也不会被解析，也是为了了解背景而用。
 5. 后面的以 Given/When/Then/And 开头的都是步骤，来阐述到底要的是什么样的需求。
 6. `Scenario Outline: Add two numbers`: 关键字Scenario Outline，和Scenario不同的是它是支持表格的形式。
 7. Scenario 和 Scenario Outline提供了特性的多个场景，可以出现多次。

### 常用的目录结构 ###

### 例子Calculator ###


### 课后练习 ###

## 总结 ##

实例化需求是一种很棒的协作探索需求的好办法，但是要用熟练了还是很有难度得。Cucumber也只是一种工具，如果不理解实例化需求说明的真正意义，它会被用得很累，好自为之。

## 参考 ##
 1. Specification by example. <http://manning.com/adzic>
 2. Cucumber <http://cukes.info>
 3. Gherkin语言：
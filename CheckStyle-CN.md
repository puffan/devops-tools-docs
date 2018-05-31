# Java 代码风格检查工具 checkstyle 

## 1.简介

Checkstyle 是一种开发工具，可帮助程序员编写符合编码标准的Java代码。
借助它，可以将检查 Java 代码编码规范度的过程自动化，以免在 QC 过程中耗费时间。
它是希望执行编码标准项目的理想选择。

Checkstyle 支持高度可配置，可以支持几乎任何编码标准。
默认包含 Sun 编码规范 和  Google Java 编码规范的示例配置文件。

这里是使用Checkstyle和Maven生成报告的[好例子](http://maven.apache.org/plugins/maven-checkstyle-plugin/checkstyle.html)。

## 2.特性

Checkstyle 可以检查源代码的许多方面。它可以发现类设计，方法设计中存在的问题。它还能够检查代码布局和格式问题。

有关可用检查的详细列表，请参阅下方 4.1 章节描述。

## 3.工具

- CheckStyle 项目托管在 GitHub 上：[https://github.com/checkstyle/checkstyle](https://github.com/checkstyle/checkstyle)

- 发布版本下载地址：[https://sourceforge.net/projects/checkstyle/files/checkstyle/](https://sourceforge.net/projects/checkstyle/files/checkstyle/)

- Maven 库地址：[http://search.maven.org/#search|gav|1|g%3A%22com.puppycrawl.tools%22%20AND%20a%3A%22checkstyle%22](http://search.maven.org/#search|gav|1|g%3A%22com.puppycrawl.tools%22%20AND%20a%3A%22checkstyle%22)

- Intellij idea 插件：[https://plugins.jetbrains.com/plugin/1065-checkstyle-idea](https://plugins.jetbrains.com/plugin/1065-checkstyle-idea)

- Jenkins 插件：[https://wiki.jenkins.io/display/JENKINS/Checkstyle+Plugin](https://wiki.jenkins.io/display/JENKINS/Checkstyle+Plugin)

## 4.检查项

标准 Checkstyle 检查适用于通用的Java编码风格，并不需要外部库。标准检查规则已自包含。

此外，Checkstyle 提供了许多可应用于源代码检查的项目。如下是按功能组织的说明。

#### 4.1 注释（Annotations）

##### 4.1 AnnotationLocation
##### 4.1.2 AnnotationOnSameLine
##### 4.1.3 AnnotationUseStyle
##### 4.1.4 MissingDeprecated
##### 4.1.5 MissingOverride
##### 4.1.6 PackageAnnotation
##### 4.1.7 SuppressWarnings
##### 4.1.8 SuppressWarningsHolder


#### 4.2 代码块（Block Checks）

##### 4.2.1 AvoidNestedBlocks（避免内嵌代码块）

自 Checkstyle 3.1 引入。

发现嵌套的代码块，即在代码中自由使用的代码块。

原理：嵌套的代码块常常是调试过程的残留代码，通常会对阅读者产生困扰。

例如，这项检查如下代码中废弃的括号

	public void guessTheOutput()
	{
	  int whichIsWhich = 0;
	  {
	      int whichIsWhich = 2;
	  }
	  System.out.println("value = " + whichIsWhich);
	}

以及调试/重构残留，如：

	// if (conditionThatIsNotUsedAnyLonger)
	{
	  System.out.println("unconditional");
	}

对于 switch 语句中的 case 而言并不隐式地形成代码块。因此为了能够引入 case 范围内的本地变量则有必要形成一个嵌套代码块。可通过设置 allowInSwitchCase 属性为 true 来将 case 中的所有语句视为合法代码块。

	switch (a)
	{
	  case 0:
	    // Never OK, break outside block
	    {
	      x = 1;
	    }
	    break;
	  case 1:
	    // Never OK, statement outside block
	    System.out.println("Hello");
	    {
	      x = 2;
	      break;
	    }
	  case 1:
	    // OK if allowInSwitchCase is true
	    {
	      System.out.println("Hello");
	      x = 2;
	      break;
	    }
	}

**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
allowInSwitchCase | 允许 case 语句中的内嵌代码块 | Boolean |   false  | 3.2

**示例配置**

检查配置

	<module name="AvoidNestedBlocks"/>

**错误消息**

	block.nested

**Package**

com.puppycrawl.tools.checkstyle.checks.blocks

**父模块**

 TreeWalker

##### 4.2.2 EmptyBlock
##### 4.2.3 EmptyCatchBlock

##### 4.2.4 LeftCurly（左花括号位置）

自 Checkstyle 3.1 引入。

检查代码块中左花括号 ('{') 的位置。该策略通过 option 属性控制字段来定义规则。


**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
option | 左花括号放置的位置 | 左括号策略 |   eol  | 3.0
ignoreEnums | 如果值为 true，则在 eol 策略下忽略枚举型 | Boolean | true | 6.9
tokens | 待检查的 tokens | subset of tokens INTERFACE_DEF, CLASS_DEF, ANNOTATION_DEF, ENUM_DEF, CTOR_DEF, METHOD_DEF, ENUM_CONSTANT_DEF, LITERAL_WHILE, LITERAL_TRY, LITERAL_CATCH, LITERAL_FINALLY, LITERAL_SYNCHRONIZED, LITERAL_SWITCH, LITERAL_DO, LITERAL_IF, LITERAL_ELSE, LITERAL_FOR, STATIC_INIT, OBJBLOCK, LAMBDA. | INTERFACE_DEF, CLASS_DEF, ANNOTATION_DEF, ENUM_DEF, CTOR_DEF, METHOD_DEF, ENUM_CONSTANT_DEF, LITERAL_WHILE, LITERAL_TRY, LITERAL_CATCH, LITERAL_FINALLY, LITERAL_SYNCHRONIZED, LITERAL_SWITCH, LITERAL_DO, LITERAL_IF, LITERAL_ELSE, LITERAL_FOR, STATIC_INIT, OBJBLOCK, LAMBDA. | 3.0

**左括号策略**

这个属性表示检查左花括号的位置。如下表格描述了合法的 options：

eol(end of line)： 左括号必须在行尾。例如：

	if (condition) {
	   ...

nl(new line) ： 左括号必须在新行。例如：

    if (condition)
    {
        ...

nlow(new line on wrap) ： 如果语句/表达式/声明 连接的左花括号跨越了多行，则使用 nl 规则。否则使用 eol 规则。nlow 全称是 "new line on wrap"。该规则下如下代码合法:

    if (condition) {
        ...

如果一个语句跨多行，则 Checkstyle 将认为如下代码合法：

    if (condition1 && condition2 &&
        condition3 && condition4)
    {
        ...

**示例配置**

检查配置

	<module name="LeftCurly"/>

配置一个使用 nl 策略

	<module name="LeftCurly">
	  <property name="option" value="nl"/>
	  <property name="tokens" value="CLASS_DEF,INTERFACE_DEF"/>
	</module>

配置一个检查枚举值定义的例子

	<module name="LeftCurly">
	  <property name="ignoreEnums" value="false"/>
	</module>
        
**错误消息**

	line.break.after
	line.new
	line.previous

**Package**

com.puppycrawl.tools.checkstyle.checks.blocks

**父模块**

 TreeWalker

##### 4.2.5 NeedBraces（是否需要花括号）

自 Checkstyle 3.0 引入。

检查代码块中的花括号。

**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
allowSingleLineStatement | 允许单行语句无花括号 | Boolean |   false  | 6.5
allowEmptyLoopBody | 允许没有执行体的循环 | Boolean | false | 6.12.1
tokens | 待检查的 tokens | subset of tokens LITERAL_DO, LITERAL_ELSE, LITERAL_FOR, LITERAL_IF, LITERAL_WHILE, LITERAL_CASE, LITERAL_DEFAULT, LAMBDA. | LITERAL_DO, LITERAL_ELSE, LITERAL_FOR, LITERAL_IF, LITERAL_WHILE. | 3.0

**示例配置**

检查配置

	<module name="NeedBraces"/>

配置检查 if 和 else 代码块需要花括号的策略

	<module name="NeedBraces">
	  <property name="tokens" value="LITERAL_IF, LITERAL_ELSE"/>
	</module>

配置允许单行无花括号 (if, while, do-while, for) 的配置

	<module name="NeedBraces">
	  <property name="allowSingleLineStatement" value="true"/>
	</module>

则如下代码块合法:

	if (obj.isValid()) return true; // OK
	while (obj.isValid()) return true; // OK
	do this.notify(); while (o != null); // OK
	for (int i = 0; ; ) this.notify(); // OK

配置允许 case, default 单行代码无花括号，则：

	<module name="NeedBraces">
	  <property name="tokens" value="LITERAL_CASE, LITERAL_DEFAULT"/>
	  <property name="allowSingleLineStatement" value="true"/>
	</module>

则如下代码块合法:

	switch (num) {
	  case 1: counter++; break; // OK
	  case 6: counter += 10; break; // OK
	  default: counter = 100; break; // OK
	}

配置允许循环无循环体:

	<module name="NeedBraces">
	  <property name="allowEmptyLoopBody" value="true"/>
	</module>
          
则如下代码块合法:

	while (value.incrementValue() < 5); // OK
	for(int i = 0; i < 10; value.incrementValue()); // OK

        
**错误消息**

	needBraces

**Package**

com.puppycrawl.tools.checkstyle.checks.blocks

**父模块**

 TreeWalker

##### 4.2.6 RightCurly

#### 4.3 类设计（Class Design）

##### 4.3.1 DesignForExtension
##### 4.3.2 FinalClass
##### 4.3.3 HideUtilityClassConstructor
##### 4.3.4 InnerTypeLast
##### 4.3.5 InterfaceIsType
##### 4.3.6 MutableException
##### 4.3.7 OneTopLevelClass
##### 4.3.8 ThrowsCount
##### 4.3.9 VisibilityModifier


#### 4.4 编码（Coding）

##### 4.4.1 ArrayTrailingComma
##### 4.4.2 AvoidInlineConditionals
##### 4.4.3 CovariantEquals
##### 4.4.4 DeclarationOrder
##### 4.4.5 DefaultComesLast
##### 4.4.6 EmptyStatement
##### 4.4.7 EqualsAvoidNull
##### 4.4.8 EqualsHashCode
##### 4.4.9 ExplicitInitialization
##### 4.4.10 FallThrough
##### 4.4.11 FinalLocalVariable
##### 4.4.12 HiddenField
##### 4.4.13 IllegalCatch
##### 4.4.14 IllegalInstantiation
##### 4.4.15 IllegalThrows
##### 4.4.16 IllegalToken
##### 4.4.17 IllegalTokenText
##### 4.4.18 IllegalType
##### 4.4.19 InnerAssignment
##### 4.4.20  MagicNumber
##### 4.4.21 MissingCtor
##### 4.4.22 MissingSwitchDefault
##### 4.4.23 ModifiedControlVariable
##### 4.4.24 MultipleStringLiterals
##### 4.4.25 MultipleVariableDeclarations
##### 4.4.26 NestedForDepth
##### 4.4.27 NestedIfDepth
##### 4.4.28 NestedTryDepth
##### 4.4.29 NoClone
##### 4.4.30 NoFinalizer
##### 4.4.31 OneStatementPerLine
##### 4.4.32 OverloadMethodsDeclarationOrder
##### 4.4.33 PackageDeclaration
##### 4.4.34 ParameterAssignment
##### 4.4.35 RequireThis
##### 4.4.36 ReturnCount
##### 4.4.37 SimplifyBooleanExpression
##### 4.4.38 SimplifyBooleanReturn
##### 4.4.39 StringLiteralEquality
##### 4.4.40 SuperClone
##### 4.4.41 SuperFinalize
##### 4.4.42 UnnecessaryParentheses
##### 4.4.43 VariableDeclarationUsageDistance


#### 4.5 文件头（Headers）

##### 4.5.1 Header
##### 4.5.2 RegexpHeader


#### 4.6 导入（Imports）

##### 4.6.1 AvoidStarImport
##### 4.6.2 AvoidStaticImport
##### 4.6.3 CustomImportOrder
##### 4.6.4 IllegalImport
##### 4.6.5 ImportControl
##### 4.6.6 ImportOrder
##### 4.6.7 RedundantImport
##### 4.6.8 UnusedImports


#### 4.7 Javadoc注释（Javadoc Comments）

##### 4.7.1 AtclauseOrder
##### 4.7.2 JavadocMethod
##### 4.7.3 JavadocPackage
##### 4.7.4 JavadocParagraph
##### 4.7.5 JavadocStyle
##### 4.7.6 JavadocTagContinuationIndentation
##### 4.7.7 JavadocType
##### 4.7.8 JavadocVariable
##### 4.7.9 NonEmptyAtclauseDescription
##### 4.7.10 SingleLineJavadoc
##### 4.7.11 SummaryJavadoc
##### 4.7.12 WriteTag

#### 4.8 度量（Metrics）

##### 4.8.1 BooleanExpressionComplexity
##### 4.8.2 ClassDataAbstractionCoupling
##### 4.8.3 ClassFanOutComplexity
##### 4.8.4 CyclomaticComplexity
##### 4.8.5 JavaNCSS
##### 4.8.6 NPathComplexity

#### 4.9 杂项（Miscellaneous）

##### 4.9.1 ArrayTypeStyle
##### 4.9.2 AvoidEscapedUnicodeCharacters
##### 4.9.3 CommentsIndentation
##### 4.9.4 DescendantToken
##### 4.9.5 FinalParameters
##### 4.9.6 Indentation
##### 4.9.7 NewlineAtEndOfFile
##### 4.9.8 OuterTypeFilename
##### 4.9.9 TodoComment
##### 4.9.10 TrailingComment
##### 4.9.11 Translation
##### 4.9.12 UncommentedMain
##### 4.9.13 UniqueProperties
##### 4.9.14 UpperEll

#### 4.10 修饰符（Modifiers）

##### 4.1.10.1 ModifierOrder
##### 4.1.10.2 RedundantModifier


#### 4.11 命名规约（Naming Conventions）

##### 4.11.1 Overview
##### 4.11.2 AbbreviationAsWordInName
##### 4.11.3 AbstractClassName
##### 4.11.4 CatchParameterName
##### 4.11.5 ClassTypeParameterName
##### 4.11.6 ConstantName
##### 4.11.7 InterfaceTypeParameterName
##### 4.11.8 LocalFinalVariableName
##### 4.11.9 LocalVariableName
##### 4.11.10 MemberName
##### 4.11.11 MethodName
##### 4.11.12 MethodTypeParameterName
##### 4.11.13 PackageName
##### 4.11.14 ParameterName
##### 4.11.15 StaticVariableName
##### 4.11.16 TypeName


#### 4.12 正则表达式（Regexp）

##### 4.12.1 Regexp
##### 4.12.2 RegexpMultiline
##### 4.12.3 RegexpOnFilename
##### 4.12.4 RegexpSingleline
##### 4.12.5 RegexpSinglelineJava


#### 4.13 规模违例（Size Violations）

##### 4.13.1 AnonInnerLength (检查：匿名内部类的长度)

自 Checkstyle 3.2 引入。

检查匿名内部类的超长长度。

原理：如果一个匿名内部类超长，以至于难以理解其类中定义的方法逻辑流程。则该长的匿名内部类通常就应该被重构为一个命名的内部类。

**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
max | 允许最长的行数 | Integer |   20  | 3.2

**示例配置**

检查代码行数最长长度值为 60 行

	<module name="AnonInnerLength">
	  <property name="max" value="60"/>
	</module>

**错误消息**

	maxLen.anonInner

CheckStyle 所有消息可以定制，如果默认的消息不符合实际需要则可以可以参考文档 4.3.1 进行自定义。

##### 4.13.2 ExecutableStatementCount（检查：可执行语句数量）

自 Checkstyle 3.2 引入。

限制某范围内可执行语句的数量。

**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
max | 允许最长的语句数 | Integer |   30  | 3.2
tokens | 检查的 tokens | 这些类型 Token 的子集：CTOR_DEF, METHOD_DEF, INSTANCE_INIT, STATIC_INIT. |   CTOR_DEF, METHOD_DEF, INSTANCE_INIT, STATIC_INIT.  | 3.2

- CTOR_DEF：构造函数定义
- METHOD_DEF：方法定义
- INSTANCE_INIT：实例初始化器（instance initializer）
- STATIC_INIT：静态初始化块

**示例配置**

直接配置检查项:
	
	<module name="ExecutableStatementCount"/>
	        
为构造函数和方法定义，配置 20 行可执行代码行数限制的检查项：
	
	<module name="ExecutableStatementCount">
	  <property name="max" value="20"/>
	  <property name="tokens" value="CTOR_DEF,METHOD_DEF"/>
	</module>

**错误消息**

	executableStatementCount

##### 4.13.3 FileLength（检查：文件长度）

自 Checkstyle 5.0 引入。

检查行数很多的源文件。

原由：如果一个源代码文件变得非常长以至于难以理解，则有必要将其重构为聚焦在一个特殊任务的几个独立类。

**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
max | 允许最长的行数 | Integer |   2000  | 3.2
fileExtensions | 检查的文件类型扩展名 | String Set |   all files  | 5.0

**示例配置**

配置允许最多 1500 行代码的检查项:
	
	<module name="FileLength">
	  <property name="max" value="1500"/>
	</module>

**错误消息**

	maxLen.file

##### 4.13.4 LineLength（检查：单行长度）

自 Checkstyle 5.0 引入。

检查单行很长的源文件。

原由：长行是很难阅读的，不管是在打印输出时，或是开发人员查看源码的屏幕空间有限（例如 IDE 显示附加的信息，如项目树、类层次结构等）。

**属性清单**

名称 |     描述     | 类型    | 默认值 | 引入版本
----|--------------|---------|-------|------
ignorePattern | 忽略的行模式 | Regular Expression |   "^$"  | 3.0
max | 允许的单行最长长度 | Integer |   80  | 3.0

**示例配置**

配置允许单行最长 120 个字符的检查项:

	<module name="LineLength">
	  <property name="max" value="120"/>
	</module>

配置忽略检查哪些以" * "开头且紧跟一个词的行（比如在 Javadoc 注释中的行）

	<module name="LineLength">
	  <property name="ignorePattern" value="^ *\* *[^ ]+$"/>
	</module>

**注意**

计算行长度时，将一个 tab 字符（'\t'） 展开的空格纳入计算结果中。默认空格数是 8。可以通过对 TreeWalker 属性 tabWidth 进行空格展开数量的全局检查设置；也可以单独为 LineLength 单个进行设置并检查。

Package 和 import 语句（符合模式 " ^(package|import) .*"）不会纳入检查。

**错误消息**

	maxLineLen

##### 4.13.5 MethodCount
##### 4.13.6 MethodLength
##### 4.13.7 OuterTypeNumber
##### 4.13.8 ParameterNumber


#### 4.14 空格（Whitespace）

##### 4.14.1 EmptyForInitializerPad
##### 4.14.2 EmptyForIteratorPad
##### 4.14.3 EmptyLineSeparator
##### 4.14.4 FileTabCharacter
##### 4.14.5 GenericWhitespace
##### 4.14.6 MethodParamPad
##### 4.14.7 NoLineWrap
##### 4.14.8 NoWhitespaceAfter
##### 4.14.9 NoWhitespaceBefore
##### 4.14.10 OperatorWrap
##### 4.14.11 ParenPad
##### 4.14.12 SeparatorWrap
##### 4.14.13 SingleSpaceSeparator
##### 4.14.14 TypecastParenPad
##### 4.14.15 WhitespaceAfter
##### 4.14.16 WhitespaceAround

### 4.2 常用规范集

#### 4.2.1 Google 规范

#### 4.2.2 Sun 规范

### 4.3 配置

#### 4.3.1 个性化消息
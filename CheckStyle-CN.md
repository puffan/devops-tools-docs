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

## 4.文档

### 4.1 检查项

标准 Checkstyle 检查适用于通用的Java编码风格，并不需要外部库。标准检查规则已自包含。

此外，Checkstyle 提供了许多可应用于源代码检查的项目。如下是按功能组织的说明。

#### 4.1.1 注释（Annotations）

##### 4.1.1.1 AnnotationLocation
##### 4.1.1.2 AnnotationOnSameLine
##### 4.1.1.3 AnnotationUseStyle
##### 4.1.1.4 MissingDeprecated
##### 4.1.1.5 MissingOverride
##### 4.1.1.6 PackageAnnotation
##### 4.1.1.7 SuppressWarnings
##### 4.1.1.8 SuppressWarningsHolder


#### 4.1.2 代码块（Block Checks）

##### 4.1.2.1 AvoidNestedBlocks
##### 4.1.2.2 EmptyBlock
##### 4.1.2.3 EmptyCatchBlock
##### 4.1.2.4 LeftCurly
##### 4.1.2.5 NeedBraces
##### 4.1.2.6 RightCurly


#### 4.1.3 类设计（Class Design）

##### 4.1.3.1 DesignForExtension
##### 4.1.3.2 FinalClass
##### 4.1.3.3 HideUtilityClassConstructor
##### 4.1.3.4 InnerTypeLast
##### 4.1.3.5 InterfaceIsType
##### 4.1.3.6 MutableException
##### 4.1.3.7 OneTopLevelClass
##### 4.1.3.8 ThrowsCount
##### 4.1.3.9 VisibilityModifier


#### 4.1.4 编码（Coding）

##### 4.1.4.1 ArrayTrailingComma
##### 4.1.4.2 AvoidInlineConditionals
##### 4.1.4.3 CovariantEquals
##### 4.1.4.4 DeclarationOrder
##### 4.1.4.5 DefaultComesLast
##### 4.1.4.6 EmptyStatement
##### 4.1.4.7 EqualsAvoidNull
##### 4.1.4.8 EqualsHashCode
##### 4.1.4.9 ExplicitInitialization
##### 4.1.4.10 FallThrough
##### 4.1.4.11 FinalLocalVariable
##### 4.1.4.12 HiddenField
##### 4.1.4.13 IllegalCatch
##### 4.1.4.14 IllegalInstantiation
##### 4.1.4.15 IllegalThrows
##### 4.1.4.16 IllegalToken
##### 4.1.4.17 IllegalTokenText
##### 4.1.4.18 IllegalType
##### 4.1.4.19 InnerAssignment
##### 4.1.4.20  MagicNumber
##### 4.1.4.21 MissingCtor
##### 4.1.4.22 MissingSwitchDefault
##### 4.1.4.23 ModifiedControlVariable
##### 4.1.4.24 MultipleStringLiterals
##### 4.1.4.25 MultipleVariableDeclarations
##### 4.1.4.26 NestedForDepth
##### 4.1.4.27 NestedIfDepth
##### 4.1.4.28 NestedTryDepth
##### 4.1.4.29 NoClone
##### 4.1.4.30 NoFinalizer
##### 4.1.4.31 OneStatementPerLine
##### 4.1.4.32 OverloadMethodsDeclarationOrder
##### 4.1.4.33 PackageDeclaration
##### 4.1.4.34 ParameterAssignment
##### 4.1.4.35 RequireThis
##### 4.1.4.36 ReturnCount
##### 4.1.4.37 SimplifyBooleanExpression
##### 4.1.4.38 SimplifyBooleanReturn
##### 4.1.4.39 StringLiteralEquality
##### 4.1.4.40 SuperClone
##### 4.1.4.41 SuperFinalize
##### 4.1.4.42 UnnecessaryParentheses
##### 4.1.4.43 VariableDeclarationUsageDistance


#### 4.1.5 文件头（Headers）

##### 4.1.5.1 Header
##### 4.1.5.2 RegexpHeader


#### 4.1.6 导入（Imports）

##### 4.1.6.1 AvoidStarImport
##### 4.1.6.2 AvoidStaticImport
##### 4.1.6.3 CustomImportOrder
##### 4.1.6.4 IllegalImport
##### 4.1.6.5 ImportControl
##### 4.1.6.6 ImportOrder
##### 4.1.6.7 RedundantImport
##### 4.1.6.8 UnusedImports


#### 4.1.7 Javadoc注释（Javadoc Comments）

##### 4.1.7.1 AtclauseOrder
##### 4.1.7.2 JavadocMethod
##### 4.1.7.3 JavadocPackage
##### 4.1.7.4 JavadocParagraph
##### 4.1.7.5 JavadocStyle
##### 4.1.7.6 JavadocTagContinuationIndentation
##### 4.1.7.7 JavadocType
##### 4.1.7.8 JavadocVariable
##### 4.1.7.9 NonEmptyAtclauseDescription
##### 4.1.7.10 SingleLineJavadoc
##### 4.1.7.11 SummaryJavadoc
##### 4.1.7.12 WriteTag

#### 4.1.8 度量（Metrics）

##### 4.1.8.1 BooleanExpressionComplexity
##### 4.1.8.2 ClassDataAbstractionCoupling
##### 4.1.8.3 ClassFanOutComplexity
##### 4.1.8.4 CyclomaticComplexity
##### 4.1.8.5 JavaNCSS
##### 4.1.8.6 NPathComplexity

#### 4.1.9 杂项（Miscellaneous）

##### 4.1.9.1 ArrayTypeStyle
##### 4.1.9.2 AvoidEscapedUnicodeCharacters
##### 4.1.9.3 CommentsIndentation
##### 4.1.9.4 DescendantToken
##### 4.1.9.5 FinalParameters
##### 4.1.9.6 Indentation
##### 4.1.9.7 NewlineAtEndOfFile
##### 4.1.9.8 OuterTypeFilename
##### 4.1.9.9 TodoComment
##### 4.1.9.10 TrailingComment
##### 4.1.9.11 Translation
##### 4.1.9.12 UncommentedMain
##### 4.1.9.13 UniqueProperties
##### 4.1.9.14 UpperEll

#### 4.1.10 修饰符（Modifiers）

##### 4.1.10.1 ModifierOrder
##### 4.1.10.2 RedundantModifier


#### 4.1.11 命名规约（Naming Conventions）

##### 4.1.11.1 Overview
##### 4.1.11.2 AbbreviationAsWordInName
##### 4.1.11.3 AbstractClassName
##### 4.1.11.4 CatchParameterName
##### 4.1.11.5 ClassTypeParameterName
##### 4.1.11.6 ConstantName
##### 4.1.11.7 InterfaceTypeParameterName
##### 4.1.11.8 LocalFinalVariableName
##### 4.1.11.9 LocalVariableName
##### 4.1.11.10 MemberName
##### 4.1.11.11 MethodName
##### 4.1.11.12 MethodTypeParameterName
##### 4.1.11.13 PackageName
##### 4.1.11.14 ParameterName
##### 4.1.11.15 StaticVariableName
##### 4.1.11.16 TypeName


#### 4.1.12 正则表达式（Regexp）

##### 4.1.12.1 Regexp
##### 4.1.12.2 RegexpMultiline
##### 4.1.12.3 RegexpOnFilename
##### 4.1.12.4 RegexpSingleline
##### 4.1.12.5 RegexpSinglelineJava


#### 4.1.13 规模违例（Size Violations）

##### 4.1.13.1 AnonInnerLength (检查：匿名内部类的长度)

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

##### 4.1.13.2 ExecutableStatementCount

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

##### 4.1.13.3 FileLength
##### 4.1.13.4 LineLength
##### 4.1.13.5 MethodCount
##### 4.1.13.6 MethodLength
##### 4.1.13.7 OuterTypeNumber
##### 4.1.13.8 ParameterNumber


#### 4.1.14 空格（Whitespace）

##### 4.1.14.1 EmptyForInitializerPad
##### 4.1.14.2 EmptyForIteratorPad
##### 4.1.14.3 EmptyLineSeparator
##### 4.1.14.4 FileTabCharacter
##### 4.1.14.5 GenericWhitespace
##### 4.1.14.6 MethodParamPad
##### 4.1.14.7 NoLineWrap
##### 4.1.14.8 NoWhitespaceAfter
##### 4.1.14.9 NoWhitespaceBefore
##### 4.1.14.10 OperatorWrap
##### 4.1.14.11 ParenPad
##### 4.1.14.12 SeparatorWrap
##### 4.1.14.13 SingleSpaceSeparator
##### 4.1.14.14 TypecastParenPad
##### 4.1.14.15 WhitespaceAfter
##### 4.1.14.16 WhitespaceAround

### 4.2 常用规范集

#### 4.2.1 Google 规范

#### 4.2.2 Sun 规范

### 4.3 配置

#### 4.3.1 个性化消息
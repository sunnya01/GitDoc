# IDEA教程

### 1，JDK相关设置

1.1 项目的JDK设置

 `File-->Project Structure...-->Platform Settings -->SDKs`

SDKs全称是Software Development Kit ，这里一定是选择JDK的安装根目录，不是JRE的目录。

这里还可以从本地添加多个JDK。使用“+”即可实现。

1.2 out目录和编译版本

`File-->Project Structure...-->Project Settings -->Project`

name：项目名

SDK：Java版本，一般都是Java8

language level：idea独有的设置。Java不同版本有不同的新特性。有时候我们用到了SDK8，但是并没有用到Java8新特性。就可以在这里进行设置，降低版本，比如选Java7。但是选了Java7，项目后续如果用到了Java8，即使SDK是Java8，也会编译错误，一般选择和SDK保持一致。

Compiler output：项目编译out目录。

### 2，详细设置

打开设置的方法：

`File-->Settings`

以下的方法都是通过此方法进入设置页。

#### 2.1，默认启动项目配置

`Settings-->Appearance & Behavior-->System Settings`

启动IDEA时，默认自动打开上次开发的项目。 如果去掉`Reopen last project on startup`前面的对勾，每次启动IDEA就会出现欢迎页。

#### 2.2，取消自动更新

`Settings-->Appearance & Behavior->System Settings--> Updates`

默认都打√了，建议检查IDE更新（check IDE updates for）的√去掉，检查插件更新的√选上。

#### 2.3，设置主题

`Settings-->Appearance & Behavior-->Appearance `

- Theme：主题，可以在这里选择不同的自带主题。
- Use custom font：菜单和窗口的字体
- Size：菜单和窗口的字体大小
- UI Options：
  - Background Image ：背景图。可以设置idea编程页面的背景图，比如美少女的图。就像QQ微信的聊天背景一样。

#### 2.4 编译器样式

**1，编译器主题**

`Settings-->Editor-->Color Scheme `

在此设置路径处设置，不要到下一级。直接选中Color Scheme就好了。

Scheme：可以选择不同的编译器主题。

**2，编译器字体和颜色**

`Settings-->Editor-->Color Scheme `

在此此设置路径的下一级，有很多具体的设置选择：

- Color Scheme Font：编译器字体和大小
- Cosole Font：控制台字体
- Cosole Colors：控制台颜色
- Debuggger：Debug相关的颜色和字体
- Java：Java相关字体颜色

温馨提示：如果选择某个font字体，中文乱码，可以在fallback font（备选字体）中选择一个支持中 文的字体。

**3，注释的字体颜色**

`Settings-->Editor-->Color Scheme-->Language Defaults `

在此设置中，有很多选项，我们可以关注一下三个：

- Block comment：修改多行注释的字体颜色 
- Doc Comment –> Text：修改文档注释的字体颜色 
- Line comment：修改单行注释的字体颜色

#### 2.5  显示行号与方法分隔符

`Settings-->Editor-->General-->Appearance  `

在此设置中，以下两个控制行号和方法分隔符

- show line numbers：显示行号
- show method separators：显示方法之间的分隔符

#### 2.6 代码智能提示功能

`Settings-->Editor-->General-->Code Completion  `

取消 **Match case** 的勾选即可，可以忽略大小写匹配。

IntelliJ IDEA 的代码提示和补充功能有一个特性： 区分大小写 。 如果想不区分大小写的话，就把这个对 勾去掉。 建议去掉勾选 。

#### 2.7 自动导包

idea 默认手动导包：Alt+Enter

自动导包：

`Settings-->Editor-->General-->Auto Import  `

选中如下两个设置：

- Add unambiguous import on the fly
- Optimize imports on the fly

#### 2.8 设置项目文件编码☆

我们很多错误，不是因为代码，而是编码！！！，特别是我们中文用户，请一定要设置！！！

`Settings-->Editor-->File Encodings`

有四个设置：

- global  encodings：UTF-8
- project encodings：UTF-8
- default encodings for properties files：UTF-8
  - Transparent native-to-ascii conversion主要用于转换ascii，显式原生内容。一般都要勾选。
- create UTF-8 files：with NO BOM 

#### 2.9 设置控制台的字符编码

`Settings-->Editor-->General-->Console  `

选择此设置

Default Encoding：UTF-8

#### 2.10 修改类头的文档注释信息

`Settings-->Editor-->File and Code Templates`

选择窗口中的Includes→File Header

如下：

```
/**
 * 
 * @author xunziqing
 * @date ${YEAR}/${MONTH}/${DAY} ${HOUR}:${MINUTE}
 * @version 1.0.0
 **/
```

效果如下，每当创建文件时，开头会附带一些信息：

```
/**
 * 
 * @author xunziqing
 * @date 2022/11/03 09:26
 * @version 1.0.0
 **/
```

### 3，工程与模块管理

#### 3.1  IDEA项目结构

层级关系：

```
project(工程) - module(模块) - package(包) - class(类)
```

具体的：

```
一个project中可以创建多个module
一个module中可以创建多个package
一个package中可以创建多个class
```

这些结构的划分，是为了方便管理功能代码。

#### 3.2  Project和Module的概念

在 IntelliJ IDEA 中，提出了Project和Module这两个概念。

在 IntelliJ IDEA 中Project是 最顶级的结构单元 ，然后就是Module。目前，主流的大型项目结构基本都是 多Module的结构，这类项目一般是 按功能划分 的，比如：user-core-module、user-facade-module和userhessian-module等等，模块之间彼此可以 相互依赖 ，有着不可分割的业务关系。因此，对于一个Project 来说：

- 当为单Module项目的时候，这个单独的Module实际上就是一个Project。 
- 当为多Module项目的时候，多个模块处于同一个Project之中，此时彼此之间具有 互相依赖 的关联 关系。 
- 当然多个模块没有建立依赖关系的话，也可以作为单独一个“小项目”运行。

#### 3.3 创建Module

建议创建“Empty空工程”，然后创建多模块，每一个模块可以独立运行，相当于一个小项目。JavaSE阶段 不涉及到模块之间的依赖。后期再学习模块之间的依赖。

1，创建一个空项目

idea点击左上角file，选中new → file 。选择 Empty Project。

命名修改，一气呵成。

2，创建Module 

在创建的空项目上，右键 new → Module → Maven   （有需求可以选择Maven Archetype 利用模板创建）

命名修改，一气呵成

**Project 和 Module的区别:**

（1）、IDEA中的Project可以被理解成当前工作空间，而每一个Module就是这个工作空间里的工作项目。Project既是最顶层的结构单元——起了目录的作用，也是最底层的工作环境——各个Module在上面工作。

（2）、一个Project中可以定义多个Module，Project与各个Module之间属于父子关系，各个Module之间则属于兄弟关系

#### 3.4 移除模块

1，移除模块（逻辑删除）

选中我们要删除的模块右键-->Remove Module 

然后在弹出的窗口中，选择Remove 即可。

2，物理删除

选中我们要删除的模块右键-->Delete

#### 3.5 导入其他模块

1，讲模块文件夹放到项目的文件夹内，与其他模块平级。

2，打开项目，就可以看到导入的模块，不过是一个普通文件夹

3，打开File -->Project Structure-->Modules-->Import Module

4，选中我们导入的文件夹。

5，接着可以一路Next下去，最后选择Overwrite。

### 4，常用代码模板

#### 4.1 非空判断

- 变量.null：if(变量 == null) 
- 变量.nn：if(变量 != null) 
- 变量.notnull：if(变量 != null) 
- ifn：if(xx == null) 
- inn：if(xx != null)

#### 4.2 遍历数组和集合

- 数组或集合变量.fori：for循环 
- 数组或集合变量.for：增强for循环 
- 数组或集合变量.forr：反向for循环 
- 数组或集合变量.iter：增强for循环遍历数组或集合

#### 4.3 输出语句

- sout：相当于System.out.println 
- soutm：打印当前方法的名称 
- soutp：打印当前方法的形参及形参对应的实参值 
- soutv：打印方法中声明的最近的变量的值 
- 变量.sout：打印当前变量值 
- 变量.soutv：打印当前变量名及变量值

#### 4.4 对象操作

- 创建对象
  - Xxx.new .var ：创建Xxx类的对象，并赋给相应的变量
  - Xxx.new .field：会将方法内刚创建的Xxx对象抽取为一个属性
- 强转
  - 对象.cast：将对象进行强转
  - 对象.castvar：将对象强转后，并赋给一个变量

#### 4.5 静态常量声明

- psf：public static final 
- psfi：public static final int 
- psfs：public static final String 
- prsf：private static final

PSVM：如下：

```
public static void main(String[] args) {
    
}
```

### 5，快捷键

#### 5.1 通用型

| 说明            | 快捷键           |
| --------------- | ---------------- |
| 复制代码-copy   | ctrl + c         |
| 粘贴-paste      | ctrl + v         |
| 剪切-cut        | ctrl + x         |
| 撤销-undo       | ctrl + z         |
| 反撤销-redo     | ctrl + shift + z |
| 保存-save all   | ctrl + s         |
| 全选-select all | ctrl + a         |

#### 5.2 提高编写速度（上

| 说明                                               | 快捷键           |
| -------------------------------------------------- | ---------------- |
| 智能提示-edit                                      | alt + enter      |
| 提示代码模板-insert live template                  | ctrl+j           |
| 使用xx块环绕-surround with ...                     | ctrl+alt+t       |
| 调出生成getter/setter/构造器等结构-generate ...    | alt+insert       |
| 自动生成返回值变量-introduce variable ...          | ctrl+alt+v       |
| 复制指定行的代码-duplicate line or selection       | ctrl+d           |
| 删除指定行的代码-delete line                       | ctrl+y           |
| 切换到下一行代码空位-start new line                | shift + enter    |
| 切换到上一行代码空位-start new line before current | ctrl +alt+ enter |
| 向上移动代码-move statement up                     | ctrl+shift+↑     |
| 向下移动代码-move statement down                   | ctrl+shift+↓     |
| 向上移动一行-move line up                          | alt+shift+↑      |
| 向下移动一行-move line down                        | alt+shift+↓      |
| 方法的形参列表提醒-parameter info                  | ctrl+p           |

#### 5.3 提高编写速度（下

| 说明                                        | 快捷键       |
| ------------------------------------------- | ------------ |
| 批量修改指定的变量名、方法名、类名等-rename | shift+f6     |
| 抽取代码重构方法-extract method ...         | ctrl+alt+m   |
| 重写父类的方法-override methods ...         | ctrl+o       |
| 实现接口的方法-implements methods ...       | ctrl+i       |
| 选中的结构的大小写的切换-toggle case        | ctrl+shift+u |
| 批量导包-optimize imports                   | ctrl+alt+o   |

#### 5.4 类结构、查找和查看源码

| 说明                                                      | 快捷键                          |
| --------------------------------------------------------- | ------------------------------- |
| 如何查看源码-go to class...                               | ctrl + 选中指定的结构 或 ctrl+n |
| 显示当前类结构，支持搜索指定的方法、属性等-file structure | ctrl+f12                        |
| 退回到前一个编辑的页面-back                               | ctrl+alt+←                      |
| 进入到下一个编辑的页面-forward                            | ctrl+alt+→                      |
| 打开的类文件之间切换-select previous/next tab             | alt+←/→                         |
| 光标选中指定的类，查看继承树结构-Type Hierarchy           | ctrl+h                          |
| 查看方法文档-quick documentation                          | ctrl+q                          |
| 类的UML关系图-show uml popup                              | ctrl+alt+u                      |
| 定位某行-go to line/column                                | ctrl+g                          |
| 回溯变量或方法的来源-go to implementation(s)              | ctrl+alt+b                      |
| 折叠方法实现-collapse all                                 | ctrl+shift+ -                   |
| 展开方法实现-expand all                                   | ctrl+shift+ +                   |

#### 5.5 查找、替换与关闭

| 说明                                               | 快捷键       |
| -------------------------------------------------- | ------------ |
| 查找指定的结构                                     | ctlr+f       |
| 快速查找：选中的Word快速定位到下一个-find next     | ctrl+l       |
| 查找与替换-replace                                 | ctrl+r       |
| 直接定位到当前行的首位-move caret to line start    | home         |
| 直接定位到当前行的末位 -move caret to line end     | end          |
| 查询当前元素在当前文件中的引用，然后按 F3 可以选择 | ctrl+f7      |
| 全项目搜索文本-find in path ...                    | ctrl+shift+f |
| 关闭当前窗口-close                                 | ctrl+f4      |

#### 5.6 调整格式

| 说明                                         | 快捷键           |
| -------------------------------------------- | ---------------- |
| 格式化代码-reformat code                     | ctrl+alt+l       |
| 使用单行注释-comment with line comment       | ctrl + /         |
| 使用/取消多行注释-comment with block comment | ctrl + shift + / |
| 选中数行，整体往后移动-tab                   | tab              |
| 选中数行，整体往前移动-prev tab              | shift + tab      |

#### 5.7 查看修改快捷键

`File-->Settings-->Keymap`

可以在这里，查询，修改并且替换。

### 6，推荐插件

如何安装？

`File-->Settings-->Plugins`

在Marketplace里搜索，然后点击install安装。

在installed里查看已经安装的插件，然后哭在这取消使用/删除。



1，Alibaba Java Coding Guidelines

阿里巴巴Java编码规范检查插件，检测代码是否存在问题，以及是否符合规范。 使用：在类中，右键，选择编码规约扫描，在下方显示扫描规约和提示。根据提示规范代码，提高代码 质量。

2，jclasslib bytecode viewer

可视化的字节码查看器。 

使用： 

1. 在 IDEA 打开想研究的类。 
2. 编译该类或者直接编译整个项目（ 如果想研究的类在 jar 包中，此步可略过）。
3. 打开“view” 菜单，选择“Show Bytecode With jclasslib” 选项。
4. 选择上述菜单项后 IDEA 中会弹出 jclasslib 工具窗口

英文设置： 在 Help -> Edit Custom VM Options …，加上

```
-Duser.language=en
```

3，Translation

注册翻译服务（有道智云、百度翻译开放平台、阿里云机器翻译）帐号，开通翻译服务并获取其应用ID 和密钥 绑定应用ID和密钥：偏好设置（设置） > 工具 > 翻译 > 常规 > 翻译引擎 > 配置… 

使用：鼠标选中文本，点击右键即可自动翻译成多国语言。 

注：请注意保管好你的应用密钥，防止其泄露。

4，Rainbow Brackets

给括号添加彩虹色，使开发者通过颜色区分括号嵌套层级，便于阅读

5，MyBatisX

一个小黑色小鸟带着蓝色眼罩。

主要是方便mybatis的开发

6，Lombok

在写代码时，可以很方便的使用它的各种注解来解决问题。
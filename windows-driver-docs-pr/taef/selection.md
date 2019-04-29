---
title: 选择
description: 选择
ms.assetid: 5DFE5B52-4D58-491c-9363-95E4A2FD680C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c427c3fac66724743d68d6096cf0423eed5566
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324783"
---
# <a name="selection"></a>选择


测试创作和执行框架 (TAEF) 提供了一种机制来有选择地运行，或忽略某些测试基于你提供的元数据信息。 以下部分介绍如何使用此选择机制与 TE.exe 的各种示例。

可以从命令提示符窗口运行 TE.exe。

``` syntax
TE <test_binaries> [/select:<selection criteria>]
```

本部分介绍 TE.exe **/选择：**<em>选择条件</em>选项。 有关 TE.exe 详细信息，请参阅[TE.exe 命令选项](te-exe-command-line-parameters.md)。

选择条件获取全局应用于在命令提示符下提及的所有测试二进制文件。 让我们考虑两个测试\_二进制文件：**示例\\CPP。SelectionCriteria1.Example.dll**并**示例\\CPP。SelectionCriteria2.Example.dll** 。 下面的示例演示属性或元数据，在这些测试中的各种级别指定\_二进制文件。 你还可以通过指定获取这 **/listproperties**命令提示符窗口中的选项。

```cpp
CPP.SelectionCriteria1.Example.dll (Owner="C1", Priority=3)
class11 (Owner="C2")
method111(Priority=1)

method112 (BackwardsCompatibility="Windows 2000")
class12
method121
CPP.SelectionCriteria2.Example.dll (Owner="WEX")
class21 (Owner="C1", Priority=2, BackwardsCompatibility="Windows XP")
method211 (Owner="C2")
class22 (Owner="U3")
method221
```

换而言之，在上述各项使用 /listproperties 测试\_二进制文件分开，则获取：

``` syntax
F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution>te Examples\CPP.SelectionCriteria1.Example.dll /listproperties
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86

F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution\Examples\CPP.SelectionCriteria1.Example.dll
        Property[Owner] = C1
        Property[Priority] = 3
    WEX::TestExecution::Examples::Class11
            Property[Owner] = C2
        WEX::TestExecution::Examples::Class11::Method111
                Property[Priority] = 1
        WEX::TestExecution::Examples::Class11::Method112
                Property[BackwardsCompatibility] = Windows2000

    WEX::TestExecution::Examples::Class12
        WEX::TestExecution::Examples::Class12::Method121
```

和：

``` syntax
F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution>te Examples\CPP.SelectionCriteria2.Example.dll /listproperties
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86

F:\fsd1.binaries.x86chk\WexTest\C1\TestExecution\Examples\CPP.SelectionCriteria2.Example.dll
        Property[Owner] = WEX
    WEX::TestExecution::Examples::Class21
            Property[BackwardsCompatibility] = Windows XP
            Property[Owner] = C1
            Property[Priority] = 2
        WEX::TestExecution::Examples::Class21::Method211
                Property[Owner] = C2

    WEX::TestExecution::Examples::Class22
            Property[Owner] = U3
        WEX::TestExecution::Examples::Class22::Method221
```

务必要注意此时该测试\_以及它们的完整路径，列出了二进制文件和类名称被列为"&lt;Namespace&gt;::&lt;ClassName&gt;"对于本机单元测试\_二进制文件和"&lt;Namespace&gt;。&lt;ClassName&gt;"在托管测试的情况下\_二进制文件。 同样，测试方法名称被列为"&lt;Namespace&gt;::&lt;ClassName&gt;::&lt;TestMethodName&gt;"本机单元测试对于\_二进制文件和"&lt;Namespace&gt;。&lt;ClassName&gt;。&lt;TestMethodName&gt;"在托管测试的情况下\_二进制文件。

换而言之，任何名称或函数的完全限定的名称是 te 中保存的内容。 这是为了使能够唯一地区分的任何方法。 有关示例，如果两个类唯一具有相同的方法名称，为类限定可帮助选择的方法对感它。 为达到此目的，仅运行这些测试在给定的测试条件相匹配选择条件有助于\_二进制文件。

在上面的示例，假设在示例中\\Cpp.SelectionCriteria1.Example.dll，可以通过任何下列选择条件中选择"Method111":

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='WEX::TestExecution::Examples::Class11::Method111'"
```

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='*Class11::Method111'"
```

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='*Method111'"
```

您可以选择"优先级"小于 2 已标记的所有测试都运行通过运行：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Priority < 2"
```

这将运行仅为示例\\CPP。SelectionCriteria1.Example.dll-在本示例中的"class11::method111"。

如果你想要运行所有测试下 class11，可以使用通配符匹配以及限定的"Name"属性来选择它，如下所示：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll
                                                               /select:"@Name='*::class11::*'"
```

在使用选择条件时，有很有用，需要注意一些事项：

-   "**并**"，"**不**"，并"**或**"是**保留**单词并**不区分大小写**。
-   **元数据属性名称和值是不区分大小写**，在示例中，示例"C2"会匹配"c2"和"C2"。 因此如果"属性"中，有一个函数的元数据，另一个具有"属性"和选择条件正在寻找"属性"，它将匹配这两种。
-   **选择查询字符串中的字符串值应包含在单引号中。在选择查询中的字符串值"？"是单个通配符字符和"\*"为 0 或更多的通配符字符。**
-   在命令提示符下，使用引号引起来时**留意弯引号时复制所选内容查询**。 如果从 Outlook 电子邮件复制所选内容查询，您可能会无意中让弯引号和 TAEF 可能无法对其进行分析。 改为键入引号。

让我们回顾的复合的选择条件，它们会执行一些快速示例。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C2' AND @Priority=2"
```

将运行：

-   示例\\CPP。SelectionCriteria2.Example.dll-class21::method211

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C2' AND @Priority=3"
```

将运行：

-   示例\\CPP。SelectionCriteria1.Example.dll-class11::method112

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='U3' oR @Priority=1"
```

将运行：

-   示例\\CPP。SelectionCriteria1.Example.dll-class11::method111
-   示例\\CPP。SelectionCriteria2.Example.dll-class22::method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"not(@BackwardsCompatibility=*)"
```

将运行所有测试 BackwardsCompatibility 值尚未指定。 （请参阅以下各项。）

-   示例\\CPP。SelectionCriteria1.Example.dll-class11::method111、 class12::method121
-   示例\\CPP。SelectionCriteria2.Example.dll-class22::method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C*'"
```

将运行所有测试所有者值开始位置与"C"（不区分大小写）。 因此前, 一个命令将运行所有测试示例中\\CPP。SelectionCriteria1.Example.dll 和示例中的所有测试\\CPP。SelectionCriteria2.Example.dll class21 下的 (即，method211)

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"not(@BackwardsCompatibility=*) OR (@Owner='C*' AND @BackwardsCompatibility='*XP*')"
```

将运行所有测试，其中是未指定 BackwardsCompatibility 或，其中该所有者名称以"C"开头，backwardsCompatibilty 值包含 XP。 请注意如何在括号"（"和"）"用于指定的优先级顺序。

在示例中，这会有选择地运行:

-   示例\\CPP。SelectionCriteria1.Example.dll-class11::method111、 class12::method121，
-   示例\\CPP。SelectionCriteria2.Example.dll-class21::method211、 class22::method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Owner='???'"
```

将仅运行有属性所有者值，该值包含仅为 3 个字符的测试。

在本示例中，这会匹配"C"，并仅在运行：

-   示例\\CPP。SelectionCriteria1.Example.dll-class12::method121

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Priority>=1"
```

注意：这是很好的示例说明如何使用"&gt;="、"&lt;="、"&gt;"和"&lt;"propertyvalues 所在 floatvalues。

在本示例中，这会运行除示例以外的所有方法\\CPP。SelectionCriteria2.Example.dll-class22::method221，尚未指定任何优先级的。 换而言之，这将运行：

-   示例\\CPP。SelectionCriteria1.Example.dll-class11::method111、 class11::method112、 class12::method121
-   示例\\CPP。SelectionCriteria2.Example.dll-class21::method211。

请注意，可以使用"/ 选择"连同其他命令选项，如"/list""/ listproperties"等。

## <a name="span-idsmartquotesspanspan-idsmartquotesspanspan-idsmartquotesspansmart-quotes"></a><span id="Smart_Quotes"></span><span id="smart_quotes"></span><span id="SMART_QUOTES"></span>弯引号


如果您通过选择条件从 Outlook 或 Word 文档后通过复制到命令提示符下，可能会弯引号遇到中选择条件。 您可以找到有关哪些弯引号的详细信息位于：<http://en.wikipedia.org/wiki/Smart_quotes>和[弯引号：适用于计算机消耗的文本隐藏的 scourge](https://blogs.msdn.microsoft.com/oldnewthing/20090225-00/?p=19033/)

无法轻松地避免弯引号-最佳方法是删除所有"双引号和后将它复制通过在命令提示符下，再重新键入查询的引号一部分单一选择条件中的引号。

没有设置，以在 Outlook 中创建消息时将其关闭选项。 若要查找此 Outlook 帮助框中键入"弯引号"。

## <a name="span-idquicknamebasedselectionspanspan-idquicknamebasedselectionspanspan-idquicknamebasedselectionspanquick-name-based-selection"></a><span id="Quick_Name_based_selection"></span><span id="quick_name_based_selection"></span><span id="QUICK_NAME_BASED_SELECTION"></span>基于所选内容的快速名称


TAEF，可以快速选择基于在命令提示符下使用 / 名称命令行参数的名称：

``` syntax
/name:<test name with wildcards>
```

等效于：

``` syntax
/select:@Name='<test name with wildcards>'
```

换而言之，你现在可以提供的名称，例如所基于的选择查询：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Name='*::class11::*'"
```

通过使用更快地 **/name**如下所示：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /name=*::class11::*
```

请注意，如果这两个 **/name**并 **/选择**提供在命令提示符处，则忽略 /name 和 /select 优先。

 

 






---
title: 选择
description: 选择
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 152cf9cd9699d577789d03938e94530bd27e64bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796407"
---
# <a name="selection"></a>选择

 (TAEF) 的测试创作和执行框架提供了一种机制，可根据您提供的元数据信息有选择地运行或省略某些测试。 以下部分介绍如何将此选择机制与 TE.exe 结合使用的各种示例。

你可以从命令提示符窗口运行 TE.exe。

``` syntax
TE <test_binaries> [/select:<selection criteria>]
```

本节介绍 TE.exe **/select**：*选择条件* 选项。 有关 TE.exe 的详细信息，请参阅 [TE.exe 命令选项](te-exe-command-line-parameters.md)。

选择条件将全局应用于在命令提示符下提到的所有测试二进制文件。 假设有两个测试 \_ 二进制文件： **示例 \\CPP.SelectionCriteria1.Example.dll** 和 **示例 \\CPP.SelectionCriteria2.Example.dll** 。 下面的示例显示了在这些测试二进制文件的各个级别上指定的属性或元数据 \_ 。 还可以通过在命令提示符窗口中指定 **/listproperties** 选项来获取此项。

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

换句话说，通过分别对这些测试二进制文件中的每一个使用/listproperties \_ ，可以获得：

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

以及：

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

请注意，在这种情况下，测试 \_ 二进制文件与其完整路径一起列出， &lt; &gt; &lt; &gt; 在本机测试 \_ 二进制文件和 "命名空间" 的情况下 &lt; &gt; &lt; ，类名作为 "namespace：： ClassName" 列出。类名 &gt; " \_ 。 同样， &lt; &gt; &lt; &gt; &lt; &gt; 在本机测试 \_ 二进制文件和 "命名空间" 的情况下 &lt; &gt; &lt; ，测试方法名称将作为 "namespace：： ClassName：： TestMethodName" 列出。ClassName &gt; 。 &lt;&gt;"TestMethodName" \_ 。

换句话说，任何名称或函数的完全限定名称都是在 te 中保存的内容。 这是为了能够唯一区分任何方法。 例如，如果两个类具有相同的方法名称，则类限定有助于唯一选择你感兴趣的方法。 为此，选择条件可帮助仅运行符合给定测试二进制文件中的条件的测试 \_ 。

在上面的示例中，如Cpp.SelectionCriteria1.Example.dll 中所示， \\ 可以选择 "Method111"，方法如下：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='WEX::TestExecution::Examples::Class11::Method111'"
```

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='*Class11::Method111'"
```

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll /select:"@Name='*Method111'"
```

可以通过运行以下方法选择运行已标记为 "Priority" 的所有测试：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Priority < 2"
```

这只会 \\ 在示例中运行CPP.SelectionCriteria1.Example.dll-"class11：： method111" 的示例。

如果要在 class11 下运行所有测试，可以使用限定的 "Name" 属性以及通配符匹配，按如下所示进行选择：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll
                                                               /select:"@Name='*::class11::*'"
```

使用选择条件时，有一些东西有助于记住：

- "**and**"、"**not**" 和 "**or**" 是 **保留** 字，不 **区分大小写**。
- **元数据属性名称和值不区分大小写**，例如，在示例中为 "c2"，将匹配 "c2" 和 "c2"。 因此，如果您有一个具有元数据 "属性" 的函数，而另一个具有 "Property" 的函数，并且选择条件正在查找 "属性"，则这两个函数都将匹配。
- **选择查询字符串中的字符串值应包含在单引号中。在选择查询中的字符串值中，"？" 是单个通配符，" \* " 是0个或多个通配符。**
- 在命令提示符下使用引号时，请 **注意在对选择查询进行复制时的智能引号**。 如果从 Outlook 电子邮件复制一个选择查询，则可能会意外出现智能引号，TAEF 可能无法对其进行分析。 改为输入引号。

让我们来看看一些复杂的复合选择条件，以及它们将执行的操作。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C2' AND @Priority=2"
```

将运行：

- 示例 \\CPP.SelectionCriteria2.Example.dll-class21：： method211

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C2' AND @Priority=3"
```

将运行：

- 示例 \\CPP.SelectionCriteria1.Example.dll-class11：： method112

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='U3' oR @Priority=1"
```

将运行：

- 示例 \\CPP.SelectionCriteria1.Example.dll-class11：： method111
- 示例 \\CPP.SelectionCriteria2.Example.dll-class22：： method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"not(@BackwardsCompatibility=*)"
```

将运行尚未指定 BackwardsCompatibility 值的所有测试。  (查看以下项。 ) 

- 示例 \\CPP.SelectionCriteria1.Example.dll-class11：： method111、class12：： method121
- 示例 \\CPP.SelectionCriteria2.Example.dll-class22：： method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Owner='C*'"
```

将运行所有测试，其中所有者值以 "C" 开头 (不区分大小写) 。 因此，前面的命令将运行示例中的所有测试 \\CPP.SelectionCriteria1.Example.dll 并在 \\ class21 (（即) method211）下CPP.SelectionCriteria2.Example.dll 示例中的所有测试。

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"not(@BackwardsCompatibility=*) OR (@Owner='C*' AND @BackwardsCompatibility='*XP*')"
```

将运行未指定 BackwardsCompatibility 或的所有测试，其中所有者名称以 "C" 开头，"backwardsCompatibilty" 值包含 XP。 请注意括号 " (" 和 ") " 如何用于指定优先级顺序。

在此示例中，这会有选择地运行：

- 示例 \\CPP.SelectionCriteria1.Example.dll-class11：： method111、class12：： method121、
- 示例 \\CPP.SelectionCriteria2.Example.dll-class21：： method211、class22：： method221

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Owner='???'"
```

将仅运行其属性所有者值仅包含3个字符的测试。

在本示例中，这将匹配 "C" 并仅运行：

- 示例 \\CPP.SelectionCriteria1.Example.dll-class12：： method121

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /select:"@Priority>=1"
```

>[!NOTE]
>这是一个很好的示例，说明了如何使用 " &gt; ="、" &lt; ="、" &gt; " 和 " &lt; "，其中 propertyvalues 为 floatvalues。

在本示例中，这将运行除示例 \\CPP.SelectionCriteria2.Example.dll-class22：： method221 以外的所有方法，其中未指定 prority。 换句话说，这会运行：

- 示例 \\CPP.SelectionCriteria1.Example.dll-class11：： method111、class11：： method112、class12：： method121
- 示例 \\CPP.SelectionCriteria2.Example.dll-class21：： method211。

请注意，可以在连同中将 "/select" 用于其他命令选项，如 "/list" "/listproperties" 等。

## <a name="smart-quotes"></a>智能引号

如果要将选择条件从 Outlook 或 Word 文档复制回你的命令提示符，则你可能会遇到选择条件中的智能引号。 可以在智能引号上找到有关智能引号的详细信息 [：用于计算机消耗的文本隐藏 scourge](https://devblogs.microsoft.com/oldnewthing/?p=19033)

无简单方法可以避免使用智能引号-最佳方法是在将其复制到命令提示符之后删除选择条件中的所有 "双引号和" 单引号，并重新键入查询的引号部分。

在 Outlook 中创建邮件时，有一个选项设置可将其关闭。 在 Outlook 帮助框中键入 "智能引号" 以找到此信息。

## <a name="quick-name-based-selection"></a>快速名称基于选择

TAEF 使用 "/name" 命令行参数，在命令提示符处使用 "" 命令行的名称进行快速选择：

``` syntax
/name:<test name with wildcards>
```

等效于：

``` syntax
/select:@Name='<test name with wildcards>'
```

换句话说，你现在可以根据名称提供一个选择查询，如下所示：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll \
/select:"@Name='*::class11::*'"
```

使用 **/name** 更快：

``` syntax
Te.exe Examples\CPP.SelectionCriteria1.Example.dll Examples\CPP.SelectionCriteria2.Example.dll /name=*::class11::*
```

请注意，如果在命令提示符处同时提供了 **/name** 和 **/select** ，则将忽略/name 并优先使用/select。

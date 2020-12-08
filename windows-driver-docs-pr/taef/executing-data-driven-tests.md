---
title: 执行数据驱动的测试
description: 执行数据驱动的测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3302e43e9b6240eaac05b370e52e3d301c893f3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801221"
---
# <a name="span-idtaefexecuting_data-driven_testsspanexecuting-data-driven-tests"></a><span id="taef.executing_data-driven_tests"></span>执行数据驱动的测试


请确保你已了解如何创作数据驱动的测试，以及如何在开始执行 DataDrivenTests 与 TAEF 的提示和技巧之前，通过 [TAEF](index.md) 执行测试。 刷新有关 [选择查询](selection.md) 如何与 TAEF 一起工作的内存可能会很有帮助。

本部分专门介绍了如何执行基于表的数据驱动的测试，但相同的基本原则也适用于基于 PICT 和基于 WMI 的数据驱动的测试。

如果只是想要运行所有测试（包括数据驱动的测试），则与 TAEF 运行它的方式没有什么不同。 我们来看一个示例，该示例使用 TAEF 将 **CPP \\ DataDrivenExample** 和 **CSharp \\ DataDrivenExample** 一起运行。 请记住，默认情况下，TAEF 在进程外运行测试。 如果要以 inproc 运行，请使用 "/inproc" 开关。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll
```

查看指定元数据的 xml 文件和头文件。 仅运行优先级为1的 datadriven 测试，如下所示：

``` syntax
TE.exe Examples\*.Tests.dll /select:"@DataSource=* And @Priority=1"
```

请记住，在 xml 文件的行级别指定的元数据将覆盖在 TestMethod 创作级别指定的元数据。

让我们再来看一看使用 TAEF 的数据驱动的测试的强大功能。 例如，您只想在 FirstTable ( # A1 函数中重现第三行。 为此，可以使用行的索引，该索引将是 2 (索引从0开始) ：

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*FirstTable*' and @Data:index=2"
```

请注意，选择条件现在具有新的命名空间 " @Data: "，可以专门用于数据驱动的测试。 当您运行上述测试时，您将注意到， \# 在进行数据驱动的测试的情况下，不会将追加到测试名称后面的常用 "索引" 改为 " \# 黑色"，这是为此行指定的特殊 "name" 元数据。 有关详细信息，请参阅 [在行级别指定元数据](metadata-overriding-data-driven-test-example.md) 。 尽管这是特殊名称，仍可以使用该名称进行选择。 索引选择可用于为真正大的数据集选择一定范围的行。 例如 (假设-not in example) 如果数据驱动的测试包含100行 (max index = 99) ，并且只想执行索引大于10且小于20的行，则现在可以轻松地将此值指定为：

``` syntax
TE.exe Examples\*.Tests.dll /select:"@Name='*MyDataDrivenTest*' and @Data:index > 10 and @Data:index < 20"
```

很多时候，您需要根据特定数据值重现，而不必经历查找其索引的问题。 在这种情况下，可以再次使用 " @Data: " 命名空间。 现在，在单元测试的本机示例中， (请参阅 [创作数据驱动的测试](data-driven-testing.md)) ，只需在 "主题" 为 "AeroBasic" 时才运行这些情况。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /select:"@Data:Theme='AeroBasic'"
```

这会显示在控制台上，如下所示：

``` syntax
StartGroup: WEX::TestExecution::Examples::DataDrivenTests::SecondTable#2 [Process: 3588; Thread: 4584]
I am in second table.
Theme supplied as AeroBasic
EndGroup: WEX::TestExecution::Examples::DataDrivenTests::SecondTable#2 [Passed]
Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

你还可以利用/listproperties 进行 datadriven 测试，以查看数据集和元数据 (在测试方法级别指定的元数据组合和数据驱动测试的行级) 。 因此，

``` syntax
TE.exe Examples\CSharp.DataDriven.Examples.dll /listproperties
```

将列出 (datadriven 的所有方法，否则) ，以及在不同级别提供和指定的元数据和数据值。

查看 [行级别的重写元数据](metadata-overriding-data-driven-test-example.md)， [指定数组参数类型](array-support-data-driven-test-example.md) 和简单的 [数据驱动示例](data-driven-testing.md) ，例如，演练提供更多见解。

 

 






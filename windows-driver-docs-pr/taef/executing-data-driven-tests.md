---
title: 执行数据驱动的测试
description: 执行数据驱动的测试
ms.assetid: E8E7A66A-6E39-442d-A195-AE4633B817FE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745cc31388aa42be04e880c8e21e483d49b5a545
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566348"
---
# <a name="span-idtaefexecutingdata-driventestsspanexecuting-data-driven-tests"></a><span id="taef.executing_data-driven_tests"></span>执行数据驱动的测试


请确保您已经知道如何创建数据驱动测试以及如何执行与测试[TAEF](index.md)开始提示和技巧的执行与 TAEF DataDrivenTests 之前。 它可能有助于以刷新您的内存如何[选择查询](selection.md)也适用于 TAEF。

本部分专门介绍执行基于的表数据驱动的测试，但同样的基本原则适用于基于 PICT 并基于 WMI 的数据驱动测试也。

如果只是想要运行所有测试，包括数据驱动的测试，则从如何将正常都运行与 TAEF 没有区别。 让我们运行的示例，请考虑我们**CPP\\DataDrivenExample**并**CSharp\\DataDrivenExample**一起使用 TAEF。 请记住，默认情况下 TAEF 运行测试扩展的过程 如果你想要运行这些进程内，使用"/ inproc"切换。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll
```

看看的 xml 文件和指定的元数据的标头文件。 仅运行数据驱动的测试具有优先级 = 1，如下所示：

``` syntax
TE.exe Examples\*.Tests.dll /select:"@DataSource=* And @Priority=1"
```

请记住在行级别在创作级别 TestMethod 指定元数据 xml 文件重写中指定的元数据。

我们来探讨更多的数据驱动的测试执行 TAEF 强大功能。 例如，要重现仅 FirstTable() 函数中的第三行。 可以使用的行，这将是 2 （索引从 0 处开始） 的索引来执行此操作：

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*FirstTable*' and @Data:index=2"
```

请注意，选择标准现在包含新的命名空间"@Data:"可以专门使用该数据驱动测试。 运行时更高版本的测试，您将注意到，而非常规\#索引的测试名称，如果你有的数据驱动的测试，可附加\#黑色追加到测试名称-这是为指定的特殊 Name 元数据此行。 请参阅[指定在行级别的元数据](metadata-overriding-data-driven-test-example.md)有关详细信息。 尽管此特殊名称，仍可以选择使用的名称。 索引选择可能会很长选择的行的大型数据集的范围。 有关示例 （假设-未在示例中） 如果你有一种数据驱动测试 100 行 (最大索引 = 99) 和仅想要执行索引大于 10 的行和少于 20 个，现在可以轻松地指定为：

``` syntax
TE.exe Examples\*.Tests.dll /select:"@Name='*MyDataDrivenTest*' and @Data:index > 10 and @Data:index < 20"
```

很多时候，将需要重现基于特定的数据值而无需费力查找其索引。 在这种情况下可以使用"@Data:"再次命名空间。 现在假设在本机的示例中的单元测试 (请参阅[创作数据驱动测试](data-driven-testing.md))，你想要运行仅这种情况下，当"主题"是"AeroBasic"。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /select:"@Data:Theme='AeroBasic'"
```

这将按如下所示显示在控制台上：

``` syntax
StartGroup: WEX::TestExecution::Examples::DataDrivenTests::SecondTable#2 [Process: 3588; Thread: 4584]
I am in second table.
Theme supplied as AeroBasic
EndGroup: WEX::TestExecution::Examples::DataDrivenTests::SecondTable#2 [Passed]
Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

你还可以利用 /listproperties 对于数据驱动测试，若要查看的数据驱动测试的数据集和元数据 （在测试方法级别和行级别指定元数据的组合）。 因此，

``` syntax
TE.exe Examples\CSharp.DataDriven.Examples.dll /listproperties
```

将列出所有方法 (数据驱动，否则为) 随元数据和数据的值可用且指定在不同级别。

看一看[行级别重写元数据](metadata-overriding-data-driven-test-example.md)，[指定数组参数类型](array-support-data-driven-test-example.md)并[数据驱动的简单示例](data-driven-testing.md)例如演练提供的详细信息见解。

 

 






---
title: 数据驱动的测试
description: 数据驱动的测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88efab6ae803c2f998f7ffc080db59e6ae6d8a15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840475"
---
# <a name="data-driven-testing"></a>数据驱动的测试


数据驱动测试是测试方法，其中测试的输入和输出值与代码分开。 这种形式通常意味着，使测试代码更具一般性的投资，只需标识所涉及的数据就能编写大量的测试用例。

数据驱动的测试非常适合用于测试使用一组输入值（这些值定义它们的行为）的区域。例如，在测试 API 时，输入和输出参数可以定义为数据源，而测试代码使用数据，使 API 调用并验证结果。

## <a name="span-iddata-driven_testing_support_in_taefspanspan-iddata-driven_testing_support_in_taefspanspan-iddata-driven_testing_support_in_taefspandata-driven-testing-support-in-taef"></a><span id="Data-driven_Testing_support_in_TAEF"></span><span id="data-driven_testing_support_in_taef"></span><span id="DATA-DRIVEN_TESTING_SUPPORT_IN_TAEF"></span>TAEF 中的数据驱动的测试支持


TAEF 提供了用于创作数据驱动测试的各种选项。 我们来了解这些选项，以便您可以选择最适合您的测试方案的选项。

**基于表的数据驱动测试** 解决方案允许您对数据参数变体进行精细控制，并定义参数类型。 在此示例中，数据源是在 XML 文件中定义的表。 你可以指定参数类型 (int、无符号 int、size \_ t、bool、double、DWORD、 \_ \_ int64 等及其同类数组变量) ，或者将 type 默认值指定为 WEX：： Common：： string (本机) 或 string (managed) 。 表中的每一行都是参数值的一组变体。 对于表中的每一行，将重新调用测试方法。 下面是基于表的数据驱动测试的 XML 数据源的代码段：

```cpp
1  <?xml version="1.0"?>
2   <Data>
3     <Table Id ="Table1">
4          <ParameterTypes>
5                  <ParameterType Name="Size">Int32</ParameterType>
6                  <ParameterType Name="Color">String</ParameterType>
7          </ParameterTypes>
8          <Row>
9                 <Parameter Name="Size">12</Parameter>
10                 <Parameter Name="Color">Blue</Parameter>
11         </Row>
12         <Row>
13                 <Parameter Name="Size">4</Parameter>
14                 <Parameter Name="Color">White</Parameter>
15         </Row>
16         <Row>
17                 <Parameter Name="Size">9</Parameter>
18                 <Parameter Name="Color">Black</Parameter>
19         </Row>
20    </Table>
21  </Data>
```

了解更多： [基于表的数据驱动的测试](table-data-source.md)。

**轻型数据驱动的测试** 支持不提供基于表的数据驱动的测试解决方案所提供的完全保真。 为了阐明：轻型数据驱动测试将数据参数限制为 WEX：： Common：： String (本机) 或 String (托管) ，就像基于表的数据驱动测试解决方案支持的各种类型。 但是，如果您正在寻找一种或两个参数的低成本且快速的数据变体 (说) 为数据驱动的测试方法，并添加一个 XML 文件，因为数据源似乎不值得用，因此，轻量数据驱动的测试可能正是您要查找的内容。 这是一个很好的示例，开发人员编写 API 的单元测试，说 OpenThemeData ( ... ) 并想要针对 "Button"、"Listbox" 和 "滚动条" 验证 API。 为此创建 XML 数据源文件的重载可能太多，但对于轻型数据驱动的测试支持，可以在源代码本身中有效地执行此操作。 如果指定了多个参数，则 TAEF 将在场景后面生成参数的 n 向组合扩展，并将为每个组合调用测试方法。 了解详细信息： [轻量数据驱动的测试](light-weight-data-driven-testing.md)。

轻型数据驱动测试所提供的 n 向组合扩展可能会消耗大量资源并提供较少的返回值，因为测试方案变得更加复杂。 在此类复杂的测试方案中，对基于组合的 **数据驱动测试** 解决方案提供的图像 (pict) 进行了大规模独立的测试。 PICT 通过生成一组精简的参数结果来提供多个值，以全面了解参数。 查找链接，了解有关 PICT 的详细信息以及如何在 [基于 PICT 的数据驱动的测试](pict-data-source.md) 解决方案中使用此解决方案。

使用 **基于 WMI 的数据驱动的测试** 支持，还可以向测试中添加前提条件，还可以根据测试计算机上可用的资源 (数据) 获取信息。 例如，如果你想要仅在计算机已加入域的情况下运行测试，并且你在运行测试时还需要域名信息。 在本例中，数据源是一个 WQL 查询。 了解有关如何在测试方案中利用 [基于 WMI 的数据驱动测试](wmi-data-source.md) 的详细信息。

为了警惕上面列出的所有选项，还可能会出现一种设计，其中以上选项的组合可能会合适。 例如，你可能想要使用 WMI 查询来获取有关所有连接到测试计算机的打印机的信息，但也可以使用基于表的数据驱动的测试构造来提前定义另一组参数。 如果你希望测试的数据来自两个单独的表，则 **多个数据源** 规范也可能会很有用，因此允许每个表在其他测试中重复使用。 阅读有关如何为测试指定多个数据源的详细信息，以及执行此操作时应用的约束： [指定多个数据源](multiple-datasources.md)

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [使用脚本语言创作数据驱动的测试](data-driven-testing-in-scripting-languages.md)
-   [表数据源](table-data-source.md)
-   [表数据源中的参数类型](parameter-types-in-table-data-sources.md)
-   [简单的数据驱动的测试示例](simple-data-driven-test-example.md)
-   [元数据覆盖数据驱动的测试示例](metadata-overriding-data-driven-test-example.md)
-   [数组支持数据驱动的测试示例](array-support-data-driven-test-example.md)
-   [数据驱动的类](data-driven-class.md)
-   [PICT 数据源](pict-data-source.md)
-   [WMI 数据源](wmi-data-source.md)
-   [轻量数据驱动的测试](light-weight-data-driven-testing.md)
-   [执行数据驱动的测试](executing-data-driven-tests.md)
-   [多个数据源](multiple-datasources.md)

 

 






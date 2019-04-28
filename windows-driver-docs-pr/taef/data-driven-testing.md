---
title: 数据驱动的测试
description: 数据驱动的测试
ms.assetid: 409CC5FD-1632-4120-95C6-60574C9BAD32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a48f8cccf8b59cfc499518f75ac46d4d4cff2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341190"
---
# <a name="data-driven-testing"></a>数据驱动的测试


数据驱动测试是一个测试方法测试的输入和输出值分隔的代码。 此打击通常意味着，在进行更多地泛型允许大量的测试用例可由只需标识所涉及的数据进行编写的测试代码小投资。

数据驱动的测试非常适合用于测试使用一组定义其行为的输入值的区域-例如，当测试 API 时，输入和输出参数可定义为数据源，并测试代码使用的数据使 API 调用，并验证结果。

## <a name="span-iddata-driventestingsupportintaefspanspan-iddata-driventestingsupportintaefspanspan-iddata-driventestingsupportintaefspandata-driven-testing-support-in-taef"></a><span id="Data-driven_Testing_support_in_TAEF"></span><span id="data-driven_testing_support_in_taef"></span><span id="DATA-DRIVEN_TESTING_SUPPORT_IN_TAEF"></span>TAEF 中数据驱动测试支持


TAEF 提供了多种用于创作数据驱动测试的选项。 因此，您可以选择哪一种最能满足您的测试方案，让我们来了解这些选项。

**基于表的数据驱动的测试**解决方案，可很好地控制上的数据参数变体，以及定义的参数类型。 在这种情况下，数据源是 XML 文件中定义的表。 可以指定参数类型 (int、 unsigned int，大小\_t，bool，加倍，DWORD \_ \_int64 等和其同类数组变体)，或具有到 WEX::Common::String （本机） 的类型默认值或字符串 （托管）。 在表中的每一行是一组参数值变体。 测试方法将重新调用表中的每一行。 下面是 XML 数据源的代码片段的基于表的数据驱动的测试：

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

若要了解更多信息：[基于表的数据驱动的测试](table-data-source.md)。

**轻型数据驱动测试**支持不提供完全保真数据驱动测试的解决方案，基于表提供了。 若要阐明：数据驱动的测试轻量限制数据参数为 WEX::Common::String(native) 或 String(managed) 与表支持的各种类型的基于的数据驱动测试解决方案。 但是，如果您正在寻找低成本且快速的数据变体 （例如一个或两个参数的） 进行数据驱动测试方法并添加 XML 文件，如数据源似乎是不值得时遇到问题，数据驱动的测试轻量可能有且仅是什么正在查找。 好的示例是编写单元测试 API 举例来说 OpenThemeData(...) 的开发人员，并且想要验证"按钮"、"Listbox"和"滚动条"API。 可能会过多的一个重载，可为此，创建一个 XML 数据源文件但与细线数据驱动测试支持无法进行此操作有效地本身的源代码中。 如果指定多个参数，则 TAEF 将生成的参数在场景的背面 n 向组合扩展并将每个组合调用测试方法。 若要了解更多信息：[数据驱动的测试的轻量级](light-weight-data-driven-testing.md)。

N 向组合扩展，光权重数据驱动测试产品/服务，无法获取昂贵并提供减少返回量作为测试方案变得更加复杂。 在这种复杂的测试方案中，提供的成对独立组合 Testing(PICT) **PICT 基于数据驱动的测试**解决方案可能是要查找的内容。 PICT 通过生成一组精简参数结果以参数获取全面的覆盖率提供了许多值。 找出的链接可了解有关 PICT 以及如何在使用此解决方案的详细信息[PICT 基于数据驱动的测试](pict-data-source.md)解决方案。

使用**基于 WMI 的数据驱动的测试**支持，还可以添加不满足前提条件到你的测试并获取基于测试计算机上的可用资源的信息 （数据）。 例如，如果你想要运行测试，仅当计算机为已加入域并运行测试时还需要域名称信息。 在这种情况下，数据源是 WQL 查询。 了解如何利用[基于 WMI 数据驱动的测试](wmi-data-source.md)在测试方案中。

要注意上面列出的所有选项，您可能还提出了以上选项的组合似乎适合的设计。 例如，你可能想要使用 WMI 查询来获取有关连接到测试计算机的所有打印机的信息，但可能有另一组可提前使用一个基于的表数据驱动测试构造定义的参数。 **多个数据源**规范可能也很有用，如果希望测试的数据来自于两个单独的表，因此可以跨其他测试可重复使用的每个表。 阅读有关如何指定测试的多个数据源以及约束将应用同时执行此操作的详细信息：[指定多个数据源](multiple-datasources.md)

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [数据驱动的测试中的脚本语言](data-driven-testing-in-scripting-languages.md)
-   [表数据源](table-data-source.md)
-   [表数据源中的参数类型](parameter-types-in-table-data-sources.md)
-   [简单数据驱动的测试示例](simple-data-driven-test-example.md)
-   [元数据重写数据驱动的测试示例](metadata-overriding-data-driven-test-example.md)
-   [数组支持数据驱动的测试示例](array-support-data-driven-test-example.md)
-   [数据驱动的类](data-driven-class.md)
-   [PICT 数据源](pict-data-source.md)
-   [WMI 数据源](wmi-data-source.md)
-   [轻量数据驱动的测试](light-weight-data-driven-testing.md)
-   [执行数据驱动的测试](executing-data-driven-tests.md)
-   [多个数据源](multiple-datasources.md)

 

 






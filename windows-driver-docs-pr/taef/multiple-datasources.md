---
title: 多个数据源
description: 多个数据源
ms.assetid: FD0B252F-1D70-4840-986F-94FF80D42246
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2518c0b91964ed13e57d4ff3a1d7c410b27f08
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350130"
---
# <a name="multiple-datasources"></a>多个数据源


当您正在寻找一个或多个数据源的组合扩展时，多个数据源非常有用 ([基于表的数据源](table-data-source.md)， [PICT 基于数据源](pict-data-source.md)，或[基于 WMI 的数据源](wmi-data-source.md)).

编写您测试的设计来高效地使用此功能极其重要。 让我们看一个示例的帮助的原因也是如此。 假设多个数据源的一部分，您要指定两个表基于数据源、 一个基于 WMI 的数据源和一个 PICT 基于数据源。 为了叙述方便，比方说，第一个表有 4 行、 第二个 5 行、 WMI 查询返回 2 个结果和 PICT 数据源生成 6 成对组合。 TAEF 将提出了两个集的参数的组合扩展。 这意味着将调用有问题的测试方法 (4 X 5 X 2 X 6 =) **240**倍 ！ 增加使用的参数的不同组合的测试方法调用的数量可能会产生逐渐减小结果，就会测试覆盖率。 因此，务必要设计经过认真考虑和权衡其他备选方法通过使用多个数据源的测试。 以下是要考虑一些的要点：

-   请确保添加值具有多个表。 如果您不需要它们分隔开来，您所能想到了有效的参数组合自己。
-   检查是否可以使用约束，而不是多个表使用 PICT 模型文件。
-   检查是否是有价值的重构到多个测试的测试用例并将从多个数据源子集关联与每个新创建子测试。

## <a name="span-idspecifymultipledatasourcesspanspan-idspecifymultipledatasourcesspanspan-idspecifymultipledatasourcesspanspecify-multiple-datasources"></a><span id="Specify_multiple_DataSources"></span><span id="specify_multiple_datasources"></span><span id="SPECIFY_MULTIPLE_DATASOURCES"></span>指定多个数据源


此处的关键方面是如何指定数据源。 让我们看看我们本机和托管的示例中的代码段。

### <a name="span-idnativespanspan-idnativespanspan-idnativespannative"></a><span id="Native"></span><span id="native"></span><span id="NATIVE"></span>本机

```cpp
1   namespace WEX { namespace TestExecution { namespace Examples
2   {
3       class AdvancedDataDrivenTests
4       {
5           TEST_METHOD_SETUP(DataDrivenSetup);
6           TEST_METHOD_CLEANUP(DataDrivenCleanup);
7
8           TEST_CLASS(AdvancedDataDrivenTests)
9
10          BEGIN_TEST_METHOD(SecondTable)
11              TEST_METHOD_PROPERTY(L"DataSource", L"Table:AdvancedDataDrivenTests.xml#Table2;Table:CppTestLevelDataSource.xml#NestedTable")
12          END_TEST_METHOD()
13
14          BEGIN_TEST_METHOD(FirstTable)
15              TEST_METHOD_PROPERTY(L"DataSource", L"Table:AdvancedDataDrivenTests.xml#Table1;"
16                  L"PICT:PictDataSource.txt;" L"WMI:SELECT Location FROM Win32_StartupCommand")
17          END_TEST_METHOD()
18      };
19  } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

请参阅行 11、 15 和 16 在上面的示例。 一般情况下，模式遵循以指定数据源是以分号分隔每个数据源规范的列表。 该规范看在托管代码也非常相似。

### <a name="span-idmanagedspanspan-idmanagedspanspan-idmanagedspanmanaged"></a><span id="Managed"></span><span id="managed"></span><span id="MANAGED"></span>托管

```cpp
[TestMethod]
[DataSource(@"Table:CSharpAdvancedDataDrivenTests.xml#FirstTable;
    WMI:SELECT ProcessId FROM Win32_Service WHERE Name='Themes'")]

public void First()
{
    Log.Comment("In CSharpAdvancedDataDrivenTests.First");
    String[] shapes = m_testContext.DataRow["Shape"] as String[];
    foreach (String shape in shapes)
    {
        Console.WriteLine("The shape is " + shape);
    }

    Int32[] lengths = m_testContext.DataRow["Length"] as Int32[];
    foreach (int length in lengths)
    {
        Console.WriteLine("The length is " + length.ToString());
    }

    String description = (String)m_testContext.DataRow["Description"];
    Boolean desktopInteract = (Boolean)m_testContext.DataRow["DesktopInteract"];
    UInt32 processId = (UInt32)m_testContext.DataRow["ProcessId"];
    Log.Comment("Themes service is running on process " + processId.ToString());
    Log.Comment("Themes service description: " + description);
}
```

示例还演示了如何在多个行中指定多个数据源。 当然，您可以在单独的一行 （如下所示），指定数据源，但您可以通过使用上面所示的构造显著提高可读性。

## <a name="span-idspecifyingdatasourceonasinglelinespanspan-idspecifyingdatasourceonasinglelinespanspan-idspecifyingdatasourceonasinglelinespanspecifying-datasource-on-a-single-line"></a><span id="Specifying_DataSource_on_a_single_line"></span><span id="specifying_datasource_on_a_single_line"></span><span id="SPECIFYING_DATASOURCE_ON_A_SINGLE_LINE"></span>在单个行上指定数据源


```cpp
[DataSource("Table:CSharpAdvancedDataDrivenTests.xml#FirstTable;WMI:SELECT ProcessId FROM Win32_Service WHERE Name='Themes'")]
```

只是为了再次重申：**将生成的每个单独的数据源的数据集的每个 n 向组合扩展一次运行的测试方法**。 例如，对于上面的托管示例中，安全地假定只有一个主题服务运行，并且知道有 3 行中提供的表数据源，测试方法将 3 次调用 （1 个）。 在本机示例的情况下，在 SecondTable 测试方法中，有两个表指定的数据源。 第一个表包含 3 个行，第二个表包含 4 行。 因此测试方法将调用为 12 倍 (3 X 4)。

## <a name="span-idconstraintsthatapplywhilespecifyingmultipledatasourcesspanspan-idconstraintsthatapplywhilespecifyingmultipledatasourcesspanspan-idconstraintsthatapplywhilespecifyingmultipledatasourcesspanconstraints-that-apply-while-specifying-multiple-datasources"></a><span id="Constraints_that_apply_while_specifying_Multiple_DataSources"></span><span id="constraints_that_apply_while_specifying_multiple_datasources"></span><span id="CONSTRAINTS_THAT_APPLY_WHILE_SPECIFYING_MULTIPLE_DATASOURCES"></span>指定多个数据源时应用的约束


仅当你想要指定基于表的数据源中的多个数据源规范时，约束都适用。 **表数据源**必须指定为表：&lt;reative XML 文件路径&gt;\#&lt;TableId&gt;。 如果 TAEF 发现"TableId"用作单独的元数据时，它将假定数据源是一个基于表的数据源并继续操作。

 

 






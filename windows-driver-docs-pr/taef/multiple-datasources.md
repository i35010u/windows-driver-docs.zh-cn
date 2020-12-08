---
title: 多个数据源
description: 多个数据源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 864ef8d39093bd4d4c2064eba25ce170093ce5a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785415"
---
# <a name="multiple-datasources"></a>多个数据源


在查找 ([基于表的数据](table-data-source.md)源、 [基于 PICT](pict-data-source.md)的数据源或 [基于 WMI 的数据源](wmi-data-source.md)) 的一个或多个数据源的组合扩展时，多个数据源很有用。

精心设计测试设计，以有效地利用此功能。 我们来看一个示例，其中包含这样的示例。 假设你想要指定两个基于表的数据源，一个基于 WMI 的数据源和一个基于 PICT 的数据源。 对于参数，假设第一个表有4行，第二个行包含5行，WMI 查询返回2个结果，并且 PICT 数据源生成6个成对组合。 TAEF 将提供这些参数集的组合扩展。 这意味着将在 4 X 5 X 2 X 6 =) **240** 次 (调用相关测试方法！ 随着测试覆盖率的增加，将测试方法的调用次数与参数的不同组合增加可能会产生更多的结果。 这使得在使用多个数据源时，使用多个数据源设计测试非常重要。 下面是你可能需要考虑的一些要点：

-   请确保它添加了一个包含多个表的值。 如果不需要单独使用这些参数，则可以自行使用参数的有效组合。
-   检查是否可以将 PICT 模型文件与约束一起使用，而不是使用多个表。
-   检查是否存在将你的测试用例重构为多个测试的值，以及如何将多个数据源中的子集与每个新创建的子测试相关联。

## <a name="span-idspecify_multiple_datasourcesspanspan-idspecify_multiple_datasourcesspanspan-idspecify_multiple_datasourcesspanspecify-multiple-datasources"></a><span id="Specify_multiple_DataSources"></span><span id="specify_multiple_datasources"></span><span id="SPECIFY_MULTIPLE_DATASOURCES"></span>指定多个数据源


此处的关键方面是如何指定数据源。 让我们看看本机和托管示例中的代码片段。

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

请参阅上述示例中的第11、15和16行。 通常，用于指定数据源的模式是每个数据源规范的以分号分隔的列表。 规范在托管代码中的外观非常类似。

### <a name="span-idmanagedspanspan-idmanagedspanspan-idmanagedspanmanaged"></a><span id="Managed"></span><span id="managed"></span><span id="MANAGED"></span>经过

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

这些示例还演示了在多行中指定多个数据源的方式。 当然，您可能已在一行上指定了数据源 (如下所示) ，但您可以使用以上所示的构造显著提高可读性。

## <a name="span-idspecifying_datasource_on_a_single_linespanspan-idspecifying_datasource_on_a_single_linespanspan-idspecifying_datasource_on_a_single_linespanspecifying-datasource-on-a-single-line"></a><span id="Specifying_DataSource_on_a_single_line"></span><span id="specifying_datasource_on_a_single_line"></span><span id="SPECIFYING_DATASOURCE_ON_A_SINGLE_LINE"></span>在单行上指定数据源


```cpp
[DataSource("Table:CSharpAdvancedDataDrivenTests.xml#FirstTable;WMI:SELECT ProcessId FROM Win32_Service WHERE Name='Themes'")]
```

只是为了重新迭代： **对于每个单独数据源生成的数据集，将为每个 n 单向组合扩展运行一次测试方法**。 例如，对于上面托管的示例，安全假设只有一个主题服务在运行，并且知道提供的表数据源中有3行，则测试方法将被调用 (1 X 3) 三次。 在本机示例中，在 SecondTable 测试方法中，指定了两个表源。 第一个表包含3行，第二个表包含4行。 因此，测试方法将被调用 (3 X 4) 的12倍。

## <a name="span-idconstraints_that_apply_while_specifying_multiple_datasourcesspanspan-idconstraints_that_apply_while_specifying_multiple_datasourcesspanspan-idconstraints_that_apply_while_specifying_multiple_datasourcesspanconstraints-that-apply-while-specifying-multiple-datasources"></a><span id="Constraints_that_apply_while_specifying_Multiple_DataSources"></span><span id="constraints_that_apply_while_specifying_multiple_datasources"></span><span id="CONSTRAINTS_THAT_APPLY_WHILE_SPECIFYING_MULTIPLE_DATASOURCES"></span>指定多个数据源时应用的约束


仅当要在多源规范中指定基于表的数据源时，约束才适用。 必须将 **表数据源** 指定为表： &lt; reative path to XML file &gt; \# &lt; TableId &gt; 。 如果 TAEF 发现以单独的元数据形式提供 "TableId"，它将假定数据源是基于单个表的数据源，然后继续。

 

 






---
title: 表数据源
description: 表数据源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adeb2d3bdb5caee2b588a65accb3851ba860341f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796395"
---
# <a name="table-data-source"></a>表数据源


请确保熟悉 [TAEF](index.md) 的基本执行，并知道如何使用它 [创作测试](authoring-tests.md) ，然后再继续此部分。

现在，你已编写了基本的测试自动化并使用 TAEF，你可以将重点放在可用于处理不同数据集的相同测试代码的情况下。 为此，TAEF 提供了数据驱动测试的 "基于表" 方法。 让我们看一个简单的示例，了解如何编写数据驱动的测试。

请考虑一个简单的非数据驱动的示例，在该示例中，你要将大小和主题打印到控制台。 在此练习中，您要将此测试转换为数据驱动的测试。

```cpp
1  namespace WEX { namespace TestExecution { namespace Examples
2  {
3     void DataDrivenTests::FirstTable()
4     {
5         int size = 12;
6         Log::Comment(String().Format(L"Size retrieved was %d", size));
7     }
8
9     void DataDrivenTests::SecondTable()
10    {
11        String theme = "Aero";
12        Log::Comment(L"Theme supplied as " + theme);
13    }
14 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

## <a name="span-iddefining_the_dataspanspan-iddefining_the_dataspanspan-iddefining_the_dataspandefining-the-data"></a><span id="Defining_the_Data"></span><span id="defining_the_data"></span><span id="DEFINING_THE_DATA"></span>定义数据


现在，您希望此函数适用于一组大小和主题。 换句话说，你需要函数可以使用的变量数据值。 为此，请在 XML 文件中定义两个表 DataDrivenTests.xml：

```cpp
1  <?xml version="1.0"?>
2  <Data>
3  <Table Id ="Table1">
4          <ParameterTypes>
5                  <ParameterType Name="Size">Int32</ParameterType>
6                  <ParameterType Name="Color">String</ParameterType>
7                  <ParameterType Name="Transparency">Boolean</ParameterType>
8          </ParameterTypes>
9          <Row Priority="1" Owner="C2">
10                 <Parameter Name="Size">12</Parameter>
11                 <Parameter Name="Color">Blue</Parameter>
12                 <Parameter Name="Transparency">True</Parameter>
13         </Row>
14         <Row Priority="2" Owner="wex">
15                 <Parameter Name="Size">4</Parameter>
16                 <Parameter Name="Color">White</Parameter>
17                 <Parameter Name="Transparency">False</Parameter>
18         </Row>
19         <Row Owner="C2">
20                 <Parameter Name="Size">9</Parameter>
21                 <Parameter Name="Color">Black</Parameter>
22                 <Parameter Name="Transparency">True</Parameter>
23         </Row>
24 </Table>
25 <Table id ="Table2">
26         <Row Description="ButtonTest" Owner="C2" Priority="1">
27                 <Parameter Name="Control">Button</Parameter>
28                 <Parameter Name="Theme">Aero</Parameter>
29         </Row>
30         <Row Description="ComboBoxTest" Priority="2">
31                 <Parameter Name="Control">ComboBox</Parameter>
32                 <Parameter Name="Theme">Classic</Parameter>
33         </Row>
34         <Row Description="ListviewTest" Owner="wex">
35                 <Parameter Name="Control">Listview</Parameter>
36                 <Parameter Name="Theme">AeroBasic</Parameter>
37         </Row>
38 </Table>
39 </Data>
```

现在，您已定义了两个表： "Table1" 和 "Table2"。 **您可以在同一个 XML 文件中定义多个测试方法的表。**

请注意，在 Table1 中，你之前定义了 ParameterTypes 并选择了 "Size" 作为整数。 **ParameterTypes 节是可选的。** 默认情况下，如果未提供参数类型信息，则它将保存为字符串。 这种情况适用于 "Table2" 中的所有参数。

表中定义的每个 "行" 都是一组数据 (参数) 值，你希望测试函数接受这些值。 第9行、第14和第19行定义了 FirstTable 函数将接受的3组数据。 类似于26、30和34的行定义 SecondTable 的数据集。

在上面的示例中，请注意第9行、第14、19、26、30和34行，可以定义特定于行的元数据。 现在有一种方法可以使用同一函数的数据集来更改元数据信息。 第一组数据 (第9行) 的优先级为1，第二组数据的优先级 (第14行) 为2，第三组数据 (第19行) 默认为函数的优先级。 **所有行都从表与之关联的函数中继承元数据。如果在行级别再次指定相同的元数据，则将重写在函数级别定义的元数据值。**

**注意：除支持的类型定义以外，XML 文件架构定义对于本机和托管代码是相同的。** 有关如何定义数据的另一个示例，请参阅下面 "托管数据驱动的测试" 部分的初始部分。 继续使用本机数据驱动的测试来了解本机代码中允许的类型。

## <a name="span-idnative_data_driven_testspanspan-idnative_data_driven_testspanspan-idnative_data_driven_testspannative-data-driven-test"></a><span id="Native_Data_driven_test"></span><span id="native_data_driven_test"></span><span id="NATIVE_DATA_DRIVEN_TEST"></span>本机数据驱动的测试


定义数据集并准备好使用后，现在需要一种方法将测试函数限定为数据驱动的测试，并将其与定义数据集的表相关联。 此操作通过在创作测试时使用额外的元数据来完成：

```cpp
1  namespace WEX { namespace TestExecution { namespace Examples
2  {
3      class DataDrivenTests
4      {
5          TEST_CLASS(DataDrivenTests);
6
7          BEGIN_TEST_METHOD(SecondTable)
8              TEST_METHOD_PROPERTY(L"DataSource", L"Table:DataDrivenTests.xml#Table2")
9              TEST_METHOD_PROPERTY(L"Priority", L"3")
10         END_TEST_METHOD()
11
12         BEGIN_TEST_METHOD(FirstTable)
13             TEST_METHOD_PROPERTY(L"Priority", L"4")
14             TEST_METHOD_PROPERTY(L"DataSource", L"Table:DataDrivenTests.xml#Table1")
15         END_TEST_METHOD()
16     };
17 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

为了使 XML 表与测试相关联，请将 "DataSource" 元数据添加到测试的方法。 通过此关联 TAEF 将使用给定的数据源来驱动测试。 数据源值包含三个部分：

1.  "Table："-将数据源标识为 XML 表。
2.  "DataDrivenTests.xml"-这是包含 XML 表的文件。
3.  " \# Table2"-按照 " \# " 分隔符，"Table2" 值标识要使用的 XML 文档中的特定表。 单个 XML 表数据源可以包含多个表。 TAEF 将查找具有与指定值匹配的 "Id" 属性的 Table 元素的 XML 文件。

在上面的示例中，您可能已在 "FirstTable" 之前定义了 "SecondTable"。 这意味着 "SecondTable" 函数将在 "FirstTable" 函数之前执行，但你在 "Table2" 之前定义了与 "FirstTable" 对应的表，该表对应于 "SecondTable"。 这是为了强调在 **数据驱动的测试的发现和执行期间表定义的顺序是不相关的。**

将数据源映射到测试方法完成后，现在可以修改此示例以从源中获取数据。 在执行此操作之前，请查看已发布的标头文件 TestData。 相关部分为：

```cpp
1    class TestData
2    {
3    public:
4        template <typename T>
5        static HRESULT __stdcall TryGetValue(_In_z_ const wchar_t* pszString, T& result)
6        {
7            return Private::TestData<T>::TryGetValue(pszString, result);
8        }
9    };
```

第5行显示了要调用的 API，以便在函数中检索数据。 查看可供检索的 [参数类型](parameter-types-in-table-data-sources.md) 。

确定-全部设置为重新编写示例：

```cpp
1  namespace WEX { namespace TestExecution { namespace Examples
2  {
3      void DataDrivenTests::FirstTable()
4      {
5          Log::Comment(L"I am in first table");
6          int size;
7          if (SUCCEEDED(TestData::TryGetValue(L"size", size)))
8          {
9              VERIFY_ARE_NOT_EQUAL(size, 0);
10             Log::Comment(String().Format(L"Size retrieved was %d", size));
11         }
12     }
13
14     void DataDrivenTests::SecondTable()
15     {
16         Log::Comment(L"I am in second table.");
17         String theme;
18         if (SUCCEEDED(TestData::TryGetValue(L"theme", theme)))
19         {
20             Log::Comment(L"Theme supplied as " + theme);
21         }
22     }
23 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

第7行和第18行是为了使测试数据驱动而发生更改的主要部分。 不是很大变化。 查看执行数据驱动的测试，以了解如何在执行数据驱动的测试的同时充分利用 TAEF。

## <a name="span-idmanaged_data_driven_testspanspan-idmanaged_data_driven_testspanspan-idmanaged_data_driven_testspanmanaged-data-driven-test"></a><span id="Managed_Data_driven_test"></span><span id="managed_data_driven_test"></span><span id="MANAGED_DATA_DRIVEN_TEST"></span>托管数据驱动的测试


假设你想要在控制台上打印矩形的坐标。 首先，将这些坐标定义为 XML 文件中的数据集。

```cpp
1  <?xml version="1.0"?>
2  <Data>
3  <Table Id="FirstTable">
4          <ParameterTypes>
5                  <ParameterType Name="Left">Int32</ParameterType>
6                  <ParameterType Name="Right">String</ParameterType>
7                  <ParameterType Name="Top">Integer</ParameterType>
8                  <ParameterType Name="Bottom">Int32</ParameterType>
9          </ParameterTypes>
10         <Row Priority="1" Owner="C2" Description="Zero rect">
11                 <Parameter Name="Left">0</Parameter>
12                 <Parameter Name="Right">0</Parameter>
13                 <Parameter Name="Top">0</Parameter>
14                 <Parameter Name="Bottom">0</Parameter>
15         </Row>
16         <Row Priority="2" Owner="wex" Description="normal rect">
17                 <Parameter Name="Left">12</Parameter>
18                 <Parameter Name="Right">25</Parameter>
19                 <Parameter Name="Top">10</Parameter>
20                 <Parameter Name="Bottom">50</Parameter>
21         </Row>
22         <Row Owner="C2" Description="invalid rect">
23                 <Parameter Name="Left">30</Parameter>
24                 <Parameter Name="Right">15</Parameter>
25                 <Parameter Name="Top">40</Parameter>
26                 <Parameter Name="Bottom">10</Parameter>
27         </Row>
28 </Table>
29 </Data>
```

定义表作用域中的数据集，在本例中为 "FirstTable"，这在上面的第3行中定义。 **您可以在同一个 XML 文件中定义多个测试方法的表。**

观察到 FirstTable 定义了 ParameterTypes，并将 "Left" 称为 "Int32"。 **ParameterTypes 节是可选的。默认情况下，如果未提供参数类型信息，则它将保存为字符串。**

查看支持的 [参数类型](parameter-types-in-table-data-sources.md)的列表。

如果指定任何其他数据类型，则测试将引发警告，并将其视为一个字符串。

**注意：类型字符串不区分大小写，但应完全按照如上所示进行拼写。**

表中定义的每个 "行" 是一组数据 (参数) 值，你希望测试函数接受这些值。 第10、16和22行定义了函数的3组数据。

在上面的示例中，请注意第10、16和22行-可以定义特定于行的元数据。 现在，你可以使用同一函数的数据集来更改元数据信息。 第一组数据 (第10行) 的优先级为1，第二组数据的优先级 (第16行) 为2，第三组数据 (第22行) 默认为函数的优先级。 **所有行都从表与之关联的函数中继承元数据。如果在行级别再次指定相同的元数据，则将重写在函数级别定义的元数据值。**

**注意：除支持的类型定义以外，XML 文件架构定义对于本机和托管代码是相同的。** 有关如何定义此操作的另一个示例，请参阅本页顶部的 "定义数据" 部分。

现在，已定义所有数据。 下面的示例演示如何访问它。

```cpp
1  namespace WEX.Examples
2  {
3      using Microsoft.VisualStudio.TestTools.UnitTesting;
4      using System;
5      using System.Collections;
6      using WEX.Logging.Interop;
7      using WEX.TestExecution;
8
9      [TestClass]
10     public class CSharpDataDrivenTests
11     {
12         [TestMethod]
15         [DataSource("Table:CSharpDataDrivenTests.xml#FirstTable")]
16         public void First()
17         {
18             Console.WriteLine("Left is " + m_testContext.DataRow["Left"].ToString());
19
20             Log.Comment("In CSharpDataDrivenTests.First");
21         }
22
23         [TestMethod]
24         public void Second()
25         {
26             Log.Comment("In CSharpDataDrivenTests.Second");
27             Verify.IsTrue(true);
28         }
29
30         public TestContext TestContext
31         {
32             get { return m_testContext; }
33             set { m_testContext = value; }
34         }
35
36         private TestContext m_testContext;
37     }
38 }
```

将 XML 表与托管代码中的给定测试方法相关联非常类似于本机代码;只需应用 "DataSource" 元数据。 与之前一样，它由三个部分组成：

1.  "Table："-用于将数据源标识为 XML 表。
2.  "CSharpDataDrivenTests.xml"-包含 XML 表的文件。
3.  " \# FirstTable"-按照 " \# " 分隔符，"FirstTable" 值标识要使用的 XML 文档中的特定表。 TAEF 将查找具有与指定值匹配的 "Id" 属性的 Table 元素的 XML 文件。

请注意，第二个函数不是数据驱动的。 **您可以选择仅使某些测试成为数据驱动的。您还可以选择让每个测试在不同的 XML 文件中定义其表。**

在第36行中，定义专用 TestContext 属性的 VSTS 建议 (<https://msdn2.microsoft.com/library/ms404699(VS.80).aspx>) 。 你还可以定义 (第30到34行) 的此属性的公共评估师。 在内部 TAEF 加载 TestContext 的字典属性，并将相应的数据集集中在一起。

TestContext 是在 VisualStudio. Microsoft.visualstudio.testtools.uitest.common.uimap.uimap>. UnitTesting 中定义的。 请参阅上述示例中的第3行。 你应在托管测试创作中包含此作为引用。 **因此，创作数据驱动的测试不需要其他引用。**

在上面的示例第18行中，演示如何在函数中检索数据。 请注意，数据在 testContext 中可用 \_ 。

## <a name="span-idname_instead_of_index_to_identify_a_datarowspanspan-idname_instead_of_index_to_identify_a_datarowspanspan-idname_instead_of_index_to_identify_a_datarowspanname-instead-of-index-to-identify-a-datarow"></a><span id="Name_instead_of_Index_to_Identify_a_DataRow"></span><span id="name_instead_of_index_to_identify_a_datarow"></span><span id="NAME_INSTEAD_OF_INDEX_TO_IDENTIFY_A_DATAROW"></span>用于标识 DataRow 的名称而不是 Index


TAEF 使你可以使用更有意义的 "Name" 属性而不是索引来标识数据源中的任何 DataRow。 为此，只需在数据源的行级添加 "Name" 元数据。 此页面上的第一个示例可以修改为使用此功能，如下所示：

```cpp
1  <?xml version="1.0"?>
2  <Data>
3  <Table id ="Table1">
4          <ParameterTypes>
5                  <ParameterType Name="Size">Int32</ParameterType>
6                  <ParameterType Name="Color">String</ParameterType>
7                  <ParameterType Name="Transparency">Boolean</ParameterType>
8          </ParameterTypes>
9          <Row Name='BlueTransparent' Priority="1" Owner="C2">
10                 <Parameter Name="Size">12</Parameter>
11                 <Parameter Name="Color">Blue</Parameter>
12                 <Parameter Name="Transparency">True</Parameter>
13         </Row>
14         <Row Priority="2" Owner="wex">
15                 <Parameter Name="Size">4</Parameter>
16                 <Parameter Name="Color">White</Parameter>
17                 <Parameter Name="Transparency">False</Parameter>
18         </Row>
19         <Row Name='BlackTransparent' Owner="C2">
20                 <Parameter Name="Size">9</Parameter>
21                 <Parameter Name="Color">Black</Parameter>
22                 <Parameter Name="Transparency">True</Parameter>
23         </Row>
24 </Table>
25 ...
39 </Data>
```

在上面修改的示例中，将 "BlueTransparent" correspondes 为索引0。 索引为1的行没有给定的特殊名称，并且索引为2的行的名称为 "BlackTransparent"。 你仍可以使用选择查询来查找 "Table1" 中的索引0或2，并将找到正确的行。 但在执行或列出 dll 时，不会看到：

```cpp
<qualified name of the test method>#<index>
```

你将看到：

```cpp
<qualified name of the test method>#<name property provided at Row level>
```

对于行级提供 "Name" 属性的行。 如果没有为任何行提供 "Name" 属性（如上面的索引1），则默认情况下，在 \# 该方法的限定名处具有 **&lt; index &gt;** 。

请注意，在行级提供 "Name" 属性的方式实质上是更改 TAEF 使用相应行数据解释方法调用实例名称的方式。

## <a name="span-iddatasource_as_a_runtime_parameterspanspan-iddatasource_as_a_runtime_parameterspanspan-iddatasource_as_a_runtime_parameterspandatasource-as-a-runtime-parameter"></a><span id="DataSource_as_a_Runtime_parameter"></span><span id="datasource_as_a_runtime_parameter"></span><span id="DATASOURCE_AS_A_RUNTIME_PARAMETER"></span>DataSource 作为运行时参数


TAEF 支持将 datasource 作为运行时参数提供。 此操作的语法如下所示：

```cpp
te <test dll names> /p:<DataSource runtime name>=Table:<DataSoure XML file>#<Table Id>
```

创作测试时，必须将 "p： &lt; DataSource 运行时名称 &gt; " 指定为数据源。 请记住，必须在运行时指定完整的字符串-XML 文件名以及表 id。 如果在运行时提供了数据源，则不应将 TableId 作为测试元数据提供。 "Table：" 前缀指定正在查找表数据源。

可以使用发布共享上提供的示例之一尝试此操作：

``` syntax
te Examples\CPP.RuntimeDataSource.Example.dll /p:MyDataSource=Table:RuntimeDataSourceExample.xml#SimpleTable
```

## <a name="span-iddatasource_as_a_resourcespanspan-iddatasource_as_a_resourcespanspan-iddatasource_as_a_resourcespandatasource-as-a-resource"></a><span id="DataSource_as_a_Resource"></span><span id="datasource_as_a_resource"></span><span id="DATASOURCE_AS_A_RESOURCE"></span>作为资源的数据源


TAEF 允许将数据源添加为测试模块的资源，前提是它符合以下内容：

对于本机测试模块，可以通过将数据源指定为资源 id 或资源名称来实现此目的。 下面是一个代码示例：

```cpp
BEGIN_TEST_METHOD(ResourceNameDataSource)
    TEST_METHOD_PROPERTY(L"DataSource", L"Table:MyResourceName#SimpleTable")
END_TEST_METHOD()
```

在此示例中，"MyResourceName" 是在 ResourceDataSource 文件中定义的资源名称：

```cpp
MyResourceName DATASOURCE_XML "ResourceDataSource.xml"
```

对于托管测试模块，只能以特定方式指定资源，如下面所示的 **源** 文件代码段中所示：

```cpp
LANGUAGE_NEUTRAL_MANAGED_RESOURCES = CSharpAdvancedDataDrivenTests.xml
```

数据源元数据规范将保持不变，与指定 DataSource XML 文件的情况相同。 与托管代码中的大小写类似，你可以将资源名称设置为与 XML 文件名相同。 因此，请务必了解 TAEF 将首先查找包含数据源名称的实际文件。 如果找不到这样的 XML 文件，则它将继续使用给定的资源名称或 id 在测试模块中查找测试资源。由于将 DataSource 指定为资源需要重新编译，因此，你可以通过将数据源 XML 文件复制到与测试 dll 相同的位置来利用这一设计，同时开发 (和命名资源名称，使其与 XML 文件名) 相同。 完成测试后，将 XML 复制回代码目录，并重新编译为资源。 别忘了从执行目录中删除 XML 文件！ :)

## <a name="span-idexample_walk-throughsspanspan-idexample_walk-throughsspanspan-idexample_walk-throughsspanexample-walk-throughs"></a><span id="Example_Walk-throughs"></span><span id="example_walk-throughs"></span><span id="EXAMPLE_WALK-THROUGHS"></span>示例演练-演练


若要理解基于表的数据驱动测试的各个方面，请阅读一些更多示例演练：

-   [简单数据驱动的示例](data-driven-testing.md)
-   [重写行级的元数据](metadata-overriding-data-driven-test-example.md)
-   [指定数组参数类型](array-support-data-driven-test-example.md)
-   [数据驱动的类](data-driven-class.md)

 

 






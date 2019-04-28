---
title: 表数据源
description: 表数据源
ms.assetid: D0CC0536-5569-47ed-8DE8-B64FF3042C51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90c098dafbaf6c14d04b30e4db95f2d99cd5b413
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341811"
---
# <a name="table-data-source"></a>表数据源


请确保您熟悉的基本执行[TAEF](index.md)并且知道如何[作者测试](authoring-tests.md)使用它，然后继续进行本部分中。

现在，可以编写基本测试自动化和使用 TAEF，可以集中在方案，进行相同测试代码可以用于对不同的数据集。 为此，TAEF 提供数据驱动测试的"表基于"方法。 让我们看看一个简单的示例，若要了解如何着手编写数据驱动测试。

请考虑简单非-数据驱动的要在其中打印的大小和主题应用于在控制台的示例。 在此练习中，会将此测试，为数据驱动测试。

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

## <a name="span-iddefiningthedataspanspan-iddefiningthedataspanspan-iddefiningthedataspandefining-the-data"></a><span id="Defining_the_Data"></span><span id="defining_the_data"></span><span id="DEFINING_THE_DATA"></span>定义数据


现在，你想上述适用于大小和主题的一组函数。 换而言之，你希望我们的函数可以使用的变量数据值。 若要执行此操作，在一个 XML 文件 DataDrivenTests.xml 定义两个表：

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

现在已定义两个表，"Table1"和"Table2"。 **可以在同一个 XML 文件中定义的多个测试方法的表。**

观察到，Table1，在您定义 ParameterTypes 提前，并选择"大小"应为整数。 **ParameterTypes 部分是可选的。** 默认情况下，如果未提供参数类型信息，将以字符串形式保存。 这是"Table2"中的所有参数的这种情况。

定义表中每个"行"是一组你想要接受的测试函数的数据 （参数） 值。 第 9、 14 和 19 行定义 3 个我们 FirstTable 函数将接受的数据集。 同样第 26、 30 和 34 行定义 SecondTable 的数据集。

请注意，行 9、 14、 19、 26，30 和在上面的示例 34-你可以定义特定于行的元数据。 现在是一种方法，若要更改使用相同的功能的数据集的元数据信息。 第一组数据 （第 9 行） 的优先级为 1，第二个集的数据 （第 14 行） 的优先级为 2 和第三个集的数据 （第 19 行） 默认为函数的优先级。 **所有行都继承与关联的表的函数的元数据。如果在行级别再次指定不同的元数据，则它将覆盖在函数级别定义的元数据值。**

**注意：XML 文件架构定义是相同的本机以及托管代码中，除了支持的类型定义。** 请参阅下面有关如何定义的数据的另一个示例的"管理数据驱动的测试"部分的开头部分。 继续使用本机数据驱动的测试以了解在本机代码中允许的类型。

## <a name="span-idnativedatadriventestspanspan-idnativedatadriventestspanspan-idnativedatadriventestspannative-data-driven-test"></a><span id="Native_Data_driven_test"></span><span id="native_data_driven_test"></span><span id="NATIVE_DATA_DRIVEN_TEST"></span>本机数据驱动的测试


使用数据集定义并可供使用，现在需要一种方法来限定为数据驱动测试的测试函数，并将其与定义数据集的表相关联。 这是通过额外的元数据的方式创作测试时：

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

若要将 XML 表与测试相关联，将添加到测试的方法的 DataSource 元数据。 通过这种关联 TAEF 将使用给定的数据源来帮助进行测试。 数据源值具有三个部分：

1.  表:-此标识为 XML 表的数据源。
2.  DataDrivenTests.xml-这是包含 XML 表的文件。
3.  '\#Table2-以下\#分隔符，Table2 值标识要使用的 XML 文档内的特定表。 单个 XML 表格数据源可以包含多个表。 TAEF 将查找具有匹配的指定的值的 Id 属性的表元素的 XML 文件。

我们可能已观察到在上面的示例中，"SecondTable""FirstTable"之前定义。 这意味着将获取"SecondTable"函数执行之前"FirstTable"函数，但定义"Table1"，对应于"FirstTable"之前"Table2"与"SecondTable"对应的表的表。 这是为了强调的是，**发现和数据驱动的测试执行期间的表定义的顺序是不相关。**

映射到测试方法完成我们的数据源后，现在可以修改示例以从源获取数据。 执行该操作之前, 看一看已发布的标头文件，TestData.h。 感兴趣的部分是：

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

第 5 行显示了要调用以检索函数中的数据的 API。 看一看可用[参数类型](parameter-types-in-table-data-sources.md)进行检索。

良好-所有设置重新编写我们的示例：

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

第 7 和 18 行是为了使测试数据驱动的更改的主要部分。 不提供大量的更改。 请看一下执行数据驱动的测试，了解如何充分利用 TAEF 执行数据驱动测试时。

## <a name="span-idmanageddatadriventestspanspan-idmanageddatadriventestspanspan-idmanageddatadriventestspanmanaged-data-driven-test"></a><span id="Managed_Data_driven_test"></span><span id="managed_data_driven_test"></span><span id="MANAGED_DATA_DRIVEN_TEST"></span>托管的数据驱动的测试


请考虑你想要在控制台上打印的矩形的坐标的一个示例。 开始使用这些坐标定义作为 XML 文件中的数据集。

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

在这种情况下"FirstTable"，在上面的第 3 行中定义表中的作用域中定义的数据集。 **可以在同一个 XML 文件中定义的多个测试方法的表。**

观察 FirstTable 定义 ParameterTypes 前期和部分还指出"Left"是"Int32"。 **ParameterTypes 部分是可选的。默认情况下，如果未提供参数类型信息，将以字符串形式保存。**

看一看的列表支持[参数类型](parameter-types-in-table-data-sources.md)。

如果指定任何其他数据类型，则测试将引发警告，并将其视为一个字符串。

**注意：类型字符串不区分大小写，但应完全按照上面所示的拼写。**

在表中，定义每个"行"是一组你想要接受的测试函数的数据 （参数） 值。 第 10、 16 和 22 行定义 3 个数据集，我们的函数。

请注意，行 10，16，并且在上面的示例 22-您可以对行定义特定元数据。 现可更改与同一函数的数据集的元数据信息的方法。 第一组数据 （第 10 行） 的优先级为 1，第二个集的数据 （第 16 行） 的优先级为 2 和第三个集的数据 （第 22 行） 默认为函数的优先级。 **所有行都继承与关联的表的函数的元数据。如果在行级别再次指定不同的元数据，则它将覆盖在函数级别定义的元数据值。**

**注意：XML 文件架构定义是相同的本机以及托管代码中，除了支持的类型定义。** 看看如何定义此宏的另一个示例的此页顶部的"定义数据"部分。

现在，可以定义的所有数据。 下面的示例演示如何访问它。

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

将 XML 表与托管代码中的给定的测试方法关联是非常类似于本机代码;只需应用 DataSource 元数据。 为之前，它是三个部分组成：

1.  表:-若要标识为 XML 表的数据源。
2.  CSharpDataDrivenTests.xml-包含 XML 表的文件。
3.  '\#FirstTable-以下\#分隔符，FirstTable 值标识要使用的 XML 文档内的特定表。 TAEF 将查找具有匹配的指定的值的 Id 属性的表元素的 XML 文件。

请注意，第二个函数不是数据驱动。 **你可以选择允许只有某些测试，以便进行数据驱动。此外可以让每个测试具有不同的 XML 文件中定义其表。**

在行 36，定义一个专用的 TestContext 属性-像 VSTS 建议 (<https://msdn2.microsoft.com/library/ms404699(VS.80).aspx>)。 您还可以对此属性 （行至第 34 30） 定义公共评估师。 在内部 TAEF 加载 TestContext 的字典属性，在焦点中相应的数据集。

TestContext Microsoft.VisualStudio.TestTools.UnitTesting 中定义。 请参阅上面的示例中的第 3 行。 您应已将此作为参考中包含你托管的测试创作。 **因此，没有其他引用所需的创作数据驱动测试。**

在上面的示例中的第 18 行中，您显示如何检索在函数中的数据。 请注意，数据也可用在 m\_testContext.DataRow。

## <a name="span-idnameinsteadofindextoidentifyadatarowspanspan-idnameinsteadofindextoidentifyadatarowspanspan-idnameinsteadofindextoidentifyadatarowspanname-instead-of-index-to-identify-a-datarow"></a><span id="Name_instead_of_Index_to_Identify_a_DataRow"></span><span id="name_instead_of_index_to_identify_a_datarow"></span><span id="NAME_INSTEAD_OF_INDEX_TO_IDENTIFY_A_DATAROW"></span>命名而不是索引为 Identify 是 DataRow


TAEF 可以有一个更有意义的 Name 属性，而不是索引来标识数据源中的任何数据行。 若要执行此操作，只需在数据源中的行级别添加 Name 元数据。 我们在此页上的第一个示例可以修改以使用此功能，如下所示：

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

在上文中修改的示例中，BlueTransparent correspondes 索引 0。 具有索引 1 行提供给它没有特殊名称且具有索引 2 的行具有名称 BlackTransparent 与之关联。 仍可以使用所选内容查询来查找索引 0 或 2 Table1 中的，它将查找正确的行。 但是，当执行或列出的 dll，而不是查看：

```cpp
<qualified name of the test method>#<index>
```

你将看到：

```cpp
<qualified name of the test method>#<name property provided at Row level>
```

"Name"属性在行级别提供的位置的行。 如果没有为任何行提供"Name"属性，如在索引 1 更高版本的情况下它将默认为无\# **&lt;索引&gt;** 在方法的限定名称。

请注意，通过提供在行级别的"Name"属性，要实质上更改 TAEF 解释的方法调用与对应的行数据的实例名称的方式。

## <a name="span-iddatasourceasaruntimeparameterspanspan-iddatasourceasaruntimeparameterspanspan-iddatasourceasaruntimeparameterspandatasource-as-a-runtime-parameter"></a><span id="DataSource_as_a_Runtime_parameter"></span><span id="datasource_as_a_runtime_parameter"></span><span id="DATASOURCE_AS_A_RUNTIME_PARAMETER"></span>作为运行时参数的数据源


TAEF 支持提供的运行时参数作为数据源。 此语法如下所示：

```cpp
te <test dll names> /p:<DataSource runtime name>=Table:<DataSoure XML file>#<Table Id>
```

创作时需考虑中的测试，必须指定"p:&lt;数据源运行时名称&gt;"作为数据源。 请记住，你必须在运行时一起-指定完整的字符串的 XML 文件名称，以及表 id。 TableId 不需要提供作为测试元数据中，如果在运行时提供数据源。 "表:"前缀指定您正在寻找的表数据源。

您可以试用此版本共享中可用的示例之一：

``` syntax
te Examples\CPP.RuntimeDataSource.Example.dll /p:MyDataSource=Table:RuntimeDataSourceExample.xml#SimpleTable
```

## <a name="span-iddatasourceasaresourcespanspan-iddatasourceasaresourcespanspan-iddatasourceasaresourcespandatasource-as-a-resource"></a><span id="DataSource_as_a_Resource"></span><span id="datasource_as_a_resource"></span><span id="DATASOURCE_AS_A_RESOURCE"></span>为资源的数据源


TAEF 可作为测试模块的资源添加数据源，只要它符合以下：

对于本机单元测试的模块，可以执行此操作通过指定数据源的资源 id 或资源名称。 下面是一个代码示例：

```cpp
BEGIN_TEST_METHOD(ResourceNameDataSource)
    TEST_METHOD_PROPERTY(L"DataSource", L"Table:MyResourceName#SimpleTable")
END_TEST_METHOD()
```

"MyResourceName"是这种情况下定义 ResourceDataSource.rc 文件中的资源名称：

```cpp
MyResourceName DATASOURCE_XML "ResourceDataSource.xml"
```

对于托管的测试模块资源只能指定以特定方式中所示**源**文件代码段如下所示：

```cpp
LANGUAGE_NEUTRAL_MANAGED_RESOURCES = CSharpAdvancedDataDrivenTests.xml
```

数据源元数据规范像以前那样发生时指定数据源 XML 文件将保持不变。 类似于托管代码中的用例，您可以制作名称作为 XML 文件的名称相同的资源。 因此，它是必须了解 TAEF 首先将寻找具有数据源名称的实际文件是否存在。 如果找不到此类的 XML 文件，然后仅将它继续寻找给定的资源名称或 id 为 test 模块中的测试资源。指定数据源，因为资源需要重新编译，因为您可以利用这种设计通过与测试 dll 相同的位置在开发时复制的数据源 XML 文件 （和命名的资源名称作为 XML 文件的名称相同）。 完成后测试，将 XML 返回到代码目录复制和重新编译为资源。 别忘了将在执行目录中删除该 XML 文件 ！ :)

## <a name="span-idexamplewalk-throughsspanspan-idexamplewalk-throughsspanspan-idexamplewalk-throughsspanexample-walk-throughs"></a><span id="Example_Walk-throughs"></span><span id="example_walk-throughs"></span><span id="EXAMPLE_WALK-THROUGHS"></span>示例演练


若要掌握各种基于表的数据驱动测试内容，执行一些详细示例演练的读取：

-   [简单数据驱动的示例](data-driven-testing.md)
-   [重写在行级别的元数据](metadata-overriding-data-driven-test-example.md)
-   [指定数组参数类型](array-support-data-driven-test-example.md)
-   [数据驱动的类](data-driven-class.md)

 

 






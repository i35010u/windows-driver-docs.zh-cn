---
title: 简单的数据驱动的测试示例
description: 简单的数据驱动的测试示例
ms.assetid: 59A897C3-C9CD-4e1c-B4BA-F81B3B3E4532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6f8d4dad8e0921c334c6391057bd29e02be291
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402296"
---
# <a name="simple-data-driven-test-example"></a>简单的数据驱动的测试示例


本部分介绍数据驱动测试的几个示例，并涵盖每个示例中的特定功能。

第一个示例是一个名为 SimpleDataDrivenExample 的基本数据驱动的测试。

在托管的示例中，你将找到如下所示的 XML 文件：

```cpp
    1  <?xml version="1.0"?>
    2  <Data>
    3    <Table Id="Table1">
    4      <ParameterTypes>
    5        <ParameterType Name="Size">Int32</ParameterType>
    6        <ParameterType Name="Color">String</ParameterType>
    7      </ParameterTypes>
    8      <Row>
    9        <Parameter Name="Size">4</Parameter>
    10       <Parameter Name="Color">White</Parameter>
    11     </Row>
    12     <Row>
    13       <Parameter Name="Size">10</Parameter>
    14       <Parameter Name="Color">Black</Parameter>
    15     </Row>
    16     <Row>
    17       <Parameter Name="Size">9</Parameter>
    18       <Parameter Name="Color">Orange</Parameter>
    19     </Row>
    20     <Row>
    21       <Parameter Name="Size">9</Parameter>
    22       <Parameter Name="Color">Blue</Parameter>
    23     </Row>
    24   </Table>
    25 </Data>
```

此 XML 文件为数据驱动的测试定义要使用的数据参数。 Top XML 节点是** &lt; 数据 &gt; **标记，它可能包含其中定义的**一个或多个 &lt; 表 &gt; **标记。 **每个表都需要与唯一的 "ID" 属性相关联。** 测试函数使用表 ID 值标识它们将在 XML 文件中使用的特定表。

在 &lt; 表 &gt; 标记中，有一个可选的** &lt; ParameterTypes &gt; **节。 在此处，可以使用** &lt; ParameterTypes &gt; **标记显式指定给定参数的数据类型。 在上面的示例中，显式指定参数 "Size" 的类型为 "Int32"，参数 "Color" 是一个字符串。 概括： **ParameterTypes 部分是可选的。默认情况下，如果未提供参数类型信息，则它将保存为字符串。**

如果比较托管和本机示例，则会注意到两者之间的唯一区别是** &lt; ParameterTypes &gt; **块。 本机 XML 文件指定的大小为本机整数类型 "int"，并使用默认类型 WEX：： Common：： String 作为颜色的类型（通过不指定）。 为方便起见，下面的示例演示了本机示例中的 XML 文件。

```cpp
    1  <?xml version="1.0"?>
    2  <Data>
    3    <Table Id="SimpleTable">
    4      <ParameterTypes>
    5        <ParameterType Name="Size">int</ParameterType>
    6      </ParameterTypes>
    7      <Row>
    8        <Parameter Name="Size">4</Parameter>
    9        <Parameter Name="Color">White</Parameter>
    10     </Row>
    11     <Row>
    12       <Parameter Name="Size">10</Parameter>
    13       <Parameter Name="Color">Black</Parameter>
    14     </Row>
    15     <Row>
    16       <Parameter Name="Size">9</Parameter>
    17       <Parameter Name="Color">Orange</Parameter>
    18     </Row>
    19     <Row>
    20       <Parameter Name="Size">9</Parameter>
    21       <Parameter Name="Color">Blue</Parameter>
    22     </Row>
    23   </Table>
    24 </Data>
```

在**本机**代码和**托管**代码中支持的参数类型列在[表数据源的参数类型](parameter-types-in-table-data-sources.md)中。

如果指定任何其他数据类型，则测试将引发警告，并将其视为一个字符串。

继续使用 XML 文件， &lt; &gt; 在两个 xml 文件中的 ParameterTypes 块之后，您可以使用一组相同的** &lt; 行 &gt; **，每个行对应于我们托管和本机示例中的一组数据。 在此特定情况下，有4个行块定义的数据集 &lt; &gt; ，每个数据块使用** &lt; &gt; 参数**标记指定参数的值。

这涉及数据源文件的各个部分的基本基础知识。 现在，让我们看看如何检索在上述 XML 文件中指定的值。

## <a name="span-idauthoring_test_to_be_a_data_driven_testspanspan-idauthoring_test_to_be_a_data_driven_testspanspan-idauthoring_test_to_be_a_data_driven_testspanauthoring-test-to-be-a-data-driven-test"></a><span id="Authoring_test_to_be_a_data_driven_test"></span><span id="authoring_test_to_be_a_data_driven_test"></span><span id="AUTHORING_TEST_TO_BE_A_DATA_DRIVEN_TEST"></span>创作测试为数据驱动的测试


由于已指定数据，因此需要一种方法将使用数据的代码或测试方法与 XML 文件中的此数据相关联。 为此，请在托管和本机示例中，通过指定 **"DataSource"** 元数据。 数据源元数据有三个部分：

1.  "Table："-将数据源标识为 XML 表。
2.  "DataDrivenTests.xml"-这是包含 XML 表的文件。
3.  " \# Table2"-按照 " \# " 分隔符，"Table2" 值标识要使用的 XML 文档中的特定表。 单个 XML 表数据源可以包含多个表。 TAEF 将查找具有与指定值匹配的 "Id" 属性的 Table 元素的 XML 文件。

同样，让我们快速了解一下涉及以上各个方面的代码。

### <a name="span-idnative_codespanspan-idnative_codespanspan-idnative_codespannative-code"></a><span id="Native_code"></span><span id="native_code"></span><span id="NATIVE_CODE"></span>本机代码

```cpp
1   class SimpleDataDrivenExample
2   {
3      BEGIN_TEST_CLASS(SimpleDataDrivenExample)
4        TEST_CLASS_PROPERTY(L"Description", L"Simple example in table-based data-driven tests")
5      END_TEST_CLASS()
6   
7      TEST_METHOD_CLEANUP(TestCleanup);
8      TEST_METHOD_SETUP(TestSetup);
9    
10     BEGIN_TEST_METHOD(DataDrivenTest)
11       TEST_METHOD_PROPERTY(L"DataSource", L"Table:SimpleDataDrivenExample.xml#SimpleTable")
11     END_TEST_METHOD()
12     ...
```

### <a name="span-idmanaged_codespanspan-idmanaged_codespanspan-idmanaged_codespanmanaged-code"></a><span id="Managed_code"></span><span id="managed_code"></span><span id="MANAGED_CODE"></span>托管代码

```cpp
    1 [TestMethod]
    2 [DataSource("Table:CSharpDataDrivenSimpleExample.xml#SimpleTable")]
    3 public void DataDrivenTest()
    4 {
    5  ...
    6 }
```

"DataSource" 是 UnitTesting 中的已知属性。 VisualStudio. Microsoft.visualstudio.testtools.uitest.common.uimap.uimap>.。

除此之外，对于托管代码中的数据驱动的测试，还需要执行一些额外的步骤。 还需要定义专用 TestContext 属性（如 <https://msdn2.microsoft.com/library/ms404699(VS.80).aspx> ）。 你还可以为此属性定义 public 评估师。 内部 TAEF 设置此 TestContext 属性，以便可以通过它访问数据。 让我们快速了解一下这部分代码：

```cpp
    1 public TestContext TestContext
    2 {
    3     get;
    4     set;
    5 }
```

## <a name="span-idretrieving_data_in_the_test_methodspanspan-idretrieving_data_in_the_test_methodspanspan-idretrieving_data_in_the_test_methodspanretrieving-data-in-the-test-method"></a><span id="Retrieving_data_in_the_Test_method"></span><span id="retrieving_data_in_the_test_method"></span><span id="RETRIEVING_DATA_IN_THE_TEST_METHOD"></span>在测试方法中检索数据


在托管代码和本机代码中检索 Api 不同。 首先，让我们了解**本机检索 API**：

```cpp
    1  void SimpleDataDrivenExample::DataDrivenTest()
    2  {
    3          int size;
    4          if (SUCCEEDED(TestData::TryGetValue(L"size", size)))
    5          {
    6              VERIFY_ARE_NOT_EQUAL(size, 0);
    7              Log::Comment(String().Format(L"Size retrieved was %d", size));
    8          }
    9
    10         String color;
    11         if (SUCCEEDED(TestData::TryGetValue(L"color", color)))
    12         {
    13             Log::Comment(L"Size retrieved was " + color);
    14         }
    15
    16         unsigned int index;
    17         if (SUCCEEDED(TestData::TryGetValue(L"index", index)))
    18         {
    19             Log::Comment(String().Format(L"At index %d", index));
    20         }
    21 }
```

请特别注意第4、11和17行。 在上述每个行之前，定义一个本地变量来保存将检索的数据。 在此处获取类型非常重要。 由于你在 XML 文件中将 "Size" 定义为 "int" 类型，因此必须定义一个 int 类型的局部变量来将其检索到。 检索 API 使用参数的名称作为字符串值进行检索，作为其第一个参数。 第二个参数是通过引用传递的本地变量，由 TAEF 代码进行设置。

此检索 API 在**TestData**中定义，并包含在所有 TAEF 测试都包含的 WexTestClass 标头中。

若要在**托管代码**中检索数据，请使用你定义的 TestContext 属性。 查看以下代码（例如）：

```cpp
    1  public void DataDrivenTest()
    2  {
    3     int size = (int)m_testContext.DataRow["Size"];
    4     Verify.AreNotEqual(size, 0);
    5     Log.Comment("Size is " + size.ToString());
    6
    7     Log.Comment("Color is " + m_testContext.DataRow["Color"]);
    8     UInt32 index = (UInt32)m_testContext.DataRow["Index"];
    9     Log.Comment("At index " + index.ToString());
    10 }
```

如果你熟悉 VSTS，你会发现上述示例类似。 使用 DataRow 并将列名指定为要尝试检索的参数的名称。

如果你在示例中查找，同一类中也存在非数据驱动的测试。 换句话说，**您可以灵活地将 DataDriven 和 NonDataDriven 测试组合到同一个测试类中。**

## <a name="span-idrunning_simpledatadrivenexample_with_taefspanspan-idrunning_simpledatadrivenexample_with_taefspanspan-idrunning_simpledatadrivenexample_with_taefspanrunning-simpledatadrivenexample-with-taef"></a><span id="Running_SimpleDataDrivenExample_with_TAEF"></span><span id="running_simpledatadrivenexample_with_taef"></span><span id="RUNNING_SIMPLEDATADRIVENEXAMPLE_WITH_TAEF"></span>通过 TAEF 运行 SimpleDataDrivenExample


请确保你已了解如何**创作数据驱动的测试**，以及如何在开始执行具有 TAEF 的 DataDrivenTests 的提示和技巧之前，**通过 TAEF 执行测试**。 对于使用 TAEF 的**选择**方式，刷新内存可能会很有帮助。

用于执行数据驱动的测试的命令提示符与通过 TAEF 执行任何一般测试并不完全相同。 若要运行上面所述的示例（本机和托管），只需运行以下命令：

<span id="TE.exe_Examples_CPP.DataDriven.Example.dll_Examples_CSharp.DataDriven.Example.dll__________________________name__Simple_"></span><span id="te.exe_examples_cpp.datadriven.example.dll_examples_csharp.datadriven.example.dll__________________________name__simple_"></span><span id="TE.EXE_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL__________________________NAME__SIMPLE_"></span>TE.exe 示例 \\CPP.DataDriven.Example.dll 示例 \\CSharp.DataDriven.Example.dll/Name： \* Simple\*  

"/Name" 根据名称添加选择条件，并仅选择你感兴趣的类。 若要从类中选择要执行的测试，您应该首先列出 dll 的所有属性。 然后，您可以决定要用于选择条件的属性。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /name:*Simple* /listproperties
f:\Examples\CPP.DataDriven.Example.dll
        WEX::TestExecution::Examples::SimpleDataDrivenExample
                Property[Description] = Simple example in table-based data-driven tests

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#0
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = White
                    Data[Size] = 4

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#1
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = Black
                    Data[Size] = 10

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#2
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#3
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = Blue
                    Data[Size] = 9

            WEX::TestExecution::Examples::SimpleDataDrivenExample::FirstNonDataDrivenTest
                    Setup: TestSetup
                    Teardown: TestCleanup

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet0
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[Data:Color] = {Purple, Maroon, Brown}

                    Data[Color] = Purple

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet1
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[Data:Color] = {Purple, Maroon, Brown}

                    Data[Color] = Maroon

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet2
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[Data:Color] = {Purple, Maroon, Brown}

                    Data[Color] = Brown

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SecondNonDataDrivenTest
                    Setup: TestSetup
                    Teardown: TestCleanup


        f:\Examples\CSharp.DataDriven.Example.dll
        WEX.Examples.CSharpDataDrivenSimpleExample
                Setup: MyClassInitialize
                Property[Description] = Simple example in table-based data-driven tests

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#0
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = White
                    Data[Size] = 4

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#1
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = Black
                    Data[Size] = 10

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#2
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#3
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = Blue
                    Data[Size] = 9

            WEX.Examples.CSharpDataDrivenSimpleExample.NonDataDrivenTest
            WEX.Examples.CSharpDataDrivenSimpleExample.SetsOfMetadataTest#metadataSet0
                    Property[Data:Color] = {Red, Green, Blue}

                    Data[Color] = Red

            WEX.Examples.CSharpDataDrivenSimpleExample.SetsOfMetadataTest#metadataSet1
                    Property[Data:Color] = {Red, Green, Blue}

                    Data[Color] = Green

            WEX.Examples.CSharpDataDrivenSimpleExample.SetsOfMetadataTest#metadataSet2
                    Property[Data:Color] = {Red, Green, Blue}

                    Data[Color] = Blue

```

现在，让我们忽略上面列出的 SetsOfMetadataTest 和 SetsOfDataTest。 如果您对这些信息感兴趣，请阅读有关[轻型数据驱动测试](light-weight-data-driven-testing.md)的详细信息。 了解各种属性和数据参数的名称和值后，就可以选择基于该数据的特定测试了。 请尝试这些操作并按照确认所选内容进行操作。

若要仅运行非数据驱动的测试，请运行：

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And_not__DataSource____"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and_not__datasource____"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND_NOT__DATASOURCE____"></span>TE.exe 示例 \\CSharp.DataDriven.Example.dll 示例 \\CPP.DataDriven.Example.dll/select： " @Name =" \* Simple \* "而不是（ @DataSource = \* ）"  

现在，若要仅运行那些数据驱动的测试，其中 color 指定为 "黑色"，请运行：

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Color__Black__"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_color__black__"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_COLOR__BLACK__"></span>TE.exe 示例 \\CSharp.DataDriven.Example.dll 示例 \\CPP.DataDriven.Example.dll/select： " @Name =" \* Simple \* "And @Data:Color =" 黑色 ""  

与 "Color" 一样， <strong> @Data: &lt; DataDrivenParameterName &gt; = &lt; DataDrivenParameterValue &gt; </strong>将根据指定的 DataDriven 参数值运行特定数据。 在上面的示例中，它将运行 WEX：： Testexecution.completed：：示例：： SimpleDataDrivenExample：:D ataDrivenTest \# 1 和 WEX。例如，CSharpDataDrivenSimpleExample. DataDrivenTest \# 1

请注意上面 listproperties 中的**测试索引**。 还可以根据索引选择上面的。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Index_1_"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_index_1_"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_INDEX_1_"></span>TE.exe 示例 \\CSharp.DataDriven.Example.dll 示例 \\CPP.DataDriven.Example.dll/select： " @Name =" \* Simple \* "And @Data:Index = 1"  

以上将运行两个选定的测试，即 @Data:Color "黑色"。 你甚至可以通过** @Data:Index &gt; lowerGuardValue 和 @Data:index &lt; upperGuardValue**将临界添加到索引选择

如果理解了 TAEF 的数据驱动测试的基础知识，请按照相同示例中的下一个类进行操作：在[行级重写元数据](metadata-overriding-data-driven-test-example.md)，并[指定数组参数类型](array-support-data-driven-test-example.md)。










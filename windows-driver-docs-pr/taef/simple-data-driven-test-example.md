---
title: 简单数据驱动的测试示例
description: 简单数据驱动的测试示例
ms.assetid: 59A897C3-C9CD-4e1c-B4BA-F81B3B3E4532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 507620097df485986b2281923014ee0c22dbdd14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522997"
---
# <a name="simple-data-driven-test-example"></a>简单数据驱动的测试示例


本部分描述了数据驱动测试的几个示例，并介绍了每个示例中的特定功能。

第一个示例是一个名 SimpleDataDrivenExample 的基本数据驱动的测试。

在托管的示例中，您将找到如下所示的 XML 文件：

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

此 XML 文件定义数据驱动的测试使用的数据参数。 顶级 XML 节点是**&lt;数据&gt;** 标记，它可能包含**一个或多个&lt;表&gt;** 在其中定义的标记。 **每个表必须是唯一的"ID"属性与相关联。** 测试函数使用的表 ID 值来标识将在 XML 文件中的特定表。

内&lt;表&gt;标记，您有一个可选**&lt;ParameterTypes&gt;** 部分。 此处可以显式指定给定的参数使用的数据类型**&lt;ParameterTypes&gt;** 标记。 在上述示例中，显式指定参数的"Int32"类型是"大小"和"Color"参数是一个字符串。 总结：**ParameterTypes 部分是可选的。默认情况下，如果未提供参数类型信息，将以字符串形式保存。**

如果进行比较的托管和本机示例时，会注意到，两者之间唯一的区别是**&lt;ParameterTypes&gt;** 块。 本机 XML 文件指定要将本机整数类型"int"的大小，并使用默认类型 WEX::Common::String 是通过不指定颜色的类型。 为方便起见，下面的示例演示本机示例中的 XML 文件。

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

中支持的参数类型**本机**并**托管**代码中，列出[此处](parameter-types-in-table-data-sources.md)。

如果指定任何其他数据类型，则测试将引发警告，并将其视为一个字符串。

执行完后的 xml 文件，之后&lt;ParameterTypes&gt;阻止这两个 XML 文件中、 具有相同组**&lt;行&gt;s**，其中每个对应于一组中的数据这两个我们托管和本机示例。 在此特定情况下，具有 4 个数据集的定义通过 4&lt;行&gt;阻止，每个指定的值使用的参数**&lt;参数&gt;** 标记。

中包含数据源文件的各个部分基本的基础的知识。 现在让我们看如何检索在上述 XML 文件中指定的值。

## <a name="span-idauthoringtesttobeadatadriventestspanspan-idauthoringtesttobeadatadriventestspanspan-idauthoringtesttobeadatadriventestspanauthoring-test-to-be-a-data-driven-test"></a><span id="Authoring_test_to_be_a_data_driven_test"></span><span id="authoring_test_to_be_a_data_driven_test"></span><span id="AUTHORING_TEST_TO_BE_A_DATA_DRIVEN_TEST"></span>创作为数据驱动测试的测试


现在，指定的数据，您需要一种方法将关联代码或测试方法将使用此 XML 文件中的数据的数据。 执行此操作-在这两个托管和本机示例-通过指定 **"数据源"** 元数据。 数据源元数据具有三个部分：

1.  表:-此标识为 XML 表的数据源。
2.  DataDrivenTests.xml-这是包含 XML 表的文件。
3.  '\#Table2-以下\#分隔符，Table2 值标识要使用的 XML 文档内的特定表。 单个 XML 表格数据源可以包含多个表。 TAEF 将查找具有匹配的指定的值的 Id 属性的表元素的 XML 文件。

再次重申，让我们快速浏览一下涵盖上述方面的代码。

### <a name="span-idnativecodespanspan-idnativecodespanspan-idnativecodespannative-code"></a><span id="Native_code"></span><span id="native_code"></span><span id="NATIVE_CODE"></span>本机代码

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

### <a name="span-idmanagedcodespanspan-idmanagedcodespanspan-idmanagedcodespanmanaged-code"></a><span id="Managed_code"></span><span id="managed_code"></span><span id="MANAGED_CODE"></span>托管的代码

```cpp
    1 [TestMethod]
    2 [DataSource("Table:CSharpDataDrivenSimpleExample.xml#SimpleTable")]
    3 public void DataDrivenTest()
    4 {
    5  ...
    6 }
```

"数据源"是 Microsoft.VisualStudio.TestTools.UnitTesting 中的已知的属性。

除此之外，对于数据驱动测试在托管代码中需要一些额外的步骤。 此外需要定义一个专用的 TestContext 属性-像 VSTS 建议 (<https://msdn2.microsoft.com/library/ms404699(VS.80).aspx>)。 您还可以对此属性定义公共评估师。 在内部 TAEF 设置此 TestContext 属性，以便可以通过它访问数据。 让我们快速看一下此部分代码：

```cpp
    1 public TestContext TestContext
    2 {
    3     get;
    4     set;
    5 }
```

## <a name="span-idretrievingdatainthetestmethodspanspan-idretrievingdatainthetestmethodspanspan-idretrievingdatainthetestmethodspanretrieving-data-in-the-test-method"></a><span id="Retrieving_data_in_the_Test_method"></span><span id="retrieving_data_in_the_test_method"></span><span id="RETRIEVING_DATA_IN_THE_TEST_METHOD"></span>在测试方法中检索数据


检索 Api 都是在托管和本机代码中不同的。 让我们先了解**本机检索 API**:

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

应特别注意 4、 11 和 17 行。 在每行之前定义一个本地变量来保存将检索的数据。 请务必获取此处的类型。 由于定义"大小"为 XML 文件中的"int"类型，因此必须定义类型为 int 检索到的本地变量。 检索 API 采用要作为字符串值作为其第一个参数检索的参数的名称。 第二个参数是在通过引用传递并由 TAEF 代码设置的本地变量。

在此检索 API 定义中**TestData.h** ，并且包含所有 TAEF 测试都包括 WexTestClass.h 标头。

若要检索的数据**托管代码**，请使用你定义的 TestContext 属性。 请参阅下面的代码 （或在示例中）：

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

如果你熟悉使用 VSTS，您会发现上面的示例类似。 使用数据行和列名称指定为要检索的参数的名称。

如果您查看示例中，此外还有同一个类中的非数据驱动的测试。 换而言之，**可以组合在同一个测试类中的数据驱动和 NonDataDriven 测试的灵活。**

## <a name="span-idrunningsimpledatadrivenexamplewithtaefspanspan-idrunningsimpledatadrivenexamplewithtaefspanspan-idrunningsimpledatadrivenexamplewithtaefspanrunning-simpledatadrivenexample-with-taef"></a><span id="Running_SimpleDataDrivenExample_with_TAEF"></span><span id="running_simpledatadrivenexample_with_taef"></span><span id="RUNNING_SIMPLEDATADRIVENEXAMPLE_WITH_TAEF"></span>运行带有 TAEF SimpleDataDrivenExample


请确保你已了解如何**创建数据驱动测试**和如何**执行测试 TAEF**开始提示和技巧的执行与 TAEF DataDrivenTests 之前。 它可能有助于以刷新您的内存如何**选择**配合 TAEF。

正在执行数据驱动测试的命令提示符下没有执行任何一般测试与 TAEF 太大不同。 若要运行上述这两个示例 （本机和托管），只需运行以下命令：

<span id="TE.exe_Examples_CPP.DataDriven.Example.dll_Examples_CSharp.DataDriven.Example.dll__________________________name__Simple_"></span><span id="te.exe_examples_cpp.datadriven.example.dll_examples_csharp.datadriven.example.dll__________________________name__simple_"></span><span id="TE.EXE_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL__________________________NAME__SIMPLE_"></span>TE.exe 示例\\CPP。DataDriven.Example.dll 示例\\CSharp.DataDriven.Example.dll /name:\*简单\*  

/Name 将添加根据名称选择条件，并选择仅感兴趣的类。 若要选择要从类中执行哪些测试，你应该首先列出的所有 dll 的属性。 然后，您可以决定要使用的选择条件的属性。

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

现在，让我们忽略 SetsOfMetadataTest 和 SetsOfDataTest 上面所列。 如果想了解这些，详细了解[轻型数据驱动测试](light-weight-data-driven-testing.md)。 现在，您知道的各种属性和数据参数名称和值，可以选择基于该特定测试。 欢迎试用并跟着介绍一起操作以确认你的选择。

若要运行仅非数据驱动测试，请运行：

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And_not__DataSource____"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and_not__datasource____"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND_NOT__DATASOURCE____"></span>TE.exe Examples\\CSharp.DataDriven.Example.dll Examples\\CPP.DataDriven.Example.dll /select:"@Name='\*Simple\*' And not(@DataSource=\*)"  

现在，若要运行驱动的测试，其中将颜色指定为"黑色"，这些数据运行：

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Color__Black__"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_color__black__"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_COLOR__BLACK__"></span>TE.exe Examples\\CSharp.DataDriven.Example.dll Examples\\CPP.DataDriven.Example.dll /select:"@Name='\*Simple\*' And @Data:Color='Black'"  

就像使用"Color"一样<strong>@Data: &lt;DataDrivenParameterName&gt;=&lt;DataDrivenParameterValue&gt;</strong>将运行基于特定的数据指定的数据驱动的参数值。 在上述情况下，它将运行 WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest\#1 和 WEX。Examples.CSharpDataDrivenSimpleExample.DataDrivenTest\#1

请注意**测试索引**listproperties 更高版本中。 您可以选择上述基于索引。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Index_1_"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_index_1_"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_INDEX_1_"></span>TE.exe Examples\\CSharp.DataDriven.Example.dll Examples\\CPP.DataDriven.Example.dll /select:"@Name='\*Simple\*' And @Data:Index=1"  

更高版本将运行相同的两个测试的@Data:Color= 黑色选择。 甚至将临界条件添加到与索引选择 **@Data:Index &gt; lowerGuardValue 和@Data:index &lt; upperGuardValue**

如果您了解数据驱动测试与 TAEF 的基础知识，遵循相同的示例中的下一步类：[重写元数据在行级](metadata-overriding-data-driven-test-example.md)，[指定数组参数类型](array-support-data-driven-test-example.md)。










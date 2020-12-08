---
title: PICT 数据源
description: PICT 数据源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dae98e42830e433b726ffab25fbda3e161549fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802137"
---
# <a name="pict-data-source"></a>PICT 数据源


请确保熟悉 TAEF 的基本执行，并知道如何使用它创作测试，然后再继续此部分。

## <a name="span-idpict_background_and_referencesspanspan-idpict_background_and_referencesspanspan-idpict_background_and_referencesspanpict-background-and-references"></a><span id="PICT_Background_and_References"></span><span id="pict_background_and_references"></span><span id="PICT_BACKGROUND_AND_REFERENCES"></span>PICT 背景和引用


PICT 代表成对的独立组合测试。 **PICT 允许单独指定每个参数的变体。** 例如，如果 API 测试依赖于两个参数： FileName 和 FileExtension，可以考虑将可能的变体分别传递给 FileName 和 for FileExtensions，如下所示：

-   FileName： a、z12390、Realllyreallyreallylonglonglonglonglonglonglonglonglonglong、normallength
-   FileExtension： txt，png，bat，doc，exe，bmp，wav

现在，你可以看到上述 (4 X 7 = 28) 的 **强制组合扩展** 可以在你认为要添加到列表中的更多变体时 **轻松地超出界限** 。 在这种测试用例方案中， **PICT 可以通过生成一组精简的参数结果来添加大量值，以获取针对输入参数的全面组合覆盖。**

## <a name="span-idpict_support_in_taefspanspan-idpict_support_in_taefspanspan-idpict_support_in_taefspanpict-support-in-taef"></a><span id="PICT_Support_in_TAEF"></span><span id="pict_support_in_taef"></span><span id="PICT_SUPPORT_IN_TAEF"></span>TAEF 中的 PICT 支持


TAEF 为基于 PICT 的测试提供内置支持。

若要利用此方法，请像往常一样为 pict.exe 编写输入模型文件。 请参阅 \* 上面提到的示例文件夹中的 .txt 文件。 如果在你的模型文件上通过在命令提示符下首先尝试使用 PICT 来尝试 PICT，则可能会很有用，如下所示：

``` syntax
pict.exe <model file> [/e:<seed file>]
```

TAEF 的最新版本共享上的其余二进制文件提供 Pict.exe。

您已经完成了创作您的模型文件 (和 seed file) 以获取 PICT，并已在命令提示符处验证了 pict.exe 该文件，您现在可以标记您的测试，让 TAEF 知道它们是 PICT 驱动的测试。 如果你熟悉 TAEF 中提供的基于表的数据驱动测试，你会发现这非常类似。

本机代码：

```cpp
1     class PictExample
2     {
3         TEST_CLASS(PictExample)
4
5         BEGIN_TEST_METHOD(SimpleTest)
6             TEST_METHOD_PROPERTY(L"DataSource", L"pict:PictExample.txt")
7         END_TEST_METHOD()
8
9         BEGIN_TEST_METHOD(TestWithSeed)
10            TEST_METHOD_PROPERTY(L"DataSource", L"pict:TestWithSeed.txt")
11            TEST_METHOD_PROPERTY(L"Pict:SeedingFile", L"TestWithSeed.sed")
12            TEST_METHOD_PROPERTY(L"Pict:Timeout", L"00:01:30")
13        END_TEST_METHOD()
14
15        BEGIN_TEST_METHOD(TestWithFunction)
16            TEST_METHOD_PROPERTY(L"DataSource", L"pict:TestWithFunction.txt")
17        END_TEST_METHOD()
18    };
```

托管代码：

```cpp
1     [TestClass]
2     public class CSharpPictExample
3     {
4         [TestMethod]
5         [DataSource("pict:ConstraintsTest.txt")]
6         [TestProperty("Pict:SeedingFile", "ConstraintsTest.seed")]
7         public void ConstraintsTest()
8         {
9             ...
10        }
11
12        [TestMethod]
13        [DataSource("pict:SumofSquareRoots.txt")]
14        public void SumOfSquareRoots()
15        {
16            ...
17        }
18
19        public TestContext TestContext
20        {
21            get { return m_testContext; }
22            set { m_testContext = value; }
23        }
24
25        private TestContext m_testContext;
26    }
```

如上面的示例所示，您需要指定模型文件的名称作为数据源。 **必须在模型文件的名称前面加上 "pict：" 前缀** ，并为测试方法提供此数据源。 对于托管测试，与任何其他使用 TAEF 的数据驱动的测试一样，必须提供 TestContext 属性 get 和 set 方法，并在类中具有相同的私有实例。

如果要将命令选项传递到 PICT，可以使用元数据来实现此目的。 使用下表将 Pict.exe 的命令选项映射到 TAEF 元数据。


| pict.exe 命令语法 |                本机 TAEF 元数据语法                |           托管的 TAEF 元数据语法            |
|-------------------------|-----------------------------------------------------------|---------------------------------------------------|
|          /o：3           |        测试 \_ 方法 \_ 属性 (L "Pict： Order"，L "3" )         |        \[TestProperty ( "Pict： Order"，"3" ) \]        |
|          /d：，           |   测试 \_ 方法 \_ 属性 (L "Pict： ValueSeparator"，L "，" )     |   \[TestProperty ( "Pict： ValueSeparator"，"，" ) \]    |
|           /a:           |                                                           | 测试 \_ 方法 \_ 属性 (L "Pict： AliasSeparator"，L " |
|          /n： ~           | 测试 \_ 方法 \_ 属性 (l "Pict： NegativeValuePrefix"，L "~" )  | \[TestProperty ( "Pict： NegativeValuePrefix"，"~" ) \] |
|      /e：测试种子       | 测试 \_ 方法 \_ 属性 (l "Pict： SeedingFile"，L "test. seed" )  | \[TestProperty ( "Pict： SeedingFile"，"test" ) \] |
|           /r            |      测试 \_ 方法 \_ 属性 (L "Pict： Random"，L "true" )       |      \[TestProperty ( "Pict： Random"，"true" ) \]      |
|          /r：33          |     测试 \_ 方法 \_ 属性 (l "Pict： RandomSeed"，L "33" )      |     \[TestProperty ( "Pict： RandomSeed"，"33" ) \]     |
|           /c            |  测试 \_ 方法 \_ 属性 (l "Pict： CaseSensitive"，L "true" )    |  \[TestProperty ( "Pict： CaseSensitive"，"true" ) \]   |

可在命令提示符处、DataSource 属性中设置上述任何元数据，也可将其设置为测试、类或模块级元数据，其优先级按顺序排列。 若要在命令提示符下设置，请使用以下语法：

``` syntax
te.exe <test dll> /Pict:Order=3 /Pict:SeedingFile=test.seed
```

若要设置 DataSource 属性中的元数据，请在 (？ ) 中追加一个带问号字符的模型文件名，然后使用一组与符号分隔的元数据名称 = 元数据值对。 使用此方法时，元数据名称的 "Pict：" 前缀是可选的。 以下是示例：

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:model.txt?Order=3&CaseSensitive=true&Random=true")
```

在幕后，TAEF 会将输入模型文件和命令选项提供给 PICT 并获取结果。 如果 PICT 产生任何错误或警告，则会看到，TAEF 会记录为警告。 对于 PICT 产生的每个结果输出行，TAEF 将重新调用该测试。

设置 "Pict： RandomSeed" 值会将 "Pict： Random" 的默认值从 false 更改为 true。 这样，便可以将 "Pict： Random" 显式设置为 false，以使 TAEF 忽略 "Pict： RandomSeed"。

**允许对模型文件执行 PICT.exe 的默认超时值为5分钟。** 如果您 PICT.exe 的模型文件更多并且需要超过5分钟的时间才能返回结果，则可以通过指定 **"Pict： Timeout"** 元数据来覆盖此超时，如上面的 CPP 示例中所示。 在此示例中，通过标准 [TAEF](taef-timeouts.md) 超时格式指定1.5 分钟超时。 与其他 PICT 元数据类似，"Pict： Timeout" 元数据会被继承，因此可以为整个类或模块指定。

你可以从测试方法及其关联的安装和清理方法中访问数据值，方法与使用 TAEF 对基于表的数据驱动测试相同，使用 TestData 类作为本机代码，并将 TestContext 用于托管代码，如下所示：

本机代码：

```cpp
1     void PictExample::SimpleTest()
2     {
3         String valueA;
4         if (SUCCEEDED(TestData::TryGetValue(L"A", valueA)))
5         {
6           Log::Comment(L"A retrieved was " + valueA);
7         }
8
9         String valueB;
10        if (SUCCEEDED(TestData::TryGetValue(L"B", valueB)))
11        {
12            Log::Comment(L"B retrieved was " + valueB);
13        }
14
15        String valueC;
16        if (SUCCEEDED(TestData::TryGetValue(L"C", valueC)))
17        {
18            Log::Comment(L"C retrieved was " + valueC);
19        }
20
21        unsigned int index;
22        if (SUCCEEDED(TestData::TryGetValue(L"index", index)))
23        {
24            Log::Comment(String().Format(L"At index %d", index));
25        }
26    }
```

托管代码：

```cpp
1      [TestClass]
2      public class CSharpPictExample
3      {
4          [TestMethod]
5          [DataSource("pict:ConstraintsTest.txt")]
6          public void ConstraintsTest()
7          {
8              Log.Comment("A is " + m_testContext.DataRow["A"]);
9              Log.Comment("B is " + m_testContext.DataRow["B"]);
10             Log.Comment("C is " + m_testContext.DataRow["C"]);
11             Log.Comment("D is " + m_testContext.DataRow["D"]);
12
13             UInt32 index = (UInt32)m_testContext.DataRow["Index"];
14             Log.Comment("At index " + index.ToString());
15        }
16
17        [TestMethod]
18        [DataSource("pict:SumofSquareRoots.txt")]
19        public void SumOfSquareRoots()
20        {
21             Log.Comment("A is " + m_testContext.DataRow["A"]);
22             Log.Comment("B is " + m_testContext.DataRow["B"]);
23
24             UInt32 index = (UInt32)m_testContext.DataRow["Index"];
25             Log.Comment("At index " + index.ToString());
26        }
27
28        public TestContext TestContext
29        {
30             get { return m_testContext; }
31             set { m_testContext = value; }
32        }
33
34        private TestContext m_testContext;
35    }
```

与 TAEF 中任何数据驱动的测试一样，"Index" 是保留的，不应用作参数名。 索引隐式引用测试方法调用的索引，如果你的测试需要，它可从测试方法访问。

**另外，请务必注意，对于基于 PICT 的测试，所有参数的数据类型假定为 WEX：： Common：： String (本机) 、String (托管) 或 VT \_ BSTR (script) 。** 转换和解释留给用户。

现在，你已完成使用 TAEF 创作基于 PICT 的测试，你可以从命令提示符调用它，并应用 TAEF 提供给它的所有命令功能：例如 **/list** 若要获取将使用 PICT 输出作为数据生成的所有测试方法的列表，请 **/listproperties** 获取测试方法名称及其关联的元数据和数据值的列表。开始之前要注意的关键事项 **是确保 pict.exe 在你的路径中。**

以下是一些示例：

``` syntax
te Examples\CPP.Pict.Example.dll /list /name:*SimpleTest*
Test Authoring and Execution Framework v2.9.3k for x86
        f:\ Examples\CPP.Pict.Example.dll
            WEX::TestExecution::Examples::PictExample
                WEX::TestExecution::Examples::PictExample::SimpleTest#0
                WEX::TestExecution::Examples::PictExample::SimpleTest#1
                WEX::TestExecution::Examples::PictExample::SimpleTest#2
                WEX::TestExecution::Examples::PictExample::SimpleTest#3
                WEX::TestExecution::Examples::PictExample::SimpleTest#4
                WEX::TestExecution::Examples::PictExample::SimpleTest#5
                WEX::TestExecution::Examples::PictExample::SimpleTest#6
                WEX::TestExecution::Examples::PictExample::SimpleTest#7
                WEX::TestExecution::Examples::PictExample::SimpleTest#8
                WEX::TestExecution::Examples::PictExample::SimpleTest#9
                WEX::TestExecution::Examples::PictExample::SimpleTest#10
                WEX::TestExecution::Examples::PictExample::SimpleTest#11
                WEX::TestExecution::Examples::PictExample::SimpleTest#12
                WEX::TestExecution::Examples::PictExample::SimpleTest#13
                WEX::TestExecution::Examples::PictExample::SimpleTest#14
                WEX::TestExecution::Examples::PictExample::SimpleTest#15
                WEX::TestExecution::Examples::PictExample::SimpleTest#16
                WEX::TestExecution::Examples::PictExample::SimpleTest#17
                WEX::TestExecution::Examples::PictExample::SimpleTest#18
                WEX::TestExecution::Examples::PictExample::SimpleTest#19
                WEX::TestExecution::Examples::PictExample::SimpleTest#20
                WEX::TestExecution::Examples::PictExample::SimpleTest#21
                WEX::TestExecution::Examples::PictExample::SimpleTest#22
                WEX::TestExecution::Examples::PictExample::SimpleTest#23
```

若要详细了解选择条件 (/select 和/name) ，请参阅选择 wiki 页。

``` syntax
te Examples\Csharp.Pict.Example.dll /listproperties /select:"@Name='*SumofSquare*'
                    and @Data:index>10
Test Authoring and Execution Framework v2.9.3k for x86
        f:\ Examples\CSharp.Pict.Example.dll
            WEX.Examples.CSharpPictExample
                WEX.Examples.CSharpPictExample.SumOfSquareRoots#11
                        Property[DataSource] = pict:SumofSquareRoots.txt
                        Data[a] = 1
                        Data[b] = ~-1
                WEX.Examples.CSharpPictExample.SumOfSquareRoots#12
                        Property[DataSource] = pict:SumofSquareRoots.txt
                        Data[a] = 2
                        Data[b] = ~-1
```

上面的示例演示如何使用索引进行选择。 您还可以选择基于数据值进行选择。

``` syntax
te Examples\Csharp.Pict.Example.dll /listproperties /select:"@Name='*SumofSquare*'
                    and (@Data:A='1' and @Data:B='1')"
Test Authoring and Execution Framework v2.9.3k for x86
        f:\ Examples\CSharp.Pict.Example.dll
            WEX.Examples.CSharpPictExample
                WEX.Examples.CSharpPictExample.SumOfSquareRoots#8
                        Property[DataSource] = pict:SumofSquareRoots.txt
                        Data[a] = 1
                        Data[b] = 1
```

## <a name="span-idpict_result_cachingspanspan-idpict_result_cachingspanspan-idpict_result_cachingspanpict-result-caching"></a><span id="PICT_Result_Caching"></span><span id="pict_result_caching"></span><span id="PICT_RESULT_CACHING"></span>PICT 结果缓存


某些模型文件可能非常复杂，可能需要更长的时间才能 Pict.exe 处理。 TAEF 尝试通过在 Te.exe 的给定执行期间缓存结果来减少结果的处理时间。 如果在同一执行运行中的后续测试引用相同的模型和 seed 文件组合，则 TAEF 将使用缓存的结果。 默认情况下，在每次执行结束时，将删除缓存的结果。

如果要继续在后续运行中利用缓存的结果，可以在执行期间在命令提示符下指定 "/persistPictResults" 选项。 每当你为命令指定 "/persistPictResults" 时，第一次执行 pict.exe 将实际执行并且可能需要很长时间，但在未修改模型和 seed 文件的情况下，所有后续运行将使用缓存的结果。 **注意：对于后续运行，你将需要继续指定 "/persistPictResults"。如果未指定任何后续运行，则在运行时将删除缓存的结果。**

如果保持 PICT 结果，并且使用缓存的数据是你在默认情况下要执行的操作，则可以将其设置为 te \_ cmd 环境变量的一部分，如下所示，无需在每次运行时都对其进行指定。 有关 te cmd 的详细信息，请参阅 [执行测试](executing-tests.md) \_ 。

``` syntax
set te_cmd = /persistPictResults
```

缓存的结果文件存储在% temp% 目录中名为 "TAEF" 的文件夹中，如果 Te.exe 有权访问它，或在从其启动 Te.exe 的当前执行目录中。 如果在执行过程中按 Ctrl + C，则唯一可能会导致不一致的状态。 在这种情况下，TAEF 将尝试删除缓存的结果，但如果无法执行此操作，则会在效果中看到错误。 此错误将提示您删除缓存的结果位置。 如果未执行此操作，可能会导致后续测试中发生未定义或错误的行为。

通过 TAEF 中的内置 PICT 支持，你现在可以在测试自动化中充分利用图像中的功能和 TAEF 中的功能。

## <a name="span-iddatasource_as_a_resourcespanspan-iddatasource_as_a_resourcespanspan-iddatasource_as_a_resourcespandatasource-as-a-resource"></a><span id="DataSource_as_a_Resource"></span><span id="datasource_as_a_resource"></span><span id="DATASOURCE_AS_A_RESOURCE"></span>作为资源的数据源


您可以在测试模块中添加 PICT 模型并播种文件作为资源。

在本机代码中，这是通过在数据源元数据中指定资源名称而不是文件名来完成的。 以下是示例：

```cpp
BEGIN_TEST_METHOD(ResourceNameDataSource)
    TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyModelResourceName?SeedingFile=MySeedingResourceName")
END_TEST_METHOD()
```

"MyModelResourceName" 和 "MySeedingResourceName" 是 .rc 文件中定义的资源名称。 资源类型需要是数据文件，这与资源类型需要为数据源 XML 的 [表数据源](table-data-source.md) 不同 \_ 。

```cpp
MyModelResourceName DATAFILE "model.txt"
MySeedingResourceName DATAFILE "seed.txt"
```

数据源元数据的值将保持不变，这与模型为文件时的值相同。 同样，在本机代码中，你可以使资源名称与文件名相同。 TAEF 将首先查找包含数据源名称的实际文件。 如果找不到该文件，则通过查看测试模块的资源来继续操作。 由于更改存储在资源中的数据源需要进行重新编译，因此，您可以通过将数据源文件复制到与测试 dll 相同的位置来利用这一设计，同时开发 (和命名资源名称，使其与文件名) 相同。 完成测试后，请移动 (不将文件) 复制回代码目录中，然后重新编译以嵌入资源。










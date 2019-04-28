---
title: PICT 数据源
description: PICT 数据源
ms.assetid: 75D3E086-C277-410d-B474-742A47ABB6AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb421c98d19598f40c31d140e2039b6271636666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355471"
---
# <a name="pict-data-source"></a>PICT 数据源


请确保您熟悉基本的 TAEF 执行，并且知道如何使用它，然后继续进行本部分中创建测试。

## <a name="span-idpictbackgroundandreferencesspanspan-idpictbackgroundandreferencesspanspan-idpictbackgroundandreferencesspanpict-background-and-references"></a><span id="PICT_Background_and_References"></span><span id="pict_background_and_references"></span><span id="PICT_BACKGROUND_AND_REFERENCES"></span>PICT 背景和引用


PICT 代表成对独立组合测试。 **PICT，可分别指定为每个参数的变体。** 例如，如果 API 测试取决于两个参数：文件名和文件扩展名，您能想到的可能的变体，以将分别传递文件名和 FileExtensions 如下所示：

-   文件名： a、 z12390，Realllyreallyreallylonglonglonglonglonglonglonglonglonglong，normallength
-   文件扩展名： txt、 png、 bat、 文档、 exe、 bmp、 wav

现在，您可以看到**暴力破解组合扩展**的更高版本 (4 X 7 = 28)**无法轻松地获取超出界限**您想象的更多的变体，以将添加到列表。 在此类测试用例方案中， **PICT 可以添加了许多值，通过生成一组精简参数结果以输入参数获取全面的组合覆盖率。**

## <a name="span-idpictsupportintaefspanspan-idpictsupportintaefspanspan-idpictsupportintaefspanpict-support-in-taef"></a><span id="PICT_Support_in_TAEF"></span><span id="pict_support_in_taef"></span><span id="PICT_SUPPORT_IN_TAEF"></span>在 TAEF PICT 支持


TAEF 提供 PICT 基于测试的内置支持。

若要这样做的优点，编写 pict.exe 你输入的模型文件便可正常。 请参阅\*上面提到的示例文件夹中的.txt 文件。 它可能有助于如果 PICT 执行，因此尝试在命令提示符下的第一个类似于按预期对您的模型文件，请尝试：

``` syntax
pict.exe <model file> [/e:<seed file>]
```

Pict.exe 现 TAEF 的最新版本共享上的二进制文件的其余部分了。

一个完成的 PICT 创作您的模型文件 （和种子文件） 和已验证它针对 pict.exe 在命令提示符下，您可以现在标记测试，以便让 TAEF 了解它们是 PICT 驱动测试。 如果您熟悉基于表的数据驱动的测试 TAEF 中可用，您将发现这非常类似。

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

托管的代码：

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

上面的示例中所示，您需要指定为数据源的模型文件的名称。 **你必须将模型文件的名称前缀"pict:"** ，并提供此数据源作为为你的测试方法。 对于托管测试时，就像使用任何其他数据驱动测试的 TAEF，必须提供的 TestContext 属性获取和设置方法，并在类中具有相同的专用实例。

如果你想要将命令选项传递给 PICT，您可以实现此目的使用元数据。 使用下表将 Pict.exe 的命令选项映射到 TAEF 元数据。


| pict.exe 命令语法 |                本机 TAEF 元数据语法                |           TAEF 元数据的托管的语法            |
|-------------------------|-----------------------------------------------------------|---------------------------------------------------|
|          /o:3           |        TEST\_METHOD\_PROPERTY(L"Pict:Order", L"3")        |        \[TestProperty("Pict:Order", "3")\]        |
|          /d:，           |   TEST\_METHOD\_PROPERTY(L"Pict:ValueSeparator", L",")    |   \[TestProperty("Pict:ValueSeparator", ",")\]    |
|           /a:           |                                                           | TEST\_METHOD\_PROPERTY(L"Pict:AliasSeparator", L" |
|          /n:~           | TEST\_METHOD\_PROPERTY(L"Pict:NegativeValuePrefix", L"~") | \[TestProperty("Pict:NegativeValuePrefix", "~")\] |
|      /e:test.seed       | TEST\_METHOD\_PROPERTY(L"Pict:SeedingFile", L"test.seed") | \[TestProperty("Pict:SeedingFile", "test.seed")\] |
|           /r            |      TEST\_METHOD\_PROPERTY(L"Pict:Random", L"true")      |      \[TestProperty("Pict:Random", "true")\]      |
|          /r:33          |     TEST\_METHOD\_PROPERTY(L"Pict:RandomSeed", L"33")     |     \[TestProperty("Pict:RandomSeed", "33")\]     |
|           /c            |  TEST\_METHOD\_PROPERTY(L"Pict:CaseSensitive", L"true")   |  \[TestProperty("Pict:CaseSensitive", "true")\]   |

按此顺序的优先级，可以在命令提示符下，在数据源属性中，或作为测试、 类或模块级别的元数据，设置的任何更高版本的元数据。 若要将其设置的命令提示符处，使用语法：

``` syntax
te.exe <test dll> /Pict:Order=3 /Pict:SeedingFile=test.seed
```

若要设置元数据的数据源属性中，追加问号字符 （？） 然后与符号分隔的元数据名称的一组使用的模型文件名称 = 元数据值对。 使用此方法时"Pict:"元数据名称的前缀是可选的。 下面是一个示例：

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:model.txt?Order=3&CaseSensitive=true&Random=true")
```

在幕后 TAEF 将提供到 PICT 所输入的模型文件和命令选项，并获取结果。 如果 PICT 生成任何错误或警告，你将看到这些记录按 TAEF 警告。 对于 PICT 生成每个生成输出行，TAEF 重新调用问题中的测试。

设置"Pict: RandomSeed"值将更改的默认值为"Pict： 随机"从 false 到 true。 这样一来，你可以显式设置"Pict： 随机"为 false，以获取 TAEF 忽略"Pict: RandomSeed"。

**允许使用 PICT.exe 在模型文件上执行并设定种子文件输入指定的默认超时值为 5 分钟。** 如果模型文件更为复杂，并且需要更多的时间超过 5 分钟的 PICT.exe 返回的结果，如指定，在上面的 CPP 示例所示，您可以重写此超时 **"Pict： 超时"** 元数据。 在示例中，1.5 分钟超时指定通过标准[TAEF 超时](taef-timeouts.md)格式。 其他 PICT 元数据，如"Pict： 超时"元数据继承，并因此可以指定对整个类或模块。

期间可以访问的数据值的给定调用从你的测试方法及其关联的设置和清理方法相同的方式一样的基于表 TAEF-对于本机代码使用 TestData 类和的 TestContext 数据驱动测试托管的代码如下所示：

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

托管的代码：

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

就像一样 TAEF 中的任何数据驱动测试与"索引"被保留并且不应作为参数名称。 索引隐式引用测试方法调用的索引，如果你的测试需要它，则可从测试方法进行访问。

**还有一点需要注意发生 PICT 时基于测试，所有参数的数据类型被假定为 WEX::Common::String （本机） String(managed) 或 VT\_BSTR(script)。** 转换和解释是留给用户。

完成创作使用 TAEF PICT 基于测试，现在可以从命令提示符下调用它，将所有 TAEF 提供的命令功能应用于它： 像 **/list**获取获取生成的所有测试方法的列表使用输出数据，为 PICT **/listproperties**以获取测试的列表以及它们是与等相关联的元数据和数据值的方法名称。对关键的一点**注意在开始之前，确保该 pict.exe 是在你的路径。**

以下是几个示例：

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

若要了解有关选择条件 (/ 选择和 /name) 请参阅选择 wiki 页面。

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

上面的示例显示如何选择使用索引。 您还可选择基于数据值。

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

## <a name="span-idpictresultcachingspanspan-idpictresultcachingspanspan-idpictresultcachingspanpict-result-caching"></a><span id="PICT_Result_Caching"></span><span id="pict_result_caching"></span><span id="PICT_RESULT_CACHING"></span>PICT 结果缓存


一些模型文件可能会非常复杂，并且可能需要更长时间才能 Pict.exe 得到处理。 TAEF 尝试通过 Te.exe 给定的执行过程中的缓存结果来缓解结果的处理时间。 如果运行在同一个执行后续测试引用相同的模型和种子文件组合，TAEF 将使用缓存的结果。 默认情况下，每次执行结束时缓存的结果会删除。

如果想要继续利用后续运行中的缓存的结果，可以指定"/ persistPictResults"命令提示符处执行期间的选项。 每当指定"/ persistPictResults"为你的命令，第一次执行实际执行 pict.exe，可能需要很长时间，但所有的后续运行将在其中的模型和播种文件都被未修改的情况下使用缓存的结果。 **注意：您将需要继续指定"/ persistPictResults"后续运行。未指定任何后续运行将删除该运行结束时缓存的结果。**

如果保留 PICT 结果，并使用缓存的数据是你想要默认情况下进行，可能会将其设置为你测试的一部分\_cmd 环境变量，如下所示，从而无需指定它在每次运行。 请参阅[执行测试](executing-tests.md)有关详细信息 te\_cmd。

``` syntax
set te_cmd = /persistPictResults
```

缓存的结果文件存储在名为"TAEF PICT"在 %temp%目录中，如果 Te.exe 有权访问它，或当前的执行目录中从 Te.exe 程序启动时所在的文件夹。 结果可能处于不一致状态的唯一情况是如果您按 Ctrl + C 在执行过程。 在这种情况下，TAEF 将尝试删除缓存的结果，但如果无法执行此操作，将看到一个错误，效果。 错误将提示您若要删除缓存的结果位置。 如果不做可能会导致在后续的测试中未定义或错误行为。

使用 TAEF 中内置 PICT 支持，您现在可以充分利用这种，PICT 中的功能以及在 TAEF 中您的测试自动化的功能。

## <a name="span-iddatasourceasaresourcespanspan-iddatasourceasaresourcespanspan-iddatasourceasaresourcespandatasource-as-a-resource"></a><span id="DataSource_as_a_Resource"></span><span id="datasource_as_a_resource"></span><span id="DATASOURCE_AS_A_RESOURCE"></span>为资源的数据源


测试模块中，可以作为资源添加 PICT 模型和种子设定的文件。

在本机代码中，这可通过在数据源元数据中指定的资源名称而不是文件名称。 下面是一个示例：

```cpp
BEGIN_TEST_METHOD(ResourceNameDataSource)
    TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyModelResourceName?SeedingFile=MySeedingResourceName")
END_TEST_METHOD()
```

"MyModelResourceName"和"MySeedingResourceName".rc 文件中定义的资源名称。 资源类型必须位于数据文件，与不同[表的数据源](table-data-source.md)的资源类型需要为数据源\_XML。

```cpp
MyModelResourceName DATAFILE "model.txt"
MySeedingResourceName DATAFILE "seed.txt"
```

数据源的元数据值时该模型是一个文件将保持不变。 同样在本机代码中，您可以制作资源名称是相同的作为文件的名称。 TAEF 将首先查看存在具有数据源名称的实际文件。 如果找不到该文件，它将继续通过在测试模块的资源中查找。 由于更改存储在资源中的数据源需要重新编译，因此可以通过覆盖数据源的文件与测试 dll 相同的位置复制在开发时利用这种设计 （和命名的文件的名称相同的资源名称）。 完成后测试 （而不是副本） 将文件移回到到代码目录和嵌入资源的重新编译。










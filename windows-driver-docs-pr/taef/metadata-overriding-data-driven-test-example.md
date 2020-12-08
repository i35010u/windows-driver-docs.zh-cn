---
title: 元数据覆盖数据驱动的测试示例
description: 元数据覆盖数据驱动的测试示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa80cc258325c0ed8472b0ec86bd64102766b851
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785421"
---
# <a name="metadata-overriding-data-driven-test-example"></a>元数据覆盖数据驱动的测试示例


本部分介绍了通过示例进行的数据驱动测试的一些高级功能。 如果你仍在介绍基础知识，你可能想要从一个 [简单的数据驱动的示例着手。](simple-data-driven-test-example.md)

引用的示例：

-   MetadataOverridingDataDrivenExample

-   DataDrivenMetadataOverridingExample

如果将此部分中所述的示例与 " [简单数据驱动示例](simple-data-driven-test-example.md) " 页中所述的示例进行比较，则您会注意到，唯一的区别在于，在测试中的各个级别上的元数据和属性已添加。 首先，让我们了解一下如何编写基本测试。

在本机示例中，观察下面代码示例中的第5行和第10行：

```cpp
1   class MetadataOverridingDataDrivenExample
2   {
3      BEGIN_TEST_CLASS(MetadataOverridingDataDrivenExample)
4          ...
5          TEST_CLASS_PROPERTY(L"Priority", L"2")
6      END_TEST_CLASS()
7    
8      BEGIN_TEST_METHOD(DataDrivenTest)
9          ...
10     TEST_METHOD_PROPERTY(L"Owner", L"wex")
11     END_TEST_METHOD()
12  }
```

因此类 "MetadataOverridingDataDrivenExample" 中定义的所有测试的优先级均为2。 请记住，测试可以将其上级别指定的任何元数据覆盖 (类或模块) 。 在这种情况下，DataDrivenTest 方法仍保持优先级2，并将其 "所有者" 定义为 "WEX"。 现在，如果这是一个非数据驱动的测试，则可以选择基于任何此/select： " @Priority = 2" 或/select： " @Owner = ' WEX '"，并在其中执行测试方法。 但 **对于数据驱动的测试，可以通过在 "行" 级别指定元数据来进一步覆盖测试方法级别适用的属性。**

让我们看看该 XML 文件以了解如何操作。

```cpp
    1  <?xml version="1.0"?>
    2  <Data>
    3    <Table Id="MetadataTable">
    4      <ParameterTypes>
    5        <ParameterType Name="Size">int</ParameterType>
    6      </ParameterTypes>
    7      <Row Priority="1">
    8        <Parameter Name="Size">4</Parameter>
    9        <Parameter Name="Color">White</Parameter>
    10      </Row>
    11      <Row Owner="C2">
    12        <Parameter Name="Size">10</Parameter>
    13        <Parameter Name="Color">Black</Parameter>
    14      </Row>
    15      <Row Priority="1" Owner="C3">
    16        <Parameter Name="Size">9</Parameter>
    17        <Parameter Name="Color">Orange</Parameter>
    18      </Row>
    19      <Row>
    20        <Parameter Name="Size">9</Parameter>
    21        <Parameter Name="Color">Blue</Parameter>
    22      </Row>
    23    </Table>
    24  </Data>
```

在前三行中，该示例通过显式指定特定数据值集的元数据来重写某些元数据。 但最后一组数据与包含它的方法具有相同的元数据： Priority = 2，Owner = WEX。

首先，让我们看一下托管代码，然后查看这些测试的选择和执行。

```cpp
1   [TestClass]
2   public class DataDrivenMetadataOverridingExample
3   {
4      [ClassInitialize]
5      [Priority(2)]
6      public static void MyClassInitialize(Object testContext)
7      {
8      }
9   
9      [TestMethod]
10     ...
11     [TestProperty("Owner", "WEX")]
12     public void DataDrivenTest()
13     {
14        ...
15     }
...
```

你将在此处完全模拟本机示例中的属性。

现在，让我们先了解一下替代的内容：

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*overriding*' and @Priority=1"
```

将运行

-   WEX.例如，DataDrivenMetadataOverridingExample. DataDrivenTest \# 0
-   WEX.例如，DataDrivenMetadataOverridingExample. DataDrivenTest \# 2

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*overriding*' and @Priority=1"
```

将运行：

-   WEX：： Testexecution.completed：：示例：： MetadataOverridingDataDrivenExample：:D ataDrivenTest \# 0
-   WEX：： Testexecution.completed：：示例：： MetadataOverridingDataDrivenExample：:D ataDrivenTest \# 2

## <a name="span-idexercise_for_the_readerspanspan-idexercise_for_the_readerspanspan-idexercise_for_the_readerspanexercise-for-the-reader"></a><span id="Exercise_for_the_reader"></span><span id="exercise_for_the_reader"></span><span id="EXERCISE_FOR_THE_READER"></span>读者的练习


作为练习，尝试添加新的元数据值。 仅改变以上示例中的选择条件，

``` syntax
/select:"@Name='*overriding*' and @Owner='WEX'"
```

将 \# \# 在托管和本机示例中运行带有索引0和3的数据驱动的测试

``` syntax
 /select:"@Name='*overriding*' and @Priority=2"
```

将运行索引为1和3的数据驱动测试 \# \# ，并在托管示例中运行 NonDataDrivenTest

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /name:*overriding* /listproperties
    F:\ Examples\CPP.DataDriven.Example.dll
        WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample
                Property[Priority] = 2

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#0
                    Property[Owner] = WEX
                    Property[Priority] = 1
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = White
                    Data[Size] = 4

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#1
                    Property[Owner] = C2
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = Black
                    Data[Size] = 10

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#2
                    Property[Owner] = C3
                    Property[Priority] = 1
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#3
                    Property[Owner] = WEX
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = Blue
                    Data[Size] = 9

    F:\ Examples\CSharp.DataDriven.Example.dll
        WEX.Examples.DataDrivenMetadataOverridingExample
                Setup: MyClassInitialize
                Property[Priority] = 2

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#0
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = WEX
                    Property[Priority] = 1

                    Data[Color] = White
                    Data[Size] = 4

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#1
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = C2

                    Data[Color] = Black
                    Data[Size] = 10

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#2
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = C3
                    Property[Priority] = 1

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#3
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = WEX

                    Data[Color] = Blue
                    Data[Size] = 9

        WEX.Examples.DataDrivenMetadataOverridingExample.NonDataDrivenTest
```

 

 






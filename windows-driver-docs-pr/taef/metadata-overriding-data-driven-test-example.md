---
title: 元数据重写数据驱动的测试示例
description: 元数据重写数据驱动的测试示例
ms.assetid: F39A556F-1816-4272-ABDE-62164AE09685
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef422f67aeca894b264e45d4013127bbaefa4b82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521189"
---
# <a name="metadata-overriding-data-driven-test-example"></a>元数据重写数据驱动的测试示例


本部分介绍了数据驱动测试例举的操作的一些高级的功能。 如果仍是否涵盖了基础知识，您可能开始想[简单数据驱动的示例。](simple-data-driven-test-example.md)

引用的示例：

-   MetadataOverridingDataDrivenExample

-   DataDrivenMetadataOverridingExample

如果进行比较的示例中介绍到的此部分涵盖[简单的数据驱动示例](simple-data-driven-test-example.md)页上，你会注意到，唯一的区别是该元数据，在测试中的不同级别的属性具有已添加。 允许第一个介绍如何编写基本测试。

在本机的示例中，观察行 5 和 10 中下面的代码示例：

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

类"MetadataOverridingDataDrivenExample"中定义的所有测试都的优先级为 2。 请记住，测试可以重写在高于其 （类或模块） 的级别上指定任何元数据。 在这种情况下，DataDrivenTest 方法仍维护优先级 2，并具有其"所有者"定义为"WEX"。 现在，如果这是非数据驱动的测试，您可以选择基于此，任何/选择:"@Priority= 2" 或 /select:"@Owner= WEX"，并在其中执行测试方法。 但**通过数据驱动测试，您可以进一步重写在测试方法级别适用的属性通过指定"行"级别的元数据。**

让我们看一下 XML 文件以了解如何。

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

在前 3 个行中，该示例重写一些元数据通过显式指定特定的数据值集的元数据。 最后一组数据但是具有不同的元数据作为包含它的方法：优先级 = 2，所有者 = WEX。

让我们看一看托管代码之前查找到的所选内容和执行这些测试。

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

将在这里也完全模拟本机示例中的属性。

现在，重写更好地了解一下：

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*overriding*' and @Priority=1"
```

将运行

-   WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest\#0
-   WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest\#2

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*overriding*' and @Priority=1"
```

将运行：

-   WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest\#0
-   WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest\#2

## <a name="span-idexerciseforthereaderspanspan-idexerciseforthereaderspanspan-idexerciseforthereaderspanexercise-for-the-reader"></a><span id="Exercise_for_the_reader"></span><span id="exercise_for_the_reader"></span><span id="EXERCISE_FOR_THE_READER"></span>留给读者进行练习


作为一个练习，请尝试添加新的元数据值。 只改变在上述示例中，选择条件

``` syntax
/select:"@Name='*overriding*' and @Owner='WEX'"
```

将运行数据驱动测试具有索引\#0 和\#中托管和本机示例 3

``` syntax
 /select:"@Name='*overriding*' and @Priority=2"
```

将运行数据驱动测试具有索引\#1 和\#3，也可以在托管的示例运行 NonDataDrivenTest

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

 

 






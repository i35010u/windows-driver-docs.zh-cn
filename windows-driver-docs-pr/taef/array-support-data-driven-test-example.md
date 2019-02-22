---
title: 数组支持数据驱动的测试示例
description: 数组支持数据驱动的测试示例
ms.assetid: ECCDE395-C887-4485-8C8F-312EFCFD16A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362c60743ed9db0252e7e42da1f871ba1e530af9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545502"
---
# <a name="array-support-data-driven-test-example"></a>数组支持数据驱动的测试示例


本部分介绍了数据驱动测试例举的操作的一些高级的功能。 如果仍是否涵盖了基础知识，您可能开始想[简单的数据驱动示例](data-driven-testing.md)。

引用的示例：

-   ArraySupportDataDrivenExample

-   CSharpDataDrivenArraySupportExample

前面部分已经提到数据驱动测试创作和执行的基础知识。 以下列表介绍了的含义**数组**TAEF 数据驱动测试的意义上说：

-   **数组为可变长度，将被视为单个参数的元素的同类类型集。**
-   **若要指定数组类型，您需要显式 ParameterTypes 块中指定的参数类型并添加一个数组 ="true"属性。**

列出了支持的参数类型[此处](parameter-types-in-table-data-sources.md)。

如果指定任何其他数据类型，则测试将引发警告，并就会认为它是一个字符串。 对于数组，将视为数据类型为类型字符串\[\]。

下面的示例演示如何指定该参数是一种基本类型的数组。 务必要注意的是，没有默认类型允许在数组-的情况下必须显式指定类型并设置**数组**参数为 true 的属性。

```cpp
1  <?xml version="1.0"?>
2  <Data>
3    <Table Id="ArraySupportTable">
4      <ParameterTypes>
5        <ParameterType Name="Size" Array="true">int</ParameterType>
6        <ParameterType Name="Color" Array="true">String</ParameterType>
7      </ParameterTypes>
8      <Row>
9        <Parameter Name="Size">4</Parameter>
10       <Parameter Name="Color">White</Parameter>
11     </Row>
12     <Row>
13       <Parameter Name="Size">
14         <Value>4</Value>
15         <Value>6</Value>
16         <Value>8</Value>
17       </Parameter>
18       <Parameter Name="Color">
19         <Value>Red</Value>
20         <Value>Green</Value>
21         <Value>Blue</Value>
22       </Parameter>
23     </Row>
24     <Row>
25       <Parameter Name="Size">
26         <Value>9</Value>
27         <Value>12</Value>
28         <Value>16</Value>
29       </Parameter>
30       <Parameter Name="Color">Orange</Parameter>
31     </Row>
32     <Row>
33       <Parameter Name="Size">9</Parameter>
34       <Parameter Name="Color">
35         <Value>White</Value>
36         <Value>Black</Value>
37       </Parameter>
38     </Row>
39   </Table>
40 </Data>
```

检查**值**标记和**数组**上面的示例中的属性。 首先，您必须显式指定类型为**大小**并**颜色**参数，并指定这些参数是数组，通过设置**数组**属性 **，则返回 true**。 然后指定在其值**&lt;值&gt;...&lt;/值&gt;** 标记。 可以有任意多个&lt;值&gt;标记可以根据需要指定任意数量的给定的行的参数数组中的值。

请注意 9、 10、 30 和 33 上面的 XML 示例中的行。 这些条目是单个值的数组元素。 换而言之，**可以指定单个值的数组元素中直接&lt;参数&gt;标记，而无需额外&lt;值&gt;标记。** 此外，**即使行中的参数具有只有一个值，它仍被视为一个元素的数组和无法否则检索。**

现在，看看 Api 的检索。

## <a name="span-idnativeretrievalspanspan-idnativeretrievalspanspan-idnativeretrievalspannative-retrieval"></a><span id="Native_Retrieval"></span><span id="native_retrieval"></span><span id="NATIVE_RETRIEVAL"></span>本机检索


数组元素可以在本机代码中，通过使用来检索**WEX::TestExecution::TestDataArray&lt; &gt;** 模板类。 请参阅已发布标头 TestData.h，有关详细信息。 **TestDataArray**类管理数组元素的生存期并提供有用的 Api 来检索数组中的特定值：

```cpp
1  namespace WEX { namespace TestExecution
2  {
3      template <typename T>
4      class TECOMMON_API TestDataArray sealed
5      {
6         ...
7      public:
8          TestDataArray();
9          ~TestDataArray();
10         const size_t GetSize() const;
11         T& operator[](size_t index);
12
13     private:
14        ...
15     };
16 } /* namespace TestExecution */ } /* namespace WEX */
```

可以通过调用获取数组的长度**GetSize** ，并可以通过使用运算符获取的特定元素**\[ \]**。

下一步的示例演示如何在代码中使用这些函数。 本机的示例中的 cpp 文件，请考虑：

```cpp
1  TestDataArray<int> sizes;
2  if (SUCCEEDED(TestData::TryGetValue(L"size", sizes)))
3  {
4      size_t count = sizes.GetSize();
5      for (size_t i = 0; i < count; ++i)
6      {
7          Log::Comment(String().Format(L"Size[%d] retrieved was %d", i, sizes[i]));
8      }
9  }
10
11 TestDataArray<String> colors;
12 if (SUCCEEDED(TestData::TryGetValue(L"color", colors)))
13 {
14     size_t count = colors.GetSize();
15     for (size_t i = 0; i < count; ++i)
16     {
17         Log::Comment(String().Format(L"Color[%d] retrieved was ", i) + colors[i]);
18     }
19 }
```

首先，定义数组类型的本地 TestDataArray。 在这种情况下，**大小**是 int 类型的数组并**颜色**是 WEX::Common::String 类型的数组。 若要检索一组 API 是类似于检索的任何变量。 在调用**TestData::TryGetValue**，要求它检索参数**大小**，并将值放入本地变量**大小**。

**请注意，尝试检索非数组指定到一个数组的参数将导致错误，则测试失败。同样，尝试检索到非数组变量中，一个数组，即使数组只有一个元素，将导致错误。**

如果数组参数中未指定 XML 行根本，尝试检索参数失败。 例如，如果某行查看，如：

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

请注意，参数**大小**，它数组中，未指定的行中。 如果您尝试检索**大小**代码，从 API 调用将返回失败返回代码。 您可以使用此定义默认数组值。

但是，通过指定一个空的参数标记可以指定一个空数组**大小**，如下所示：

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

在这种情况下，尝试检索**大小**会成功，但数组大小将为 0。

## <a name="span-idmanagedretrievalspanspan-idmanagedretrievalspanspan-idmanagedretrievalspanmanaged-retrieval"></a><span id="Managed_Retrieval"></span><span id="managed_retrieval"></span><span id="MANAGED_RETRIEVAL"></span>托管的检索


托管的检索像以前一样仍几乎相同-只有你需要确保检索到适当的数组类型的本地变量的值。 请考虑下面的托管的示例：

```cpp
1  Int32[] sizes = m_testContext.DataRow["Size"] as Int32[];
2  foreach (int size in sizes)
3  {
4          Verify.AreNotEqual(size, 0);
5          Console.WriteLine("Size is " + size.ToString());
6  }
7
8  String[] colors = m_testContext.DataRow["Color"] as String[];
9  foreach (String color in colors)
10 {
11         Console.WriteLine("Color is " + color);
12 }
```

类似于本机检索，如果数组参数未指定所有尝试检索的 XML 行中该参数返回类型的对象**System.DBNull**。 例如，如果某行查看，如：

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

请注意，参数**大小**，它数组中，未指定的行中。 如果您尝试检索**大小**代码，从 API 调用将返回类型的对象**DBNull**。 如果表中有任何此类值，你可能想要它们从上下文转换为对象首先检索和比较针对对象的类型后采取适当步骤**typeof(System.DBNull)** 或您的类型exepecting 它为。

但是，您可以通过指定一个空的参数标记指定一个空数组**大小**，如下所示：

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

在这种情况下，尝试检索**大小**succeessfully 返回类型的空数组**System.Int32\[\]**。

## <a name="span-idexecutionspanspan-idexecutionspanspan-idexecutionspanexecution"></a><span id="Execution"></span><span id="execution"></span><span id="EXECUTION"></span>执行


执行数据驱动测试支持数组是从执行任何其他数据驱动的测试没有什么不同。 仅要点的区别是，**在数组数据参数，而不是"等于"表示"包含"的情况下的选择条件更改 sematics。**

若要查看这意味着，假设你想要选择所有数据驱动测试位置**颜色**数组包含值**白色**。 若要执行此操作，运行：

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

此命令将运行数据驱动的测试具有索引\#0 和\#3 在两个以上的方案。

您可以生成更复杂查询的说，例如，在其中选择仅测试**颜色**数组包含**白色**并**颜色**数组包含**黑色**，这会仅选择数据驱动测试具有索引\#3。 作为一个练习，请尝试编写并执行此查询自己。

 

 






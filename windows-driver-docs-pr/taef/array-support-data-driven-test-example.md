---
title: 数组支持数据驱动的测试示例
description: 数组支持数据驱动的测试示例
ms.assetid: ECCDE395-C887-4485-8C8F-312EFCFD16A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80891fa370f9e172e713001cd3582ba7886965e3
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402290"
---
# <a name="array-support-data-driven-test-example"></a>数组支持数据驱动的测试示例


本部分介绍了通过示例进行的数据驱动测试的一些高级功能。 如果你仍在介绍基础知识，你可能想要从一个[简单的数据驱动的示例](data-driven-testing.md)着手。

引用的示例：

-   ArraySupportDataDrivenExample

-   CSharpDataDrivenArraySupportExample

前面几节已介绍数据驱动的测试创作和执行的基本知识。 下面的列表讨论 TAEF 数据驱动的测试意义中**数组**的含义：

-   **数组是可变长度、同类类型的元素，这些元素将被视为单个参数。**
-   **若要指定数组类型，需要显式指定 ParameterTypes 块中的参数类型，并添加 Array = "true" 属性。**

[表数据源的参数类型](parameter-types-in-table-data-sources.md)中列出了支持的参数类型。

如果指定任何其他数据类型，则测试将引发警告，并将其视为一个字符串。 对于数组，数据类型将被视为字符串类型 \[ \] 。

下面的示例演示如何指定该参数是一个基本类型的数组。 需要注意的是，在数组的情况下不允许使用默认类型-必须显式指定类型并将参数的**数组**特性设置为 true。

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

在上面的示例中检查**值**标记和**数组**特性。 首先，必须显式指定**大小**和**颜色**参数的类型，并指定这些参数是数组，方法是将**数组**特性设置为**true**。 然后，将值指定为** &lt; ... &gt; &lt;/Value &gt; **标记。 您可以根据需要为任意数量 &lt; &gt; 的值标记指定数组中给定行的参数的任意数目的值。

请注意上面的 XML 示例中的第9、10、30和33行。 这些项是单值数组元素。 换言之，**您可以在参数标记中直接指定单个值数组元素 &lt; ， &gt; 而无需其他 &lt; 值 &gt; 标记。** 此外，**即使行中的参数只有一个值，仍会将其视为一个元素的数组，否则无法进行检索。**

现在，请看一下检索 Api。

## <a name="span-idnative_retrievalspanspan-idnative_retrievalspanspan-idnative_retrievalspannative-retrieval"></a><span id="Native_Retrieval"></span><span id="native_retrieval"></span><span id="NATIVE_RETRIEVAL"></span>本机检索


可以使用**WEX：： testexecution.completed &lt; &gt; ：： TestDataArray**模板类在本机代码中检索数组元素。 有关详细信息，请参阅发布的标头 TestData。 **TestDataArray**类管理数组元素的生存期，并提供有用的 api 来检索数组中的特定值：

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

可以通过调用**GetSize**来获取数组的长度，并使用运算符获取特定元素 **\[\]** 。

下一个示例演示如何在代码中使用这些函数。 请考虑本机示例中的 cpp 文件：

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

首先，定义数组类型的本地 TestDataArray。 在这种情况下，**大小**是 int 类型的数组，**颜色**是 WEX：： Common：： String 类型的数组。 用于检索数组的 API 与检索任何变量的 API 类似。 调用**TestData：： TryGetValue**，请求它检索参数**大小**，并将该值放入本地变量**大小**。

**请注意，尝试将未指定的非数组指定参数检索到数组中会导致错误并导致测试失败。同样，即使数组只包含一个元素，也会尝试将数组检索到非数组变量中，这会导致错误。**

如果根本没有在 XML 行中指定数组参数，则尝试检索参数会失败。 例如，如果某行如下所示：

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

请注意，行中未指定参数**大小**，即数组。 如果尝试从代码中检索**大小**，则 API 调用将返回失败的返回代码。 您可以使用此定义一个默认的数组值。

另一方面，可以指定一个空数组，方法是指定**大小**为的空参数标记，如下所示：

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

在这种情况下，尝试检索**大小**会成功，但数组大小为0。

## <a name="span-idmanaged_retrievalspanspan-idmanaged_retrievalspanspan-idmanaged_retrievalspanmanaged-retrieval"></a><span id="Managed_Retrieval"></span><span id="managed_retrieval"></span><span id="MANAGED_RETRIEVAL"></span>托管检索


托管检索与之前完全相同，需要确保将值检索到适当数组类型的局部变量中。 请考虑以下托管示例：

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

与本机检索类似，如果根本没有在 XML 行中指定数组参数，则尝试检索参数将返回类型为**DBNull**的对象。 例如，如果某行如下所示：

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

请注意，行中未指定参数**大小**，即数组。 如果尝试从代码中检索**大小**，则 API 调用会返回类型为**DBNull**的对象。 如果表中有任何此类值，则可能需要先将它们从上下文中检索到对象，然后在将对象类型与**typeof （exepecting）** 或要将其转换为的类型进行比较之后采取适当的措施。

另一方面，你可以指定一个空数组，方法是指定**大小**为的空参数标记，如下所示：

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

在这种情况下，尝试检索**大小**succeessfully 将返回类型为**system.object \[ \] **的空数组。

## <a name="span-idexecutionspanspan-idexecutionspanspan-idexecutionspanexecution"></a><span id="Execution"></span><span id="execution"></span><span id="EXECUTION"></span>操作


执行支持数组的数据驱动的测试与执行任何其他数据驱动的测试没有区别。 唯一的关键点在于，**在数组数据参数的情况下，选择条件的 sematics 会更改为表示 "contains" 而不是 "等于"。**

若要查看这意味着什么，假设要选择**颜色**数组包含值**白色**的所有数据驱动的测试。 若要执行此操作，请运行：

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

\#在上述两种情况下，此命令将运行索引为0和3的数据驱动的测试 \# 。

您可以生成更复杂的查询，例如，仅选择**color**数组包含**白色**的测试，**颜色**数组包含**黑色**，这只会选择带有索引3的数据驱动的测试 \# 。 作为练习，尝试自行编写和执行此查询。

 

 






---
title: 数据驱动的类
description: 数据驱动的类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd55a093d79ccfcc9aa6b3973d047b8d7f5b59ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840479"
---
# <a name="span-idtaefdata-driven_classspandata-driven-class"></a><span id="taef.data-driven_class"></span>数据驱动的类


请确保熟悉 TAEF 的基本执行，并知道如何使用它创作测试，然后再继续此部分。 你可能还需要浏览简单的数据驱动的测试示例。 在本部分中，您将创建一个基于 *表* 的数据驱动测试的数据驱动型测试类，但这种方法适用于基于 *WMI* 或 *基于 PICT* 的数据驱动的测试。

## <a name="span-idwhentouse_ddcspanspan-idwhentouse_ddcspanwhen-to-use-a-data-driven-class"></a><span id="whentouse_ddc"></span><span id="WHENTOUSE_DDC"></span>何时使用数据驱动类？


有时，多个测试可能依赖于相同的输入数据。 测试 Api 时，可能需要运行包含相同数据的多个 API 测试，以获得一致的 API 行为视图。 执行方案级测试时，可能需要确保用相同的数据测试方案中的所有步骤。 在这种情况下，在类级别指定测试数据很有用。

## <a name="span-idauthoring_ddcspanspan-idauthoring_ddcspanauthoring-data-driven-class"></a><span id="authoring_ddc"></span><span id="AUTHORING_DDC"></span>创作数据驱动类


您可以指定给定的类是数据驱动的，这与您指定给定测试是数据驱动的方式类似。 在类级别应用 **数据源** 元数据。 值标识感兴趣的特定数据源。 下面的示例演示如何为数据驱动类指定以下属性：

### <a name="span-idnative1_authoringspanspan-idnative1_authoringspannative-code"></a><span id="native1_authoring"></span><span id="NATIVE1_AUTHORING"></span>本机代码

```cpp
1     class 2     {
2         BEGIN_TEST_CLASS(DataDrivenClassExample)
3             TEST_CLASS_PROPERTY(L"DataSource", L"Table:DataDrivenClassExample.xml#ClassTable")
4         END_TEST_CLASS()
5
6         TEST_METHOD(Test1);
7       {
8         int size;
9           if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"size", size)</span>))
10          {
11              VERIFY_ARE_NOT_EQUAL(size, 0);
12              Log::Comment(String().Format(L"Size retrieved was %d", size));
13          }
14  
15          String color;
16          if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"color", color)</span>))
17          {
18              Log::Comment(L"Color retrieved was " + color);
19          }
20      }
21         TEST_METHOD(Test2);
22      {
23          int size;
24          if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"size", size)</span>))
25          {
26              VERIFY_ARE_NOT_EQUAL(size, 0);
27              Log::Comment(String().Format(L"Size retrieved was %d", size));
28          }
29  
30          String color;
31          if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"color", color)</span>))
32          {
33              Log::Comment(L"Color retrieved was " + color);
34          }
35      } 
36    };
```

### <a name="span-idmanaged1_authoringspanspan-idmanaged1_authoringspanmanaged-code"></a><span id="managed1_authoring"></span><span id="MANAGED1_AUTHORING"></span>托管代码

```cpp
1     [TestClass]
2     public class CSharpDataDrivenClassExample
3     {
4         [ClassInitialize]
5         [DataSource("Table:CSharpDataDrivenClassExample.xml#ClassTable")]
6         public static void MyClassInitialize(Object testContext)
7         {
8         }
9
10        [TestMethod]
11        public void Test1()
12        {
13            int size = (int)m_testContext.DataRow["Size"];
14            Verify.AreNotEqual(size, 0);
15            Log.Comment("Size is " + size.ToString());
16
18            Log.Comment("Color is " + m_testContext.DataRow["Color"]);
19        }
20
21        [TestMethod]
22        public void Test2()
23        {
24            int size = (int)m_testContext.DataRow["Size"];
25            Verify.AreNotEqual(size, 0);
26            Log.Comment("Size is " + size.ToString());
27
28            Log.Comment("Color is " + m_testContext.DataRow["Color"]);
29        }
30
31        public TestContext TestContext
32        {
33            get { return m_testContext; }
34            set { m_testContext = value; }
35        }
36
37        private TestContext m_testContext;
38    }
```

在这些示例中， **本机代码** 示例中的第3行和 **托管代码** 示例中的第5行是在 TAEF 中为数据驱动的测试类指定数据源的建议方法。

在上述 **托管代码** 示例中，第13、18、24和28行说明了如何将数据提供给托管代码的测试方法。

在下面的代码示例中，第4、11、20和27行显示了如何将数据提供给本机代码的测试方法。 请注意，*_你将在数据驱动类的表中定义的数据 (行) 可用于类 (Test1 和 Test2) 中的测试方法，其方式与对数据驱动的测试完全相同。_* _

### <span id="native2_authoring"></span><span id="NATIVE2_AUTHORING"></span>

构造数据驱动类的 _ *DataSource** XML 文件的方式与对数据驱动测试的处理方式完全相同。 下面的示例演示本机类和托管类的 XML 文件。

### <a name="span-idnative3_authoringspanspan-idnative3_authoringspannative"></a><span id="native3_authoring"></span><span id="NATIVE3_AUTHORING"></span>本机

```cpp
1 <?xml version="1.0"?>
2 <Data>
3   <Table Id="ClassTable">
4     <ParameterTypes>
5       <ParameterType Name="Size">int</ParameterType>
6     </ParameterTypes>
7     <Row>
8       <Parameter Name="Size">4</Parameter>
9       <Parameter Name="Color">White</Parameter>
10    </Row>
11    <Row>
12      <Parameter Name="Size">10</Parameter>
13      <Parameter Name="Color">Black</Parameter>
14    </Row>
15    <Row>
16      <Parameter Name="Size">9</Parameter>
17      <Parameter Name="Color">Orange</Parameter>
18    </Row>
19    <Row>
20      <Parameter Name="Size">9</Parameter>
21      <Parameter Name="Color">Blue</Parameter>
22    </Row>
23  </Table>
24</Data>
```

### <a name="span-idmanged2_authoringspanspan-idmanged2_authoringspanmanaged"></a><span id="manged2_authoring"></span><span id="MANGED2_AUTHORING"></span>经过

```cpp
1 <?xml version="1.0"?>
2 <Data>
3   <Table Id="ClassTable">
4     <ParameterTypes>
5       <ParameterType Name="Size">Int32</ParameterType>
6       <ParameterType Name="Color">String</ParameterType>
7     </ParameterTypes>
8     <Row>
9      <Parameter Name="Size">4</Parameter>
10      <Parameter Name="Color">White</Parameter>
11    </Row>
12    <Row>
13      <Parameter Name="Size">10</Parameter>
14      <Parameter Name="Color">Black</Parameter>
15    </Row>
16    <Row>
17      <Parameter Name="Size">9</Parameter>
18      <Parameter Name="Color">Orange</Parameter>
19    </Row>
20    <Row>
21      <Parameter Name="Size">9</Parameter>
22      <Parameter Name="Color">Blue</Parameter>
23    </Row>
24  </Table>
25</Data>
```

## <a name="span-idbehindscene_ddcspanspan-idbehindscene_ddcspanbehind-the-scenes-or-what-to-expect"></a><span id="behindscene_ddc"></span><span id="BEHINDSCENE_DDC"></span>在幕后或预期的情况如何？


默认情况下，当你在 TAEF 中创作测试时，类中的执行顺序与类中的测试方法编码顺序相同。 因此，在前面的示例中， **Test1** 将始终在 **Test2** 之前执行。 由于包含 **Test1** 和 **Test2** 的类是数据驱动类，因此，所有类方法将为在 **DataSource** 中定义的每个数据行执行一次。 换句话说， **Test1** 和 **Test2** 对第0行执行 \# 。 然后，这些方法的执行顺序与第1行相同， \# 依此类推，直到 TAEF 执行所有行。

## <a name="span-idexecuting_ddcspanspan-idexecuting_ddcspanexecuting-tests-in-a-data-driven-class"></a><span id="executing_ddc"></span><span id="EXECUTING_DDC"></span>在数据驱动类中执行测试


如果用 **/list** 命令选项执行示例测试二进制文件，则上一节中的执行顺序将变为清晰。

### <a name="span-idnative1_executingspanspan-idnative1_executingspannative"></a><span id="native1_executing"></span><span id="NATIVE1_EXECUTING"></span>本机

``` syntax
TE.exe Examples\CPP.AdvancedDataDriven.Examples.dll /name:*class* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CPP.AdvancedDataDriven.Examples.dll
            WEX::TestExecution::Examples::DataDrivenClassExample#0
                WEX::TestExecution::Examples::DataDrivenClassExample#0::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#0::Test2
            WEX::TestExecution::Examples::DataDrivenClassExample#1
                WEX::TestExecution::Examples::DataDrivenClassExample#1::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#1::Test2
            WEX::TestExecution::Examples::DataDrivenClassExample#2
                WEX::TestExecution::Examples::DataDrivenClassExample#2::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#2::Test2
            WEX::TestExecution::Examples::DataDrivenClassExample#3
                WEX::TestExecution::Examples::DataDrivenClassExample#3::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#3::Test2
```

### <a name="span-idmanaged1_executingspanspan-idmanaged1_executingspanmanaged"></a><span id="managed1_executing"></span><span id="MANAGED1_EXECUTING"></span>经过

``` syntax
TE.exe Examples\CSharp.AdvancedDataDriven.Examples.dll /name:*class* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CSharp.AdvancedDataDriven.Examples.dll
            WEX.Examples.CSharpDataDrivenClassExample#0
                WEX.Examples.CSharpDataDrivenClassExample#0.Test1
                WEX.Examples.CSharpDataDrivenClassExample#0.Test2
            WEX.Examples.CSharpDataDrivenClassExample#1
                WEX.Examples.CSharpDataDrivenClassExample#1.Test1
                WEX.Examples.CSharpDataDrivenClassExample#1.Test2
            WEX.Examples.CSharpDataDrivenClassExample#2
                WEX.Examples.CSharpDataDrivenClassExample#2.Test1
                WEX.Examples.CSharpDataDrivenClassExample#2.Test2
            WEX.Examples.CSharpDataDrivenClassExample#3
                WEX.Examples.CSharpDataDrivenClassExample#3.Test1
                WEX.Examples.CSharpDataDrivenClassExample#3.Test2
```

请注意，上述示例中的索引类似于数据驱动的测试。 数据驱动类中的每一行都由索引标识。 与在数据驱动的测试中一样， **您可以选择在 XML 文件的行级别指定元数据，并在列出或执行测试时打印该名称，从而为行指定更有意义的短 *名称* 。**

同样，你可以使用 **/listproperties** 选项来确认数据是否确实已在类级别上指定和可用。

### <a name="span-idnative2_executingspanspan-idnative2_executingspannative"></a><span id="native2_executing"></span><span id="NATIVE2_EXECUTING"></span>本机

``` syntax
F:\ Examples\CPP.AdvancedDataDriven.Examples.dll
    WEX::TestExecution::Examples::DataDrivenClassExample#0
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = White
            Data[Size] = 4
        WEX::TestExecution::Examples::DataDrivenClassExample#0::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#0::Test2

    WEX::TestExecution::Examples::DataDrivenClassExample#1
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = Black
            Data[Size] = 10
        WEX::TestExecution::Examples::DataDrivenClassExample#1::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#1::Test2

    WEX::TestExecution::Examples::DataDrivenClassExample#2
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = Orange
            Data[Size] = 9
        WEX::TestExecution::Examples::DataDrivenClassExample#2::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#2::Test2

    WEX::TestExecution::Examples::DataDrivenClassExample#3
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = Blue
            Data[Size] = 9
        WEX::TestExecution::Examples::DataDrivenClassExample#3::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#3::Test2
```

### <a name="span-idmanaged2_executingspanspan-idmanaged2_executingspanmanaged"></a><span id="managed2_executing"></span><span id="MANAGED2_EXECUTING"></span>经过

``` syntax
F:\ Examples\CSharp.AdvancedDataDriven.Examples.dll
    WEX.Examples.CSharpDataDrivenClassExample#0
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = White
            Data[Size] = 4
        WEX.Examples.CSharpDataDrivenClassExample#0.Test1
        WEX.Examples.CSharpDataDrivenClassExample#0.Test2

    WEX.Examples.CSharpDataDrivenClassExample#1
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = Black
            Data[Size] = 10
        WEX.Examples.CSharpDataDrivenClassExample#1.Test1
        WEX.Examples.CSharpDataDrivenClassExample#1.Test2

    WEX.Examples.CSharpDataDrivenClassExample#2
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = Orange
            Data[Size] = 9
        WEX.Examples.CSharpDataDrivenClassExample#2.Test1
        WEX.Examples.CSharpDataDrivenClassExample#2.Test2

    WEX.Examples.CSharpDataDrivenClassExample#3
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = Blue
            Data[Size] = 9
        WEX.Examples.CSharpDataDrivenClassExample#3.Test1
        WEX.Examples.CSharpDataDrivenClassExample#3.Test2
```

您可以将所有执行规则应用于数据驱动的类。 您可以将您的选择查询基于可在 **/listproperties** 选项中列出的任何内容。

## <a name="span-idddtests_ddcspanspan-idddtests_ddcspandata-driven-tests-in-a-data-driven-class"></a><span id="ddtests_ddc"></span><span id="DDTESTS_DDC"></span>数据驱动类中的数据驱动的测试


不会以任何方式限制数据驱动类中数据驱动的测试的来自。 编写 API 测试时，此方法非常有用。 可以在类级别的 **数据源** 中保留类中所有测试的通用数据。 在标记为数据驱动的方法的数据 **源** 元数据中指定特定于测试方法的数据。

注意：在这种情况下，执行顺序稍微复杂一些。

下面的示例演示了前面两个示例二进制文件如何与 */list* 命令选项一起呈现。

### <a name="span-idnative1_ddtestsspanspan-idnative1_ddtestsspannative"></a><span id="native1_ddtests"></span><span id="NATIVE1_DDTESTS"></span>本机

``` syntax
TE.exe Examples\CPP.AdvancedDataDriven.Examples.dll /name:*nested* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CPP.AdvancedDataDriven.Examples.dll
            WEX::TestExecution::Examples::NestedDataDrivenExample#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#3
            WEX::TestExecution::Examples::NestedDataDrivenExample#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#3
            WEX::TestExecution::Examples::NestedDataDrivenExample#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#3
            WEX::TestExecution::Examples::NestedDataDrivenExample#3
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#3
```

### <a name="span-idmanaged1_ddtestsspanspan-idmanaged1_ddtestsspanmanaged"></a><span id="managed1_ddtests"></span><span id="MANAGED1_DDTESTS"></span>经过

``` syntax
TE.exe Examples\CSharp.AdvancedDataDriven.Examples.dll /name:*nested* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CSharp.AdvancedDataDriven.Examples.dll
            WEX.Examples.CSharpDataDrivenNestedExample#0
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#3
            WEX.Examples.CSharpDataDrivenNestedExample#1
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#3
            WEX.Examples.CSharpDataDrivenNestedExample#2
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#3
            WEX.Examples.CSharpDataDrivenNestedExample#3
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#3
```

**注意：** 在这种情况下，唯一的限制是，这两个示例的表不能在同一 **DataSource 文件** 中。 换句话说，数据驱动类的数据 **源** 以及它所包含的数据驱动的测试方法必须不同。

请注意，在我们的示例中，方法 **Test2** 是数据驱动类中的数据驱动的测试。 例如，在 WEX 行中 **。例如，CSharpDataDrivenNestedExample \# 3. Test2 \# 0**， **\# 3** 是类的索引， **\# 0** 是该类中数据驱动的测试的索引。 **Test2** 可以访问这两个表：它所属的类实例的行中的数据以及其自己的数据 **源** 表的当前行中的数据。 换言之， **类级别的数据和测试方法级别的数据将聚合在一起，并在测试方法执行期间可用。**

发生冲突的情况下会发生什么情况-如果在类级和方法级别同时指定了相同的数据名称， TAEF 处理此条件的方式与处理元数据属性的方式相同。 **在方法级别的行中指定的数据将覆盖在类级别的行中指定的数据。**

例如，如果有一个名为 **Size** 的参数，同时在类级别和测试方法级别指定，则请考虑这种情况。 在类级别， **大小** 定义为 *字符串数组* 类型，但在测试方法级别，定义为 *int*。在这种情况下， *int* 类型会在测试方法级别重写 *字符串数组* 类型，并在测试的 **设置** 和 **拆卸** 方法中重写。 但是，在类级别 **设置** 和 **拆卸** 方法， **大小** 为 *字符串数组* 数据类型。

如果代码中有任何此类冲突的数据，TAEF 将在执行过程中显示警告并列出属性，但冲突数据不会导致任何失败。

 

 






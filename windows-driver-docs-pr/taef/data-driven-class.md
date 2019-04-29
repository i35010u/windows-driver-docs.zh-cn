---
title: 数据驱动的类
description: 数据驱动的类
ms.assetid: 2998D5BB-A873-4df9-86B2-88937736862F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee3b8cc16d499907771381a5a00d44a003640c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385068"
---
# <a name="span-idtaefdata-drivenclassspandata-driven-class"></a><span id="taef.data-driven_class"></span>数据驱动的类


请确保您熟悉 TAEF 基本执行并且知道如何创建在继续进行本部分之前使用的测试。 您可能想要通过简单的数据驱动测试的示例演练。 在本部分中，你将使数据驱动的测试类，它基于*基于的表*数据驱动的测试，但相同的方法适用于*基于 WMI*或*PICT 基于*数据驱动的测试。

## <a name="span-idwhentouseddcspanspan-idwhentouseddcspanwhen-to-use-a-data-driven-class"></a><span id="whentouse_ddc"></span><span id="WHENTOUSE_DDC"></span>何时使用数据驱动类？


有些的时候当多个测试可能取决于相同的输入数据。 当测试 Api 时，可能想要使用相同的数据运行多个 API 测试，以获取 API 行为的一致视图。 执行方案级别测试时，你可能想要确保所有你的方案中的步骤都使用相同的数据经过测试。 在这些情况下，它可用于指定在类级别的测试数据。

## <a name="span-idauthoringddcspanspan-idauthoringddcspanauthoring-data-driven-class"></a><span id="authoring_ddc"></span><span id="AUTHORING_DDC"></span>创作数据驱动的类


你指定给定的类为数据驱动到指定给定的测试是数据驱动的方式类似的方式。 您将应用**数据源**在类级别的元数据。 值标识感兴趣的特定数据源。 下面的示例演示如何指定这些属性的数据驱动的类：

### <a name="span-idnative1authoringspanspan-idnative1authoringspannative-code"></a><span id="native1_authoring"></span><span id="NATIVE1_AUTHORING"></span>本机代码

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

### <a name="span-idmanaged1authoringspanspan-idmanaged1authoringspanmanaged-code"></a><span id="managed1_authoring"></span><span id="MANAGED1_AUTHORING"></span>托管的代码

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

在这些示例中，行中的 3**本机代码**示例，并在第 5 行**托管代码**示例是在 TAEF 中指定的数据驱动的测试类的数据源的建议的方式。

在中**托管代码**上述示例中，13、 18、 24 和 28 行显示如何使数据可用于托管代码的测试方法。

在下面的代码示例中，4、 11、 20 和 27 各行显示如何使数据可用于本机代码的测试方法。 请注意，***使完全相同的方式将对数据驱动测试中定义数据驱动类表 （行） 可用于在类 （Test1 和 Test2） 中的测试方法中的数据。***

### <span id="native2_authoring"></span><span id="NATIVE2_AUTHORING"></span>

在构造**数据源**中完全一样的方式将数据驱动测试的数据驱动的类的 XML 文件。 以下示例演示用于本机和托管类的 XML 文件。

### <a name="span-idnative3authoringspanspan-idnative3authoringspannative"></a><span id="native3_authoring"></span><span id="NATIVE3_AUTHORING"></span>本机

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

### <a name="span-idmanged2authoringspanspan-idmanged2authoringspanmanaged"></a><span id="manged2_authoring"></span><span id="MANGED2_AUTHORING"></span>托管

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

## <a name="span-idbehindsceneddcspanspan-idbehindsceneddcspanbehind-the-scenes-or-what-to-expect"></a><span id="behindscene_ddc"></span><span id="BEHINDSCENE_DDC"></span>隐藏在场景或希望得到什么？


默认情况下，创作 TAEF 中的测试类中的执行顺序时，在其中编码类中的测试方法的顺序相同。 因此，在上一示例中， **Test1**将始终执行之前**Test2**。 因为此类包含**Test1**并**Test2**是一个数据驱动的类，方法将执行一次为每个数据行中定义的类的所有**数据源**。 换而言之， **Test1**并**Test2**执行行\#0。 然后，这些方法执行的行的相同顺序\#1，依此类推直到 TAEF 执行的所有行。

## <a name="span-idexecutingddcspanspan-idexecutingddcspanexecuting-tests-in-a-data-driven-class"></a><span id="executing_ddc"></span><span id="EXECUTING_DDC"></span>执行数据驱动的类中的测试


如果您执行与示例测试二进制文件 **/list**命令选项，从上一节的执行顺序就变得显而易见。

### <a name="span-idnative1executingspanspan-idnative1executingspannative"></a><span id="native1_executing"></span><span id="NATIVE1_EXECUTING"></span>本机

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

### <a name="span-idmanaged1executingspanspan-idmanaged1executingspanmanaged"></a><span id="managed1_executing"></span><span id="MANAGED1_EXECUTING"></span>托管

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

请注意上面的示例中的索引是类似于数据驱动的测试。 数据驱动的类中的每一行都由索引标识。 在数据驱动测试中，就像**您可以选择向任意行提供更有意义的短*名称*通过 XML 文件中指定行级别的元数据并打印该名称而不是列出或执行时的索引测试。**

同样，使用 **/listproperties**选项以确认数据是否确实指定的和可用在类级别。

### <a name="span-idnative2executingspanspan-idnative2executingspannative"></a><span id="native2_executing"></span><span id="NATIVE2_EXECUTING"></span>本机

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

### <a name="span-idmanaged2executingspanspan-idmanaged2executingspanmanaged"></a><span id="managed2_executing"></span><span id="MANAGED2_EXECUTING"></span>托管

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

可以将执行的所有规则都应用到的数据驱动的类。 你可以根据你选择的查询可以列出中的任何内容 **/listproperties**选项。

## <a name="span-idddtestsddcspanspan-idddtestsddcspandata-driven-tests-in-a-data-driven-class"></a><span id="ddtests_ddc"></span><span id="DDTESTS_DDC"></span>数据驱动的类中的数据驱动的测试


您不会在数据驱动的类中的数据驱动测试任何方式来自被限制。 编写 API 测试时，此方法可能很有用。 可以在类级别的所有测试的常用数据保留在类中**数据源**。 可以指定是在特定的测试方法的数据**数据源**标记为数据驱动的方法的元数据。

注意：在这种情况下，执行顺序是更复杂一些。

下面的示例演示与上一示例中两个二进制文件的呈现方式 */list*命令选项。

### <a name="span-idnative1ddtestsspanspan-idnative1ddtestsspannative"></a><span id="native1_ddtests"></span><span id="NATIVE1_DDTESTS"></span>本机

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

### <a name="span-idmanaged1ddtestsspanspan-idmanaged1ddtestsspanmanaged"></a><span id="managed1_ddtests"></span><span id="MANAGED1_DDTESTS"></span>托管

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

**注意：** 在这种情况下唯一的限制是，对于两个示例的表不能在同一个**数据源文件**。 换而言之，**数据源**适用的数据驱动的类和数据驱动的测试方法，它包含必须与此不同。

请注意，方法**Test2**在我们的示例是数据驱动的类中的数据驱动测试。 例如，在行**WEX。Examples.CSharpDataDrivenNestedExample\#3.Test2\#0**，  **\#3**是类、 索引和 **\#0**是索引为使该类中的数据驱动测试。 **Test2**可以访问这两个表： 类实例的行中的数据属于哪个 it 和其自己的当前行中的数据**数据源**表。 换而言之，**类级别的数据和测试方法级别的数据聚合在一起，并可在测试方法执行过程。**

什么情况下会发生冲突的数据-如果在类级别和方法级别指定相同的数据名称？ TAEF 中它处理元数据属性的相同方式处理这种情况。 **在方法级别的行中指定的数据重写在类级别的行中指定的数据。**

例如，具有名为的参数时，请考虑用例**大小**指定在类级别和在测试方法级别。 在类级别**大小**定义为*字符串数组*类型，但在测试方法级别，它被定义为*int*。在这种情况下， *int*键入替代*字符串数组*类型在测试方法级别，以及在**安装**并**拆卸**测试的方法。 但是在**安装程序**并**拆卸**方法在类级别**大小**具有*字符串数组*数据类型。

如果在代码中包含任何此类冲突的数据，TAEF 显示在执行期间的警告，并列出属性，但冲突数据不会导致任何故障。

 

 






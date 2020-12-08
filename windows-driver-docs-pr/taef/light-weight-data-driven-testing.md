---
title: 轻量数据驱动的测试
description: 轻量数据驱动的测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f97e9b249621c828584a00230e5509e59aeff97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785423"
---
# <a name="span-idtaeflight-weight_data-driven_testingspanlight-weight-data-driven-testing"></a><span id="taef.light-weight_data-driven_testing"></span>轻量数据驱动的测试


在某些情况下，可能会出现这样的情况：完整的 XML 数据源和基于表的数据驱动测试在测试方案需求上可能太大。 轻型数据驱动测试允许在测试的数据非常简单且可轻松表示为元数据时，快速轻松地获取数据驱动的测试支持。 让我们使用一个示例并了解如何操作。

轻型数据驱动测试的数据表示为测试、类或模块级别)  (的一组元数据。 对于此集合中的每个值，将对集合中的每个值执行相关的测试方法以及关联的安装和拆卸方法。 让我们看看如何在本机代码中创作：

```cpp
1  #include "WexString.h"
2  #include "WexTestClass.h"
3
4  using namespace WEX::Common;
5  using namespace WEX::TestExecution;
6  using namespace WEX::Logging;

7  namespace WEX { namespace TestExecution { namespace Examples
8  {
9      class SimpleDataDrivenExample
10     {
11         TEST_CLASS(SimpleDataDrivenExample);
12         ...
13         BEGIN_TEST_METHOD(SetsOfDataTest)
14             TEST_METHOD_PROPERTY(L"Data:Color", L"{Purple, Maroon, Brown}")
15         END_TEST_METHOD()
16     };
```

请注意 \_ \_ 第14行中的测试方法属性的参数值。 测试元数据值以 "{" 开头，以 "}" 结尾，指示已指定了逗号或分号分隔的值列表。 TAEF 会重新执行此测试方法，SetsOfDataTest 对此集中的每个值都 ( # A1。

另请注意，元数据名称以 "Data：" 开头。 这意味着元数据集实际上是为数据驱动的测试参数指定变体，可用于实际测试方法，这与基于表的数据驱动测试中的数据参数非常类似：

```cpp
11     ...
12
13     void SimpleDataDrivenExample::SetsOfDataTest()
14     {
15         String color;
16         if (SUCCEEDED(TestData::TryGetValue(L"color", color)))
17         {
18             Log::Comment(L"Color retrieved was " + color);
19         }
20     }
21 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

使用托管代码时，数据集的规范和检索与本机示例非常类似。 我们一起来看一下：

```cpp
1  namespace WEX.Examples
2  {
3      using Microsoft.VisualStudio.TestTools.UnitTesting;
4      using System;
5      using System.Collections;
6      using System.Data;
7      using WEX.Logging.Interop;
8      using WEX.TestExecution;
9
10     [TestClass]
11     public class CSharpDataDrivenSimpleExample
12     {
13         ...
14         [TestMethod]
15         [TestProperty("Data:Color", "{Red, Green, Blue}")]
16         public void SetsOfMetadataTest()
17         {
18             Log.Comment("Color is " + m_testContext.DataRow["Color"]);
19         }
20
21         public TestContext TestContext
22         {
23             get { return m_testContext; }
24             set { m_testContext = value; }
25         }
26
27         private TestContext m_testContext;
28     }
29 }
```

与基于表的数据驱动测试的情况一样，指定为元数据的数据集将允许通过 TestContext 进行检索。**请注意，为了保持数据驱动的测试轻型权重，参数类型将始终为本机代码中的 WEX：： Common：： String () 和托管代码中的字符串 ()**

**如果指定了多个数据值，则将获得所有可能值的 catersian 产品，并且将为每个组合调用测试方法。**

此外，还可以将某些元数据集 (如 [ThreadingModel metadata sets](threading-models.md)) 以及为同一测试方法指定的数据集。 在这种情况下，所有元数据集和数据集的组合扩展都将由 TAEF 生成，并且将使用每个组合来调用考虑的测试方法。

## <a name="span-idmetadataexpansionspanspan-idmetadataexpansionspanspan-idmetadataexpansionspanspecial-cases---data-driven-test-with-a-sets-of-metadata-or-data"></a><span id="metadataExpansion"></span><span id="metadataexpansion"></span><span id="METADATAEXPANSION"></span>特殊情况-具有一组元数据或数据的数据驱动的测试


您可以使用依赖于基于表的数据驱动测试的测试方法，并为其指定一组数据或元数据。 例如，测试方法可以在基于表的数据驱动测试中指定 "大小" 和 "颜色"，并希望在 "透明度" 参数设置为 true 后执行所有行，然后将其设置为 false。 在这种情况下，可以将 "透明度" 指定为数据驱动测试的集 "{true，false}"。 **需要注意的是，如果元数据集中的参数与基于数据驱动的行中的参数冲突，行级别参数类型和值将重写元数据集的值。**

## <a name="span-idexecuting_tests_with_sets_of_data___metadataspanspan-idexecuting_tests_with_sets_of_data___metadataspanspan-idexecuting_tests_with_sets_of_data___metadataspanexecuting-tests-with-sets-of-data--metadata"></a><span id="Executing_tests_with_Sets_of_data___metadata"></span><span id="executing_tests_with_sets_of_data___metadata"></span><span id="EXECUTING_TESTS_WITH_SETS_OF_DATA___METADATA"></span>执行包含一组数据/元数据的测试


执行包含数据集的测试非常直观。 让我们看看示例测试的/listproperties 输出：

``` syntax
1   te Examples\CPP.DataDriven.Example.dll /name:*SetsOfDataTest* /listproperties
2
3   Test Authoring and Execution Framework v2.9.3k for x64
4
5           f:\ Examples\CPP.SimpleDataDriven.Example.dll
6               WEX::TestExecution::Examples::SimpleDataDrivenExample<
7                   WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet0
8                           Property[Data:Color] = {Purple, Maroon, Brown}
9
10                          Data[Color] = Purple
11
12                  WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet1
13                          Property[Data:Color] = {Purple, Maroon, Brown}
14
15                          Data[Color] = Maroon
16
17                  WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet2
18                          Property[Data:Color] = {Purple, Maroon, Brown}
19
20                          Data[Color] = Brown
```

在上面的示例中，请注意第7、12和17行。 使用数据集中的值，将元数据集索引追加到测试方法的每个调用。 此索引的格式为：

```cpp
<namespace qualified test method name>#metadataSet<metadataIndex>
```

第8、13和18行显示已为此轻型数据驱动测试支持指定的元数据集。 在这种情况下，该集包含紫色、褐紫红色和棕色的颜色。 第10、15和20行显示此集中的实际值，此值对于测试的当前调用处于活动状态。 对于 SetsOfMetadataTest \# metadataSet1，此方法的第二次调用时，该集合中的活动参数值为 "褐紫红色"

您可以选择数据值或名称，就像在基于表的数据驱动测试中一样。 例如，你可以选择 SetsOfDataTest \# metadataSet1，方法是选择查询（如 **/select:@Data:Color = "褐紫红色"** 或 **/name： \* \# metadataSet1）。**

有关快速参考，请参阅托管测试示例中的/listproperties 输出，如下所示：

``` syntax
te Examples\CSharp.DataDriven.Example.dll /name:*SetsOfMetadataTest* /listproperties

Test Authoring and Execution Framework v2.9.3k for x64

        f:\ Examples\CSharp.DataDrivenSimple.Example.dll
            WEX.Examples.CSharpDataDrivenSimpleExample
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

 

 






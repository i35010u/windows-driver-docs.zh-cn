---
title: 轻量数据驱动的测试
description: 轻量数据驱动的测试
ms.assetid: A7070E38-A545-4156-B441-C0E6ACE569F5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de8346e911d3ae47eb06e1b8e987c8b7df7cebcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355505"
---
# <a name="span-idtaeflight-weightdata-driventestingspanlight-weight-data-driven-testing"></a><span id="taef.light-weight_data-driven_testing"></span>轻量数据驱动的测试


有可能需要完整的 XML 数据源的情况下，基于表的数据驱动的测试可能太过繁复的测试方案的需要。 数据驱动的测试的轻量级允许快速而简单的方法时为你的测试数据简单，可以轻松地表示为元数据获取数据驱动测试的支持。 让我们使用示例，请参阅如何。

轻量数据驱动测试的数据表示为一组元数据 （在测试、 类或模块级别）。 对于每个此集中的值，将为集合中的每个值执行问题，以及关联的安装和拆解方法中的测试方法。 让我们看看如何创作这在本机代码中：

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

请注意参数值，用于测试\_方法\_第 14 行中的属性。 测试元数据值以开始"{"结尾"}"已指定，该值指示逗号或分号分隔的值列表。 TAEF 将重新执行问题，SetsOfDataTest() 一次针对此集中的每个值中的测试方法。

此外请注意，元数据名称开头"的数据:"。 这意味着元数据集实际上指定变体，数据驱动测试参数，并可用于实际的测试方法更像一个表中的数据参数基于的数据驱动测试如下所示：

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

使用托管代码，而规范和检索的数据集是非常类似于本机示例。 让我们来实际操作一下：

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

在表的情况下就像基于的数据驱动的测试中，指定为元数据，数据集将允许通过 TestContext.DataRow 检索。**请注意，若要保留数据驱动的测试轻量，参数类型将始终是 WEX::Common::String （在本机代码中） 和字符串 （在托管代码中）**

**如果指定了多个数据值，将获取所有可能的值的 catersian 产品并将每个组合调用测试方法。**

为进一步可能有一些元数据集 (如[ThreadingModel 元数据集](threading-models.md)) 以及为相同的测试方法指定的数据集。 这种情况下将由 TAEF 生成的所有元数据集和数据集的组合扩展并中问题的测试方法将调用每个组合使用。

## <a name="span-idmetadataexpansionspanspan-idmetadataexpansionspanspan-idmetadataexpansionspanspecial-cases---data-driven-test-with-a-sets-of-metadata-or-data"></a><span id="metadataExpansion"></span><span id="metadataexpansion"></span><span id="METADATAEXPANSION"></span>特殊情况-数据驱动测试的元数据或数据集


您可能有一个测试方法依赖于基于的表数据驱动测试，以及为其指定的数据或元数据集。 例如，测试方法可能具有参数"大小"和"颜色"指定表中基于数据驱动的测试，想要执行一次使用"透明"参数设置为 true，然后将设置为 false 的所有行。 在这种情况下，"透明"无法为数据驱动测试指定为一组"{true，false}"。 **务必要注意发生冲突的元数据中的参数的情况设置与基于表的数据驱动的行，行级别的参数类型和值将重写元数据设置的值。**

## <a name="span-idexecutingtestswithsetsofdatametadataspanspan-idexecutingtestswithsetsofdatametadataspanspan-idexecutingtestswithsetsofdatametadataspanexecuting-tests-with-sets-of-data--metadata"></a><span id="Executing_tests_with_Sets_of_data___metadata"></span><span id="executing_tests_with_sets_of_data___metadata"></span><span id="EXECUTING_TESTS_WITH_SETS_OF_DATA___METADATA"></span>执行测试用的数据集 / 元数据


执行包含的数据集的测试是非常直观。 让我们看看我们的示例测试 /listproperties 输出：

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

请注意，行 7、 12 和 17 在上面的示例。 元数据设置索引获取附加到每个调用测试方法与在数据集中的值。 此索引的形式：

```cpp
<namespace qualified test method name>#metadataSet<metadataIndex>
```

8、 13 和 18 行显示为细线数据驱动测试支持指定的元数据集。 在这种情况下一组包含颜色紫色、 褐紫红色和 brown。 10、 15 和 20 行显示处于活动状态的测试的当前调用此集中的实际值。 对于 SetsOfMetadataTest\#metadataSet1，此方法，从一组活动参数值的第二个调用为"褐紫红色"

可以选择上的数据值或基于数据驱动的测试就像你可以在表中的名称。 例如，您可以选择 SetsOfDataTest\#由所选内容查询 metadataSet1 喜欢 **/select:@Data:Color= 褐紫红色**或 **/名称：\*\#metadataSet1**

为方便参考，/listproperties 托管测试示例输出如下所示：

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

 

 






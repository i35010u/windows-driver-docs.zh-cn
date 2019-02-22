---
title: 执行组
description: 执行组
ms.assetid: CC196843-A225-4193-9386-EE024B5D0B68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 828b4728513b6a977ab3f085d5ca11661dba2543
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555971"
---
# <a name="execution-groups"></a>执行组


请确保您熟悉的基本执行[TAEF](index.md)并且知道如何[作者测试](authoring-tests.md)使用它，然后继续进行本部分中。 您可能想要通过用户指南中列出的某些数据驱动的测试示例演练。

## <a name="span-idscenario-basedtestingwithtaefspanspan-idscenario-basedtestingwithtaefspanspan-idscenario-basedtestingwithtaefspanscenario-based-testing-with-taef"></a><span id="Scenario-Based_Testing_with_TAEF"></span><span id="scenario-based_testing_with_taef"></span><span id="SCENARIO-BASED_TESTING_WITH_TAEF"></span>使用 TAEF 基于方案的测试


当谈及场景级别测试时，实际上都谈论一系列测试，其中执行下一次测试有意义才成功进行了上一个测试在方案中。 在某些情况下，您可能甚至没有需要执行下一步测试时，如果前面的测试失败的所有信息。 向此目标，同时保持为测试方法和测试方案，从而允许执行的单位 TAEF 支持所谓的"ExecutionGroup"s。 您可以基于方案的测试中 TAEF 无论时仍有其他功能，如数据驱动的测试。 如果您设计你的方案利用数据驱动的测试，可以应用在类级别使用 TAEF 提供的数据驱动的类功能的数据驱动的支持。 **通过将应用在类级别的数据驱动的支持，可以具有的所有测试您的类中的每一行按顺序执行。**

此页将集中讨论如何指定"ExecutionGroup"的测试类中的序列。

## <a name="span-idexecutiongroupsspanspan-idexecutiongroupsspanspan-idexecutiongroupsspanexecution-groups"></a><span id="Execution_Groups"></span><span id="execution_groups"></span><span id="EXECUTION_GROUPS"></span>执行组


在讨论之前执行组，务必要注意和记住**TAEF，在测试类中的执行顺序是在其中你具有限定它们为测试 order\_对于本机代码或添加了的METHOD(...)\[TestMethod\]属性之前在托管代码方法**。 TAEF 不保证类本身的执行顺序。

**现在，在基于方案的测试中，它可能不足以只保证执行顺序，还需要保证所有以前的测试在方案中成功，再继续下一测试在方案中。** 这是概念的可以在其中找到的"ExecutionGroup"非常有用。

请考虑本机示例：

```cpp
1     class ExecutionDependencyExample
2     {
3         BEGIN_TEST_CLASS(ExecutionDependencyExample)
4             TEST_CLASS_PROPERTY(L"ExecutionGroup", L"DependentTests")
5         END_TEST_CLASS()
6
7         TEST_METHOD(Test1)
8         {
9             Log::Comment(L"Test1 passes.");
10        }
11
12        TEST_METHOD(Test2)
13        {
14            Log::Comment(L"Test2 fails.");
15            VERIFY_ARE_EQUAL(2, 3);
16        }
17
18        TEST_METHOD(Test3)
19        {
20            Log::Comment(L"Test3 is blocked; so you shouldn&#39;t see this.");
21        }
22    };
```

请参阅上面的 c + + 文件代码段中的第 4 行。 在此特定情况下，你正在限定类 ExecutionDependencyExample 属于名为"DependentTests""ExecutionGroup"内的所有测试。 这意味着"Test1"、"Test2"和"Test3"是"DependentTests"执行组的一部分。 如前文所述，当且仅当 Test1 获取已成功执行，并将传递，将获取执行 Test2。 同样会执行 Test3 当且仅当 Test2 获取已成功执行，并将传递。

你将看到 Test2 设计失败 （请参阅第 14 行和上面的第 15）。

Test2 在我们"DependentTests""ExecutionGroup"中失败，因为 Test3 不会立即执行，并改为将其标记为阻止。 请尝试的运行上述测试并查看这是否的确属实。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll
Test Authoring and Execution Framework v2.93k for x86

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1
Test1 passes.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1 
    [Passed]

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2
Test2 fails.
Error: Verify: AreEqual(2, 3) - Values (2, 3) [File: >f:source\executiondependencyexample\executiondependencyexample.cpp,
Function: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2, Line:21] 
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2[Failed] 

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test3
Blocked: This test belongs to an execution group and depends on the previous test being executed in the same environment successfully. The dependent test must be selected for execution, must request the same execution environment (e.g. 'ThreadingModel') and must be executed successfully.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test3 [Blocked]

Non-passing Tests:
    WEX::TestExecution::Examples::ExecutionDependencyExample::Test2 [Failed]
    WEX::TestExecution::Examples::ExecutionDependencyExample::Test3 [Blocked]

Summary: Total=3, Passed=1, Failed=1, Blocked=1, Not Run=0, Skipped=0
```

请注意，作为预测，传递 Test1、 Test2 失败，和 Test3 已被阻止。 与 Test3，TAEF 记录一条消息指出 Test3 属于某个执行组和未成功执行前面的测试。

此错误消息还指出，应选择当前测试正在执行的属于同一 ExecutionGroup 之前的所有测试。 换而言之，如果你尝试运行仅 Test2 在运行时使用选择条件，您会发现，Test2 将无法按原样执行依赖于 Test1，正在同一 ExecutionGroup 的一部分。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll /name:*Test2*
Test Authoring and Execution Framework v2.9.3k for x86

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2
Blocked: This test belongs to an execution group and depends on the previous test being executed in the same environment successfully. The dependent test must be selected for execution, must request the same execution environment (e.g. 'ThreadingModel') and must be executed successfully.

EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2 [Blocked]

Summary: Total=1, Passed=0, Failed=0, Blocked=1, Not Run=0, Skipped=0
```

如果选择 Test1，这是 ExecutionGroup 中的第一个测试，但是，它将成功地运行。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll /name:*Test1*
Test Authoring and Execution Framework v2.9.3k for x86
StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1
Test1 passes.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1 [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

此外，如果您有不属于 ExecutionGroup 的测试，它们将不考虑执行结果的继续操作它们 ExecutionGroup 内测试执行。 还有可能有多个 ExecutionGroup 类中。 但是请注意 ExecutionGroup 不能跨类。 如果这样做，将改为将它们视为两个单独 ExecutionGroups，一个在每个类。

消息还指出，应在 Test3 Test2 与相同的环境中运行。 允许尝试了解一些更详细地这个方面。 由于成为 ExecutionGroup 实际上意味着正在基于方案的测试的一部分，它就变得至关重要的所有测试请求并因此在同一环境中执行。 例如，如果线程处理模型内 ExecutionGroup 发生更改，您将看到被阻止的测试。 例如，在上述示例中，Test2 旨在成功执行，但有 ThreadingModel 属性设置为 MTA，如果仍将阻止 Test3。

我们来看另一个示例：示例\\TAEF\\CSharp\\ExecutionDependentGroupsExample （请参阅最新的 TAEF 版本共享）

```cpp
1     [TestClass]
2     public class CSharpExecutionDependentGroupsExample
3     {
4         //First Execution Group: Test1, Test2
5         [TestMethod]
6         [TestProperty("ExecutionGroup", "First Execution Group")]
7         public void Test1()
8         {
9             Log.Comment("Part of First Execution Group");
10        }
11        [TestMethod]
12        [TestProperty("ExecutionGroup", "First Execution Group")]
13        public void Test2()
14        {
15            Log.Comment("Part of First Execution Group");
16        }
17
18        //Second Execution Group: Test3, Test4. Test4 fails
19        [TestMethod]
20        [TestProperty("ExecutionGroup", "Second Execution Group")]
21        public void Test3()
22        {
23            Log.Comment("Part of Second Execution Group");
24        }
25        [TestMethod]
26        [TestProperty("ExecutionGroup", "Second Execution Group")]
27        public void Test4()
28        {
29            Log.Comment("Part of Second Execution Group - last in group fails");
30            Verify.IsTrue(false);
31        }
32
33        //Third Execution Group: Test5, Test6, Test7. Test6 fails, Test7 will be blocked.
34        [TestMethod]
35        [TestProperty("ExecutionGroup", "Third Execution Group")]
36        public void Test5()
37        {
38            Log.Comment("Part of Third Execution Group");
39        }
40        [TestMethod]
41        [TestProperty("ExecutionGroup", "Third Execution Group")]
42        public void Test6()
43        {
44            Log.Comment("Part of Third Execution Group - middle in this set of 3 fails");
45            Verify.IsTrue(false);
46        }
47        [TestMethod]
48        [TestProperty("ExecutionGroup", "Third Execution Group")]
49        public void Test7()
50        {
51            Log.Comment("Part of Third Execution Group");
52        }
53
54        //Fourth Execution Group: Test8, Test9
55        [TestMethod]
56        [TestProperty("ExecutionGroup", "Fourth Execution Group")]
57        public void Test8()
58        {
59            Log.Comment("Part of Fourth Execution Group");
60        }
61        [TestMethod]
62        [TestProperty("ExecutionGroup", "Fourth Execution Group")]
63        public void Test9()
64        {
65            Log.Comment("Part of Fourth Execution Group");
66        }
67    }
```

此示例中有 4 个不同的执行组：

-   "第一个执行组"包含 Test1、 Test2;这两种应传递成功。
-   "第二个执行组"包含 Test3 和 Test4。 Test4 处于此 ExecutionGroup 中的最后一个测试，它将失败。
-   "第三个执行组"包含 Test5、 Test6 和 Test7。 Test5 执行并成功通过，尽管从上一 ExecutionGroup Test4 失败。 Test6 设计失败，这将导致 Test7 才会被阻止。
-   "第四个执行组"包含 Test8 和 Test9。 再次重申，虽然从上一 ExecutionGroup Test7 已被阻止是由于为 Test6 失败，因此 Test8 将成功执行，并将 Test9 如此。

可以了解在此示例中更好地 ExecutionGroups，让我们来列出在此示例中的属性。

``` syntax
te Examples\CSharp.ExecutionDependentGroups.Example.dll /listproperties
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ \Examples\CSharp.ExecutionDependentGroups.Example.dll
            WEX.Examples.CSharpExecutionDependentGroupsExample
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test1
                        Property[ExecutionGroup] = First Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test2
                        Property[ExecutionGroup] = First Execution Group

                WEX.Examples.CSharpExecutionDependentGroupsExample.Test3
                        Property[ExecutionGroup] = Second Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test4
                        Property[ExecutionGroup] = Second Execution Group

                WEX.Examples.CSharpExecutionDependentGroupsExample.Test5
                        Property[ExecutionGroup] = Third Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test6
                        Property[ExecutionGroup] = Third Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test7
                        Property[ExecutionGroup] = Third Execution Group

                WEX.Examples.CSharpExecutionDependentGroupsExample.Test8
                        Property[ExecutionGroup] = Fourth Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test9
                        Property[ExecutionGroup] = Fourth Execution Group
```

在执行上述测试时，以下输出确认的预测的执行顺序。

``` syntax
te Examples\CSharp.ExecutionDependentGroups.Example.dll
Test Authoring and Execution Framework v2.9.3k for x86

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test1

Part of First Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test1 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test2

Part of First Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test2 [Passed]

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test3

Part of Second Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test3 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test4

Part of Second Execution Group - last in group fails
Error: Verify: IsTrue [File: Need_Symbols, Function: Test4, Line: 0] 
Error: [HRESULT: 0x80131604]. Operation failed: 'WEX.Examples.CSharpExecutionDependentGroupsExample.Test4'.
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test4 [Failed]

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test5

Part of Third Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test5 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test6

Part of Third Execution Group - middle in this set of 3 fails
Error: Verify: IsTrue [File: Need_Symbols, Function: Test6, Line: 0] 
Error: [HRESULT: 0x80131604]. Operation failed: 'WEX.Examples.CSharpExecutionDependentGroupsExample.Test6'.
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test6 [Failed] 
Error: WEX.Examples.CSharpExecutionDependentGroupsExample.Test7 belongs to an execution group and depends
       on the previous test being executed in the same environment successfully.
Error: Please make sure that the dependent test is selected for execution, requests the same execution .
       environment metadata(e.g. 'ThreadingModel') and that it executed successfully.
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test7
Blocked EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test7 [Blocked]

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test8

Part of Fourth Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test8 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test9

Part of Fourth Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test9 [Passed]

Failed Tests:
    WEX.Examples.CSharpExecutionDependentGroupsExample.Test4
    WEX.Examples.CSharpExecutionDependentGroupsExample.Test6

Summary: Total=9, Passed=6, Failed=2, Blocked=1, Not Run=0, Skipped=0
```

请注意，测试执行顺序是按预期方式。

 

 






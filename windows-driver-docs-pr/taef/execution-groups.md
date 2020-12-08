---
title: 执行组
description: 执行组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 945a8354c12589334f30b01a72595b7ed4ee0e7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785443"
---
# <a name="execution-groups"></a>执行组


请确保熟悉 [TAEF](index.md) 的基本执行，并知道如何使用它 [创作测试](authoring-tests.md) ，然后再继续此部分。 你可能还需要浏览用户指南中列出的一些数据驱动的测试示例。

## <a name="span-idscenario-based_testing_with_taefspanspan-idscenario-based_testing_with_taefspanspan-idscenario-based_testing_with_taefspanscenario-based-testing-with-taef"></a><span id="Scenario-Based_Testing_with_TAEF"></span><span id="scenario-based_testing_with_taef"></span><span id="SCENARIO-BASED_TESTING_WITH_TAEF"></span>通过 TAEF 进行基于方案的测试


当您谈论方案级别的测试时，您实际上就是讨论一系列测试，在这种情况下，只有在方案中的以前测试成功时，执行下一个测试才有意义。 在某些情况下，如果上一次测试失败，您甚至可能没有执行下一个测试所需的所有信息。 为此，同时将执行单元保持为测试方法并允许测试方案，TAEF 支持所谓的 "ExecutionGroup"。 可以在 TAEF 中使用基于方案的测试，而无需考虑数据驱动测试等其他功能。 如果设计方案来利用数据驱动的测试，则可以使用 TAEF 提供的数据驱动类功能，在类级别应用数据驱动的支持。 **通过在类级别应用数据驱动的支持，可以按顺序对每一行执行类中的所有测试。**

本页重点介绍如何在类中将一系列测试指定为 "ExecutionGroup"。

## <a name="span-idexecution_groupsspanspan-idexecution_groupsspanspan-idexecution_groupsspanexecution-groups"></a><span id="Execution_Groups"></span><span id="execution_groups"></span><span id="EXECUTION_GROUPS"></span>执行组


在讨论执行组之前，请务必注意， **在 TAEF 中，在类中执行测试的顺序就是您在使用本机代码的情况下将其限定为测试 \_ 方法 ( ) ，或者在 \[ \] 托管代码的情况下将 TestMethod 属性添加到方法之前**。 TAEF 不保证类本身的执行顺序。

**现在，在基于方案的测试中，如果只是保证执行顺序，则还需要确保方案中以前的所有测试都已成功完成，然后再继续下一次测试。** 在这里，你可以找到 "ExecutionGroup" 的概念。

假设有一个本机示例：

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
20            Log::Comment(L"Test3 is blocked; so you shouldn't see this.");
21        }
22    };
```

请参阅上述 c + + 文件代码段中的第4行。 在此特定情况下，你将限定类 ExecutionDependencyExample 中的所有测试，使其属于名为 "DependentTests" 的 "ExecutionGroup"。 这意味着 "Test1"、"Test2" 和 "Test3" 是 "DependentTests" 执行组的一部分。 如前所述，当且仅当 Test1 成功执行并通过时，才会执行 Test2。 当且仅当 Test2 成功执行并通过时，才会执行类似的 Test3。

你将看到 Test2 已设计为失败 (请参阅上面的第14和15行) 。

由于 "DependentTests" "ExecutionGroup" 中的 Test2 失败，将不会执行 Test3，而是将其标记为 "已阻止"。 允许尝试运行上述测试，并查看是否确实确实如此。

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

请注意，正如预测、Test1 通过、Test2 失败和 Test3 被阻止。 对于 Test3，TAEF 记录一条消息，指出 Test3 属于执行组，而以前的测试未成功执行。

此错误消息还指出应选择属于同一 ExecutionGroup 的当前正在执行的测试之前的所有测试。 换句话说，如果尝试在运行时使用选择条件仅运行 Test2，则会发现 Test2 将被阻止，因为它的执行依赖于 Test1，因而是同一 ExecutionGroup 的一部分。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll /name:*Test2*
Test Authoring and Execution Framework v2.9.3k for x86

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2
Blocked: This test belongs to an execution group and depends on the previous test being executed in the same environment successfully. The dependent test must be selected for execution, must request the same execution environment (e.g. 'ThreadingModel') and must be executed successfully.

EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2 [Blocked]

Summary: Total=1, Passed=0, Failed=0, Blocked=1, Not Run=0, Skipped=0
```

不过，如果选择 "Test1"，即 ExecutionGroup 中的第一个测试，则它将成功运行。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll /name:*Test1*
Test Authoring and Execution Framework v2.9.3k for x86
StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1
Test1 passes.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1 [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

此外，如果你的测试不属于 ExecutionGroup，则它们将会执行，而不考虑在 ExecutionGroup 中执行测试的执行结果。 在一个类中也可以有多个 ExecutionGroup。 但请注意，ExecutionGroup 不能跨各个类。 如果这样做，它们将被视为两个独立的 ExecutionGroups，每个类一个。

该消息还指出，应在与 Test2 相同的环境中运行 Test3。 让我们更详细地了解这一点。 由于是 ExecutionGroup 的一部分，这实际上意味着是基于方案的测试的一部分，因此，所有测试请求并因此在相同的环境中执行，这一点非常重要。 例如，如果线程模型在 ExecutionGroup 内发生更改，则会看到 "已阻止的测试"。 例如，在上面的示例中，Test2 设计为成功执行，但将 "ThreadingModel" 属性设置为 "MTA"，则仍会阻止 Test3。

让我们看另一个示例：示例 \\ TAEF \\ CSharp \\ ExecutionDependentGroupsExample (请参阅最新的 TAEF 发布共享) 

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

此示例包含4个不同的执行组：

-   "第一个执行组" 包含 Test1、Test2;这两个应成功通过。
-   "第二个执行组" 包含 Test3 和 Test4。 Test4 是此 ExecutionGroup 的最后一次测试，失败。
-   "第三执行组" 包含 Test5、Test6 和 Test7。 Test5 会成功执行并传递，尽管之前 ExecutionGroup 中的 Test4 失败。 Test6 设计为失败，这将导致 Test7 被阻止。
-   "第四个执行组" 包含 Test8 和 Test9。 同样，althought Test7 从以前的 ExecutionGroup 被阻止，因为 Test6 发生了故障，Test8 将成功执行，并将 Test9。

为了更好地理解本例中的 ExecutionGroups，让我们来列出此示例中的属性。

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

执行上述测试后，以下输出可确认预测的执行顺序。

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

请注意，测试执行顺序与预期相同。

 

 






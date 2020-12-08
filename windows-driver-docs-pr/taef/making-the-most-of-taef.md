---
title: 充分利用 TAEF
description: 充分利用 TAEF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8986cb6dc11509270b6bce7e485d4d4764e380ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785425"
---
# <a name="making-the-most-of-taef"></a>充分利用 TAEF


测试创作和执行框架为您提供了一个强大的平台，用于创作和执行您的测试。 若要充分利用 TAEF，最好先了解一些后台功能细节。 本页讨论一些提示和功能，这些提示和功能将帮助你创作测试，以优化并充分利用 TAEF。 请确保熟悉用 TAEF 创作和执行测试的基础知识。

## <a name="span-idset-up__or_initialize__and_clean-up_methodsspanspan-idset-up__or_initialize__and_clean-up_methodsspanspan-idset-up__or_initialize__and_clean-up_methodsspanset-up-or-initialize-and-clean-up-methods"></a><span id="Set-up__or_Initialize__and_Clean-up_Methods"></span><span id="set-up__or_initialize__and_clean-up_methods"></span><span id="SET-UP__OR_INITIALIZE__AND_CLEAN-UP_METHODS"></span>设置 (或初始化) 和清理方法


程序集级别的设置和清理方法 (也称为 *装置*) ，每次 DLL 执行时都会运行一次。 同样，类级别设置和清理方法对每个类运行一次。 对于类中的所有测试，测试级别设置和清理方法都是相同的，并且在类中的每个测试前后调用一次。

每个程序集只能有一个程序集级别设置和清理方法，每个类有一个类级别设置和清理方法，每个类都有一个测试设置和清理方法。 请注意，类安装和清理方法在托管代码中是静态的，但不是 c + + 代码中的静态方法。

如果 (默认情况下启用异常) ，则在第一个失败的验证调用上将终止任何方法的执行。 如果已明确禁用基于异常的验证调用 (请参阅创作测试) 详细信息部分中的 "验证" 部分，你将需要使用显式条件语句来控制验证调用失败后的控制流。

如果在安装方法中发生故障 (通过基于异常的验证失败，或者安装程序显式返回故障) ，则会将遵循的测试视为 "受阻" 并记录为这样。 例如，如果类级别的安装方法失败，则类中的所有测试方法均被视为 "已阻止"，其中每个方法都将记录为这样。 除此之外，如果在安装方法中发生失败，则不会调用清理方法。

## <a name="span-idtest_methodspanspan-idtest_methodspanspan-idtest_methodspantest-method"></a><span id="Test_Method"></span><span id="test_method"></span><span id="TEST_METHOD"></span>测试方法


不需要显式记录测试结果。 如果测试中的所有验证调用均已成功，则测试将记录为 "已通过"。 在第一个验证调用失败的情况下，测试方法的执行将终止 (，除非已明确禁用基于异常的验证调用-在这种情况下，条件语句将在之后确定控制流，而不考虑以下) 并且测试将被标记为 "失败"。

同样，如果验证 (依赖于返回类型，并且确定帮助器方法调用调用的成功) 包装器，则无需显式检查并记录其结果。

## <a name="span-idspecifying_metadataspanspan-idspecifying_metadataspanspan-idspecifying_metadataspanspecifying-metadata"></a><span id="Specifying_Metadata"></span><span id="specifying_metadata"></span><span id="SPECIFYING_METADATA"></span>指定元数据


元数据查找是分层的。 这意味着，如果 select 语句是 **/select： " @Priority = 2"**，并且 TestMethod 未指定优先级，则 TAEF 将在包含它的类上查找。 如果类级别的元数据未指定，则 TAEF 将在程序集级别上查找。

因此，如果你希望类中的所有或大多数测试都具有相同的 "Priority"，或者说 "Owner"，只需在类级别指定它即可。 对于属于此规则的一个或多个例外测试，你可以在 "TestMethod" 级别显式提供元数据。 有关详细信息，请参阅以下测试：

```cpp
1    namespace WEX { namespace UnitTests { namespace Samples
2    {
3        //
4        // Declare module level properties
5        //
6        BEGIN_MODULE() //This metadata applies to all the classes and tests in this module or assembly
7            MODULE_PROPERTY(L"GroupOwner", L"SomeGroup")
8        END_MODULE()
9        class PremiumBankAccountTests
10       {
11           //
12           // Declare this class to be a test class with an'advanced' declaration
13           // Use advanced declaration when you want to set metadata on the class
14           //
15           BEGIN_TEST_CLASS(PremiumBankAccountTests) //This metadata applies to all the test in this class
16               TEST_CLASS_PROPERTY(L"Priority", L"2")
17               TEST_CLASS_PROPERTY(L"DevOwner", L"Someone")
18               TEST_CLASS_PROPERTY(L"PMOwner", L"Someone")
19           END_TEST_CLASS()
20           //
21           // Declare class setup - a method that runs after class constructor
22           // and before any test class methods and test setup method
23           //
24           TEST_CLASS_SETUP(SetDefaultAccountType);
25           //
26           // Declare class cleanup - a methods that runs after all the class test methods and test setup method
27           // and before the class destructor
28           //
29           TEST_CLASS_CLEANUP(ResetDefaultAccountType);
30           //
31           // Declare test setup and cleanup - methods that run before and after the execution
32           // of every test method correspondingly
33           //
34           TEST_METHOD_SETUP(CreateBankAccount);
35           TEST_METHOD_CLEANUP(DestroyBankAccount);
36           //
37           // Declare test methods with an 'advanced' declaration
38           // Use advanced declaration when you want to set metadata on the methods
39           //
40           BEGIN_TEST_METHOD(DebitTest)
41               TEST_METHOD_PROPERTY(L"BVT", L"TRUE")
42               TEST_METHOD_PROPERTY(L"PERF", L"TRUE")
43               TEST_METHOD_PROPERTY(L"STRESS", L"FALSE")
44               TEST_METHOD_PROPERTY(L"Priority", L"1") //Overrides the Class level Priority value
45           END_TEST_METHOD()
46           BEGIN_TEST_METHOD(CreditTest)
47               TEST_METHOD_PROPERTY(L"BVT", L"TRUE")
48               TEST_METHOD_PROPERTY(L"PERF", L"FALSE")
49               TEST_METHOD_PROPERTY(L"STRESS", L"TRUE")
50               TEST_METHOD_PROPERTY(L"GroupOwner", L"SomeGroupTest") //Overrides the GroupOwner specified at the Module level
51           END_TEST_METHOD()
52   
53           std::unique_ptr<BankAccount> m_spBankAccount;
54           BankAccountType m_defaultType;
55       };
56   } /* namespace Samples */ } /* namespace UnitTests */ } /* namespace WEX */
```

注意：对于托管测试，按类似方式进行创作。 模块级别与托管中的程序集级别标记相同。 ***对于托管代码中的程序集级别或类级别的元数据规范，必须在静态初始值设定项方法之前提供标记。*** 这可能意味着，如果你的测试还没有，则可能必须提供一个空的初始值设定项。 此设计专门用于确保 VSTS 兼容性。

如果是基于表的数据驱动的测试，则可以进一步执行此操作，并通过在行级别指定测试级别元数据来覆盖它们。 有关详细信息，请参阅 [元数据重写数据驱动的测试示例](metadata-overriding-data-driven-test-example.md) 。

 

 






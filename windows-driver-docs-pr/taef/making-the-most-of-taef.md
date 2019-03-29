---
title: 充分利用 TAEF
description: 充分利用 TAEF
ms.assetid: DCB06C5A-DF2C-4e1c-A297-C9AA5496D162
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bd97d7aca5a8888e413b1e5f0bab13f0c2d6db8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349552"
---
# <a name="making-the-most-of-taef"></a>充分利用 TAEF


测试创作和执行框架提供了一个强大的平台来创作和执行测试。 它可能会有所帮助了解一些后台工作 TAEF 的详细信息，以便充分利用它。 此页介绍了一些提示和功能，可帮助您编写测试，以便优化并充分利用 TAEF 的功能。 请确保您熟悉的创作和执行使用 TAEF 测试基础知识。

## <a name="span-idset-uporinitializeandclean-upmethodsspanspan-idset-uporinitializeandclean-upmethodsspanspan-idset-uporinitializeandclean-upmethodsspanset-up-or-initialize-and-clean-up-methods"></a><span id="Set-up__or_Initialize__and_Clean-up_Methods"></span><span id="set-up__or_initialize__and_clean-up_methods"></span><span id="SET-UP__OR_INITIALIZE__AND_CLEAN-UP_METHODS"></span>设置 （或 Initialize） 和清除方法


在程序集级别的设置和清理方法 (也称为*装置*)，每次 DLL 执行获取运行一次。 同样在类级别设置和清理方法获取每个类一次运行。 测试级别设置和清理方法是相同的类中的所有测试和每个测试类中一次之前和之后调用。

可能仅有一个程序集级别的安装程序和每个程序集清理方法、 一个类级别设置和清理方法，每个类和每个类的一个测试设置和清理方法。 请注意，类设置和清理方法是在托管代码中，静态的但不是静态 c + + 代码中。

如果启用了异常终止执行进行的任何方法 （默认情况下），第一个失败的验证调用。 如果已显式禁用基于异常的验证调用 （请参阅创作的详细信息的测试中的验证部分），将需要具有显式条件语句，以验证调用失败后控制的控制流。

在其中安装程序方法中发生故障的情况下 （通过基于异常的方式验证失败或由安装程序显式返回失败），要遵循的测试是否被视为"已阻止"，且这种情况下记录。 例如，如果您的类级别安装方法失败，在类中的所有测试方法被都视为"已阻止"，这种情况下将记录每个。 除此之外，如果安装程序方法中发生故障，则不会调用清理方法。

## <a name="span-idtestmethodspanspan-idtestmethodspanspan-idtestmethodspantest-method"></a><span id="Test_Method"></span><span id="test_method"></span><span id="TEST_METHOD"></span>测试方法


它不需要显式记录测试结果。 如果在测试中的所有验证调用都成功，测试将被记录为"通过"。 在第一个验证发出的调用失败，该测试方法的执行将终止 （除非显式禁用了基于异常验证调用-这种情况下在条件语句将确定的控制流那里后但而不考虑以下保存），测试将被标记为"失败"。

同样，如果已验证 （取决于返回类型以及确定成功） 帮助器方法调用调用周围的包装器，您无需显式检查并记录其结果。

## <a name="span-idspecifyingmetadataspanspan-idspecifyingmetadataspanspan-idspecifyingmetadataspanspecifying-metadata"></a><span id="Specifying_Metadata"></span><span id="specifying_metadata"></span><span id="SPECIFYING_METADATA"></span>指定元数据


元数据查找是分层的。 这意味着，如果您的 select 语句 **/选择:"@Priority= 2"**，和你 TestMethod 未指定优先级，如果 TAEF 将看看包含它的类。 如果类级别元数据没有指定它，TAEF 将程序集级别查找。

因此，如果所需的全部或大部分测试在您的类具有相同的"优先级"，或说"所有者，你可以获取，通过只在类级别指定它。 是此规则的例外的一个或少数几个测试，可以显式提供"TestMethod"级别的元数据。 请参阅以下测试的详细信息：

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

注意：对于托管测试创作完成与此类似。 模块级别等同于程序集级别标记中托管。 ***对于程序集级别或在托管代码中的类级别的元数据规范，必须提供之前的静态初始值设定项方法标记。*** 这可能意味着可能需要提供空的初始值设定项，如果你的测试还没有一个。 这种设计是为了确保 VSTS 兼容性而推出的。

对于表基于数据驱动的测试可以进一步这一个步骤，并通过指定其在行级别重写测试级别的元数据。 请参阅[元数据重写数据驱动测试示例](metadata-overriding-data-driven-test-example.md)有关详细信息。

 

 






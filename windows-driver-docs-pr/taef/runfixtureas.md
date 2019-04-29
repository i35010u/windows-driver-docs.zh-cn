---
title: RunFixtureAs
description: TAEF 提供了一种机制来执行测试装置比其相应的测试在不同上下文中。
ms.assetid: FAFF5265-5268-412E-86A5-149B187B1376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098241eb5ad4ed03950eff668265d9db41e9d57b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324736"
---
# <a name="runfixtureas"></a>RunFixtureAs


TAEF 使用 RunFixtureAs 之外所对应的测试的上下文中执行测试装置 （模块、 类和测试级别设置和清理功能）。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


-   [Te.Service](te-service.md)必须安装并在计算机上运行，以便从非提升 Te.exe 过程中，运行提升的测试装置或作为本地系统运行测试装置。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


RunFixtureAs 可以在模块、 类和或测试级别应用，并将测试树中自上而下继承。 若要支持的功能，可以选择不在树中，RunFixtureAs 给定级别的 RunFixtureAs 继承：\[作用域\]也支持元数据。

例如，如果模块被标记为与 RunFixtureAs = 系统，可以将类 (ClassA) 标记为 RunFixtureAs:Test = 默认值。 在这种情况下，模块和类装置将运行为系统，但将在测试级别装置 ClassA 中的与 Te.exe 相同的上下文中运行 （尽管仍在不同于测试的进程）。

RunFixtureAs:\[作用域\]元数据值不测试树中自上而下继承; 它仅适用于指定的作用域。

## <a name="span-iddeterministicguaranteesspanspan-iddeterministicguaranteesspanspan-iddeterministicguaranteesspandeterministic-guarantees"></a><span id="Deterministic_Guarantees"></span><span id="deterministic_guarantees"></span><span id="DETERMINISTIC_GUARANTEES"></span>确定性保证


-   默认值 （如果不指定了任何 RunFixtureAs 值）、 测试和装置，并保证能够在同一进程中运行。
-   如果装置标有 Test 以外的有效 RunFixtureAs 值，则将在不同于测试的进程中运行装置。 这意味着，即使使用运行方式标记测试 = 提升和 RunFixtureAs = 提升，测试将在已提升进程中运行和其装置将在单独的已提升进程中运行。
-   （例如，类的设置和清理装置将运行在同一进程中） 在同一进程中将始终运行匹配装置对的给定作用域。

## <a name="span-idrunfixtureastypesspanspan-idrunfixtureastypesspanspan-idrunfixtureastypesspanrunfixtureas-types"></a><span id="RunFixtureAs_Types_"></span><span id="runfixtureas_types_"></span><span id="RUNFIXTUREAS_TYPES_"></span>RunFixtureAs 类型


TAEF 支持以下 RunFixtureAs 类型，指定的测试元数据：

<span id="System"></span><span id="system"></span><span id="SYSTEM"></span>**系统**  
TAEF 作为本地系统运行装置。

**请注意**  运行如本地系统不应创建任何 UI 测试装置。 如果您的装置需要创建或与 UI 交互，您需要与 UI 相关中的代码移动到单独的可执行文件启动台式机上使用 CreateProcessAsUser 测试。

 

<span id="Elevated"></span><span id="elevated"></span><span id="ELEVATED"></span>**提升的权限**  
TAEF 可确保装置提升的进程中运行生成要在其中运行装置，如有必要提升的进程。

**请注意**  执行 TAEF 的用户必须是 administrators 组的成员才能执行装置标有 RunFixtureAs = 提升。 这是由于非管理员不具有提升的拆分令牌。

 

<span id="Default"></span><span id="default"></span><span id="DEFAULT"></span>**默认值**  
TAEF 作为 Te.exe （但仍在不同于测试的进程内） 在同一上下文中运行装置。

<span id="Broker"></span><span id="broker"></span><span id="BROKER"></span>**Broker**  
TAEF 沉浸式 Broker 进程中运行装置。

**注意**  
-   在 Windows 8 和更高版本的操作系统上仅支持代理。
-   必须在系统上启用测试签名策略。 有关详细信息[TESTSIGNING 启动配置选项](https://msdn.microsoft.com/library/windows/hardware/ff553484)。
-   使用远程运行测试 RunFixtureAs = Broker 当前不支持。
-   当执行带有 RunFixtureAs = Broker TAEF 将使用"TE。对于固定例程执行，不是"TE ProcessHost.Broker.exe"过程。ProcessHost.exe"。

 

<span id="UIAccess"></span><span id="uiaccess"></span><span id="UIACCESS"></span>**UIAccess**  
TAEF 使用 UIAccess 执行级别标记-向上某个进程中运行装置。 有关 UI 自动化应用程序的 UIAccess 信息，请参阅[Windows 完整性机制设计](https://msdn.microsoft.com/library/bb625963)。

**注意**  
-   在 Vista 和更高版本的操作系统才支持 UIAccess。
-   在计算机上，必须从 Program Files 文件夹下的文件夹运行 TAEF 二进制文件。
-   使用远程运行测试 RunFixtureAs = UIAccess' 当前不支持。
-   当执行带有 RunFixtureAs = UIAccess' TAEF 将使用"TE。对于固定例程执行，不是"TE ProcessHost.UIAccess.exe"过程。ProcessHost.exe"。

 

<span id="Test"></span><span id="test"></span><span id="TEST"></span>**测试**  
TAEF 在装置中的相同进程或上下文运行作为测试。

**请注意**  未不指定任何 RunFixtureAs 设置时，这是默认 TAEF 行为。

 

## <a name="span-idrunfixtureasscopespanspan-idrunfixtureasscopespanspan-idrunfixtureasscopespanrunfixtureasscope"></a><span id="RunFixtureAs__scope_"></span><span id="runfixtureas__scope_"></span><span id="RUNFIXTUREAS__SCOPE_"></span>RunFixtureAs:\[作用域\]


TAEF 支持以下 RunFixtureAs:\[作用域\]测试元数据由指定的值。

<span id="RunFixtureAs_Module__RunFixtureAs_Assembly__or_RunFixtureAs_Dll"></span><span id="runfixtureas_module__runfixtureas_assembly__or_runfixtureas_dll"></span><span id="RUNFIXTUREAS_MODULE__RUNFIXTUREAS_ASSEMBLY__OR_RUNFIXTUREAS_DLL"></span>**RunFixtureAs:Module**， **RunFixtureAs:Assembly**，或**RunFixtureAs:Dll**  
RunFixtureAs 值将仅适用于测试层次结构中在模块级别节点。

<span id="RunFixtureAs_Class"></span><span id="runfixtureas_class"></span><span id="RUNFIXTUREAS_CLASS"></span>**RunFixtureAs:Class**  
RunFixtureAs 值将仅适用于测试层次结构中的类级节点。

<span id="RunFixtureAs_Method_or_RunFixtureAs_Test"></span><span id="runfixtureas_method_or_runfixtureas_test"></span><span id="RUNFIXTUREAS_METHOD_OR_RUNFIXTUREAS_TEST"></span>**RunFixtureAs:Method**或**RunFixtureAs:Test**  
RunFixtureAs 值将仅适用于测试层次结构中的测试级别节点。

## <a name="span-idmarkingtestswithrunfixtureasspanspan-idmarkingtestswithrunfixtureasspanspan-idmarkingtestswithrunfixtureasspanmarking-tests-with-runfixtureas"></a><span id="Marking_Tests_with_RunFixtureAs"></span><span id="marking_tests_with_runfixtureas"></span><span id="MARKING_TESTS_WITH_RUNFIXTUREAS"></span>将标记与 RunFixtureAs 测试


```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   运行方式提升 MyTestSetup 和 MyTestCleanup
-   MyClassSetup 和 MyClassCleanup 以 System 身份运行 （在同一进程中作为 MyTestMethod）
-   MyModuleSetup 和 MyModuleCleanup 以 System 身份运行 （在同一进程中作为 MyTestMethod）

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   运行方式提升 MyTestSetup 和 MyTestCleanup
-   运行方式提升 MyClassSetup 和 MyClassCleanup
-   MyModuleSetup 和 MyModuleCleanup 以 System 身份运行 （在同一进程中作为 MyTestMethod）

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"System")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   Restricted 作为运行 MyTestMethod
-   运行方式提升 MyTestSetup 和 MyTestCleanup
-   MyClassSetup 和 MyClassCleanup 以 System 身份运行
-   MyModuleSetup MyModuleCleanup 运行方式和受限制 （在同一进程中作为 MyTestMethod）

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"System")
        TEST_METHOD_PROPERTY(L"RunFixtureAs:Test", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   作为 Restricted MyTestMethod2 运行
-   运行方式提升; MyTestSetup 和 MyTestCleanupRunFixtureAs:Test 作用域应用于 MyTests 类中的所有测试方法
-   MyClassSetup 和 MyClassCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）
-   MyModuleSetup 和 MyModuleCleanup 运行其各自的上下文中测试进程 （用于 MyTestMethod 系统） 和 MyTestMethod2 的受限制

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"System")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   作为 Restricted MyTestMethod2 运行
-   作为系统 MyTestMethod 和 MyTestMethod2 的提升 MyTestSetup 和 MyTestCleanup 运行
-   MyClassSetup 和 MyClassCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）
-   MyModuleSetup 和 MyModuleCleanup 运行其各自的上下文中测试进程 （用于 MyTestMethod 系统） 和 MyTestMethod2 的受限制

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Default")
        TEST_CLASS_PROPERTY(L"RunFixtureAs:Test", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   作为 Restricted MyTestMethod2 运行
-   MyTestSetup 和 MyTestCleanup MyTestMethod 和 MyTestMethod2 的运行方式提升
-   为默认值运行 MyClassSetup 和 MyClassCleanup （Te.exe 与相同的上下文中当前正在运行，尚未在不同于 MyTestMethod 和 MyTestMethod2 的进程内）
-   MyModuleSetup 和 MyModuleCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
    MODULE_PROPERTY(L"RunFixtureAs:Test", L"Test")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   作为 Restricted MyTestMethod2 运行
-   MyTestSetup 和 MyTestCleanup MyTestMethod 和 MyTestMethod2 与相同的进程中运行
-   运行方式提升 MyClassSetup 和 MyClassCleanup
-   MyModuleSetup 和 MyModuleCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
    MODULE_PROPERTY(L"RunFixtureAs:Test", L"Test")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   作为 Restricted MyTestMethod2 运行
-   MyTestSetup 和 MyTestCleanup MyTestMethod2 作为 MyTestMethod 和在提升的进程在同一进程中运行
-   运行方式提升 MyClassSetup 和 MyClassCleanup
-   MyModuleSetup 和 MyModuleCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs:Class", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

上面的示例将运行测试和装置，如下所示：

-   作为系统运行 MyTestMethod
-   作为 Restricted MyTestMethod2 运行
-   MyTestSetup 和 MyTestCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）
-   运行方式提升 MyClassSetup 和 MyClassCleanup
-   MyModuleSetup 和 MyModuleCleanup 以 System 身份运行 （在不同于 MyTestMethod 进程）

 

 






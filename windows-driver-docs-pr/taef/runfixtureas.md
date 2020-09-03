---
title: RunFixtureAs
description: TAEF 提供一种机制，用于在与相应测试不同的上下文中执行测试装置。
ms.assetid: FAFF5265-5268-412E-86A5-149B187B1376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bafef9d16ff2b190ae937cdd6a0197778439f50
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402766"
---
# <a name="runfixtureas"></a>RunFixtureAs


TAEF 使用 RunFixtureAs 来执行测试装置 (模块、类和测试级安装程序和清理) 函数在上下文中，而不是相应测试 () 。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


-   [Te](te-service.md) 必须在计算机上安装并运行服务，才能从非提升的 Te.exe 进程运行提升的测试装置，或将测试装置作为本地系统运行。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>叙述


RunFixtureAs 可以应用于模块、类或测试级别，并将在测试树中被继承。 为了支持在树的给定级别上退出 RunFixtureAs 继承功能， \[ 还支持 RunFixtureAs：范围 \] 元数据。

例如，如果模块标记有 RunFixtureAs = System，则可以将类 (ClassA) 标记为 RunFixtureAs： Test = Default。 在这种情况下，模块和类装置将作为系统运行，但 ClassA 中的测试级别装置将与 Te.exe (在同一上下文中运行，尽管仍在不同于测试) 的进程中运行。

RunFixtureAs： \[ 作用域 \] 元数据值不会沿着测试树向下继承; 它仅适用于指定的作用域。

## <a name="span-iddeterministic_guaranteesspanspan-iddeterministic_guaranteesspanspan-iddeterministic_guaranteesspandeterministic-guarantees"></a><span id="Deterministic_Guarantees"></span><span id="deterministic_guarantees"></span><span id="DETERMINISTIC_GUARANTEES"></span>确定性保证


-   默认情况下 (如果未指定任何 RunFixtureAs 值) ，则保证测试和装置在同一进程中运行。
-   如果为装置标记的 RunFixtureAs 值不是 "Test"，则该装置将在与测试不同的进程中运行。 这意味着，即使测试标记为 RunAs = 升高且 RunFixtureAs = 提升，该测试也会在提升的进程中运行，并且其装置会在单独的提升进程中运行。
-   给定作用域的匹配装置对将始终在同一进程中运行 (例如，类的设置和清理装置将在同一进程中运行) 。

## <a name="span-idrunfixtureas_types_spanspan-idrunfixtureas_types_spanspan-idrunfixtureas_types_spanrunfixtureas-types"></a><span id="RunFixtureAs_Types_"></span><span id="runfixtureas_types_"></span><span id="RUNFIXTUREAS_TYPES_"></span>RunFixtureAs 类型


TAEF 支持以下 RunFixtureAs 类型，这些类型由测试元数据指定：

<span id="System"></span><span id="system"></span><span id="SYSTEM"></span>**主板**  
TAEF 将装置作为本地系统运行。

**注意**   作为本地系统运行的测试装置不应创建任何 UI。 如果你的夹具需要创建 UI 或与 UI 交互，则需要将与 UI 相关的代码移到使用 CreateProcessAsUser 从测试中启动的独立可执行文件。

 

<span id="Elevated"></span><span id="elevated"></span><span id="ELEVATED"></span>**较**  
TAEF 可确保在提升的进程中运行装置，如有必要，请根据需要生成要运行的装置。

**注意**   执行 TAEF 的用户必须是 administrators 组的成员，才能执行标有 RunFixtureAs = 升高的装置。 这是因为，非管理员没有要提升的拆分令牌。

 

<span id="Default"></span><span id="default"></span><span id="DEFAULT"></span>**缺省值**  
TAEF 在与 Te.exe (相同的上下文中运行装置，但仍在不同于测试) 的进程中运行。

<span id="Broker"></span><span id="broker"></span><span id="BROKER"></span>**中间**  
TAEF 运行 "沉浸式代理" 进程中的装置。

**注意**  
-   只有 Windows 8 及更高版本的操作系统才支持 "Broker"。
-   必须在系统上启用测试签名策略。 有关详细信息，请查看 [TESTSIGNING Boot 配置选项](../install/the-testsigning-boot-configuration-option.md)。
-   当前不支持通过 "RunFixtureAs = Broker" 远程运行测试。
-   使用 "RunFixtureAs = Broker" TAEF 执行时，将使用 "TE.ProcessHost.Broker.exe" 进程执行夹具，而不是 "TE.ProcessHost.exe"。

 

<span id="UIAccess"></span><span id="uiaccess"></span><span id="UIACCESS"></span>**UIAccess**  
TAEF 在使用 UIAccess 执行级别标记的进程中运行装置。 有关适用于 UI 自动化应用程序的 UIAccess 的信息，请参阅 [Windows 完整性机制设计](/previous-versions/dotnet/articles/bb625963(v=msdn.10))。

**注意**  
-   仅在 Vista 和更高版本的操作系统上支持 UIAccess。
-   TAEF 二进制文件必须从计算机上 Program Files 文件夹下的文件夹运行。
-   当前不支持通过 "RunFixtureAs = UIAccess" 远程运行测试。
-   使用 "RunFixtureAs = UIAccess" TAEF 执行时，将使用 "TE.ProcessHost.UIAccess.exe" 进程执行夹具，而不是 "TE.ProcessHost.exe"。

 

<span id="Test"></span><span id="test"></span><span id="TEST"></span>**考试**  
TAEF 运行与测试相同的进程或上下文中的装置。

**注意**   如果未指定 RunFixtureAs 设置，这是默认的 TAEF 行为。

 

## <a name="span-idrunfixtureas__scope_spanspan-idrunfixtureas__scope_spanspan-idrunfixtureas__scope_spanrunfixtureasscope"></a><span id="RunFixtureAs__scope_"></span><span id="runfixtureas__scope_"></span><span id="RUNFIXTUREAS__SCOPE_"></span>RunFixtureAs： \[ 作用域\]


TAEF 支持以下 RunFixtureAs： \[ 范围 \] 值，这些值由测试元数据指定。

<span id="RunFixtureAs_Module__RunFixtureAs_Assembly__or_RunFixtureAs_Dll"></span><span id="runfixtureas_module__runfixtureas_assembly__or_runfixtureas_dll"></span><span id="RUNFIXTUREAS_MODULE__RUNFIXTUREAS_ASSEMBLY__OR_RUNFIXTUREAS_DLL"></span>**RunFixtureAs： Module**、 **RunFixtureAs： Assembly**或 **RunFixtureAs： Dll**  
RunFixtureAs 值将仅应用于测试层次结构中的模块级别节点。

<span id="RunFixtureAs_Class"></span><span id="runfixtureas_class"></span><span id="RUNFIXTUREAS_CLASS"></span>**RunFixtureAs：类**  
RunFixtureAs 值将仅应用于测试层次结构中的类级别节点。

<span id="RunFixtureAs_Method_or_RunFixtureAs_Test"></span><span id="runfixtureas_method_or_runfixtureas_test"></span><span id="RUNFIXTUREAS_METHOD_OR_RUNFIXTUREAS_TEST"></span>**RunFixtureAs： Method** 或 **RunFixtureAs： Test**  
RunFixtureAs 值将仅应用于测试层次结构中的测试级别节点。

## <a name="span-idmarking_tests_with_runfixtureasspanspan-idmarking_tests_with_runfixtureasspanspan-idmarking_tests_with_runfixtureasspanmarking-tests-with-runfixtureas"></a><span id="Marking_Tests_with_RunFixtureAs"></span><span id="marking_tests_with_runfixtureas"></span><span id="MARKING_TESTS_WITH_RUNFIXTUREAS"></span>用 RunFixtureAs 标记测试


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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestSetup 和 MyTestCleanup 以提升的权限运行
-   MyClassSetup 和 MyClassCleanup 在与 MyTestMethod 相同的进程内作为系统 (运行) 
-   MyModuleSetup 和 MyModuleCleanup 在与 MyTestMethod 相同的进程内作为系统 (运行) 

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestSetup 和 MyTestCleanup 以提升的权限运行
-   MyClassSetup 和 MyClassCleanup 以提升的权限运行
-   MyModuleSetup 和 MyModuleCleanup 在与 MyTestMethod 相同的进程内作为系统 (运行) 

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 以提升的权限运行
-   MyClassSetup 和 MyClassCleanup 运行方式系统
-   MyModuleSetup 和 MyModuleCleanup 在与 MyTestMethod 相同的进程内作为受限 (运行) 

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestMethod2 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 以提升的权限运行;RunFixtureAs：测试范围应用于 Mytests.dll 类中的所有测试方法
-   MyClassSetup 和 MyClassCleanup 在除) MyTestMethod 外的不同进程中运行 (
-   MyModuleSetup 和 MyModuleCleanup 在其各自测试过程的上下文中运行， (System for MyTestMethod，并限制 MyTestMethod2) 

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestMethod2 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 以系统的形式运行 MyTestMethod 和 MyTestMethod2 的提升
-   MyClassSetup 和 MyClassCleanup 在除) MyTestMethod 外的不同进程中运行 (
-   MyModuleSetup 和 MyModuleCleanup 在其各自测试过程的上下文中运行， (System for MyTestMethod，并限制 MyTestMethod2) 

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestMethod2 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 在 MyTestMethod 和 MyTestMethod2 上都以提升的权限运行
-   MyClassSetup 和 MyClassCleanup 作为默认 (在当前运行 Te.exe 的上下文中运行，但在与 MyTestMethod 和 MyTestMethod2 不同的进程内) 
-   MyModuleSetup 和 MyModuleCleanup 在除) MyTestMethod 外的不同进程中运行 (

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestMethod2 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 在与 MyTestMethod 和 MyTestMethod2 相同的进程中运行
-   MyClassSetup 和 MyClassCleanup 以提升的权限运行
-   MyModuleSetup 和 MyModuleCleanup 在除) MyTestMethod 外的不同进程中运行 (

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

前面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestMethod2 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 在与 MyTestMethod 相同的进程中运行，并在 MyTestMethod2 的提升的进程中运行
-   MyClassSetup 和 MyClassCleanup 以提升的权限运行
-   MyModuleSetup 和 MyModuleCleanup 在除) MyTestMethod 外的不同进程中运行 (

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

上面的示例将按如下所示运行测试和装置：

-   MyTestMethod 作为系统运行
-   MyTestMethod2 以受限方式运行
-   MyTestSetup 和 MyTestCleanup 在除) MyTestMethod 外的不同进程中运行 (
-   MyClassSetup 和 MyClassCleanup 以提升的权限运行
-   MyModuleSetup 和 MyModuleCleanup 在除) MyTestMethod 外的不同进程中运行 (

 


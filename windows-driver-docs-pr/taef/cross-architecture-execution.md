---
title: 跨体系结构执行
description: 跨体系结构执行
ms.assetid: 6E7F53A0-7C6A-4063-8300-31E1853EDD04
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e3bfad7f506ff4882566553bf70a0b1171e542
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385074"
---
# <a name="cross-architecture-execution"></a>跨体系结构执行


TAEF 支持从不同的体系结构具有相同命令行-运行测试的功能，提供运行测试的操作系统支持它们。 这意味着，-例如-x64*和*x86 测试 (在 x64 操作系统) 可以使用单个 te.exe 命令行执行。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


若要运行测试的不同体系结构与 te.exe 本身，该体系结构的 TAEF 二进制文件需要可供 te.exe。 目标体系结构可以是任意的：

-   x86
-   x64
-   ia64

TAEF 将查找名为目标体系结构中相对于原始 te.exe 为该体系结构的 TAEF 二进制文件的文件夹中。

## <a name="span-idexecutingtestsforadifferentarchitecturespanspan-idexecutingtestsforadifferentarchitecturespanspan-idexecutingtestsforadifferentarchitecturespanexecuting-tests-for-a-different-architecture"></a><span id="Executing_Tests_for_a_Different_Architecture"></span><span id="executing_tests_for_a_different_architecture"></span><span id="EXECUTING_TESTS_FOR_A_DIFFERENT_ARCHITECTURE"></span>测试执行为不同的体系结构


执行不同的体系结构的测试不需要额外配置-只需将给定的 DLL 作为参数传递给 te.exe。 TAEF 将检查二进制文件来标识它的目标体系结构，并实例化正确的主机进程以加载和运行测试。 例如，可以检查 te.exe x86 x64 测试 DLL，并将启动 x64 进程以运行测试：

**c:\\taef\\x86&gt;te x64\\Scenario.Tests.dll**

由于 te.exe 命令行可能需要多个测试 DLL，您可以混合体系结构和 TAEF 将为给定的测试 DLL 选择正确的主机进程：

**c:\\taef\\x86&gt;te x64\\Scenario.Tests.dll x86\\Scenario.Tests.dll x64\\UI。Tests.dll**

这允许 TAEF 用户以了解更多的测试覆盖率通过单个命令行，最终会形成单个日志的所有结果。 如果没有此功能，必须一起拉取到自己的命令行，单独执行每个体系结构的测试，并从每个结果运行组合。

如果给定的测试文件是否*不*特定体系结构 (例如，C#二进制文件的编译为纯 IL)，然后使用相同的体系结构 te.exe 传递给运行。

## <a name="span-idselectingtestsbyarchitecturespanspan-idselectingtestsbyarchitecturespanspan-idselectingtestsbyarchitecturespanselecting-tests-by-architecture"></a><span id="Selecting_Tests_by_Architecture"></span><span id="selecting_tests_by_architecture"></span><span id="SELECTING_TESTS_BY_ARCHITECTURE"></span>选择体系结构通过的测试


TAEF 自动应用于需要特定的体系结构的测试文件的体系结构元数据。 体系结构元数据的值是需要运行测试，并且将是之一的体系结构：

-   x86
-   x64
-   ia64

若要选择特定的体系结构的测试，可用于选择语言匹配的体系结构元数据。 例如，如果测试文件夹中包括的 x86 和 x64 测试文件，则下面的命令行将运行仅 x64 测试：

**c:\\taef\\x86&gt;te 测试\\\*。Tests.dll /select:@Architecture= x64**

## <a name="span-iderrorsspanspan-iderrorsspanspan-iderrorsspanerrors"></a><span id="Errors"></span><span id="errors"></span><span id="ERRORS"></span>错误


不存在必需的目标体系结构二进制文件的情况下将不同的体系结构编译一个测试文件传递到 TAEF 将导致一条错误消息。 下面的示例演示 x86 te.exe 尝试运行 x64 测试，而无需填充具有所需的二进制文件的 x64 子文件夹：

``` syntax
c:\>te x64\Scenario.Tests.dll
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86
Error: Please copy all x64 TAEF binaries to the 'c:\taef\x86\x64' directory in order to run x64 tests from this process. 
Error: Failed to create the ProcessHostController. TE.ProcessHost.exe may be unavailable. Terminating execution...
Error: No test cases were executed.
```

 

 






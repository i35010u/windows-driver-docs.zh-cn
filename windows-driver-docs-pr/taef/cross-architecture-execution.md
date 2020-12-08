---
title: 跨体系结构执行
description: 跨体系结构执行
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8101e95eb2eabe415cf3fb19b41ac8692f1ed4d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790869"
---
# <a name="cross-architecture-execution"></a>跨体系结构执行


TAEF 支持通过相同的命令行从不同的体系结构运行测试的能力，前提是运行测试的操作系统支持它们。 这意味着，例如，可使用单个 "te.exe" 命令行在 x64 OS) 上执行 x64 *和* x86 测试 (。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


若要为不同于 "te.exe" 本身的体系结构运行测试，该体系结构的 TAEF 二进制文件必须可用于 "te.exe"。 目标体系结构可以是以下任一内容：

-   x86
-   X64
-   ia64

TAEF 会在一个名为的文件夹中查找相对于该体系结构的 TAEF 二进制文件的原始 "te.exe" 的目标体系结构。

## <a name="span-idexecuting_tests_for_a_different_architecturespanspan-idexecuting_tests_for_a_different_architecturespanspan-idexecuting_tests_for_a_different_architecturespanexecuting-tests-for-a-different-architecture"></a><span id="Executing_Tests_for_a_Different_Architecture"></span><span id="executing_tests_for_a_different_architecture"></span><span id="EXECUTING_TESTS_FOR_A_DIFFERENT_ARCHITECTURE"></span>针对不同的体系结构执行测试


针对不同的体系结构执行测试不需要额外的配置-只需将给定的 DLL 作为参数传递给 "te.exe" 即可。 TAEF 将检查二进制文件以确定其目标体系结构，并实例化正确的主机进程，以便加载和运行测试。 例如，x86 "te.exe" 可以检查 x64 测试 DLL，并将启动一个 x64 进程来运行测试：

**c： \\ taef \\ x86 &gt; te x64 \\Scenario.Tests.dll**

由于 "te.exe" 命令行可以接受多个测试 DLL，因此，您可以混合体系结构，TAEF 将为给定的测试 DLL 选择正确的主机进程：

**c： \\ taef \\ x86 &gt; te x64 \\Scenario.Tests.dll x86 \\Scenario.Tests.dll x64 \\UI.Tests.dll**

这允许 TAEF 用户从单个命令行获取更多测试覆盖率，并将所有结果汇总到单个日志中。 如果没有此功能，则必须将每个体系结构的测试一起提取到自己的命令行中，分别执行并组合每个运行的结果。

如果给定的测试文件 *不* 是特定于体系结构的 (例如，将编译为纯 IL) 的 c # 二进制文件，则将使用与传递到的 "te.exe" 相同的体系结构来运行。

## <a name="span-idselecting_tests_by_architecturespanspan-idselecting_tests_by_architecturespanspan-idselecting_tests_by_architecturespanselecting-tests-by-architecture"></a><span id="Selecting_Tests_by_Architecture"></span><span id="selecting_tests_by_architecture"></span><span id="SELECTING_TESTS_BY_ARCHITECTURE"></span>按体系结构选择测试


TAEF 会自动将 "体系结构" 元数据应用于测试需要特定体系结构的文件。 "体系结构" 元数据的值是运行测试所需的体系结构，并且是以下各项之一：

-   x86
-   X64
-   ia64

若要为特定体系结构选择测试，可以使用选择语言来匹配 "体系结构" 元数据。 例如，如果 "测试" 文件夹包含 x86 和 x64 测试文件的混合，则以下命令行将仅运行 x64 测试：

**c： \\ taef \\ X86 &gt; te 测试 \\ \*.Tests.dll /select:@Architecture = "x64"**

## <a name="span-iderrorsspanspan-iderrorsspanspan-iderrorsspanerrors"></a><span id="Errors"></span><span id="errors"></span><span id="ERRORS"></span>错误


如果在没有所需的目标体系结构二进制文件的情况下将为其他体系结构编译的测试文件传递到 TAEF，则将导致错误消息。 下面的示例演示了一个 x86 "te.exe"，它尝试运行 x64 测试，而不使用所需的二进制文件填充 "x64" 子文件夹：

``` syntax
c:\>te x64\Scenario.Tests.dll
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86
Error: Please copy all x64 TAEF binaries to the 'c:\taef\x86\x64' directory in order to run x64 tests from this process. 
Error: Failed to create the ProcessHostController. TE.ProcessHost.exe may be unavailable. Terminating execution...
Error: No test cases were executed.
```

 

 





